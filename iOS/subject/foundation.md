讲了两种方法参数的类型区别：  
[setValue和setObject的区别](https://blog.csdn.net/reylen/article/details/8666522)

>引发的问题是 NSMutableDictionary 的 key 能是什么类型？满足什么条件？  
>
>key 可以是任意类型，不能为 nil，要满足 NSCopying 协议  

  
说是实现原理，其实只是讲了如何实现一个自定义的类作为 key：  
[NSDictionary实现原理](https://blog.csdn.net/linshaolie/article/details/41494303)

【未读】真正的实现原理：  
[NSDictionary底层实现原理](https://juejin.im/post/5b03cc6e6fb9a07acf567bb8)

[iOS instancetype 和 id 区别详解](https://juejin.im/entry/588022572f301e00697c8756)
>产生了一个想法：  
>如果是一个工厂类，工厂方法应该用 instancetype 还是 id ，个人感觉是 id，因为如果用 instancetype 可能会返回工厂类的类型。
>
>验证了一下，结果如下：  
>1.编译器会有警告，提示返回的类型不匹配，但是运行起来不会有错误  
>2.虽然不会有问题，但按照编码规范还是应该使用 id