Toll-Free Bridging 译为“无缝桥接”，这个机制是指部分类型的 CoreFoundation 和 Foundation 对象的相互替代使用  
下面这篇文章有一个小节讲的内容很变态，利用 CFDictionary 创建了一个修改了“键的内存管理语义”的字典，普通字典的键要求实现 NSCopying 协议，因为对象被当做键传递给字典时，字典会 copy 该对象（这就是键的内存管理语义）。文章中创建了一个键的内存管理语义为 retain 的字典，堪称变态，同理继续这个变态的想法，如果我们将“值的内存管理语义”都改为什么都不做（正常的字典是 retain 和 release），那么就能创建一个不改变值引用计数的字典（但是估计值被释放后，这里变成野指针该崩还是要崩的，所以并没有什么价值，只是单纯的变态，同时好奇类似 NSPointerArray 之类的对象是如何实现的，应该不是这种方法吧）。  
[Toll-Free Bridging](https://www.jianshu.com/p/c53f2eb116ae)  

另一篇关于 Toll-Free Bridging 的文章，讲了 Toll-Free Bridging 是如何实现的（类簇相关），关于 bridge 操作也讲的比较好  
[Toll-Free Bridging](http://gracelancy.com/blog/2014/04/21/toll-free-bridging/)