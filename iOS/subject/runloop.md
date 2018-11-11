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

总结的很到位  
[解密-神秘的 RunLoop](http://ios.jobbole.com/85635/)

>什么是RunLoop?  
>从字面上看:运行循环、跑圈  
>其实它内部就是do-while循环,在这个循环内部不断的处理各种任务(比如Source、Timer、Observer)  
>一个线程对应一个RunLoop,主线程的RunLoop默认已经启动,子线程的RunLoop需要手动启动(调用run方法)  
>RunLoop只能选择一个Mode启动,如果当前Mode中没有任何Soure、Timer、Observer,那么就直接退出RunLoop  
>
>在开发中如何使用RunLoop?什么应用场景?  
>开启一个常驻线程(让一个子线程不进入消亡状态,等待其他线程发来消息,处理其他事件)  
>在子线程中开启一个定时器  
>在子线程中进行一些长期监控  
>可以控制定时器在特定模式下执行  
>可以让某些事件(行为、任务)在特定模式下执行  
>可以添加Observer监听RunLoop的状态,比如监听点击事件的处理(在所有点击事件之前做一些事情)  

孙源关于 Runloop 的分享：  
[Runloop](http://v.youku.com/v_show/id_XODgxODkzODI0.html?spm=a2h0k.8191407.0.0&from=s1.8-1-1.2)