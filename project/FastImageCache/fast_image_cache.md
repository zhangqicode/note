### 概述
* 仓库地址：[FastImageCache](https://github.com/path/FastImageCache#what-fast-image-cache-does)
* 一篇中文简介，基本讲清了 FastImageCache 做了什么：[iOS图片加载速度极限优化—FastImageCache解析](https://blog.cnbang.net/tech/2578/)


### 要点总结
* FastImageCache 做了三件事：内存映射、解码图片、字节对齐
* 内存映射是避免了内存复制。传统的图片使用方式中读取一张图片是先从磁盘读取到内核缓冲区，再由内核缓冲区复制到用户空间。内存映射免除了这一步复制。
* 解码图片是避免的解码过程。提前将图片解码成位图，存储在磁盘中。
* 字节对齐是避免 Core Animation 在使用图像数据前拷贝数据。Core Animation 使用的数据是需要对齐字节的，传统过程中提供给 Core Animation 的数据未必是对齐的，那么就需要做一次拷贝将字节对齐。（还有一层含义，下文有详细说明）

### 内存映射
* 内存映射是在 FICImageTableChunk 中完成的，通过 mmap 机制实现的
* 简单的介绍了 mmap ：[瞜一眼 mmap](https://everettjf.github.io/2018/09/01/mmap/)
* 详细的介绍了 mmap ：[认真分析mmap：是什么 为什么 怎么用](https://www.cnblogs.com/huxiao-tee/p/4660352.html)

### 解码图片
* 这个地方的实现有点绕，首先创建一个 entry，这个 entry 内部的 bytes 已经做好内存映射了
* 然后用 entry 的 bytes 创建一个 bitmap，这个位图使用 bytes 中的数据，反过来如果我们在位图中绘制内容，也会同步到 bytes 对应的内存中
* 将图片绘制到 bitmap 上，这相当于将已经解码的图片数据对应到 bytes 中，然后调用 entry 的 flush 方法，进行 mmap 机制的同步（即写入磁盘）

### 字节对齐
* 字节对齐有两层含义，第一层是字节块对齐，第二层是 Core Animation 使用图像数据时的字节对齐（去除杂质）
* 字节块对齐处理的是 CPU 获取字节块时的优化工作，例如 CPU 需要获取的数据在两个字节块中，CPU 就需要加载两个字节块，然后将需要的字节保留组成所需的字节块，对齐后则直接加载所需的字节块即可。
* 在 FastImageCache 中是在 FICImageTableChunk 中实现的，据我不靠谱的观察，字节块对齐不需要额外的工作，图像数据对齐后这里自动就对齐了
* 使用图像数据时的字节对齐是指，如果图像数据的字节块中包含杂质（例如一个字节块 64 字节，其中有 60 字节是图像数据，最后 4 字节是其它数据，对于 Core Animation 来说这 4 字节就是杂质），Core Animation 会复制这个字节块的前 60 字节图像数据，最后 4 字节以 0 填充
* 图像数据的对齐是用 FICByteAlignForCoreAnimation 实现的，有意思的是这里是按照图像的行数据进行对齐，而不是整个图像的数据进行对齐，猜测是绘制时是按行进行取用数据的，只有按行对齐才能避免 Core Animation 复制数据

### 使用流程
* 我们来简单总结一下 FastImageCache 是如何工作的
* 核心类是 FICImageCache 和 FICImageTable，FICImageTable 是数据存储的基本框架结构，FICImageCache 是管理类，我们主要与 FICImageCache 打交道
* 我们通过 FICImageCache 的 retrieveImageForEntity 等方法获取 image，取到后直接给 imageView 等组件赋值即可
* 那么 FICImageCache 是如何获取原始数据的呢？通过其 FICImageCacheDelegate 类型的代理获取。这也是 FastImageCache 不够方便的地方，我们需要自己实现代理方法，处理图片下载等工作。
* FICImageCache 通过代理拿到数据后调用 _processImage 方法来处理图片，将图片数据放在一个 FICEntityImageDrawingBlock 中传递给 imageTable 的 setEntryForEntityUUID 方法
* 在 setEntryForEntityUUID 方法中，imageTable 会生成对应的 chunk 与 entry，使用 entry 的 bytes 创建位图，使用传进来的 FICEntityImageDrawingBlock 将图像绘制在位图上，那么解压后的图像数据就对应到了 bytes 中，然后调用 entry 的 flush 方法将数据映射回磁盘文件中
* retrieveImageForEntity 方法内部真正获取图片的地方调用了 newImageForEntityUUID ，这里面就比较简单了，找到对应的 entry，将其 bytes 转换成 UIImage。这时候拿到的 UIImage 就是已经解压过且字节对齐的数据了。

### 资料
* 一篇精简扼要的原理介绍，可以作为提纲来了解 FastImageCache：[FastImageCache 原理](https://juejin.im/entry/5b9876ccf265da0ab41e3f50)
* 一篇十分详细的分析：[iOS高效图片 IO 框架是如何炼成的](https://simplecodesky.com/2018/04/10/ios-efficient-image-io/)





