# ScrollerViewReader

你的代码中的问题在于，你试图在 `ScrollViewReader` 的 `content` 闭包中使用 `ScrollView`。然而，`ScrollViewReader` 的目的是允许你控制其内部的 `ScrollView` 的滚动位置，所以你应该将 `ScrollView` 放在 `ScrollViewReader` 的外部。

此外，你需要为你想要滚动到的视图设置一个 ID，然后你可以使用这个 ID 来滚动到这个视图。以下是修复后的代码：

```swift
ScrollView(.vertical, showsIndicators: false) {
    ScrollViewReader { proxy in
        VStack {
            // 系统信息模块
            // ...

            // 已接收文件模块
            // ...

            // 连接模块
            VStack {
                // ...
            }
            .id(bottomID) // 设置 ID
            .padding(.bottom, 20)
            .padding(.top, 20)
        }
        .onAppear(perform: {
            proxy.scrollTo(bottomID, anchor: .bottom) // 滚动到指定的 ID
        })
    }
}
```

在这个修复后的版本中，我们将 `ScrollView` 移动到了 `ScrollViewReader` 的外部，并为连接模块设置了一个 ID。然后，在 `onAppear` 方法中，我们使用 `proxy.scrollTo(_:anchor:)` 方法来滚动到连接模块。

---



---

# Text设置字体间距

在SwiftUI中，你可以使用`kerning`方法来设置字体间距。以下是一个例子：

```swift
Text("Hello, World!")
    .kerning(2) // 设置字体间距为2
```

在这个例子中，"Hello, World!"的字体间距被设置为2。你可以根据需要调整这个值。

---

# 自定义tabbar
https://blog.csdn.net/qqwyuli/article/details/126455895


---

# 自定义ViewModifer

在 SwiftUI 中，自定义 ﻿ViewModifier 可以用于封装常见的视图修饰符。使用 ﻿ViewModifier 可以简化代码和提高可重用性。下面我将示范如何创建和使用自定义的 ﻿ViewModifier。

**创建自定义 ViewModifier**

要创建一个自定义的 ﻿ViewModifier，需要遵循 ﻿ViewModifier 协议并实现其方法 ﻿body(content:)。你还可以增加自定义的属性来使修饰符更加灵活。

以下是一个示例，创建一个带有圆角、阴影和自定义背景颜色的修饰符。

  

```swift
import SwiftUI

  

// 定义自定义的 ViewModifier

struct CustomCardModifier: ViewModifier {

    var cornerRadius: CGFloat

    var shadowColor: Color

    var shadowRadius: CGFloat

    var backgroundColor: Color

  

    func body(content: Content) -> some View {

        content

            .padding()

            .background(backgroundColor)

            .cornerRadius(cornerRadius)

            .shadow(color: shadowColor, radius: shadowRadius)

    }

}

  

extension View {

    // Helper 方法，方便使用自定义的 ViewModifier

    func customCardModifier(cornerRadius: CGFloat = 10, shadowColor: Color = .black, shadowRadius: CGFloat = 5, backgroundColor: Color = .white) -> some View {

        self.modifier(CustomCardModifier(cornerRadius: cornerRadius, shadowColor: shadowColor, shadowRadius: shadowRadius, backgroundColor: backgroundColor))

    }

}
```

**使用自定义 ViewModifier**

你可以通过 .modifier 或定义的 helper 方法来使用自定义的 ﻿ViewModifier。以下是示例代码：

  

```swift
import SwiftUI

  

struct ContentView: View {

    var body: some View {

        VStack {

            Text("Hello, World!")

                .customCardModifier(cornerRadius: 15, shadowColor: .gray, shadowRadius: 10, backgroundColor: .orange)

                .padding()

  

            Text("Another styled text")

                .customCardModifier(backgroundColor: .blue)

                .padding()

        }

    }

}

  

@main

struct MyApp: App {

    var body: some Scene {

        WindowGroup {

            ContentView()

        }

    }

}
```

**详细解读**

**1. 自定义** ﻿ViewModifier **结构体:**

1. 创建 ﻿CustomCardModifier 结构体并使其遵循 ﻿ViewModifier 协议。

2. 定义 ﻿cornerRadius, ﻿shadowColor, ﻿shadowRadius, ﻿backgroundColor 等属性来定制修饰符的行为。

3. 实现 ﻿body(content:) 方法，在这个方法中对视图进行修饰。

**2. 扩展** ﻿View**:**

1. 扩展 ﻿View 协议，添加一个方便使用的 ﻿customCardModifier 方法。

2. ﻿customCardModifier 方法内部调用 ﻿self.modifier(CustomCardModifier(...))，将修饰符应用到视图上。

**3. 在视图中使用自定义 ViewModifier:**

1. 在视图中使用 ﻿customCardModifier 对文本进行样式设置。

2. 通过指定不同的参数来灵活地自定义视图的外观。

自定义 ﻿ViewModifier 可帮助你封装和重用复杂的视图修改逻辑，提高代码的整洁性和维护性。

---

# SwiftUI 的视图



在 SwiftUI 中，没有与 UIKit 中的 `viewDidLoad` 直接对应的 API，因为 SwiftUI 的设计理念与 UIKit 不同。然而，你可以使用 `onAppear` 和 `onDisappear` 方法来实现类似的功能。

`onAppear` 方法会在视图即将出现在屏幕上时被调用，你可以在这里执行一些初始化操作。例如：

```swift
Text("Hello, World!")
    .onAppear {
        print("Text is about to appear.")
    }
```

`onDisappear` 方法会在视图即将从屏幕上消失时被调用，你可以在这里执行一些清理操作。例如：

```swift
Text("Hello, World!")
    .onDisappear {
        print("Text is about to disappear.")
    }
```

请注意，`onAppear` 和 `onDisappear` 只是在视图即将出现或消失时被调用，它们并不保证视图已经完全加载或卸载。在 SwiftUI 中，视图的生命周期是由框架管理的，你不需要（也不能）手动加载或卸载视图。

---

# NavifgationLink BUG

当在List中使用NavigationLinker时会出现，不能在每个cell中都放一个NavigationLink，不然swiftUI会识别不到。
https://www.jianshu.com/p/70d1123d5a66

---
# Combine与SwiftUI

是的，SwiftUI也采用了响应式编程的范式。

在SwiftUI中，UI是以声明式的方式来定义的，你只需要描述UI应该如何根据不同的状态进行显示，而不需要关心状态变化时如何更新UI。当状态变化时，SwiftUI会自动更新UI。

SwiftUI中的`@State`，`@Binding`，`@ObservedObject`，`@EnvironmentObject`等属性包装器都是响应式编程的一部分。它们允许你创建可观察的数据源，当这些数据源发生变化时，所有依赖这些数据源的UI都会自动更新。

例如，你可以创建一个`@State`变量，然后在UI中使用这个变量。当这个变量的值发生变化时，所有使用这个变量的UI都会自动更新。

总的来说，SwiftUI的设计理念是响应式的，它使得在Swift中进行响应式编程变得更加简单和直观。

---

# SwiftUI 视图占据整个 UIViewController，包括 navigationBar
如果你希望 SwiftUI 视图占据整个 UIViewController，包括 navigationBar，你可以将 SwiftUI 视图的 UIHostingController 设置为 UINavigationController 的 rootViewController。这样，SwiftUI 视图就会占据整个屏幕，包括 navigationBar 的区域。

以下是一个示例：

```swift
import SwiftUI

class YourViewController: UIViewController {
    override func viewDidLoad() {
        super.viewDidLoad()

        // 创建 SwiftUI 视图
        let swiftUIView = ContentView()

        // 创建承载 SwiftUI 视图的 UIHostingController
        let hostingController = UIHostingController(rootView: swiftUIView)

        // 创建 UINavigationController 并设置其 rootViewController
        let navigationController = UINavigationController(rootViewController: hostingController)

        // 添加为子视图控制器
        self.addChild(navigationController)

        // 添加视图并设置约束
        navigationController.view.translatesAutoresizingMaskIntoConstraints = false
        self.view.addSubview(navigationController.view)

        NSLayoutConstraint.activate([
            navigationController.view.leadingAnchor.constraint(equalTo: self.view.leadingAnchor),
            navigationController.view.trailingAnchor.constraint(equalTo: self.view.trailingAnchor),
            navigationController.view.topAnchor.constraint(equalTo: self.view.topAnchor),
            navigationController.view.bottomAnchor.constraint(equalTo: self.view.bottomAnchor)
        ])

        navigationController.didMove(toParent: self)
    }
}
```

在这个示例中，`ContentView` 是你的 SwiftUI 视图。你需要将其替换为你实际的 SwiftUI 视图。

---

在 Objective-C 中，你可以通过设置 UIViewController 的 navigationController 的 `navigationBarHidden` 属性为 `YES` 来隐藏导航栏。你可以在 `viewWillAppear:` 方法中设置这个属性，以确保每次视图出现时导航栏都会被隐藏。

以下是一个示例：

```objc
- (void)viewWillAppear:(BOOL)animated {
    [super viewWillAppear:animated];
    
    // 隐藏导航栏
    [self.navigationController setNavigationBarHidden:YES animated:animated];
}
```

如果你希望在视图消失时恢复导航栏，你可以在 `viewWillDisappear:` 方法中设置 `navigationBarHidden` 为 `NO`：

```objc
- (void)viewWillDisappear:(BOOL)animated {
    [super viewWillDisappear:animated];
    
    // 显示导航栏
    [self.navigationController setNavigationBarHidden:NO animated:animated];
}
```

这样，当你的视图出现时，导航栏会被隐藏，当你的视图消失时，导航栏会再次显示。


在 Swift 中，你可以使用类似的方式在 UIViewController 中设置 toolbar。以下是一个示例：

```swift
override func viewDidLoad() {
    super.viewDidLoad()
    
    // 显示 toolbar
    self.navigationController?.setToolbarHidden(false, animated: false)
    
    // 创建工具栏按钮
    let button1 = UIBarButtonItem(barButtonSystemItem: .add, target: self, action: #selector(button1Clicked))
    let button2 = UIBarButtonItem(barButtonSystemItem: .edit, target: self, action: #selector(button2Clicked))
    
    // 创建一个 flexible space，它会自动占据剩余的空间，将按钮推向右边
    let flexibleSpace = UIBarButtonItem(barButtonSystemItem: .flexibleSpace, target: nil, action: nil)
    
    // 设置工具栏按钮
    self.toolbarItems = [flexibleSpace, button1, button2]
}

@objc func button1Clicked() {
    // 处理 button1 的点击事件
}

@objc func button2Clicked() {
    // 处理 button2 的点击事件
}
```

在这个示例中，我们创建了两个工具栏按钮，并通过一个 flexible space 将它们推向右边。你可以根据你的需求调整这些按钮和 flexible space 的顺序和数量。


在 UIKit 中，你可以通过以下步骤在 UIViewController 中设置 toolbar：

1. 首先，确保你的 UIViewController 是 UINavigationController 的一部分，因为 toolbar 是 UINavigationController 提供的功能。

2. 然后，你可以通过设置 UINavigationController 的 `toolbarHidden` 属性为 `NO` 来显示 toolbar。

3. 最后，你可以通过设置 UIViewController 的 `toolbarItems` 属性来添加工具栏按钮（UIBarButtonItem）。

以下是一个示例：

```objc
- (void)viewDidLoad {
    [super viewDidLoad];
    
    // 显示 toolbar
    [self.navigationController setToolbarHidden:NO animated:NO];
    
    // 创建工具栏按钮
    UIBarButtonItem *button1 = [[UIBarButtonItem alloc] initWithBarButtonSystemItem:UIBarButtonSystemItemAdd target:self action:@selector(button1Clicked:)];
    UIBarButtonItem *button2 = [[UIBarButtonItem alloc] initWithBarButtonSystemItem:UIBarButtonSystemItemEdit target:self action:@selector(button2Clicked:)];
    
    // 创建一个 flexible space，它会自动占据剩余的空间，将按钮推向右边
    UIBarButtonItem *flexibleSpace = [[UIBarButtonItem alloc] initWithBarButtonSystemItem:UIBarButtonSystemItemFlexibleSpace target:nil action:nil];
    
    // 设置工具栏按钮
    self.toolbarItems = @[flexibleSpace, button1, button2];
}

- (void)button1Clicked:(id)sender {
    // 处理 button1 的点击事件
}

- (void)button2Clicked:(id)sender {
    // 处理 button2 的点击事件
}
```

在这个示例中，我们创建了两个工具栏按钮，并通过一个 flexible space 将它们推向右边。你可以根据你的需求调整这些按钮和 flexible space 的顺序和数量。


如果你希望按钮位于 navigationBar 的右边，你应该使用 `navigationItem.rightBarButtonItem` 属性，而不是 `toolbarItems`。以下是一个示例：

```swift
override func viewDidLoad() {
    super.viewDidLoad()
    
    // 创建导航栏按钮
    let button = UIBarButtonItem(barButtonSystemItem: .add, target: self, action: #selector(buttonClicked))
    
    // 设置导航栏右侧按钮
    self.navigationItem.rightBarButtonItem = button
}

@objc func buttonClicked() {
    // 处理 button 的点击事件
}
```

在这个示例中，我们创建了一个 UIBarButtonItem，并将其设置为 navigationItem 的右侧按钮。当你运行这段代码时，你会在 navigationBar 的右侧看到这个按钮。



---

在 Swift 中，没有宏（Macro）的概念，这是因为 Swift 设计者们认为宏在某些情况下可能会导致代码的混乱和不安全。然而，你可以使用 Swift 的其他特性来实现类似的功能。

例如，你可以使用全局常量来定义一些常用的值，这类似于在 C 或 Objective-C 中使用 `#define` 宏来定义常量。以下是一个示例：

```swift
let MyConstant = 42
```

你也可以使用函数来封装一些常用的代码，这类似于在 C 或 Objective-C 中使用宏来定义一些常用的代码片段。以下是一个示例：

```swift
func MyFunction() {
    // 在这里执行一些操作
}
```

如果你需要定义一些可以在编译时确定的值，你可以使用编译器标记（Compiler Flag）。你可以在你的项目设置中添加编译器标记，然后在代码中使用 `#if` 和 `#endif` 来根据这些标记执行不同的代码。以下是一个示例：

```swift
#if DEBUG
    print("Debug mode")
#else
    print("Release mode")
#endif
```

在这个示例中，如果你在你的项目设置中定义了 `DEBUG` 标记，那么 `print("Debug mode")` 将会被执行，否则 `print("Release mode")` 将会被执行。

在 Swift 中，你可以直接使用这个 Objective-C 类的方法，因为 Swift 和 Objective-C 是可以互操作的。你需要做的只是在你的 Swift 文件中导入你的项目的自动生成的头文件，然后你就可以像在 Objective-C 中一样使用这个类的方法了。

以下是一个示例：

```swift
import UIKit

// 请将 YourProjectName 替换为你的实际项目名称
import YourProjectName

class YourSwiftClass {
    func yourMethod() {
        let text = "Hello, world!"
        let width: CGFloat = 100
        let font = UIFont.systemFont(ofSize: 16)
        
        // 使用 IDODemoUtility 的方法
        let height = IDODemoUtility.getLabelheight(text, width: width, font: font)
        print(height)
    }
}
```

在这个示例中，我们首先导入了项目的自动生成的头文件，然后在 `yourMethod` 方法中使用了 `IDODemoUtility` 的 `getLabelheight:width:font:` 方法。

请注意，你需要将 `YourProjectName` 替换为你的实际项目名称。当你在 Objective-C 项目中添加 Swift 代码时，Xcode 会自动创建一个名为 `YourProjectName-Swift.h` 的头文件，你可以通过这个头文件在 Objective-C 代码中访问你的 Swift 代码。同样，当你在 Swift 代码中需要访问 Objective-C 代码时，你需要导入一个名为 `YourProjectName.h` 的头文件。

对于宏 `#define lang(key) [IDODemoUtility langWithKey:key]`，你可以在 Swift 中创建一个全局函数来实现类似的功能：

```swift
func lang(_ key: String) -> String {
    return IDODemoUtility.lang(withKey: key)
}
```

然后你就可以在你的 Swift 代码中像这样使用 `lang` 函数：

```swift
let text = lang("your_key")
```

---

# `.border` 和 `.overlay`

在 SwiftUI 中，`.border` 和 `.overlay` 都可以用来给视图添加额外的视觉效果，但它们的用途和效果是不同的。

`.border` 修饰符用于在视图的边缘添加一个边框。你可以指定边框的颜色和宽度。例如：

```swift
Text("Hello, World!")
    .border(Color.red, width: 2)
```

这会在文本视图周围添加一个红色的边框，边框的宽度是 2。

`.overlay` 修饰符则更为强大，它可以在视图的前面或者后面添加任何类型的视图。例如，你可以使用 `.overlay` 在一个图片上添加一个半透明的黑色矩形，以创建一个暗化的效果：

```swift
Image("example-image")
    .overlay(Rectangle().foregroundColor(.black).opacity(0.5))
```

在这个例子中，`Rectangle` 视图被添加到了图片的前面，然后我们使用 `.foregroundColor` 和 `.opacity` 修饰符来改变它的颜色和透明度。

总的来说，`.border` 是一种特殊的 `.overlay`，它添加的是一个固定的、在视图边缘的边框。而 `.overlay` 则可以添加任何类型的视图，这些视图可以位于原视图的前面或者后面。

## 边框

https://www.cnblogs.com/ZJT7098/p/17468224.html





在 SwiftUI 中，你不能直接在视图构建器中使用 `if` 语句。你需要使用三元运算符来根据条件选择不同的视图。这是一个修改后的例子：

```swift
ForEach(viewModel.selectedImages.indices, id: \.self) { index in
    Button {
        selected = index
        selectedImage = viewModel.selectedImages[index]
    } label: {
        Image(uiImage: viewModel.selectedImages[index])
            .resizable()
            .aspectRatio(contentMode: .fit)
            .frame(width: 100, height: 118)
            .padding(.all, 4)
    }
    .overlay(
        selectedImage == viewModel.selectedImages[index] ?
        RoundedRectangle(cornerRadius: 8).stroke(.purple, lineWidth: 1) : nil
    )
}
```

在这个例子中，如果 `selectedImage` 等于 `viewModel.selectedImages[index]`，我们就添加一个紫色的边框；否则，我们不添加任何东西（`nil`）。


在 SwiftUI 中，视图构建器（ViewBuilder）是一种特殊的函数，它可以让你在函数体中像在正常的 SwiftUI 视图中一样使用声明式语法来构建视图。视图构建器可以返回一个或多个视图，并且可以根据条件动态地决定返回哪些视图。

例如，下面的代码定义了一个接受一个布尔值和两个视图作为参数的函数。这个函数会根据布尔值的值返回不同的视图：

```swift
@ViewBuilder
func conditionalView(showRed: Bool, redView: some View, blueView: some View) -> some View {
    if showRed {
        redView
    } else {
        blueView
    }
}
```

你可以像这样使用这个函数：

```swift
conditionalView(showRed: true, redView: Text("Red").foregroundColor(.red), blueView: Text("Blue").foregroundColor(.blue))
```

在这个例子中，因为 `showRed` 是 `true`，所以 `conditionalView` 函数会返回 `redView`。

视图构建器可以处理各种复杂的视图构建逻辑，包括条件语句、循环和嵌套的视图。这使得你可以在函数中使用和在正常的 SwiftUI 视图中一样的声明式语法来构建视图。

---

# swiftUI的视图构建器`ViewBuilder`

SwiftUI 的视图构建器（ViewBuilder）是一个特殊的函数或闭包，它可以让你在函数或闭包中使用声明式的语法来构建和返回一个视图。视图构建器通过将多个视图组合成一个复合视图，使得 SwiftUI 的语法更加简洁和易读。

例如，你可以使用视图构建器来创建一个包含多个文本视图的垂直堆栈：

```swift
VStack {
    Text("Hello, world!")
    Text("This is a SwiftUI ViewBuilder example.")
}
```

在这个例子中，`VStack` 是一个接受视图构建器的函数。在 `{}` 中的代码就是一个视图构建器，它创建并返回了两个 `Text` 视图。

视图构建器可以嵌套使用，这使得你可以创建复杂的视图层次结构。例如，你可以在一个 `VStack` 中嵌套一个 `HStack`：

```swift
VStack {
    Text("Hello, world!")
    HStack {
        Text("This is a SwiftUI")
        Text("ViewBuilder example.")
    }
}
```

在这个例子中，`VStack` 和 `HStack` 都是接受视图构建器的函数，它们分别创建了垂直和水平的视图堆栈。

在 SwiftUI 中，视图构建器（ViewBuilder）是一种特殊的函数，它可以让你在函数体中像在正常的 SwiftUI 视图中一样使用声明式语法来构建视图。视图构建器可以返回一个或多个视图，并且可以根据条件动态地决定返回哪些视图。

例如，下面的代码定义了一个接受一个布尔值和两个视图作为参数的函数。这个函数会根据布尔值的值返回不同的视图：

```swift
@ViewBuilder
func conditionalView(showRed: Bool, redView: some View, blueView: some View) -> some View {
    if showRed {
        redView
    } else {
        blueView
    }
}
```

你可以像这样使用这个函数：

```swift
conditionalView(showRed: true, redView: Text("Red").foregroundColor(.red), blueView: Text("Blue").foregroundColor(.blue))
```

在这个例子中，因为 `showRed` 是 `true`，所以 `conditionalView` 函数会返回 `redView`。

视图构建器可以处理各种复杂的视图构建逻辑，包括条件语句、循环和嵌套的视图。这使得你可以在函数中使用和在正常的 SwiftUI 视图中一样的声明式语法来构建视图。

**在 SwiftUI 中，你不能直接在视图构建器中使用 `if` 语句。你需要使用三元运算符来根据条件选择不同的视图。**

---

# swiftUI的Group

在 SwiftUI 中，`Group` 是一种特殊的视图，它可以将多个视图组合在一起，但不会在屏幕上添加额外的视觉效果。这对于组织和重构代码非常有用，特别是当你需要在一个视图中包含多于 10 个子视图的时候（这是 SwiftUI 的限制）。

例如，以下代码创建了一个包含两个文本视图的组：

```swift
Group {
    Text("Hello, World!")
    Text("SwiftUI is awesome!")
}
```

在这个例子中，`Group` 视图包含了两个 `Text` 视图。这两个 `Text` 视图会按照它们在 `Group` 中的顺序显示在屏幕上。

请注意，`Group` 不会改变它的子视图的布局。它只是一个用来组织和包装视图的容器。如果你需要改变子视图的布局，你可以使用其他的容器视图，如 `HStack`、`VStack` 或 `ZStack`。

 Group内只能包含同类型的视图吗？

不，`Group` 可以包含任何类型的视图。`Group` 是一个非常灵活的容器，它可以包含任意数量和类型的子视图。这是一个例子：

```swift
Group {
    Text("Hello, World!")
    Button("Tap me") {
        print("Button tapped!")
    }
    Image("example-image")
}
```

在这个例子中，`Group` 包含了一个 `Text` 视图、一个 `Button` 视图和一个 `Image` 视图。这些视图可以是任何类型，不需要是相同的类型。

请注意，虽然 `Group` 可以包含任何类型的视图，但它不会改变它的子视图的布局。它只是一个用来组织和包装视图的容器。如果你需要改变子视图的布局，你可以使用其他的容器视图，如 `HStack`、`VStack` 或 `ZStack`。

---

# swiftUI的`ViewModifer`

为了提高代码的复用率，你可以将这个 `Button` 的样式封装为一个单独的 `ViewModifier` 或者一个自定义的 `ButtonStyle`。

以下是如何创建一个自定义的 `ViewModifier`：

```swift
struct CustomButtonModifier: ViewModifier {
    let isSelected: Bool

    func body(content: Content) -> some View {
        content
            .cornerRadius(8)
            .padding(.all, 4)
            .overlay(
                isSelected ?
                RoundedRectangle(cornerRadius: 8).stroke(Color.purple, lineWidth: 1) : nil
            )
            .padding(2)
    }
}
```

然后，你可以使用 `.modifier(_:)` 方法来应用这个 `ViewModifier`：

```swift
Button(action: {}) {
    Text("Button")
}.modifier(CustomButtonModifier(isSelected: true))
```

如果你想要更深入地自定义按钮的样式，你可以创建一个自定义的 `ButtonStyle`。这会让你能够控制按钮的所有样式，包括它的内容和行为。

---

# swiftUI自定义collectionView

两种技术方案：
1. 使用ScrollView与HStack
2. 使用ScrollView与LazyHStack
区别：
LazyHStack的 子视图是延时创建的，面对大量数据时表现更好。

在 SwiftUI 中，`List` 视图默认是垂直的，不能直接设置为横向的。如果你想创建一个横向的列表，你可以使用 `ScrollView` 和 `HStack`。

这是一个例子：

```swift
struct ContentView: View {
    var body: some View {
        ScrollView(.horizontal, showsIndicators: false) {
            HStack {
                ForEach(0..<10) { index in
                    Text("Item \(index)")
                        .frame(width: 100, height: 100)
                        .background(Color.red)
                        .cornerRadius(10)
                        .padding()
                }
            }
        }
    }
}
```

在这个例子中，我们创建了一个横向的 `ScrollView`，然后在其中添加了一个 `HStack`。`HStack` 中包含了多个 `Text` 视图，每个 `Text` 视图都有一个固定的宽度和高度，以及一个红色的背景。我们使用 `ForEach` 来创建这些 `Text` 视图，这样我们就得到了一个横向的列表。

请注意，`ScrollView` 和 `List` 在某些方面是不同的。例如，`List` 支持自动的行高计算和分隔线，而 `ScrollView` 则不支持。如果你需要这些功能，你可能需要使用 `UITableView` 或者 `UICollectionView`，并通过 `UIViewRepresentable` 来在 SwiftUI 中使用它们。



---

# `LazyVStack` 与 `LazyHStack`

在 SwiftUI 中，`LazyVStack` 是一个用于垂直排列其子视图的视图。它与 `VStack` 类似，但有一个重要的区别：`LazyVStack` 会延迟创建其子视图，直到它们即将显示在屏幕上。

这意味着如果你有一个包含大量行的 `LazyVStack`，并且这些行在初始加载时并未全部显示在屏幕上，那么 `LazyVStack` 只会创建显示在屏幕上的行。当用户滚动 `LazyVStack` 时，它会创建更多的行。这可以提高性能，特别是对于包含大量行的列表。

以下是一个 `LazyVStack` 的例子：

```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        ScrollView {
            LazyVStack {
                ForEach(0..<1000) { index in
                    Text("Row \(index)")
                }
            }
        }
    }
}
```

在这个例子中，我们创建了一个 `ScrollView` 和一个 `LazyVStack`。`LazyVStack` 包含 1000 行，但在初始加载时，只有显示在屏幕上的行会被创建。当用户滚动 `ScrollView` 时，`LazyVStack` 会创建更多的行。


## 使用`LazyHstavck` 创建`CollectionView`
todo:

## 使用`LazyVstack`创建`List`

在 SwiftUI 中，你可以使用 `@State` 属性来跟踪选中的行。然后，你可以在 `LazyVStack` 中的每一行添加一个点击事件，当用户点击一行时，更新选中的行。以下是一个例子：

```swift
import SwiftUI

struct ContentView: View {
    @State private var selectedRow: Int?

    var body: some View {
        ScrollView {
            LazyVStack {
                ForEach(0..<10) { index in
                    Text("Item \(index)")
                        .frame(maxWidth: .infinity)
                        .padding()
                        .background(self.selectedRow == index ? Color.blue : Color.white)
                        .onTapGesture {
                            self.selectedRow = index
                        }
                }
            }
        }
    }
}
```

在这个例子中，我们首先定义了一个 `@State` 属性 `selectedRow` 来跟踪选中的行。然后，我们创建了一个 `ScrollView` 和一个 `LazyVStack`。

在 `LazyVStack` 中，我们使用 `ForEach` 来创建每一行。每一行都是一个 `Text` 视图，显示了项的索引。

我们使用 `onTapGesture` 来添加一个点击事件。当用户点击一行时，我们更新 `selectedRow` 为这一行的索引。

我们使用 `background(self.selectedRow == index ? Color.blue : Color.white)` 来设置背景色。如果这一行是选中的行（即 `selectedRow` 等于这一行的索引），我们使用蓝色；否则，我们使用白色。

请注意，这个例子创建的是一个简单的滚动视图，它只支持单选。如果你需要支持多选，你需要使用一个集合来跟踪选中的行。

---


# 为button添加外框线

#SwiftUI
在 SwiftUI 中，你可以使用 `.border` 修饰符为 Button 添加外框线。这是一个例子：

```swift
Button(action: {
    print("Button tapped!")
}) {
    Text("Tap me")
}
.border(Color.red, width: 2)
```

在这个例子中，按钮有一个红色的外框线，线的宽度是 2。你可以根据需要更改颜色和宽度。

你可以使用一个状态变量来跟踪按钮是否被选中，然后根据这个状态变量来决定是否显示边框。这是一个例子：

```swift
struct ContentView: View {
    @State private var isSelected = false

    var body: some View {
        Button(action: {
            isSelected.toggle()
        }) {
            Text("Tap me")
        }
        .overlay(
            isSelected ? RoundedRectangle(cornerRadius: 10).stroke(Color.red, lineWidth: 2) : nil
        )
    }
}
```

在这个例子中，当按钮被点击时，`isSelected` 状态变量会切换它的值。然后，我们使用三元运算符来决定是否在按钮上添加一个边框。如果 `isSelected` 是 `true`，我们就添加一个红色的边框；否则，我们不添加任何东西（`nil`）。





---

# `.border`和`.overlay`

在 SwiftUI 中，`.border` 和 `.overlay` 都可以用来给视图添加额外的视觉效果，但它们的用途和效果是不同的。

`.border` 修饰符用于在视图的边缘添加一个边框。你可以指定边框的颜色和宽度。例如：

```swift
Text("Hello, World!")
    .border(Color.red, width: 2)
```

这会在文本视图周围添加一个红色的边框，边框的宽度是 2。

`.overlay` 修饰符则更为强大，它可以在视图的前面或者后面添加任何类型的视图。例如，你可以使用 `.overlay` 在一个图片上添加一个半透明的黑色矩形，以创建一个暗化的效果：

```swift
Image("example-image")
    .overlay(Rectangle().foregroundColor(.black).opacity(0.5))
```

在这个例子中，`Rectangle` 视图被添加到了图片的前面，然后我们使用 `.foregroundColor` 和 `.opacity` 修饰符来改变它的颜色和透明度。

总的来说，`.border` 是一种特殊的 `.overlay`，它添加的是一个固定的、在视图边缘的边框。而 `.overlay` 则可以添加任何类型的视图，这些视图可以位于原视图的前面或者后面。


---
# `#Preview`

## 在objc项目中使用Swift预览

SwiftUI Previews in Objective-C: Simplifying Interactive Interface DevelopmentSwiftUI Previews in Objective-C: Simplifying Interactive Interface Developmenthackernoon.comMaksym Sytyi@ze8c

SwiftUI offers a valuable tool for previewing your interactive interface in real-time. Let's look at how to integrate SwiftUI previews into your Objective-C project. You can also get good helpers that will make previewing easier. 

Helpers for displaying interactive Previews

First, create a wrapper for the UIViewController 


```swift
import SwiftUI

struct VCWrapper: UIViewControllerRepresentable {

private let vc: UIViewController

init(vc: UIViewController) {

self.vc = vc

}

func makeUIViewController(context: Context) -> UIViewController { vc }

func updateUIViewController(_ uiViewController: UIViewController, context: Context) {}
}
```


Then, create an extension for UIViewController for easy wrapper access.


```swift
import UIKit

extension UIViewController {

var preview: VCWrapper { VCWrapper(vc: self) }
}
```


Finally, add a new file, PreviewScene implementing the protocol PreviewProvider


```swift
import SwiftUI

struct PreviewScene: PreviewProvider {

static var previews: some View {

}
}
```


Project with Storyboard

Create a simple UIViewController in Storyboard and add a Storyboard ID to the UIViewController. 

ViewController.h


```objc
#import <UIKit/UIKit.h>

@interface ViewController : UIViewController

@property (weak, nonatomic) IBOutlet UILabel *switcherIndicator;

@end
```


ViewController.m


```objc
#import "ViewController.h"
#import <SwiftUI/SwiftUI.h>

@interface ViewController ()

@end

@implementation ViewController

- (void)viewDidLoad {

[super viewDidLoad];

}

- (IBAction)switchToggle:(id)sender {

UISwitch *switcher = sender;

self.switcherIndicator.text = switcher.isOn ? @"🟢" : @"🔴";
}

@end
```


ViewController in Stryboard

Add a line to PreviewScene to show a preview of the UIViewController from the Storyboard.

UIStoryboard(name: "Main", bundle: nil)

.instantiateViewController(identifier: "ViewController")

.preview

Project without Storyboard

Create a CustomVC without a Storyboard, just programmatically 

CustomVC.h


```objc
#import <UIKit/UIkit.h>

@interface CustomVC : UIViewController

@property UILabel *lbl;

@end
```


CustomVC.m


```objc
#import "CustomVC.h"
#import "UILib.h"

@interface CustomVC ()

@end

@implementation CustomVC

- (void)viewDidLoad {

[super viewDidLoad];

self.view.backgroundColor = [UIColor grayColor];

UIButton *btn = [UILib btn:30 y:100 caption:@"TapMe"];

[btn addTarget:self action:@selector(tapBtn) forControlEvents:UIControlEventTouchUpInside];

[self.view addSubview:btn];

self.lbl = [UILib label:160 y:100];

self.lbl.text = @"txt";

[self.view addSubview:self.lbl];
}

- (void)tapBtn {

self.lbl.text = @"ButtonTapped";
}

@end
```


Before adding a preview, you must add an import to {YourProjectName}-Bridging-Header.h, which is created when you first add a quick file to the project.


```objc
#import "CustomVC.h"

// Add this UIViewController to the PreviewScene

CustomVC()

.preview
```


Conclusion

SwiftUI preview integration provides various ways to improve your Objective-C development workflow. Whether you're working with storyboards or code, SwiftUI Preview offers a quick way to visualize UI changes without running the simulator.


查看原网页: https://hackernoon.com/swiftui-previews-in-objective-c-simplifying-interactive-interface-development
Cubox 链接: https://cubox.pro/my/card?id=7227573868116838159

其他方法：
https://ikyle.me/blog/2020/swiftui-previews-uikit-objc

---

# swiftUI的预览功能

SwiftUI的预览功能是通过Xcode的Canvas面板实现的。当你在Xcode中编辑SwiftUI视图时，Canvas面板会实时显示你的视图的预览。

在底层，SwiftUI预览使用了macOS的一种特性，叫做XPC（Cross-Process Communication）。XPC是一种允许不同进程之间通信的机制。在这种情况下，Xcode和预览进程是两个不同的进程。

当你在Xcode中编辑SwiftUI视图时，Xcode会将你的代码发送到预览进程。预览进程会编译和运行你的代码，然后将生成的视图渲染成图像。这个图像然后被发送回Xcode，并在Canvas面板中显示。

这种设计有几个优点。首先，由于预览是在一个单独的进程中运行的，所以即使你的代码有错误，也不会影响到Xcode。其次，由于预览进程可以独立于Xcode运行，所以你可以在编辑代码的同时查看预览，这使得开发过程更加流畅。

请注意，虽然我们可以理解这个过程的大致原理，但是具体的实现细节是Apple的专有信息，不公开的。

## 与flutter的热重载的对比

SwiftUI的预览功能和Flutter的热重载功能在某些方面是相似的，但在实现和目标上有所不同。

1. 目标：两者都旨在提高开发者的生产力，通过提供实时反馈来加速开发过程。SwiftUI的预览功能让开发者可以在Xcode中实时看到UI的变化，而Flutter的热重载功能让开发者可以在设备或模拟器上立即看到代码更改的效果。

2. 实现：两者的实现方式不同。SwiftUI的预览功能是通过XPC（跨进程通信）在一个单独的进程中运行预览，然后将渲染的图像发送回Xcode。而Flutter的热重载功能是通过在运行时替换旧的Dart代码来实现的，这需要Dart虚拟机的支持。

3. 范围：SwiftUI的预览功能主要用于预览UI，而Flutter的热重载功能可以应用于任何代码更改，包括UI和逻辑。

总的来说，虽然两者都提供了实时反馈，但SwiftUI的预览功能更侧重于UI设计，而Flutter的热重载功能更侧重于整体的开发过程。

---
