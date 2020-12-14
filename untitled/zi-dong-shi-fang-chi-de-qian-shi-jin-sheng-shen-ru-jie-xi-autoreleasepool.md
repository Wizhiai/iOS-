---
description: 这篇文章会在源代码层面介绍 Objective-C 中自动释放池，以及方法的 autorelease 的具体实现。
---

# 自动释放池的前世今生 ---- 深入解析 autoreleasepool

### 从 main 函数开始 <a id="&#x4ECE;-main-&#x51FD;&#x6570;&#x5F00;&#x59CB;"></a>

`main` 函数可以说是在整个 iOS 开发中非常不起眼的一个函数，它很好地隐藏在 `Supporting Files` 文件夹中，却是整个 iOS 应用的入口。

`main.m` 文件中的内容是这样的：

```text
int main(int argc, char * argv[]) {
    NSString * appDelegateClassName;
    @autoreleasepool {
        // Setup code that might create autoreleased objects goes here.
        appDelegateClassName = NSStringFromClass([AppDelegate class]);
        }
        return UIApplicationMain(argc, argv, nil, appDelegateClassName);
}
```

其中autoreleasepool里包含了仅一句代码，且有一注释：

// Setup code that might create autoreleased objects goes here.

在这里创建那些可能会自动释放的对象，而这里的作用是根据

```text
[AppDelegate class]
```

获取一个类名，然后传回去。

