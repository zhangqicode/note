## 关于 weakself 与 strongself

可以确定的是下面这样写其实并没有什么用

```
- (void)viewDidLoad {
    [super viewDidLoad];
    
    ZZMemoryVC *vc = [[ZZMemoryVC alloc] init];
    __weak typeof(vc) weakSelf = vc;
    dispatch_async(dispatch_get_main_queue(), ^{
        __strong typeof(weakSelf) strongSelf = weakSelf;
        NSLog(@"%@", strongSelf);
    });
    
    // Do any additional setup after loading the view, typically from a nib.
}
```
