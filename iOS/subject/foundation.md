讲了两种方法参数的类型区别：  
[setValue和setObject的区别](https://blog.csdn.net/reylen/article/details/8666522)

>引发的问题是 NSMutableDictionary 的 key 能是什么类型？满足什么条件？  
>
>key 可以是任意类型，不能为 nil，要满足 NSCopying 协议  

  
说是实现原理，其实只是讲了如何实现一个自定义的类作为 key：  
[NSDictionary实现原理](https://blog.csdn.net/linshaolie/article/details/41494303)

【未读】真正的实现原理：  
[NSDictionary底层实现原理](https://juejin.im/post/5b03cc6e6fb9a07acf567bb8)