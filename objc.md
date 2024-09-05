# 什么是objc

脱胎与C语言，具备面向对象编程的一门语言，语法可读性差，贴近硬件

# 与Swift的区别
Swift 和 Objective-C 是两种用于开发 iOS 和 macOS 应用的编程语言。虽然它们都由 Apple 推出，但在设计理念、语法和功能上有许多显著的区别。以下是一些关键区别：

### 1. 语法和可读性

- **Swift**：语法简洁，现代化，强调代码的可读性和可维护性。
  ```swift
  let message = "Hello, World!"
  print(message)
  ```
  
- **Objective-C**：语法较为冗长，基于 C 语言的语法，使用大量的方括号和关键字。
  ```objc
  NSString *message = @"Hello, World!";
  NSLog(@"%@", message);
  ```

### 2. 类型安全和类型推断

- **Swift**：强类型语言，具有类型安全和类型推断特性，减少了运行时错误。
  ```swift
  let number = 42  // Swift 自动推断 number 的类型为 Int
  ```
- **Objective-C**：类型系统较为宽松，允许更多的动态类型检查。
  ```objc
  NSNumber *number = @42;
  ```

### 3. 内存管理

- **Swift**：使用自动引用计数（ARC）进行内存管理，且默认情况下所有对象都是强引用。提供了 `weak` 和 `unowned` 引用来避免循环引用。
  ```swift
  class Person {
      weak var friend: Person?
  }
  ```
- **Objective-C**：也使用 ARC，但需要显式地标记属性为 `strong`、`weak`、`assign` 等。
  ```objc
  @interface Person : NSObject
  @property (nonatomic, weak) Person *friend;
  @end
  ```

### 4. 函数和方法

- **Swift**：函数和方法定义更为简洁，支持函数重载和默认参数。
  ```swift
  func greet(name: String, withMessage message: String = "Hello") {
      print("\(message), \(name)!")
  }
  greet(name: "Alice")  // 输出 "Hello, Alice!"
  ```
- **Objective-C**：方法定义较为冗长，不支持函数重载。
  ```objc
  - (void)greetWithName:(NSString *)name message:(NSString *)message {
      NSLog(@"%@, %@!", message, name);
  }
  [self greetWithName:@"Alice" message:@"Hello"];
  ```

### 5. 面向协议编程

- **Swift**：强调面向协议编程（POP），提供了强大的协议扩展和默认实现。
  ```swift
  protocol Greetable {
      func greet()
  }

  extension Greetable {
      func greet() {
          print("Hello!")
      }
  }

  struct Person: Greetable {}
  let person = Person()
  person.greet()  // 输出 "Hello!"
  ```
- **Objective-C**：支持协议（protocol），但没有协议扩展和默认实现。
  ```objc
  @protocol Greetable <NSObject>
  - (void)greet;
  @end

  @interface Person : NSObject <Greetable>
  @end

  @implementation Person
  - (void)greet {
      NSLog(@"Hello!");
  }
  @end
  ```

### 6. 错误处理

- **Swift**：提供了现代化的错误处理机制，通过 `do-catch` 语句处理错误。
  ```swift
  enum FileError: Error {
      case fileNotFound
  }

  func readFile() throws {
      throw FileError.fileNotFound
  }

  do {
      try readFile()
  } catch {
      print("Error: \(error)")
  }
  ```
- **Objective-C**：使用 `NSError` 和 `@try-@catch` 进行错误处理，较为繁琐。
  ```objc
  NSError *error = nil;
  [self readFile:&error];
  if (error) {
      NSLog(@"Error: %@", error);
  }
  ```

### 7. 访问控制

- **Swift**：提供了更细粒度的访问控制，包括 `open`、`public`、`internal`、`fileprivate` 和 `private`。
  ```swift
  public class PublicClass {}
  private class PrivateClass {}
  ```
- **Objective-C**：访问控制较为简单，主要通过 `@public`、`@protected` 和 `@private` 来控制。
  ```objc
  @interface MyClass : NSObject {
  @private
      int privateVar;
  @protected
      int protectedVar;
  @public
      int publicVar;
  }
  @end
  ```

### 8. 集成和互操作性

- **Swift**：可以与 Objective-C 无缝互操作，允许在同一个项目中混合使用两种语言。
  ```swift
  // 使用 Objective-C 类
  let obj = MyClass()
  obj.someMethod()
  ```
- **Objective-C**：可以调用 Swift 代码，但需要一些桥接和配置。
  ```objc
  // 使用 Swift 类
  MyClass *obj = [[MyClass alloc] init];
  [obj someMethod];
  ```

### 总结

Swift 是一种现代化的编程语言，设计理念更加注重安全性、可读性和开发效率，而 Objective-C 作为一种较为传统的语言，虽然功能强大，但语法相对复杂。Swift 的出现和普及极大地提升了 iOS 和 macOS 开发的效率和体验。



# OC中Block的概念


在Objective-C中，Block是一种特殊的数据类型，它可以封装一段代码，这段代码可以在任何时候执行，或者作为方法的参数传递。Block可以捕获和存储其周围的任何局部变量的值。

Block的基本语法如下：

```objective-c
returnType (^blockName)(parameterTypes) = ^returnType(parameters) {...};
```

例如，一个没有参数和返回值的Block可以这样定义：

```objective-c
void (^simpleBlock)(void) = ^{
    NSLog(@"This is a block");
};
```

然后，你可以像调用函数一样调用Block：

```objective-c
simpleBlock(); // 输出 "This is a block"
```

Block在Objective-C中的使用非常广泛，例如在动画、排序操作、并发编程等场景中。

---
# 常量
在Objective-C中，你可以在类的实现文件外部声明一个全局常量。以下是如何声明一个全局字符串常量的示例：

在你的.h文件中，你可以声明一个extern常量：

```objective-c
// MyClass.h
extern NSString * const MyConstant;
```

然后，在你的.m文件中，你可以定义这个常量：

```objective-c
// MyClass.m
NSString * const MyConstant = @"MyConstantValue";
```

在这个例子中，`MyConstant`是一个全局的NSString常量，它的值是`MyConstantValue`。因为它是一个const常量，所以你不能改变它的值。

你可以在你的项目的任何地方使用这个常量，只要包含了它的声明。例如，你可以在其他类中使用`MyConstant`，只要在那个类的文件中导入了`MyClass.h`。

---
# OC中实现超时处理

## 1.GCD与信号量

在Objective-C中，你可以使用GCD（Grand Central Dispatch）来实现方法的超时处理。以下是一个示例：

```objective-c
dispatch_queue_t queue = dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0);
dispatch_semaphore_t semaphore = dispatch_semaphore_create(0);

dispatch_async(queue, ^{
    // 在这里调用你的方法
    [self yourMethod];

    // 当你的方法完成后，发送一个信号
    dispatch_semaphore_signal(semaphore);
});

// 等待你的方法完成或者超时
long timeoutResult = dispatch_semaphore_wait(semaphore, dispatch_time(DISPATCH_TIME_NOW, 5.0 * NSEC_PER_SEC));

if (timeoutResult == 0) {
    // 在超时时间内你的方法已经完成
} else {
    // 你的方法在超时时间内未完成，执行超时处理
}
```

在上述代码中，我们首先创建了一个全局队列和一个信号量。然后，我们在全局队列中异步执行你的方法，并在方法完成后发送一个信号。最后，我们等待信号或者超时。如果在超时时间内收到了信号，那么你的方法已经完成。如果在超时时间内未收到信号，那么你的方法未在超时时间内完成，我们可以执行超时处理。

## 2.performSelector延时函数

```Objective-C
[self performSelector:@selector(timeOut) withObject:nil afterDelay:10]; // 设置一个延时函数

 // 取消超时效果
 [NSObject cancelPreviousPerformRequestsWithTarget:self selector:@selector(timeOut) object:nil];
```

---
# OC中添加swift

## 在OC文件中添加UIKit或者swiftUI视图

1. 在工程中创建一个swift文件（选择自动生成头文件）；
2.  创建一个继承自 `UIViewController` 的 Swift 视图控制器类。
```swift
import UIKit
 
class MySwiftViewController: UIViewController {
    override func viewDidLoad() {
        super.viewDidLoad()
        // 设置UI
    }
}

```

3. 在 Objective-C 中使用这个 Swift 视图控制器。首先，确保你的 Objective-C 类头文件包含以下内容：
```Objc
#import <UIKit/UIKit.h>
#import "ProductModuleName-Swift.h"
 
@interface MyObjectiveCViewController : UIViewController
@end

```

其中 `ProductModuleName-Swift.h` 是自动生成的头文件，它允许 Objective-C 代码导入并访问 Swift 代码。`ProductModuleName` 是你的项目的模块名，通常与你的项目名称相同。

4.  在 Objective-C 视图控制器中，你现在可以实例化并推送 Swift 视图控制器：
```Objc
@implementation MyObjectiveCViewController
 
- (void)someMethodToPresentSwiftViewController {
    MySwiftViewController *swiftViewController = [[MySwiftViewController alloc] init];
    [self presentViewController:swiftViewController animated:YES completion:nil];
}
 
@end

```

或者使swift视图充满整个屏幕(可以将其当作ContentView)
```objc
#import "ViewController.h"

@interface ViewController ()

@end

@implementation ViewController

  

- (void)viewDidLoad {

    [super viewDidLoad];

    // Do any additional setup after loading the view.

    SwiftUIViewController *swiftUIViewController = [[SwiftUIViewController alloc] init];

    [self addChildViewController:swiftUIViewController];

    [self.view addSubview:swiftUIViewController.view];

    swiftUIViewController.view.frame = self.view.bounds;

    [swiftUIViewController didMoveToParentViewController:self];

}

@end
```

5. 现在你可以自由的修改你的swiftUI视图或UIKit的ViewController了

==OC中将某个VC充满父视图==
```objc
    SwiftUIViewController *swiftUIViewController = [[SwiftUIViewController alloc] init];

    [self addChildViewController:swiftUIViewController];

    [self.view addSubview:swiftUIViewController.view];

    swiftUIViewController.view.frame = self.view.bounds;

    [swiftUIViewController didMoveToParentViewController:self];
```



## 使用swiftUI 文件

在Objective-C项目中使用Swift UI文件需要以下步骤：

1. 首先，你需要在你的Objective-C项目中创建一个新的Swift文件。当你创建新的Swift文件时，Xcode会询问你是否要创建一个名为“YourProjectName-Bridging-Header.h”的桥接头文件。你需要选择“Create Bridging Header”。

2. 然后，你可以在新创建的Swift文件中编写你的Swift UI代码。

3. 为了让Objective-C代码能够访问你的Swift UI代码，你需要在Swift UI代码前添加`@objc`关键字，并且你的Swift UI代码需要继承自`NSObject`。例如：

```swift
import SwiftUI

@objc(MySwiftUIView)
class MySwiftUIView: NSObject {
    @objc
    func makeUIView(context: Context) -> UIView {
        let hostingController = UIHostingController(rootView: ContentView())
        return hostingController.view
    }
}
```

4. 然后，你可以在Objective-C代码中通过`MySwiftUIView`类来创建和使用你的Swift UI视图。例如：

```objective-c
#import "YourProjectName-Swift.h"

MySwiftUIView *swiftUIView = [[MySwiftUIView alloc] init];
UIView *view = [swiftUIView makeUIViewWithContext:nil];
[self.view addSubview:view];
```

注意，你需要将`YourProjectName`替换为你的项目名称。

# CGRectMake
`CGRectMake`是一个在Objective-C中用于创建CGRect结构的函数。CGRect是一个结构，用于描述一个矩形的位置和尺寸。

`CGRectMake`函数接受四个参数：x, y, width, height。其中，x和y定义了矩形左上角的位置，width和height定义了矩形的宽度和高度。

这是一个例子：

```objective-c
CGRect rect = CGRectMake(0, 0, 100, 100);
```

在这个例子中，我们创建了一个新的CGRect，其左上角位于(0,0)，宽度和高度都是100。
# OC 与swift

在Objective-C文件中直接编写Swift代码是不被允许的。Objective-C和Swift是两种不同的编程语言，它们有各自的语法规则和编译器。然而，你可以在同一个项目中同时使用Objective-C和Swift代码，这是通过Xcode提供的混编功能实现的。

如果你想在Objective-C项目中使用Swift代码，你可以按照以下步骤操作：

1. 在Xcode中，选择"File" -> "New" -> "File..."，然后选择"Swift File"，创建一个新的Swift文件。

2. 当你第一次添加Swift文件到Objective-C项目时，Xcode会询问你是否要创建一个名为"[YourProjectName]-Swift.h"的头文件。这个头文件是一个桥接文件，它让你可以在Objective-C代码中访问Swift代码。选择"Create Bridging Header"。

3. 在Swift文件中，你可以编写你的Swift代码。如果你想让这些代码可以在Objective-C中访问，你需要确保你的Swift类继承自Objective-C类，比如NSObject，或者你的Swift方法和属性被标记为@objc。

4. 在Objective-C文件中，你可以通过导入"[YourProjectName]-Swift.h"头文件，来访问Swift代码。

这是一个简单的示例：

Swift代码（在MySwiftClass.swift文件中）：

```swift
import Foundation

@objc class MySwiftClass: NSObject {
    @objc func greet() -> String {
        return "Hello from Swift!"
    }
}
```

Objective-C代码（在MyObjectiveCClass.m文件中）：

```objective-c
#import "MyProjectName-Swift.h"

@implementation MyObjectiveCClass

- (void)use

Swift

Class {
    MySwiftClass *mySwiftClass = [[MySwiftClass alloc] init];
    NSLog(@"%@", [mySwiftClass greet]);
}

@end
```

请注意，你需要将"MyProjectName"替换为你实际的项目名。

---

# OC 中的ScrollView

在Objective-C中，你可以使用以下步骤来设置一个ScrollView：

1. 首先，创建一个UIScrollView实例，并设置其大小和位置：

```objective-c
UIScrollView *scrollView = [[UIScrollView alloc] initWithFrame:CGRectMake(0, 0, self.view.frame.size.width, self.view.frame.size.height)];
```

2. 然后，设置UIScrollView的contentSize属性。这个属性决定了滚动视图可以滚动的区域：

```objective-c
scrollView.contentSize = CGSizeMake(self.view.frame.size.width, self.view.frame.size.height * 2);
```

3. 如果你想要UIScrollView有弹性滚动效果，你可以设置其alwaysBounceVertical和alwaysBounceHorizontal属性：

```objective-c
scrollView.alwaysBounceVertical = YES;
scrollView.alwaysBounceHorizontal = YES;
```

4. 最后，将UIScrollView添加到你的视图中：

```objective-c
[self.view addSubview:scrollView];
```

5. 如果你想在UIScrollView中添加视图，你可以创建一个视图，然后将其添加到UIScrollView中：

```objective-c
UIView *contentView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, scrollView.contentSize.width, scrollView.contentSize.height)];
[scrollView addSubview:contentView];
```

这样，你就创建了一个可以滚动的ScrollView，并在其中添加了一个视图

---
# UI布局

## 1.添加ScrollView避开NavigationBar

在添加UIScrollView时，如果你不希望它覆盖NavigationBar，你需要正确地设置UIScrollView的frame或者使用AutoLayout来设置其约束。

如果你使用frame来设置UIScrollView的位置和大小，你需要考虑到NavigationBar的高度。例如，你可以这样设置UIScrollView的frame：

```objective-c
CGFloat navigationBarHeight = self.navigationController.navigationBar.frame.size.height;
CGFloat statusBarHeight = [UIApplication sharedApplication].statusBarFrame.size.height;
UIScrollView *scrollView = [[UIScrollView alloc] initWithFrame:CGRectMake(0, navigationBarHeight + statusBarHeight, self.view.frame.size.width, self.view.frame.size.height - navigationBarHeight - statusBarHeight)];
[self.view addSubview:scrollView];
```

如果你使用AutoLayout来设置UIScrollView的位置和大小，你可以设置UIScrollView的顶部约束等于NavigationBar的底部。例如，你可以使用Masonry这样设置：

```objective-c
UIScrollView *scrollView = [[UIScrollView alloc] init];
[self.view addSubview:scrollView];
[scrollView mas_makeConstraints:^(MASConstraintMaker *make) {
    make.top.equalTo(self.mas_topLayoutGuideBottom);
    make.left.right.bottom.equalTo(self.view);
}];
```

注意，`mas_topLayoutGuideBottom`表示的是包括状态栏和导航栏在内的顶部布局指南的底部，所以这样设置可以确保UIScrollView不会覆盖NavigationBar。



```Objective-C
 make.left.right.bottom.mas_equalTo(0);
```

---

# 使用Xcode instrument查看方法占用时间

https://blog.csdn.net/ycf03211230/article/details/62429433

---

# OC检测类的方法

`isKindOfClass:` 是 Objective-C 中的一个方法，用于确定一个对象是否是一个特定类的实例，或者是那个类的子类的实例。

例如，如果你有一个 `NSObject` 对象 `object`，你可以这样检查它是否是 `NSString` 类的实例：

```objective-c
if ([object isKindOfClass:[NSString class]]) {
    // object 是 NSString 或其子类的实例
}
```

如果 `object` 是 `NSString` 或其子类的实例，那么这个表达式就会返回 `YES`。否则，它会返回 `NO`。

这种类型检查在处理动态类型的数据时非常有用，可以避免因为错误的类型而导致的运行时错误。

在 Objective-C 中，如果 `object` 是 `nil`，那么调用 `isKindOfClass:` 方法会返回 `NO`。

这是因为在 Objective-C 中，向 `nil` 发送任何消息都会返回 `0` 或 `nil`，并且不会引发异常。所以，如果 `object` 是 `nil`，`[object isKindOfClass:[SomeClass class]]` 将安全地返回 `NO`，而不会引发任何错误。

这是 Objective-C 的一种特性，使得在不进行显式的 `nil` 检查的情况下，代码仍然可以安全地运行。


---
# weakself
在 Objective-C 中，`WEAKSELF` 通常是一个宏，用于创建一个弱引用的 `self`，以避免在闭包或者 block 中产生循环引用。

循环引用是当两个或更多的对象互相持有对方的强引用，导致它们都不能被释放，从而造成内存泄漏。

`WEAKSELF` 的常见定义如下：

```objective-c
#define WEAKSELF typeof(self) __weak weakSelf = self;
```

然后在 block 或闭包中使用 `weakSelf` 代替 `self`：

```objective-c
WEAKSELF
[someObject someMethodWithCompletion:^{
    [weakSelf doSomething];
}];
```

在这个例子中，`weakSelf` 是对 `self` 的一个弱引用，即使 block 持有了 `weakSelf`，也不会增加 `self` 的引用计数。这样就避免了循环引用，当 `self` 应该被释放时，它可以被正确地释放。

在Objective-C中，`self`是当前对象的一个引用。当你在一个block中使用`self`时，block会创建一个对`self`的强引用。如果`self`同时也保持了对这个block的强引用（例如，你把这个block赋值给了`self`的一个属性），那么就会产生一个强引用循环，导致`self`和block都无法被释放，从而引发内存泄漏。

为了解决这个问题，我们通常会在block中使用`weak self`或者`__weak typeof(self) weakSelf`。这样，block就会创建一个对`self`的弱引用，不会增加`self`的引用计数。这样就可以避免强引用循环，即使`self`保持了对block的强引用，`self`也可以正常被释放。

然后在block内部，我们通常会使用`strongSelf`来创建一个对`weakSelf`的强引用，确保在block执行期间`self`不会被释放。这样做的一个常见模式是：

```objective-c
__weak typeof(self) weakSelf = self;
[self doSomethingWithCompletion:^{
    __strong typeof(self) strongSelf = weakSelf;
    if (strongSelf) {
        // 在这里使用 strongSelf
    }
}];
```

这样，即使`self`在block执行期间被其他代码释放，block内部的代码也可以正确执行，不会因为`self`被释放而导致崩溃。

---
# OC 语法
LeiZiKang: 解释这段代码- (void)setIsUpdateOta:(BOOL)isUpdateOta{

GitHub Copilot: 这段代码是 Objective-C 语言中的一个 setter 方法的定义。它用于设置一个名为 `isUpdateOta` 的布尔值属性。

这个方法接受一个布尔值参数 `isUpdateOta`，然后将其赋值给类的实例变量（通常是一个名为 `_isUpdateOta` 的实例变量）。

这段代码可能是这样的：

```objective-c
- (void)setIsUpdateOta:(BOOL)isUpdateOta{
    _isUpdateOta = isUpdateOta;
}
```

在这段代码中，`_isUpdateOta = isUpdateOta;` 这行代码将传入的参数 `isUpdateOta` 赋值给 `_isUpdateOta` 实例变量。这样，当你在其他地方使用 `isUpdateOta` 属性时，就会使用你设置的这个值。

LeiZiKang: 解释这段代码
[data isKindOfClass:[IDOCoreDeviceCheckFirmwareModel class]]

GitHub Copilot: 这段代码是 Objective-C 语言中的一个类型检查。它检查 `data` 对象是否是 `IDOCoreDeviceCheckFirmwareModel` 类的实例。

`isKindOfClass:` 是 Objective-C 中的一个方法，用于确定一个对象是否是一个特定类的实例，或者是那个类的子类的实例。

如果 `data` 是 `IDOCoreDeviceCheckFirmwareModel` 类的实例，或者是 `IDOCoreDeviceCheckFirmwareModel` 的子类的实例，那么这个表达式就会返回 `YES`。否则，它会返回 `NO`。

这种类型检查在处理动态类型的数据时非常有用，可以避免因为错误的类型而导致的运行时错误。

LeiZiKang: 解释这串代码
+ (void)checkFirmwareVersionWithParameter:(NSDictionary *)parameter andBlock:(void(^)(NSInteger resultCode, id data))block {
    IDOCoreDeviceCheckFirmwareReq *req = [[IDOCoreDeviceCheckFirmwareReq alloc]init];
    req.mac = [parameter objectForKey:@"mac"];
    req.language = [parameter objectForKey:@"language"];
    req.otaVersion = [parameter objectForKey:@"otaVersion"];
    req.deviceName = [parameter objectForKey:@"deviceName"];
    req.type = [parameter objectForKey:@"type"];
    req.phoneModel = [IDORouterCore handleOpenURLStr:@"IDOCorePlatform://data/IDOVFDevice/getPhoneMobile"];
    req.deviceId = [parameter objectForKey:@"deviceId"];
    req.appVersion = APPVERSION;
    
   // req.mainURL = @"http://8.129.184.121:8091";//测试环境
    req.session.requestSerializer = [AFJSONRequestSerializer serializer];
    [IDOHttpReq startHttpRequestWithReq:req success:^(IDOHttpRes *httpRes, id responseObject) {
        IDOCoreDeviceCheckFirmwareRes * res = (IDOCoreDeviceCheckFirmwareRes *) httpRes;
        IDOCoreDeviceCheckFirmwareModel * responsModel = res.returnValue;
        
        
        if (block) {
            block(0,responsModel);
        }
    } successReturnError:^(IDOHttpRes *httpRes, id resposeObject, NSString *status) {
        if (block) {
            block(1,nil);
        }
    } fail:^(NSError *error) {
        if (block) {
            block(2,nil);
        }
    }];
}

GitHub Copilot: 这段代码是 Objective-C 中的一个类方法，用于检查固件版本。它接受一个字典参数 `parameter` 和一个回调 `block`。

1. 首先，创建一个 `IDOCoreDeviceCheckFirmwareReq` 对象 `req`。

2. 然后，从 `parameter` 字典中获取各种参数并设置到 `req` 对象中。

3. `req.phoneModel` 是通过调用 `IDORouterCore` 的 `handleOpenURLStr:` 方法获取的。

4. `req.appVersion` 被设置为 `APPVERSION`，这可能是一个预定义的常量。

5. `req.session.requestSerializer` 被设置为一个 `AFJSONRequestSerializer` 的实例，这意味着请求将以 JSON 格式发送。

6. 然后，使用 `IDOHttpReq` 的 `startHttpRequestWithReq:success:successReturnError:fail:` 方法开始一个 HTTP 请求。这个方法接受一个请求对象 `req` 和三个回调：成功回调、成功但返回错误的回调、失败回调。

7. 在成功的回调中，它将响应对象转换为 `IDOCoreDeviceCheckFirmwareRes` 类型，并从中获取返回值 `returnValue`，然后将其作为参数调用 `block`。

8. 在成功但返回错误的回调和失败的回调中，它直接调用 `block`，并传入错误码和 `nil`。

LeiZiKang: 其中的data是什么？

GitHub Copilot: 在这段代码中，`data` 是一个回调函数 `block` 的参数。这个 `block` 函数在调用时会接收两个参数：一个是 `resultCode`，表示结果的状态码，另一个是 `data`，表示返回的数据。

在成功的回调中，`data` 被设置为 `responsModel`，这是 `IDOCoreDeviceCheckFirmwareRes` 对象的 `returnValue` 属性。这个 `returnValue` 属性可能包含了关于固件版本的信息。

在成功但返回错误的回调和失败的回调中，`data` 被设置为 `nil`，表示没有返回数据。

所以，`data` 的具体内容和类型取决于 HTTP 请求的结果和 `IDOCoreDeviceCheckFirmwareRes` 的 `returnValue` 属性。

LeiZiKang: OC中如何检测一个数不为空？

GitHub Copilot: 在 Objective-C 中，你可以使用 `nil` 来检查一个对象是否为空。但是，对于基本数据类型（如 int、float、double 等），它们不是对象，所以不能直接用 `nil` 来检查。

对于 NSNumber 对象，你可以这样检查：

```objective-c
NSNumber *number = ... // 你的数字
if (number != nil) {
    // number 不为空
}
```

对于基本数据类型，你需要自己定义什么是“空”。例如，你可能会认为 0 是“空”的：

```objective-c
int number = ... // 你的数字
if (number != 0) {
    // number 不为空
}
```

如果你想检查一个数不仅不为空，而且不为 0，你可以这样做：

```objective-c
NSNumber *number = ... // 你的数字
if (number != nil && [number intValue] != 0) {
    // number 不为空且不为 0
}
```

LeiZiKang: 解释isKindOfClass

GitHub Copilot: `isKindOfClass:` 是 Objective-C 中的一个方法，用于确定一个对象是否是一个特定类的实例，或者是那个类的子类的实例。

例如，如果你有一个 `NSObject` 对象 `object`，你可以这样检查它是否是 `NSString` 类的实例：

```objective-c
if ([object isKindOfClass:[NSString class]]) {
    // object 是 NSString 或其子类的实例
}
```

如果 `object` 是 `NSString` 或其子类的实例，那么这个表达式就会返回 `YES`。否则，它会返回 `NO`。

这种类型检查在处理动态类型的数据时非常有用，可以避免因为错误的类型而导致的运行时错误。

LeiZiKang: 如果object为nil呢？

GitHub Copilot: 在 Objective-C 中，如果 `object` 是 `nil`，那么调用 `isKindOfClass:` 方法会返回 `NO`。

这是因为在 Objective-C 中，向 `nil` 发送任何消息都会返回 `0` 或 `nil`，并且不会引发异常。所以，如果 `object` 是 `nil`，`[object isKindOfClass:[SomeClass class]]` 将安全地返回 `NO`，而不会引发任何错误。

这是 Objective-C 的一种特性，使得在不进行显式的 `nil` 检查的情况下，代码仍然可以安全地运行。

LeiZiKang: OC 中的WEAKSELF是什么？

GitHub Copilot: 在 Objective-C 中，`WEAKSELF` 通常是一个宏，用于创建一个弱引用的 `self`，以避免在闭包或者 block 中产生循环引用。

循环引用是当两个或更多的对象互相持有对方的强引用，导致它们都不能被释放，从而造成内存泄漏。

`WEAKSELF` 的常见定义如下：

```objective-c
#define WEAKSELF typeof(self) __weak weakSelf = self;
```

然后在 block 或闭包中使用 `weakSelf` 代替 `self`：

```objective-c
WEAKSELF
[someObject someMethodWithCompletion:^{
    [weakSelf doSomething];
}];
```

在这个例子中，`weakSelf` 是对 `self` 的一个弱引用，即使 block 持有了 `weakSelf`，也不会增加 `self` 的引用计数。这样就避免了循环引用，当 `self` 应该被释放时，它可以被正确地释放。

LeiZiKang: 解释这段代码：NSString *speed = [NSString stringWithFormat:@"%02ld'%02ld\"",(long)s/60,(long)s%60];

GitHub Copilot: 这段代码是在 Objective-C 中创建一个格式化的字符串 `speed`，表示以分钟和秒为单位的时间。

`NSString` 的 `stringWithFormat:` 方法用于创建一个格式化的字符串。它的参数是一个格式字符串和一系列变量，这些变量将被插入到格式字符串中。

在这个例子中，格式字符串是 `@"%02ld'%02ld\""`，其中 `%02ld` 是一个占位符，表示一个两位数的长整数，如果不足两位则前面补 0。

`(long)s/60` 和 `(long)s%60` 是两个表达式，分别计算 `s` 的分钟数和秒数。`s` 是以秒为单位的时间，`/60` 计算分钟数，`%60` 计算剩余的秒数。

所以，如果 `s` 是 125，那么 `speed` 将被设置为 `@"02'05\""`，表示 2 分钟 5 秒。

LeiZiKang: 解释这段代码
+ (NSString *)speedWithTime:(NSInteger)second distance:(CGFloat)distance{
   
    if (distance < 0.01) {
        return @"00'00\"";
    }
    else{
        /**< 转换成s/m */
        // 进行优化修改 DistanceCode已经过期
        NSInteger s = floor(second * [IDOSportUnitHelper distanceUnitScale] / distance);
        NSString *speed = [NSString stringWithFormat:@"%02ld'%02ld\"",(long)s/60,(long)s%60];
        if ([speed isEqualToString:@"0'0\""]) {
            return @"00'00\"";
        }
        /**< 最大配速为99‘99“ */
        if (speed.length > 6) {
            return @"99'59\"";
        }
        return speed;
    }
}


GitHub Copilot: 这段 Objective-C 代码定义了一个类方法 `speedWithTime:distance:`，用于计算并返回一个表示速度的字符串。速度是根据给定的时间（以秒为单位）和距离（可能是以米或英里为单位）计算的。

1. 如果距离小于 0.01（可能是为了避免除以零的错误），则返回速度为 "00'00\"".

2. 否则，计算速度（以秒/米为单位）。这里使用了 `floor` 函数和 `IDOSportUnitHelper` 的 `distanceUnitScale` 方法来进行单位转换。

3. 使用 `NSString` 的 `stringWithFormat:` 方法创建一个格式化的字符串，表示以分钟和秒为单位的速度。

4. 如果计算出的速度为 "0'0\"", 则返回 "00'00\"".

5. 如果速度的字符串长度大于 6（即超过 "99'59\""），则返回 "99'59\"".

6. 最后，如果没有触发以上任何条件，就返回计算出的速度。

这个方法可能用于运动或健身应用中，用于计算运动员的配速（即完成特定距离所需的时间）。

LeiZiKang: 配速是如何计算的？

GitHub Copilot: 配速通常是指在运动或健身活动中，完成特定距离所需的时间。它通常用于跑步、自行车骑行、游泳等活动，用于衡量运动员的速度。

配速的计算公式是：

```
配速 = 时间 / 距离
```

在这个公式中，时间通常以秒或分钟为单位，距离通常以米或公里为单位。所以，配速的单位通常是 "分钟/公里" 或 "秒/米"。

例如，如果一个跑步者跑了 10 公里，用时 50 分钟，那么他的配速就是 50 分钟 / 10 公里 = 5 分钟/公里。这意味着他每跑 1 公里需要 5 分钟的时间。

在你提供的代码中，配速是通过以下公式计算的：

```
配速 = 时间 * 距离单位比例 / 距离
```

这里的 "距离单位比例" 是通过 `IDOSportUnitHelper` 的 `distanceUnitScale` 方法获取的，可能是用于将距离从一种单位转换为另一种单位（例如，从米转换为公里）。

LeiZiKang: Xcode的模拟器iOS版本放在那个文件目录下？

GitHub Copilot: Xcode 的 iOS 模拟器的系统版本文件通常存放在以下目录：

```
~/Library/Developer/CoreSimulator/Profiles/Runtimes
```

在这个目录下，你可以看到各种 iOS 版本的模拟器文件，例如 "iOS 14.4.simruntime" 等。

请注意，"~" 符号代表你的用户主目录。你可以在 Finder 中按下 "Shift + Command + G"，然后输入上述路径来快速访问这个目录。

另外，这个路径可能会随着 Xcode 的版本变化，所以如果你找不到这个目录，可能需要检查你的 Xcode 版本或者在网上搜索最新的路径。

LeiZiKang: 解释这段代码 if (textField.text.length >= 8) {
        term ++ ;
        ruleSytle = ruleSytle | IDOPasswordRuleSytleLength; // 长度
    }

GitHub Copilot: 这段 Objective-C 代码是在检查一个文本字段（`textField`）的文本长度是否大于或等于8。如果是，那么它会增加 `term` 的值，并且更新 `ruleSytle` 的值。

1. `if (textField.text.length >= 8)`：这是一个条件判断，检查 `textField` 的文本长度是否大于或等于8。

2. `term ++ ;`：如果上述条件为真，那么 `term` 的值会增加1。这可能是在计数满足某些条件的项的数量。

3. `ruleSytle = ruleSytle | IDOPasswordRuleSytleLength;`：这是一个位运算。`|` 是位或运算符，它会将 `ruleSytle` 和 `IDOPasswordRuleSytleLength` 的每一位进行或运算。这通常用于设置或更新位标志。在这个例子中，它可能是在设置 `ruleSytle` 的 "长度" 标志。

`IDOPasswordRuleSytleLength` 是一个预定义的常量，可能在枚举 `IDOPasswordRuleSytle` 中定义，用于表示密码规则的不同样式。在这个例子中，它可能表示密码需要满足的最小长度。

LeiZiKang: &&

GitHub Copilot: 在 Objective-C（以及许多其他编程语言）中，`&&` 是逻辑与运算符。它用于连接两个布尔表达式，如果且仅当这两个表达式都为 `true` 时，整个表达式的结果才为 `true`。

例如：

```objective-c
if (a > 0 && b > 0) {
    // 如果 a 和 b 都大于 0，那么这个代码块会被执行
}
```

在这个例子中，只有当 `a` 和 `b` 都大于 0 时，`if` 语句的条件才为 `true`，所以只有在这种情况下，`if` 语句的代码块才会被执行。

值得注意的是，`&&` 运算符具有短路行为。也就是说，如果左边的表达式为 `false`，那么整个表达式的结果就已经可以确定为 `false`，右边的表达式就不会被计算。这可以用于避免在右边的表达式中可能出现的错误，例如除以零或者访问 `nil` 对象。

LeiZiKang: 或

GitHub Copilot: 在 Objective-C（以及许多其他编程语言）中，`||` 是逻辑或运算符。它用于连接两个布尔表达式，如果这两个表达式中至少有一个为 `true`，那么整个表达式的结果就为 `true`。

例如：

```objective-c
if (a > 0 || b > 0) {
    // 如果 a 或 b 至少有一个大于 0，那么这个代码块会被执行
}
```

在这个例子中，只要 `a` 或 `b` 中至少有一个大于 0，`if` 语句的条件就为 `true`，所以在这种情况下，`if` 语句的代码块会被执行。

值得注意的是，`||` 运算符具有短路行为。也就是说，如果左边的表达式为 `true`，那么整个表达式的结果就已经可以确定为 `true`，右边的表达式就不会被计算。这可以用于避免在右边的表达式中可能出现的错误，例如除以零或者访问 `nil` 对象。

LeiZiKang: oc如何在一个NSObject类中写一个方法？

GitHub Copilot: 在 Objective-C 中，你可以在 `NSObject` 类或其子类中定义方法。以下是一个简单的例子：

```objective-c
#import <Foundation/Foundation.h>

@interface MyObject : NSObject

- (void)myMethod;

@end

@implementation MyObject

- (void)myMethod {
    NSLog(@"This is my method!");
}

@end
```

在这个例子中，我们首先定义了一个 `MyObject` 类，它是 `NSObject` 的子类。然后我们在 `MyObject` 类的接口部分（`@interface` 和 `@end` 之间）声明了一个方法 `myMethod`。

然后，在 `MyObject` 类的实现部分（`@implementation` 和 `@end` 之间），我们实现了 `myMethod` 方法。在这个方法中，我们使用 `NSLog` 函数打印一条消息。

你可以通过创建 `MyObject` 类的实例并调用 `myMethod` 方法来使用这个方法，如下所示：

```objective-c
MyObject *obj = [[MyObject alloc] init];
[obj myMethod];  // 输出 "This is my method!"
```

LeiZiKang: 如何写一个带输入参数的函数呢？

GitHub Copilot: 在 Objective-C 中，你可以在方法声明和实现中包含输入参数。以下是一个带有输入参数的方法的例子：

```objective-c
#import <Foundation/Foundation.h>

@interface MyObject : NSObject

- (void)greetWithName:(NSString *)name;

@end

@implementation MyObject

- (void)greetWithName:(NSString *)name {
    NSLog(@"Hello, %@", name);
}

@end
```

在这个例子中，`greetWithName:` 方法接受一个 `NSString` 类型的参数 `name`。在方法的实现中，我们使用 `NSLog` 函数和格式化字符串来打印一条包含 `name` 的消息。

你可以通过创建 `MyObject` 类的实例并调用 `greetWithName:` 方法来使用这个方法，如下所示：

```objective-c
MyObject *obj = [[MyObject alloc] init];
[obj greetWithName:@"World"];  // 输出 "Hello, World"
```

LeiZiKang: 如何写一个OC的基础方法？请展示

GitHub Copilot: 在 Objective-C 中，你可以在类的定义中声明和实现方法。以下是一个基础方法的例子：

```objective-c
#import <Foundation/Foundation.h>

@interface MyObject : NSObject

- (void)basicMethod;

@end

@implementation MyObject

- (void)basicMethod {
    NSLog(@"This is a basic method in Objective-C.");
}

@end
```

在这个例子中，我们首先定义了一个 `MyObject` 类，它是 `NSObject` 的子类。然后我们在 `MyObject` 类的接口部分（`@interface` 和 `@end` 之间）声明了一个方法 `basicMethod`。

然后，在 `MyObject` 类的实现部分（`@implementation` 和 `@end` 之间），我们实现了 `basicMethod` 方法。在这个方法中，我们使用 `NSLog` 函数打印一条消息。

你可以通过创建 `MyObject` 类的实例并调用 `basicMethod` 方法来使用这个方法，如下所示：

```objective-c
MyObject *obj = [[MyObject alloc] init];
[obj basicMethod];  // 输出 "This is a basic method in Objective-C."
```

LeiZiKang: 在其中写一个输入字符串打印的函数

GitHub Copilot: 在 Objective-C 中，你可以创建一个接受字符串输入并打印的方法。以下是一个例子：

```objective-c
#import <Foundation/Foundation.h>

@interface MyObject : NSObject

- (void)printString:(NSString *)inputString;

@end

@implementation MyObject

- (void)printString:(NSString *)inputString {
    NSLog(@"%@", inputString);
}

@end
```

在这个例子中，`printString:` 方法接受一个 `NSString` 类型的参数 `inputString`。在方法的实现中，我们使用 `NSLog` 函数来打印 `inputString`。

你可以通过创建 `MyObject` 类的实例并调用 `printString:` 方法来使用这个方法，如下所示：

```objective-c
MyObject *obj = [[MyObject alloc] init];
[obj printString:@"Hello, World!"];  // 输出 "Hello, World!"
```

LeiZiKang: OC的.m和.h文件是用来干嘛的？

GitHub Copilot: 在 Objective-C 中，`.h` 和 `.m` 文件是用来组织和定义类的。

1. `.h` 文件：这是头文件，通常用来声明类的接口。这包括类的属性（variables）、方法（functions）和任何需要公开的信息。头文件是公开的，可以被其他类引用和使用。

例如：

```objective-c
// MyObject.h
#import <Foundation/Foundation.h>

@interface MyObject : NSObject

- (void)myMethod;

@end
```

2. `.m` 文件：这是实现文件，通常用来实现类的方法。这是类的主体部分，包含了类的具体逻辑和行为。

例如：

```objective-c
// MyObject.m
#import "MyObject.h"

@implementation MyObject

- (void)myMethod {
    NSLog(@"This is my method!");
}

@end
```

在这个例子中，`MyObject.h` 文件声明了 `MyObject` 类和一个方法 `myMethod`。然后在 `MyObject.m` 文件中，我们实现了 `myMethod` 方法。

LeiZiKang: 如何设置返回值

GitHub Copilot: 在 Objective-C 中，你可以在方法声明和实现中指定返回值类型。以下是一个返回字符串的方法的例子：

```objective-c
#import <Foundation/Foundation.h>

@interface MyObject : NSObject

- (NSString *)getGreeting;

@end

@implementation MyObject

- (NSString *)getGreeting {
    return @"Hello, World!";
}

@end
```

在这个例子中，`getGreeting` 方法的返回类型是 `NSString *`，表示这个方法会返回一个字符串。在方法的实现中，我们使用 `return` 语句来返回一个字符串。

你可以通过创建 `MyObject` 类的实例并调用 `getGreeting` 方法来获取返回值，如下所示：

```objective-c
MyObject *obj = [[MyObject alloc] init];
NSString *greeting = [obj getGreeting];
NSLog(@"%@", greeting);  // 输出 "Hello, World!"
```

在这个例子中，`getGreeting` 方法的返回值被赋值给了 `greeting` 变量，然后我们使用 `NSLog` 函数来打印 `greeting`。

LeiZiKang: 如何设置两个返回值？

GitHub Copilot: 在 Objective-C 中，方法只能有一个返回值。但是，如果你需要返回多个值，你可以使用以下几种方法：

1. 使用指针参数：你可以将需要返回的额外值作为方法的指针参数。在方法内部，你可以通过这些指针参数来修改它们的值。

```objective-c
#import <Foundation/Foundation.h>

@interface MyObject : NSObject

- (void)getTwoValues:(int *)value1 value2:(int *)value2;

@end

@implementation MyObject

- (void)getTwoValues:(int *)value1 value2:(int *)value2 {
    *value1 = 10;
    *value2 = 20;
}

@end
```

使用方法：

```objective-c
MyObject *obj = [[MyObject alloc] init];
int value1, value2;
[obj getTwoValues:&value1 value2:&value2];
NSLog(@"value1: %d, value2: %d", value1, value2);  // 输出 "value1: 10, value2: 20"
```

2. 使用数组或字典：你可以将需要返回的值放入一个数组或字典中，然后返回这个数组或字典。

```objective-c
#import <Foundation/Foundation.h>

@interface MyObject : NSObject

- (NSArray *)getTwoValues;

@end

@implementation MyObject

- (NSArray *)getTwoValues {
    return @[@10, @20];
}

@end
```

使用方法：

```objective-c
MyObject *obj = [[MyObject alloc] init];
NSArray *values = [obj getTwoValues];
NSLog(@"value1: %@, value2: %@", values[0], values[1]);  // 输出 "value1: 10, value2: 20"
```

LeiZiKang: 如何返回一个NSdinc

GitHub Copilot: 在 Objective-C 中，你可以返回一个 `NSDictionary` 对象。以下是一个例子：

```objective-c
#import <Foundation/Foundation.h>

@interface MyObject : NSObject

- (NSDictionary *)getPersonInfo;

@end

@implementation MyObject

- (NSDictionary *)getPersonInfo {
    return @{@"name": @"John Doe", @"age": @30};
}

@end
```

在这个例子中，`getPersonInfo` 方法返回一个 `NSDictionary` 对象，这个对象包含了两个键值对：`"name"` 和 `"age"`。

你可以通过创建 `MyObject` 类的实例并调用 `getPersonInfo` 方法来获取返回的 `NSDictionary` 对象，如下所示：

```objective-c
MyObject *obj = [[MyObject alloc] init];
NSDictionary *personInfo = [obj getPersonInfo];
NSLog(@"Name: %@, Age: %@", personInfo[@"name"], personInfo[@"age"]);  // 输出 "Name: John Doe, Age: 30"
```


---

# OC面向对象

Objective-C全面支持面向对象编程，包括面向对象开发的四大支柱 −

- 封装
- 数据隐藏
- 继承
- 多态性


---
# 排序

在Objective-C中，你可以使用NSArray的`sortedArrayUsingComparator:`方法来对数组进行排序。以下是一个示例，展示了如何使用这个方法来对一个NSNumber数组进行从小到大的排序：

```objective-c
NSArray *numbers = @[@3, @1, @2];
NSArray *sortedNumbers = [numbers sortedArrayUsingComparator:^NSComparisonResult(id  _Nonnull obj1, id  _Nonnull obj2) {
    if ([obj1 integerValue] > [obj2 integerValue]) {
        return NSOrderedDescending;
    } else if ([obj1 integerValue] < [obj2 integerValue]) {
        return NSOrderedAscending;
    } else {
        return NSOrderedSame;
    }
}];

NSLog(@"%@", sortedNumbers); // 输出: "(1, 2, 3)"
```

在这个示例中，`sortedArrayUsingComparator:`方法接收一个block作为参数。这个block接收两个参数，表示要比较的两个元素，然后返回一个NSComparisonResult值，表示这两个元素的排序关系。

如果你想对字符串数组进行字母顺序排序，你可以使用NSString的`compare:`方法，如下所示：

```objective-c
NSArray *strings = @[@"banana", @"apple", @"cherry"];
NSArray *sortedStrings = [strings sortedArrayUsingSelector:@selector(compare:)];

NSLog(@"%@", sortedStrings); // 输出: "(apple, banana, cherry)"
```

在这个示例中，`sortedArrayUsingSelector:`方法接收一个selector作为参数，这个selector表示用于比较元素的方法。`compare:`方法是NSString的一个方法，它可以用来按字母顺序比较字符串。

---

# IndexPath

`NSIndexPath` 是 iOS 开发中的一个类，用于在树形或者表格数据结构中标识特定的节点。在表格视图（`UITableView`）或者集合视图（`UICollectionView`）中，`NSIndexPath` 常常被用来标识特定的行或者项。

`NSIndexPath * indexPath` 是声明了一个指向 `NSIndexPath` 对象的指针变量 `indexPath`。这个 `indexPath` 变量可以用来存储一个 `NSIndexPath` 对象的内存地址。

在 `UITableView` 中，`NSIndexPath` 有两个重要的属性：`section` 和 `row`。`section` 表示当前的节点在哪一个分区（section），`row` 表示当前的节点是分区中的哪一行。通过这两个属性，我们可以精确地定位到表格中的任何一个单元格。

例如，你可以这样创建一个 `NSIndexPath` 对象，并访问它的 `section` 和 `row` 属性：

```objective-c
NSIndexPath *indexPath = [NSIndexPath indexPathForRow:0 inSection:0];
NSInteger section = indexPath.section;
NSInteger row = indexPath.row;
```

在这个例子中，`indexPath` 表示的是表格中第一个分区的第一行。

---
# `__kindof`

这两种写法的主要区别在于`__kindof`关键字的使用。

`+ (IDOSetPressureSwitchBluetoothModel *)currentModel;`这种写法表示`currentModel`方法返回一个`IDOSetPressureSwitchBluetoothModel`类型的对象。

而`+ (__kindof IDOSetPressureSwitchBluetoothModel *)currentModel;`这种写法表示`currentModel`方法返回一个`IDOSetPressureSwitchBluetoothModel`类型或其子类类型的对象。

`__kindof`关键字在Objective-C中被用来表示一个类型可能是一个类或其子类。这在处理集合或者返回值可能是多种类型的情况下非常有用。例如，如果你有一个返回`NSArray<__kindof UIView *> *`的方法，那么这个数组可以包含`UIView`的任何子类的对象。

总的来说，`__kindof`关键word提供了一种灵活的方式来处理可能是多种类型的情况，而不需要显式地进行类型转换。


---
# 属性修饰符

这两个属性的主要区别在于它们的内存管理策略，即`strong`和`copy`。

1. `@property (nonatomic,strong) NSArray<NSDictionary*>* future;`：这里使用了`strong`关键字，这意味着`future`属性将保持对赋给它的对象的强引用。这就是说，只要`future`属性存在，赋给它的对象就不会被销毁。

2. `@property (nonatomic,copy) NSArray<NSDictionary*>* future;`：这里使用了`copy`关键字，这意味着当你设置`future`属性时，它将创建赋给它的对象的一个副本，并保持对这个副本的强引用。这对于可变对象（如`NSMutableArray`）特别有用，因为即使原始对象改变了，`future`属性持有的副本仍然保持不变。

总的来说，你应该根据你的具体需求来选择使用`strong`还是`copy`。如果你想要保持对对象的引用，并且不需要保护自己免受原始对象改变的影响，那么你应该使用`copy`。如果你只是想要保持对对象的引用，那么你应该使用`strong`。

`strong`和`copy`都是Objective-C属性（property）的属性修饰符（property attribute）。它们用于指定Objective-C对象如何管理属性的内存。

- `strong`：这是默认的属性修饰符。当你创建一个属性并使用`strong`修饰符时，这个属性会保持对赋给它的对象的强引用。只要这个属性存在，那么这个对象就不会被销毁。这是实现对象所有权和内存管理的主要方式。

- `copy`：当你创建一个属性并使用`copy`修饰符时，这个属性会创建赋给它的对象的一个副本，并保持对这个副本的强引用。这对于可变对象（如`NSMutableString`或`NSMutableArray`）特别有用，因为即使原始对象改变了，属性持有的副本仍然保持不变。

这两个修饰符都是Objective-C自动引用计数（ARC）内存管理模型的一部分，它们帮助开发者管理对象的生命周期，避免内存泄漏和野指针。

---

oc 是一个运行时检测类型的语言，不是严格的类型安全语言，其类型在运行时判断而非在init时判断。


---

# OC的tableView

```objc
- (UITableViewCellEditingStyle)tableView:(UITableView *)tableView editingStyleForRowAtIndexPath:(NSIndexPath *)indexPath

{

    BaseCellModel * cellModel = nil;

    if (_model.is2dArray) {

        cellModel = _model.cellModels[indexPath.section][indexPath.row];

    }else {

        cellModel = _model.cellModels[indexPath.row];

    }

    if (cellModel.isDelete && !tableView.isEditing) {

        return UITableViewCellEditingStyleDelete;

    }else if (cellModel.isMoveRow) {

        return UITableViewCellEditingStyleNone;

    }

    return UITableViewCellEditingStyleNone;

}
```

这段代码是UITableView的代理方法，用于确定特定行的编辑样式。编辑样式决定了当表格视图处于编辑模式时，行的左侧应该显示什么样的控件（例如删除按钮或者插入按钮）。

以下是对这段代码的详细解释：

1. `BaseCellModel * cellModel = nil;`：定义一个名为`cellModel`的变量，类型为`BaseCellModel`，并初始化为`nil`。

2. `_model.is2dArray`：检查`_model`对象的`is2dArray`属性。如果`is2dArray`为`true`，则`cellModels`是一个二维数组，每个部分包含多行；如果`is2dArray`为`false`，则`cellModels`是一个一维数组，只包含行。

3. `cellModel.isDelete && !tableView.isEditing`：如果`cellModel`的`isDelete`属性为`true`，并且表格视图当前不处于编辑模式，那么返回`UITableViewCellEditingStyleDelete`，表示该行的编辑样式为删除。

4. `cellModel.isMoveRow`：如果`cellModel`的`isMoveRow`属性为`true`，那么返回`UITableViewCellEditingStyleNone`，表示该行没有特定的编辑样式。

5. `return UITableViewCellEditingStyleNone;`：如果以上所有条件都不满足，那么返回`UITableViewCellEditingStyleNone`，表示该行没有特定的编辑样式。

总的来说，这段代码根据`cellModel`的属性和表格视图的状态，决定了每一行的编辑样式。


---

# 使用MBProgressHUD来显示警告

在Objective-C中，你可以使用MBProgressHUD库来显示一个警告。以下是一个简单的示例：

```objective-c
#import "MBProgressHUD.h"

// 在你的方法中
MBProgressHUD *hud = [MBProgressHUD showHUDAddedTo:self.view animated:YES];
hud.mode = MBProgressHUDModeText;
hud.label.text = @"这是一个警告";
hud.offset = CGPointMake(0.f, MBProgressMaxOffset);
[hud hideAnimated:YES afterDelay:3.f];
```

在这个示例中，我们首先导入了MBProgressHUD库。然后，我们使用`showHUDAddedTo:animated:`方法在当前视图上创建并显示一个新的HUD。我们将HUD的模式设置为`MBProgressHUDModeText`，这意味着HUD只显示文本，没有任何其他的指示器。然后，我们设置HUD的文本为"这是一个警告"。我们将HUD的偏移量设置为`(0.f, MBProgressMaxOffset)`，这将使HUD显示在屏幕的底部。最后，我们使用`hideAnimated:afterDelay:`方法在3秒后隐藏HUD。

# 使用SVProgressHUD显示警告
要使用 SVProgressHUD 显示一个警告，你可以使用 `showErrorWithStatus:` 方法。这个方法接受一个字符串参数，这个字符串将作为错误信息显示在 HUD 上。例如：

```objective-c
[SVProgressHUD showErrorWithStatus:@"这是一个警告"];
```

这行代码将显示一个带有 "这是一个警告" 文本的错误 HUD。

---

# 播放音频

在Objective-C中，你可以使用AVFoundation框架来读取和播放MP3文件。以下是一个简单的例子：

首先，你需要在你的文件顶部导入AVFoundation框架：

```objective-c
#import <AVFoundation/AVFoundation.h>
```

然后，你可以创建一个AVAudioPlayer实例来读取和播放MP3文件：

```objective-c
NSError *error;
NSString *filePath = [[NSBundle mainBundle] pathForResource:@"yourfile" ofType:@"mp3"];
NSURL *fileURL = [NSURL fileURLWithPath:filePath];

AVAudioPlayer *audioPlayer = [[AVAudioPlayer alloc] initWithContentsOfURL:fileURL error:&error];

if (error) {
    NSLog(@"Error in audioPlayer: %@", [error localizedDescription]);
} else {
    [audioPlayer prepareToPlay];
    [audioPlayer play];
}
```

在这个例子中，`yourfile.mp3`应该是你的项目资源中的一个文件。如果你的MP3文件在其他位置，你需要提供正确的文件路径。

请注意，你需要在真实的设备上测试这个代码，因为模拟器可能无法播放音频。

在Objective-C中，你可以使用AVAudioPlayer的`pause`和`stop`方法来暂停和停止播放音频文件。

以下是如何暂停和停止音频播放的示例：

```objective-c
// 暂停播放
[audioPlayer pause];

// 停止播放
[audioPlayer stop];
```

请注意，`pause`方法会暂停音频播放，但不会改变播放位置，所以你可以随时调用`play`方法来恢复播放。而`stop`方法会停止播放并将播放位置重置为开始，所以如果你再次调用`play`方法，音频将从头开始播放。

如果你想在停止播放后从上次的位置继续播放，你应该使用`pause`方法而不是`stop`方法。


---

# 保存Userdefault

在Objective-C中，你可以使用NSUserDefaults类来存储简单的数据，如字符串。以下是如何将字符串存储到NSUserDefaults的示例：

```objective-c
NSString *yourString = @"This is a string";
NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];


[

defaults setObject:yourString forKey:@"MyStringKey"];
[defaults synchronize];
```

在这个例子中，`yourString`是你想要存储的字符串，`MyStringKey`是你用来检索这个字符串的键。`synchronize`方法是用来立即保存数据的，虽然在大多数情况下这不是必需的，因为iOS系统会定期自动保存NSUserDefaults中的数据，但是在某些情况下，你可能希望立即保存数据。

然后，你可以使用以下代码来检索你的字符串：

```objective-c
NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
NSString *myString = [defaults stringForKey:@"MyStringKey"];
```

如果没有找到对应的键，`stringForKey:`方法将返回nil。


# 在OC中定义全局文件来存储字符串

在Objective-C中，你可以创建一个头文件（﻿.h），在其中定义所有的全局字符串常量。

以下是一种可能的实现方式：

1. 创建一个新的头文件（如：﻿StringConstants.h）。
StringConstants.h：
```objc


  

#import <Foundation/Foundation.h>

  

extern NSString *const BackgroundTasks;

extern NSString *const AnotherStringConstant;

// 定义更多的字符串常量...
```

在这个文件中，我们使用﻿extern关键字声明了全局的字符串常量。这些常量在其他文件中都是可见的，但需要在一个﻿.m文件中进行定义和初始化。

2. 在对应的﻿.m文件中，定义并初始化这些常量。

﻿StringConstants.m：

  

```objc
#import "StringConstants.h"

  

NSString *const BackgroundTasks = @"后台任务";

NSString *const AnotherStringConstant = @"另一个字符串常量";

// 初始化更多的字符串常量...
```

3. 然后，在需要使用这些字符串常量的地方，导入﻿StringConstants.h头文件：

  
```objc

#import "StringConstants.h"

  

...

  

-   (void)yourMethod {

    NSLog(@"%@", BackgroundTasks);

}
```

注意，字符串的实际内容需要在﻿.m文件中定义，而不是在头文件中。头文件中只是声明了字符串的存在，而实际的内容是在﻿.m文件中赋值的。


# 字符串比较

在Objective-C中，字符串比较不能使用`==`运算符，因为`==`比较的是两个字符串的内存地址，而不是它们的内容。你应该使用`isEqualToString:`方法来比较两个字符串的内容。以下是修正后的代码：

```objective-c
NSString *currentVCName = NSStringFromClass([currentVC class]);

if ([currentVCName isEqualToString:@"CAMImagePickerCameraViewController"]) {
    // ...
}
```

在这段代码中，我们使用`isEqualToString:`方法来检查`currentVCName`是否等于`@"CAMImagePickerCameraViewController"`。如果等于，那么这个条件就会为真。