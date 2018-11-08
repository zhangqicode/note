简要的 Runloop 介绍，总结的很好：  
[Runloop](https://hit-alibaba.github.io/interview/iOS/ObjC-Basic/Runloop.html)

Runloop 的源码分析，非常详尽，而且提供了 Runloop 的诸多使用场景，以及与其它机制的联系，如自动释放池、GCD等：  
[iOS刨根问底-深入理解RunLoop](http://www.cnblogs.com/kenshincui/p/6823841.html)

>读这篇文章时想到了一个问题：  
>我们在什么场景下会需要在子线程里启动 Runloop？
>
>个人想到了两个场景：  
>1.轮询获取信息，例如获取即时消息、实时性要求较高的交互场景
>2.定时上报信息，例如地图应用中上报位置

