
# 简介

Swift 是由苹果公司开发的一种通用编程语言，首次发布于 2014 年 6 月 2 日。在苹果的年度开发者大会 WWDC（Worldwide Developers Conference）上，Swift 被正式介绍给开发者社区。  
  
Swift 设计的主要目标是提供一种现代、安全和高效的编程语言，替代 Objective-C 作为 iOS、macOS、watchOS 和 tvOS 应用开发的主要语言。以下是 Swift 的一些关键特性：  
  
### 关键特性  
1. **现代语法**：  
- Swift 具有简洁和易读的现代语法，借鉴了许多其他编程语言的优点，使得编写代码更加直观和高效。  
  
2. **类型安全和内存管理**：  
- Swift 是一种类型安全的语言，编译器会在编译时进行类型检查，防止类型错误。  
- Swift 使用自动引用计数（ARC）来管理内存，有效防止内存泄漏。  
  
3. **高性能**：  
- Swift 经过优化，能够生成高效的机器代码，性能接近或者超过 Objective-C。  
  
4. **互动式开发**：  
- Swift 提供了一个名为 Playground 的工具，允许开发者以互动方式编写和测试代码，实时查看结果。  
  
5. **安全性**：  
- Swift 通过强类型系统、可选类型（Optionals）和错误处理机制，减少了许多常见的编程错误，如空指针异常和数组越界。  
  
### 示例代码  
以下是一个简单的 Swift 程序示例，展示了基本的语法和功能：  
  
```swift  
import Foundation  
  
// 定义一个函数，计算两个整数的和  
func add(a: Int, b: Int) -> Int {  
return a + b  
}  
  
// 主程序入口  
let x = 5  
let y = 10  
print("x = \(x), y = \(y)")  
  
let sum = add(a: x, b: y)  
print("Sum: \(sum)")  
```  
  
在这个示例中，我们定义了一个函数 `add` 来计算两个整数的和，并在主程序中调用该函数，输出结果。  
  
### 使用场景  
Swift 主要用于以下场景：  
- iOS 应用开发  
- macOS 应用开发  
- watchOS 应用开发  
- tvOS 应用开发  
- 服务器端开发（通过 Swift on the server 项目）  
  
### 学习资源  
如果你对学习 Swift 感兴趣，可以参考以下资源：  
- [The Swift Programming Language](https://docs.swift.org/swift-book/)（官方书籍）  
- [Swift Playgrounds](https://www.apple.com/swift/playgrounds/)（互动学习工具）  
- [Hacking with Swift](https://www.hackingwithswift.com/)（社区资源）  
  
总的来说，Swift 是一门强大且现代的编程语言，适合苹果生态系统中的应用程序开发，同时也在不断扩展到其他领域。

---

# Swift的特性

## ARC
- **Swift**：
    
    - Swift 使用自动引用计数（Automatic Reference Counting, ARC）进行内存管理。
    - ARC 在编译时插入内存管理代码，因此在运行时没有额外的垃圾回收（Garbage Collection）开销。
    - ARC 的内存管理模型在很多情况下比垃圾回收更高效，但需要开发者注意避免循环引用。

## 函数是一等公民 && 闭包

Swift让我们可以像使用任何其他类型（例如字符串和整数）一样使用函数。这意味着你可以创建一个函数并将其赋给一个变量，使用该变量调用该函数，甚至将该函数作为参数传递给其他函数。
以这种方式使用的函数称为闭包，尽管它们的工作方式与函数类似，但它们的编写方式略有不同。

## 尾随语法

``` swift
import Foundation

  

func travel(action: (String) -> Void) {

}

  
travel { (str: String) in

}
```



---

# 集合

Sets are collections of values just like arrays, except they have two differences:  
集合是值的集合，就像数组一样，除了它们有两个区别：

1. Items aren’t stored in any order; they are stored in what is effectively a random order.  
    项目不是以任何顺序存储的;它们实际上是以随机顺序存储的。
2. No item can appear twice in a set; all items must be unique.  
    任何项都不能在一个集合中出现两次;所有项都必须是唯一的。

You can create sets directly from arrays, like this:  
你可以直接从数组中创建集合，像这样：

```swift
let colors = Set(["red", "green", "blue"])
```

When you look at the value of `colors` inside the playground output you’ll see it doesn’t match the order we used to create it. It’s not really a _random_ order, it’s just _unordered_ – Swift makes no guarantees about its order. Because they are unordered, you can’t read values from a set using numerical positions like you can with arrays.  
当你在playground输出中查看 `colors` 的值时，你会发现它与我们创建它的顺序不匹配。它不是一个真正的随机顺序，它只是无序的- Swift不保证它的顺序。因为它们是无序的，所以你不能像读数组那样使用数值位置从集合中读取值。

If you try to insert a duplicate item into a set, the duplicates get ignored. For example:  
如果尝试将重复项插入到集合中，则会忽略重复项。举例来说：

```swift
let colors2 = Set(["red", "green", "blue", "red", "blue"])
```

The final `colors2` set will still only include red, green, and blue once.  
最终 `colors2` 集仍将仅包括红色、绿色和蓝色一次。

### 为什么集合是无序的？
在Swift中，集合（`Set`）是无序的，其本质原因与其底层实现和设计目标有关。以下是一些关键点解释了为什么集合是无序的：

### 1. **底层数据结构**
集合通常使用哈希表（Hash Table）作为其底层数据结构。哈希表通过哈希函数将元素映射到一个位置（桶）上，以实现快速的插入、查找和删除操作。然而，哈希表中的元素并没有特定的顺序，因为它们的位置是由哈希值决定的，这些哈希值通常是不可预测的。

### 2. **集合的设计目标**
集合的主要设计目标是高效地检查元素是否存在、快速插入和删除元素。这些操作在哈希表中可以在平均情况下达到常数时间复杂度 \(O(1)\)。为了实现这些性能优势，集合放弃了对元素顺序的控制。

### 3. **哈希函数的不可预测性**
哈希函数将元素映射到哈希表中的位置，这个映射过程通常是不可预测的。即使对于相同的集合，不同的哈希函数实现或不同的哈希种子值（用于安全性和防止哈希冲突攻击）可能会导致元素在哈希表中的顺序不同。

### 4. **集合的定义**
集合的定义本身就强调了其无序性。集合是一种数学概念，表示一组不重复的元素，而不关心这些元素的顺序。因此，Swift的`Set`类型也遵循这一数学定义。

### 5. **性能优化**
为了实现高性能，集合在内部可能会对元素进行重新排列。这种重新排列是为了优化哈希表的性能，例如减少冲突和优化内存布局。这种优化进一步导致了集合的无序性。

### 示例代码

以下是一个简单的示例，展示了集合的无序性：

```swift
var set: Set<Int> = [1, 2, 3, 4, 5]

for element in set {
    print(element)
}

// 可能的输出顺序不固定，例如：
// 3
// 1
// 5
// 2
// 4
```

在这个示例中，每次运行程序时，集合元素的输出顺序可能会不同，因为集合是无序的。

### 总结

Swift中的集合是无序的，其本质原因在于其底层实现使用了哈希表，这种数据结构的设计目标是提供高效的插入、查找和删除操作，而不是维护元素的顺序。集合的数学定义也强调了无序性，这与其在计算机科学中的实现方式相一致。


---
# 元组

Tuples allow you to store several values together in a single value. That might sound like arrays, but tuples are different:  
元组允许您将多个值存储在一个值中。这听起来像数组，但元组是不同的：

1. You can’t add or remove items from a tuple; they are fixed in size.  
    不能在元组中添加或删除项;它们的大小是固定的。
2. You can’t change the type of items in a tuple; they always have the same types they were created with.  
    不能更改元组中项的类型;它们始终具有与创建时相同的类型。
3. You can access items in a tuple using numerical positions or by naming them, but Swift won’t let you read numbers or names that don’t exist.  
    你可以使用数字位置或命名来访问元组中的项，但Swift不会让你读取不存在的数字或名称。

Tuples are created by placing multiple items into parentheses, like this:  
元组是通过将多个项目放入括号中来创建的，如下所示：

```swift
var name = (first: "Taylor", last: "Swift")
```

You then access items using numerical positions starting from 0:  
然后，您可以使用从0开始的数字位置访问项目：

```swift
name.0
```

Or you can access items using their names:  
或者，您可以使用项目名称访问项目：

```swift
name.first
```

Remember, you can change the values inside a tuple after you create it, but not the _types_ of values. So, if you tried to change `name` to be `(first: "Justin", age: 25)` you would get an error.  
请记住，您可以在创建元组后更改元组内部的值，但不能更改值的类型。因此，如果您尝试将 `name` 更改为 `(first: "Justin", age: 25)` ，您会收到错误。

> [!元组就是匿名的结构体] 
> 元组实际上只是一个没有名称的结构体，就像一个匿名结构体一样。


---

# 字典

If you try to read a value from a dictionary using a key that doesn’t exist, Swift will send you back `nil` – nothing at all. While this might be what you want, there’s an alternative: we can provide the dictionary with a default value to use if we request a missing key.  
如果你试图使用一个不存在的键从字典中读取一个值，Swift会返回 `nil` -什么都没有。虽然这可能是您想要的，但还有一种替代方法：如果我们请求缺少键，我们可以为字典提供一个默认值。

To demonstrate this, let’s create a dictionary of favorite ice creams for two people:  
为了证明这一点，让我们为两个人创建一个最喜欢的冰淇淋字典：

```swift
let favoriteIceCream = [
    "Paul": "Chocolate",
    "Sophie": "Vanilla"
]
```

We can read Paul’s favorite ice cream like this:  
我们可以这样解读保罗最喜欢的冰淇淋：

```swift
favoriteIceCream["Paul"]
```

But if we tried reading the favorite ice cream for Charlotte, we’d get back nil, meaning that Swift doesn’t have a value for that key:  
但是如果我们尝试阅读夏洛特最喜欢的冰淇淋，我们会返回nil，这意味着Swift没有该键的值：

```swift
favoriteIceCream["Charlotte"]
```

We can fix this by giving the dictionary a default value of “Unknown”, so that when no ice cream is found for Charlotte we get back “Unknown” rather than nil:  
我们可以通过给字典一个默认值“Unknown”来解决这个问题，这样当没有找到夏洛特的冰淇淋时，我们会返回“Unknown”而不是nil：

```swift
favoriteIceCream["Charlotte", default: "Unknown"]
```

> [!注意]
>请记住，不能保证字典中的键存在。这就是为什么从字典中阅读一个值可能什么也没有返回--您可能请求了一个不存在的键！
>

> [!Note]
> 这是因为Swift只对字典和数组有特殊的语法;其他类型必须使用尖括号语法，比如set。


---

# 字符串

## 多行字符串
在 Swift 中，使用三重引号 (﻿""") 来表示多行字符串字面量。多行字符串字面量允许你在字符串中包含换行符和其他格式，而无需使用 ﻿\n 等转义字符。这使得编写和阅读包含复杂格式的字符串更加直观。

**多行字符串字面量的用法**

**基本示例**


```swift
let multilineString = """

这是一个

多行字符串

字面量示例。

"""
```

在上述示例中，字符串会被解释为：

  

这是一个

多行字符串

字面量示例。

**保留缩进和空格**

多行字符串字面量会默认保留缩进和空格。这对于在代码中保持字符串的格式和排版非常有用。

  

```swift
let indentedString = """

    这是一段缩进的

    多行字符串。

    """
```

在上述示例中，如果打算保持缩进，可以将最左边的列设置为每行代码缩进的基准。

**包含引号和转义字符**

你可以在三重引号中包含单引号和双引号，而无需进行转义，但如果需要包含三重引号本身，则需要使用转义字符。

  

```swift
let quoteString = """

这是一个包含 "双引号" 和 '单引号' 的字符串。

"""
```

**自动添加新行**

每次换行都会被解释为字符串中的一个新行：

  
```swift

let newLineString = """

第一行

第二行

第三行

"""
```

**替换传统字符串中的换行符**

将传统字符串中的 ﻿\n 运算符替换为多行字符串字面量可以使字符串更易读：

  

```swift
let traditionalString = "第一行\n第二行\n第三行"

let multilineString = """

第一行

第二行

第三行

"""
```

**示例：格式化简单多行文本**

  

``` swift
import UIKit

  

class ViewController: UIViewController {

  

    override func viewDidLoad() {

        super.viewDidLoad()

  

        let footNotes = """

        1、本人出镜，视频时长需要在10-60s

        2、展露全脸，着装得体，尽量为半身或全身视频

        3、视频环境干净整洁、光线明亮

        4、内容丰富和有氛围感的视频更容易通过

        5、视频尽量竖屏，竖屏展示效果会更好

        """

        let textView = UITextView(frame: CGRect(x: 20, y: 50, width: 280, height: 200))

        textView.text = footNotes

        textView.font = UIFont.systemFont(ofSize: 16)

        textView.textColor = UIColor.black

        textView.backgroundColor = UIColor.lightGray

        textView.isEditable = false

  

        self.view.addSubview(textView)

    }

}
```

在这个示例中，我们使用三重引号来创建多行字符串 ﻿footNotes，它包含了带有换行的信息，用于设置 ﻿UITextView 的内容。

**总结**

三重引号在 Swift 中使处理多行字符串变得更加简洁和易读。无论是显示多行文本、保留缩进、包含引号和转义字符，还是替换传统字符串的 ﻿\n 运算符，多行字符串字面量都提供了一种方便的方法来处理复杂的字符串内容。

---

# Date

在 Swift 中，日期和时间的表示主要使用 `Date` 类型。`Date` 类型是 Foundation 框架的一部分，它表示一个特定的时间点，独立于时区。

### 基本用法

以下是一些 `Date` 类型的基本用法示例：

#### 创建当前日期和时间

```swift
import Foundation

let currentDate = Date()
print("Current date and time: \(currentDate)")
```

#### 创建特定日期和时间

可以使用 `DateComponents` 和 `Calendar` 来创建特定的日期和时间：

```swift
var dateComponents = DateComponents()
dateComponents.year = 2024
dateComponents.month = 6
dateComponents.day = 24
dateComponents.hour = 10
dateComponents.minute = 30

let calendar = Calendar.current
if let specificDate = calendar.date(from: dateComponents) {
    print("Specific date and time: \(specificDate)")
}
```

#### 格式化日期

使用 `DateFormatter` 来格式化日期和时间：

```swift
let dateFormatter = DateFormatter()
dateFormatter.dateStyle = .medium
dateFormatter.timeStyle = .medium

let formattedDate = dateFormatter.string(from: currentDate)
print("Formatted date and time: \(formattedDate)")
```

#### 解析日期字符串

使用 `DateFormatter` 来解析日期字符串：

```swift
let dateString = "2024-06-24 10:30:00"
let dateFormatter = DateFormatter()
dateFormatter.dateFormat = "yyyy-MM-dd HH:mm:ss"

if let parsedDate = dateFormatter.date(from: dateString) {
    print("Parsed date and time: \(parsedDate)")
}
```

#### 比较日期

可以使用标准的比较运算符来比较两个 `Date` 实例：

```swift
let earlierDate = Date(timeIntervalSinceNow: -3600) // 1 hour ago
let laterDate = Date(timeIntervalSinceNow: 3600) // 1 hour later

if earlierDate < laterDate {
    print("Earlier date is before later date")
}
```

### `Date` 类型的特性

- `Date` 类型表示的时间点是绝对的，与时区无关。
- `Date` 类型的内部表示是一个 `TimeInterval`，即自参考时间点（通常是 2001-01-01 00:00:00 UTC）以来的秒数。
- `Date` 类型提供了许多方法和属性来进行日期计算、比较和格式化。

### 示例代码

以下是一个综合示例，展示了如何使用 `Date` 类型进行各种操作：

```swift
import Foundation

// 获取当前日期和时间
let currentDate = Date()
print("Current date and time: \(currentDate)")

// 创建特定日期和时间
var dateComponents = DateComponents()
dateComponents.year = 2024
dateComponents.month = 6
dateComponents.day = 24
dateComponents.hour = 10
dateComponents.minute = 30

let calendar = Calendar.current
if let specificDate = calendar.date(from: dateComponents) {
    print("Specific date and time: \(specificDate)")
}

// 格式化日期
let dateFormatter = DateFormatter()
dateFormatter.dateStyle = .medium
dateFormatter.timeStyle = .medium

let formattedDate = dateFormatter.string(from: currentDate)
print("Formatted date and time: \(formattedDate)")

// 解析日期字符串
let dateString = "2024-06-24 10:30:00"
dateFormatter.dateFormat = "yyyy-MM-dd HH:mm:ss"

if let parsedDate = dateFormatter.date(from: dateString) {
    print("Parsed date and time: \(parsedDate)")
}

// 比较日期
let earlierDate = Date(timeIntervalSinceNow: -3600) // 1 hour ago
let laterDate = Date(timeIntervalSinceNow: 3600) // 1 hour later

if earlierDate < laterDate {
    print("Earlier date is before later date")
}
```

通过这些示例，你可以看到如何在 Swift 中使用 `Date` 类型来处理日期和时间。



---

# 循环
在 Swift 中，`for`、`forEach` 和 `ForEach` 都可以用来遍历集合，但它们的用途和行为是不同的：

1. `for` 是 Swift 的一个控制流语句，它可以用来遍历集合，如数组和字典。它是最常见的遍历方法，可以在任何地方使用。

```swift
let numbers = [1, 2, 3, 4, 5]
for number in numbers {
    print(number)
}
```

2. `forEach` 是 `Array`、`Set` 和 `Dictionary` 的一个方法，它接受一个闭包作为参数，对集合中的每个元素执行这个闭包。与 `for` 不同，`forEach` 不能使用 `break` 或 `continue` 来控制循环，也不能使用 `return` 来提前退出函数。

```swift
let numbers = [1, 2, 3, 4, 5]
numbers.forEach { number in
    print(number)
}
```

3. `ForEach` 是 SwiftUI 的一个结构体，它用来在 SwiftUI 的视图中遍历集合。`ForEach` 会为集合中的每个元素创建一个视图，并将这些视图添加到父视图中。

```swift
struct ContentView: View {
    let numbers = [1, 2, 3, 4, 5]

    var body: some View {
        List {
            ForEach(numbers, id: \.self) { number in
                Text("\(number)")
            }
        }
    }
}
```

在这个例子中，`ForEach` 为 `numbers` 数组中的每个元素创建了一个 `Text` 视图，并将这些视图添加到了 `List` 中。


---


## forloop
```swift
import Foundation

var forLoop = 0
// for
for i in 0..<3 {
    forLoop += i
}
// while
while forLoop > 1 {
    forLoop -= 1
}

// do-while
repeat {
    forLoop *= 2
} while (forLoop <= 2^10)
            
print(forLoop)
print(2^10) // 此处是2进制吗？```
```

swift中函数是一等公民，可以当变量去用


## `for`、`forEach` 和 `ForEach`

在 Swift 中，`for`、`forEach` 和 `ForEach` 都可以用来遍历集合，但它们的用途和行为是不同的：

1. `for` 是 Swift 的一个控制流语句，它可以用来遍历集合，如数组和字典。它是最常见的遍历方法，可以在任何地方使用。

```swift
let numbers = [1, 2, 3, 4, 5]
for number in numbers {
    print(number)
}
```

2. `forEach` 是 `Array`、`Set` 和 `Dictionary` 的一个方法，它接受一个闭包作为参数，对集合中的每个元素执行这个闭包。与 `for` 不同，`forEach` 不能使用 `break` 或 `continue` 来控制循环，也不能使用 `return` 来提前退出函数。

```swift
let numbers = [1, 2, 3, 4, 5]
numbers.forEach { number in
    print(number)
}
```

3. `ForEach` 是 SwiftUI 的一个结构体，它用来在 SwiftUI 的视图中遍历集合。`ForEach` 会为集合中的每个元素创建一个视图，并将这些视图添加到父视图中。

```swift
struct ContentView: View {
    let numbers = [1, 2, 3, 4, 5]

    var body: some View {
        List {
            ForEach(numbers, id: \.self) { number in
                Text("\(number)")
            }
        }
    }
}
```

在这个例子中，`ForEach` 为 `numbers` 数组中的每个元素创建了一个 `Text` 视图，并将这些视图添加到了 `List` 中。


## 元组的使用

在Swift中，函数的参数可以是任何类型，包括元组（tuple）。元组可以用来将多个值组合成一个复合值。以下是一个示例，展示了如何定义一个接受位置和颜色元组作为参数的函数：

```swift
func updateItem(position: (x: Int, y: Int), color: (r: Int, g: Int, b: Int)) {
    let (x, y) = position
    let (r, g, b) = color
    print("Position is (\(x), \(y))")
    print("Color is (\(r), \(g), \(b))")
    // 在这里添加你的代码来更新item
}
```

你可以像这样调用这个函数：

```swift
updateItem(position: (x: 10, y: 20), color: (r: 255, g: 255, b: 255))
```

在这个例子中，`updateItem`函数接受两个参数：`position`和`color`。`position`是一个包含两个`Int`值的元组，`color`是一个包含三个`Int`值的元组。在函数体中，我们使用元组解构来获取元组中的值。然后，我们打印出这些值。你可以在这个函数中添加你的代码来根据这些值来更新item。

你已经有了一个可以调整图像大小的扩展方法。接下来，你可以使用这个方法来调整图像的大小，并将调整后的图像保存到文件系统中。以下是一个示例：

```swift
import UIKit

let fileManager = FileManager.default
let documentsDirectory = fileManager.urls(for: .documentDirectory, in: .userDomainMask).first!
let filePath = documentsDirectory.appendingPathComponent("resizedImage.png")

if let image = UIImage(named: "your_image_name"), // 从asset或者其他地方获取你的原始图片
   let data = image.resize(to: CGSize(width: 410, height: 494)).pngData() {
    do {
        try data.write(to: filePath)
        print("Image saved at \(filePath)")
    } catch {
        print("Error: \(error)")
    }
}
```

在这个例子中，我们首先获取了一个`UIImage`对象，然后使用你的`resize(to:)`方法来调整图像的大小。然后，我们将调整后的图像转换为PNG数据，并将数据写入到文件系统中。

请注意，你需要替换`"your_image_name"`为你的原始图片的名称。如果你的图片在asset中，你可以直接使用图片的名称。如果你的图片在文件系统中，你需要先获取图片的路径，然后使用`UIImage(contentsOfFile:)`来创建`UIImage`对象。



---

# swift中的高阶语法

在Swift中，高阶函数是接受至少一个函数作为输入或返回一个函数的函数。Swift的数组有几个内置的高阶函数，如`map`、`filter`和`reduce`。

以下是如何使用这些函数的示例：

1. `map`：这个函数接受一个闭包作为参数，这个闭包接受数组的元素类型作为输入，并返回一个新的值。`map`函数返回一个新的数组，这个数组包含原数组中每个元素经过闭包处理后的结果。

```swift
let numbers = [1, 2, 3, 4, 5]
let squaredNumbers = numbers.map { $0 * $0 } // [1, 4, 9, 16, 25]
```

2. `filter`：这个函数接受一个闭包作为参数，这个闭包接受数组的元素类型作为输入，并返回一个布尔值。`filter`函数返回一个新的数组，这个数组只包含原数组中使闭包返回`true`的元素。

```swift
let numbers = [1, 2, 3, 4, 5]
let evenNumbers = numbers.filter { $0 % 2 == 0 } // [2, 4]
```

3. `reduce`：这个函数接受一个初始值和一个闭包作为参数。这个闭包接受两个参数：累积的值和数组的元素，然后返回一个新的累积值。`reduce`函数返回一个值，这个值是通过将闭包应用于数组的每个元素和累积的值来得到的。

```swift
let numbers = [1, 2, 3, 4, 5]
let sum = numbers.reduce(0, { $0 + $1 }) // 15
```

在这些示例中，我们使用了Swift的闭包语法和`$0`、`$1`等快捷参数名。这些参数名表示闭包的第一个、第二个等参数。


## `flatMap`

在 Swift 中，`flatMap` 是一个非常有用的方法，它可以用于多种不同的数据类型和场景，主要用途包括：

1. **处理可选值（Optionals）**
2. **处理集合类型（如数组）**
3. **处理嵌套集合**

### 1. 处理可选值（Optionals）

当处理可选值时，`flatMap` 可以用来安全地解包可选值并对其进行转换。与 `map` 不同的是，`flatMap` 还可以处理返回的结果是可选值的情况，并将嵌套的可选值“展平”。

```swift
let number: Int? = 5
let result = number.flatMap { value in
    return value > 0 ? "\(value) is positive" : nil
}

print(result) // 输出: Optional("5 is positive")
```

在这个例子中，如果 `number` 是 `nil`，`flatMap` 会返回 `nil`。如果 `number` 有值且大于 0，则返回一个字符串。

### 2. 处理集合类型（如数组）

当处理集合类型时，`flatMap` 可以用来将每个元素映射到一个新的集合，然后将这些集合展平成一个单一的集合。

```swift
let numbers = [1, 2, 3, 4]
let result = numbers.flatMap { number in
    return Array(repeating: number, count: number)
}

print(result) // 输出: [1, 2, 2, 3, 3, 3, 4, 4, 4, 4]
```

在这个例子中，每个数字被映射到一个包含该数字重复次数的数组，然后 `flatMap` 将这些数组展平成一个单一的数组。

### 3. 处理嵌套集合

`flatMap` 也可以用来处理嵌套集合，将多层嵌套的集合展平成一个单一的集合。

```swift
let nestedNumbers = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
let result = nestedNumbers.flatMap { $0 }

print(result) // 输出: [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

在这个例子中，嵌套的数组被展平成一个单一的数组。

### 总结

`flatMap` 在处理可选值和集合类型时非常有用，可以用来解包可选值、映射和展平嵌套集合。它的主要优势在于能够避免嵌套的结构，并且在处理返回结果为可选值或集合的情况下，提供了简洁的解决方案。


## `reduce`

在 Swift 中，`reduce` 是一个强大的高阶函数，用于将序列（如数组）的元素组合成一个单一的值。`reduce` 方法通过应用一个闭包（closure）来合并序列中的每个元素，最终生成一个累积的结果。

### `reduce` 的基本用法

`reduce` 方法有两个参数：
1. 一个初始值，这个值用于存储和返回最终的累积结果。
2. 一个闭包，这个闭包接受两个参数：累积结果和序列中的当前元素，然后返回一个新的累积结果。

## `map`

在 Swift 中，`map` 是一个常用的高阶函数，用于将集合中的每个元素转换为一个新的值，并返回一个包含这些新值的集合。`map` 函数不会改变原集合，而是生成一个新的集合。

### 基本用法

假设我们有一个整数数组，并希望将每个整数都乘以 2，我们可以使用 `map` 来实现：

```swift
let numbers = [1, 2, 3, 4, 5]
let doubledNumbers = numbers.map { (number) in
    return number * 2
}
print(doubledNumbers)  // 输出: [2, 4, 6, 8, 10]
```

在这个例子中：
- `numbers` 是原始数组。
- `map` 函数接受一个闭包，该闭包将数组中的每个元素 `number` 乘以 2 并返回。
- `doubledNumbers` 是一个新的数组，包含了 `numbers` 中每个元素乘以 2 的结果。

### 使用简写闭包语法

Swift 提供了简写闭包语法，使得代码更简洁：

```swift
let doubledNumbers = numbers.map { $0 * 2 }
print(doubledNumbers)  // 输出: [2, 4, 6, 8, 10]
```

在这个例子中，`$0` 表示闭包的第一个参数，即数组中的每个元素。

### 其他例子

#### 将字符串数组转换为它们的长度

假设我们有一个字符串数组，并希望将每个字符串转换为它的长度：

```swift
let words = ["apple", "banana", "cherry"]
let lengths = words.map { $0.count }
print(lengths)  // 输出: [5, 6, 6]
```

#### 将整数数组转换为字符串数组

```swift
let numbers = [1, 2, 3, 4, 5]
let stringNumbers = numbers.map { String($0) }
print(stringNumbers)  // 输出: ["1", "2", "3", "4", "5"]
```

#### 将字典的值转换为字符串

假设我们有一个字典，并希望将字典的值转换为字符串：

```swift
let dictionary = ["a": 1, "b": 2, "c": 3]
let stringValues = dictionary.map { "\($0.key): \($0.value)" }
print(stringValues)  // 输出: ["a: 1", "b: 2", "c: 3"]
```

### 嵌套使用 `map`

`map` 也可以嵌套使用。例如，假设我们有一个二维数组，并希望将其中的每个元素都加 1：

```swift
let matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
let incrementedMatrix = matrix.map { row in
    row.map { $0 + 1 }
}
print(incrementedMatrix)  // 输出: [[2, 3, 4], [5, 6, 7], [8, 9, 10]]
```

在这个例子中，我们对每一行使用 `map`，然后对每一行中的每个元素再次使用 `map` 来实现加 1 的操作。

### 总结

`map` 是一个强大的高阶函数，用于将集合中的每个元素转换为一个新的值。它非常适合在不改变原集合的情况下生成一个新的集合。通过熟练使用 `map`，可以使代码更加简洁和高效。

### 语法

```swift
let result = sequence.reduce(initialResult) { (accumulator, element) -> ResultType in
    // Combine accumulator and element to produce a new accumulator
}
```

### 示例

#### 1. 求和

通过 `reduce` 计算数组中所有元素的和：

```swift
let numbers = [1, 2, 3, 4, 5]
let sum = numbers.reduce(0) { (accumulator, number) in
    return accumulator + number
}

print(sum) // 输出: 15
```

在这个例子中，初始值是 `0`，然后闭包逐个将数组中的每个数字加到累积结果中。

#### 2. 连接字符串

通过 `reduce` 将字符串数组连接成一个单一的字符串：

```swift
let words = ["Hello", "world", "Swift", "is", "awesome"]
let sentence = words.reduce("") { (accumulator, word) in
    return accumulator + (accumulator.isEmpty ? "" : " ") + word
}

print(sentence) // 输出: "Hello world Swift is awesome"
```

在这个例子中，初始值是一个空字符串 `""`，然后闭包逐个将数组中的每个单词连接到累积结果中，并在单词之间添加空格。

#### 3. 计算乘积

通过 `reduce` 计算数组中所有元素的乘积：

```swift
let numbers = [1, 2, 3, 4, 5]
let product = numbers.reduce(1) { (accumulator, number) in
    return accumulator * number
}

print(product) // 输出: 120
```

在这个例子中，初始值是 `1`，然后闭包逐个将数组中的每个数字乘到累积结果中。

### 使用简化的闭包语法

由于 Swift 的类型推断和闭包语法的简洁性，可以将上面的例子进一步简化：

```swift
let numbers = [1, 2, 3, 4, 5]
let sum = numbers.reduce(0, +)
print(sum) // 输出: 15

let words = ["Hello", "world", "Swift", "is", "awesome"]
let sentence = words.reduce("", { $0 + ($0.isEmpty ? "" : " ") + $1 })
print(sentence) // 输出: "Hello world Swift is awesome"
```

在这些简化的例子中，我们使用了操作符 `+` 作为闭包，或者使用了简化的闭包语法。

### 总结

`reduce` 是一个非常灵活和强大的函数，适用于各种场景，包括求和、计算乘积、连接字符串等。通过提供一个初始值和一个闭包，`reduce` 可以将序列中的元素合并成一个单一的结果。


---
# 数据结构

## 结构体与类 

在 Swift 中，`struct` 和 `class` 各自有不同的特性和用途。通常情况下，`struct` 的性能开销确实会比 `class` 小，但这并不是绝对的，具体还要看使用场景和操作。以下是一些关键点，帮助你理解 `struct` 和 `class` 的性能差异：

### 1. 值类型 vs 引用类型

- **`struct` 是值类型**：
  - 每次赋值或传递时，都会创建一个副本（拷贝）。
  - 适合用于轻量级的数据存储，尤其是不可变数据。
  - 在栈上分配内存，通常更高效。

- **`class` 是引用类型**：
  - 赋值或传递时，传递的是引用。
  - 适合用于需要共享状态或需要继承的场景。
  - 在堆上分配内存，可能会有额外的性能开销。

### 2. 内存管理

- **`struct`**：
  - 由于是值类型，不涉及引用计数（ARC），因此没有 ARC 的性能开销。
  - 小的 `struct` 通常在栈上分配内存，性能更好。

- **`class`**：
  - 由于是引用类型，涉及引用计数（ARC），会有一些性能开销。
  - 在堆上分配内存，堆内存管理相对复杂，性能开销更大。

### 3. 线程安全

- **`struct`**：
  - 由于是值类型，每次赋值或传递都会创建副本，因此天然是线程安全的。
  - 不会出现多个线程同时修改同一个实例的情况。

- **`class`**：
  - 由于是引用类型，多个线程可能会同时访问和修改同一个实例，需要额外的同步机制来保证线程安全。

### 4. 使用场景

- **`struct`**：
  - 适用于表示轻量级的数据结构，例如几何数据（点、矩形）、颜色、范围等。
  - 适用于不可变的数据，或者数据变化不会影响其他实例的情况。

- **`class`**：
  - 适用于需要共享状态的场景，例如视图控制器、网络请求管理器等。
  - 适用于需要继承和多态的场景。

### 5. 性能比较

虽然在很多情况下 `struct` 的性能开销比 `class` 小，但这并不是绝对的。以下是一些具体的性能考虑：

- **小数据量**：对于小的数据量，`struct` 的性能通常优于 `class`，因为它们通常在栈上分配内存，且不涉及引用计数。
- **大数据量**：对于大数据量，`struct` 的拷贝操作可能会导致性能问题。在这种情况下，可以考虑使用 `class` 或者通过 `struct` 内部使用 `class` 引用来优化性能。

### 结论

- 使用 `struct` 时，如果你的数据是轻量级的、不可变的，或者不需要共享状态，那么 `struct` 通常是更好的选择。
- 使用 `class` 时，如果你的数据需要共享状态、需要继承和多态，或者数据量较大且频繁拷贝会导致性能问题，那么 `class` 是更合适的选择。

总的来说，`struct` 通常在性能上相对 `class` 更有优势，但具体选择还需要根据实际使用场景来决定。


### 类摘要
1. 类和结构类似，因为它们都可以让您使用属性和方法创建自己的类型。
2. 一个类可以从另一个类继承，并且它获得父类的所有属性和方法。谈论类层次结构是很常见的 – 一个类基于另一个类，而另一个类本身又基于另一个类。
3. 您可以使用 `final` 关键字标记类，这将阻止其他类从该类继承。
4. 方法覆盖允许子类将其父类中的方法替换为新的实现。
5. 当两个变量指向同一个类实例时，它们都指向同一块内存——改变一个变量会改变另一个。
6. 类可以具有反初始化器（`deinit`），这是在类的实例被销毁时运行的代码。
7. 类不像结构那样强制执行常量 – 如果属性被声明为变量，则无论类实例是如何创建的，都可以更改它


## 拓展`Extension`

扩展允许您向现有类型添加方法，使它们执行最初没有设计要做的事情。

Swift 不允许你在扩展中添加存储的属性，因此你必须使用计算属性来代替。例如，我们可以向整数添加新的 `isEven` 计算属性，如果它包含偶数，则返回 true：

```swift
extension Int {
    var isEven: Bool {
        return self % 2 == 0
    }
}
```

Swift也允许你为`protocol`添加`extension`

## 协议`protocol`

1. 协议描述符合类型必须具有的方法和属性，但不提供这些方法的实现。
2. 您可以在其他协议之上构建协议，类似于类。
3. 扩展允许您向特定类型（如 `Int`）添加方法和计算属性。
4. 协议扩展允许您向协议添加方法和计算属性。
5. 面向协议的编程是将应用程序架构设计为一系列协议，然后使用协议扩展提供默认方法实现的做法。

## 属性

**计算属性与存储属性**

swift 为我们提供了两种变体：存储属性和计算属性，前者将值隐藏在某个内存中以供以后使用，后者是计算属性，每次调用值时都会重新计算。在幕后，计算属性实际上只是一个恰好属于您的结构体的函数调用。

在 Swift 中，属性分为两类：存储属性和计算属性。每类属性都有其独特的功能和用途。

### 存储属性（Stored Properties）

存储属性是直接存储在实例中的常量或变量。它们可以是变量属性（`var`）或常量属性（`let`）。

#### 示例

```swift
struct Person {
    var firstName: String
    var lastName: String
    let birthYear: Int
}

let person = Person(firstName: "John", lastName: "Doe", birthYear: 1990)
print(person.firstName)  // 输出: John
print(person.birthYear)  // 输出: 1990
```

在上面的例子中，`firstName` 和 `lastName` 是变量存储属性，可以修改；`birthYear` 是常量存储属性，一旦初始化后就不能修改。

### 计算属性（Computed Properties）

计算属性不直接存储值，而是提供一个 getter 和一个可选的 setter 来间接获取和设置其他属性或变量的值。

#### 示例

```swift
struct Rectangle {
    var width: Double
    var height: Double

    var area: Double {
        return width * height
    }

    var perimeter: Double {
        return 2 * (width + height)
    }
}

let rect = Rectangle(width: 10.0, height: 5.0)
print(rect.area)  // 输出: 50.0
print(rect.perimeter)  // 输出: 30.0
```

在这个例子中，`area` 和 `perimeter` 是计算属性，它们通过计算 `width` 和 `height` 的值来返回结果。

#### 带有 setter 的计算属性

计算属性可以有一个可选的 setter，用于设置值。

```swift
struct Rectangle {
    var width: Double
    var height: Double

    var area: Double {
        get {
            return width * height
        }
        set {
            // 假设新的面积值是 newValue
            // 这里我们简单地将新的面积分配给宽度
            width = newValue / height
        }
    }
}

var rect = Rectangle(width: 10.0, height: 5.0)
print(rect.area)  // 输出: 50.0

rect.area = 100.0
print(rect.width)  // 输出: 20.0
```

在这个例子中，`area` 属性不仅可以通过计算返回矩形的面积，还可以通过设置新的面积来调整矩形的宽度。

### 属性观察器（Property Observers）

属性观察器监视和响应属性值的变化。可以为存储属性（除了常量存储属性）和计算属性的 setter 添加属性观察器。

#### 示例

```swift
struct StepCounter {
    var totalSteps: Int = 0 {
        willSet(newTotalSteps) {
            print("About to set totalSteps to \(newTotalSteps)")
        }
        didSet {
            if totalSteps > oldValue {
                print("Added \(totalSteps - oldValue) steps")
            }
        }
    }
}

var stepCounter = StepCounter()
stepCounter.totalSteps = 200  // 输出: About to set totalSteps to 200
                              //       Added 200 steps
stepCounter.totalSteps = 360  // 输出: About to set totalSteps to 360
                              //       Added 160 steps
```

在这个例子中，`totalSteps` 属性有两个观察器：`willSet` 在新值被设置之前调用，`didSet` 在新值被设置之后调用。

### 总结

- **存储属性**：直接存储在实例中的常量或变量。
- **计算属性**：不直接存储值，而是通过 getter 和 setter 来间接获取和设置值。
- **属性观察器**：用于监视和响应属性值的变化，适用于存储属性和计算属性的 setter。

通过理解和使用这些属性类型，你可以更灵活地管理和操作 Swift 中的数据。

```swift
import Foundation
struct A {
    let a = 1
    var b: Int {
        return a * 2
    }
}
let a = A()
print(a.b)
```

使用断点调试这段代码时，会发现a会在A被init时就初始化，但是b只有在b被调用是才会被set，计算属性每次被调用时都会重新计算其值，或者说，计算属性会在运行时才会计算其值

### 使用场景

决定使用哪个部分取决于您的`property`的价值是否取决于其他数据，部分还取决于性能。性能部分很简单：如果在属性的值没有改变的情况下定期读取属性，那么使用存储的属性将比使用计算属性快得多。另一方面，如果您的属性很少被读取，甚至可能根本不被读取，那么使用计算属性可以使您不必计算其值并将其存储在某个地方。
当涉及到依赖关系时——你的属性的值是否依赖于你的其他属性的值——那么表就被翻转了：这是一个计算属性有用的地方，因为你可以确定它们返回的值总是考虑到最新的程序状态。


### `lazy`
在 Swift 中，`lazy` 关键字用于声明一个惰性存储属性。惰性存储属性在第一次访问时才会被初始化，而不是在实例初始化时立即初始化。这样可以延迟一些计算开销较大的属性的初始化，直到确实需要它们为止。

### 使用场景

惰性存储属性通常用于以下场景：

1. **初始化开销较大**：如果属性的初始化需要进行复杂的计算或占用大量资源，可以使用 `lazy` 来延迟其初始化。
2. **依赖于其他属性**：如果属性的值依赖于某些其他属性的值，并且这些属性在实例初始化时还未完全初始化，则可以使用 `lazy`。

### 语法

使用 `lazy` 关键字声明一个属性：

```swift
class Example {
    lazy var someProperty: SomeType = {
        // 计算并返回初始值
        return SomeType()
    }()
}
```

### 示例

以下是一个具体示例，展示了如何使用 `lazy` 属性：

```swift
class DataManager {
    lazy var data: [String] = {
        // 模拟一个耗时的初始化过程
        print("Loading data...")
        return ["Data1", "Data2", "Data3"]
    }()
    
    init() {
        print("DataManager initialized")
    }
}

let manager = DataManager()
print("Before accessing data")
print(manager.data)  // 访问时才会初始化并输出 "Loading data..."
print("After accessing data")
```

#### 输出结果

```
DataManager initialized
Before accessing data
Loading data...
["Data1", "Data2", "Data3"]
After accessing data
```

从输出结果可以看出，`data` 属性的初始化被延迟到第一次访问时才进行。

### 注意事项

1. **只能用于变量属性**：`lazy` 只能用于变量属性（`var`），不能用于常量属性（`let`），因为常量在实例初始化时必须有一个确定的值。
2. **线程安全**：Swift 的 `lazy` 属性在多线程环境下并不是线程安全的。如果多个线程同时访问一个 `lazy` 属性，可能会导致属性被初始化多次。需要确保在多线程环境下使用合适的同步机制来保证线程安全。
3. **不能用于全局变量或静态属性**：`lazy` 只能用于类或结构体的实例属性，不能用于全局变量或静态属性。

### 总结

`lazy` 关键字在 Swift 中用于声明惰性存储属性，这些属性在第一次访问时才会被初始化。它们适用于初始化开销较大或依赖于其他属性的场景。通过合理使用 `lazy` 属性，可以优化程序的性能和资源管理。


## 枚举
在 Swift 中，`enum`（枚举）是一种强大的数据类型，用于定义一组相关的值。枚举不仅仅是简单的值集合，它们还可以关联额外的数据，并且可以包含方法和计算属性。Swift 的枚举与其他编程语言中的枚举相比，更加灵活和强大。

### 枚举的本质

1. **类型定义**：
   枚举定义了一种类型，它可以用来表示一组相关的值。这些值被称为枚举的成员。

   ```swift
   enum CompassPoint {
       case north
       case south
       case east
       case west
   }
   ```

2. **关联值**：
   枚举的成员可以有不同类型的关联值，这使得枚举非常灵活。

   ```swift
   enum Barcode {
       case upc(Int, Int, Int, Int)
       case qrCode(String)
   }
   ```

3. **原始值**：
   枚举的成员可以预先有一个相同类型的默认值（原始值），这些原始值可以是字符串、字符或任意整型或浮点型值。

   ```swift
   enum Planet: Int {
       case mercury = 1
       case venus
       case earth
       case mars
   }
   ```

4. **方法和计算属性**：
   枚举可以包含实例方法、类型方法和计算属性，使得枚举更加功能化。

   ```swift
   enum CompassPoint {
       case north
       case south
       case east
       case west

       func description() -> String {
           switch self {
           case .north:
               return "North"
           case .south:
               return "South"
           case .east:
               return "East"
           case .west:
               return "West"
           }
       }
   }
   ```

### 枚举的内存布局

在 Swift 中，枚举的内存布局是高度优化的。编译器会根据枚举的定义选择合适的内存布局，以确保高效的存储和访问。一般来说，枚举的内存布局取决于以下几个因素：

1. **枚举成员的数量**：
   编译器会为每个枚举成员分配一个唯一的整型标识符，这些标识符通常是从 0 开始的连续整数。

2. **关联值的存在与否**：
   如果枚举成员包含关联值，编译器会为这些关联值分配额外的内存空间。不同枚举成员的关联值可能会影响枚举的整体内存布局。

### 示例

以下是一个更复杂的示例，展示了枚举的多种特性：

```swift
enum Vehicle {
    case car(make: String, model: String, year: Int)
    case bicycle(make: String, gearCount: Int)
    case bus(routeNumber: Int)

    func description() -> String {
        switch self {
        case .car(let make, let model, let year):
            return "Car: \(make) \(model), \(year)"
        case .bicycle(let make, let gearCount):
            return "Bicycle: \(make), \(gearCount) gears"
        case .bus(let routeNumber):
            return "Bus: Route \(routeNumber)"
        }
    }
}

let myCar = Vehicle.car(make: "Toyota", model: "Corolla", year: 2020)
print(myCar.description())  // 输出: Car: Toyota Corolla, 2020

let myBike = Vehicle.bicycle(make: "Giant", gearCount: 21)
print(myBike.description())  // 输出: Bicycle: Giant, 21 gears
```

在这个示例中，`Vehicle` 枚举不仅定义了不同类型的车辆，还为每个车辆类型关联了不同的数据，并提供了一个方法来描述车辆的信息。

### 枚举的嵌套

‌**[Swift](https://www.baidu.com/s?sa=re_dqa_generate&wd=Swift&rsv_pq=9a8dc5a6004fda67&oq=swift%E7%9A%84enum%E5%B5%8C%E5%A5%97enum%2C%E5%AD%90enum%E5%8F%AF%E4%BB%A5%E4%BD%9C%E4%B8%BAcase%E4%BD%BF%E7%94%A8%E5%90%97%3F&rsv_t=bfa57chFFGvZFGAZ0TQwpnVPsQFq7sCVYfCZW75HMiu60VEf4SXU9HTLbS8&tn=baidu&ie=utf-8)的[enum](https://www.baidu.com/s?sa=re_dqa_generate&wd=enum&rsv_pq=9a8dc5a6004fda67&oq=swift%E7%9A%84enum%E5%B5%8C%E5%A5%97enum%2C%E5%AD%90enum%E5%8F%AF%E4%BB%A5%E4%BD%9C%E4%B8%BAcase%E4%BD%BF%E7%94%A8%E5%90%97%3F&rsv_t=bfa57chFFGvZFGAZ0TQwpnVPsQFq7sCVYfCZW75HMiu60VEf4SXU9HTLbS8&tn=baidu&ie=utf-8)支持嵌套enum，子enum可以作为case使用。**‌

在Swift中，枚举（enum）是一种强大的数据类型，它允许你定义一组相关的值。Swift的枚举不仅可以包含基本的值类型（如整数、浮点数、字符串等），还可以包含关联值（associated values），这使得枚举能够表示更复杂的数据结构。此外，Swift还支持嵌套枚举，即在一个枚举类型内部定义另一个枚举类型。这种嵌套结构允许你创建更复杂的枚举层次结构，以适应复杂的业务需求。

子enum作为case使用时，可以定义在父enum的某个case中，或者作为独立的枚举类型被其他枚举引用。这种嵌套和引用机制使得Swift的枚举系统非常灵活和强大，能够应对各种复杂的数据表示需求。例如，你可以定义一个表示颜色的枚举，然后在其中嵌套一个表示颜色的深浅或类型的子枚举，或者在不同的枚举之间共享相同的子枚举定义，以避免代码重复和提高代码的可维护性。

总的来说，Swift的enum支持嵌套enum，子enum可以作为case使用，这种特性使得Swift的枚举系统更加灵活和强大，能够适应各种复杂的数据表示需求。

### 总结

Swift 中的 `enum` 是一种灵活且功能强大的数据类型，它不仅可以定义一组相关的值，还可以关联额外的数据，包含方法和计算属性。它的内存布局由编译器优化，以确保高效的存储和访问。通过使用枚举，开发者可以创建更加清晰和结构化的代码。





---


# Swift的闭包

闭包（Closure）是自包含的函数代码块，可以在代码中被传递和使用。闭包能够捕获和存储其所在上下文中的常量和变量。Swift 中的闭包与 C 和 Objective-C 中的 blocks 以及其他编程语言中的匿名函数或 lambda 表达式类似。

### 闭包的定义

闭包有三种形式：
1. **全局函数**：有名字但不能捕获任何值。
2. **嵌套函数**：有名字并且可以捕获封闭函数内的值。
3. **闭包表达式**：无名字，使用轻量级语法，可以捕获上下文中的常量和变量。

### 闭包表达式的语法

闭包表达式的基本语法如下：

```swift
{ (parameters) -> returnType in
    statements
}
```

### 示例

#### 1. 基本闭包表达式

```swift
let greetingClosure = { (name: String) -> String in
    return "Hello, \(name)!"
}

let greeting = greetingClosure("Alice")
print(greeting) // 输出 "Hello, Alice!"
```

#### 2. 简化闭包表达式

Swift 提供了多种简化闭包表达式的方式：

- **根据上下文推断参数和返回类型**：

```swift
let greetingClosure = { name in
    "Hello, \(name)!"
}

let greeting = greetingClosure("Bob")
print(greeting) // 输出 "Hello, Bob!"
```

- **单表达式闭包隐式返回**：

```swift
let greetingClosure = { name in "Hello, \(name)!" }

let greeting = greetingClosure("Charlie")
print(greeting) // 输出 "Hello, Charlie!"
```

- **使用速记参数名**：

```swift
let greetingClosure: (String) -> String = { "Hello, \($0)!" }

let greeting = greetingClosure("Dave")
print(greeting) // 输出 "Hello, Dave!"
```

### 捕获值

闭包可以捕获和存储其所在上下文中的常量和变量。例如：

```swift
func makeIncrementer(incrementAmount: Int) -> () -> Int {
    var total = 0
    let incrementer: () -> Int = {
        total += incrementAmount
        return total
    }
    return incrementer
}

let incrementByTwo = makeIncrementer(incrementAmount: 2)
print(incrementByTwo()) // 输出 2
print(incrementByTwo()) // 输出 4
```

在这个例子中，闭包 `incrementer` 捕获了 `total` 和 `incrementAmount` 变量，并在每次调用时对它们进行操作。

### 总结

闭包是功能强大的工具，允许你在代码中传递和使用函数代码块。它们可以捕获和存储其所在上下文中的常量和变量，提供了灵活和简洁的代码结构。Swift 提供了多种简化闭包表达式的方式，使得闭包的使用更加方便和直观。

## 与oc Block的区别

Objective-C 中的 block 和 Swift 中的闭包（closure）在功能上非常相似，但在语法和实现细节上有一些显著的区别。以下是两者之间的主要区别：

### 语法

#### Objective-C 中的 Block

Objective-C 中的 block 使用 `^` 符号来定义，语法相对较为复杂。例如：

```objective-c
void (^simpleBlock)(void) = ^{
    NSLog(@"Hello, Objective-C Block");
};

simpleBlock();
```

带参数和返回值的 block：

```objective-c
int (^sumBlock)(int, int) = ^(int a, int b) {
    return a + b;
};

int result = sumBlock(3, 5);
NSLog(@"Result: %d", result); // 输出 "Result: 8"
```

#### Swift 中的 闭包

Swift 中的闭包使用 `{}` 符号来定义，语法更为简洁。例如：

```swift
let simpleClosure = {
    print("Hello, Swift Closure")
}

simpleClosure()
```

带参数和返回值的闭包：

```swift
let sumClosure: (Int, Int) -> Int = { (a, b) in
    return a + b
}

let result = sumClosure(3, 5)
print("Result: \(result)") // 输出 "Result: 8"
```

### 捕获变量

两者都可以捕获上下文中的变量，但实现细节有所不同。

#### Objective-C 中的 Block

在 Objective-C 中，block 会自动捕获上下文中的变量，但默认情况下，这些变量是以 `const` 方式捕获的。如果需要修改捕获的变量，需要使用 `__block` 修饰符。

```objective-c
__block int counter = 0;
void (^incrementBlock)(void) = ^{
    counter++;
    NSLog(@"Counter: %d", counter);
};

incrementBlock(); // 输出 "Counter: 1"
incrementBlock(); // 输出 "Counter: 2"
```

#### Swift 中的 闭包

在 Swift 中，闭包可以直接捕获并修改上下文中的变量。

```swift
var counter = 0
let incrementClosure = {
    counter += 1
    print("Counter: \(counter)")
}

incrementClosure() // 输出 "Counter: 1"
incrementClosure() // 输出 "Counter: 2"
```

### 内存管理

#### Objective-C 中的 Block

在 Objective-C 中，**block 默认是在栈上分配的，如果需要在栈外使用（比如保存为属性或传递到其他函数），需要进行复制操作（`Block_copy` 或 `copy` 方法）**。

```objective-c
typedef void (^MyBlock)(void);

MyBlock block = ^{
    NSLog(@"Hello, Block");
};

MyBlock copiedBlock = [block copy];
```

#### Swift 中的 闭包

**在 Swift 中，闭包默认是在堆上分配的，不需要显式复制。Swift 使用自动引用计数（ARC）来管理闭包的内存**。

### 语法简化

Swift 提供了更多的语法糖来简化闭包的定义和使用，例如：

- 参数类型和返回类型的推断
- 速记参数名（$0, $1, ...）
- 单表达式闭包的隐式返回

```swift
let sumClosure: (Int, Int) -> Int = { $0 + $1 }
```

### 总结

尽管 Objective-C 中的 block 和 Swift 中的闭包在功能上非常相似，但 Swift 的闭包在语法上更为简洁，内存管理更为自动化，并且提供了更多的语法糖来简化代码编写。Objective-C 的 block 则更为显式，特别是在内存管理和变量捕获方面需要更多的手动操作。

## swift闭包

可以理解为没有函数名的函数
```swift
//: [Previous](@previous)

import Foundation

// 闭包就是匿名函数
var oldArray = [1,5,3,2,4]
var array = oldArray.sorted(by: { (a,b) -> Bool in
    return a < b
})
print(array)

let 偶数 = oldArray.filter {
    $0 % 2 == 0
}
print(偶数)

// 例子：算n的阶乘
// 正常的函数法
func facorial(of n: Int64) -> Int64 {
    return (1...n).reduce(1, *)
}
facorial(of: 20)

let yes : (Int) -> Int  = { num in
    return (1...num).reduce(1, *)
}
yes(20)

//: [Next](@next)
```

### 逃逸闭包

在Swift中，`Result`类型是一个枚举，用于表示成功或失败的操作结果。它有两个情况：`.success`和`.failure`，每种情况都可以携带一个值。

你可以将`Result`类型与闭包一起使用，以处理异步操作的结果。以下是一个示例：

```swift
enum NetworkError: Error {
    case invalidURL
}

func fetchData(from url: String, completion: @escaping (Result<Data, NetworkError>) -> Void) {
    guard let url = URL(string: url) else {
        completion(.failure(.invalidURL))
        return
    }

    // 假设我们正在进行网络请求
    DispatchQueue.global().asyncAfter(deadline: .now() + 1) {
        let data = Data() // 假设这是从网络获取的数据
        completion(.success(data))
    }
}
```

在这个例子中，我们定义了一个`fetchData(from:completion:)`函数，它接受一个URL字符串和一个逃逸闭包作为参数。这个闭包的参数是一个`Result`类型，如果操作成功，它将携带一个`Data`对象；如果操作失败，它将携带一个`NetworkError`对象。

你可以这样使用这个函数：

```swift
fetchData(from: "https://example.com") { result in
    switch result {
    case .success(let data):
        print("获取到数据: \(data)")
    case .failure(let error):
        print("发生错误: \(error)")
    }
}
```

在这个例子中，我们调用`fetchData(from:completion:)`函数，并传入一个闭包来处理结果。如果操作成功，我们打印获取到的数据；如果操作失败，我们打印错误。

闭包的执行线程取决于它被调用的上下文。如果闭包在主线程上被调用，那么它就会在主线程上执行。如果它在后台线程上被调用，那么它就会在后台线程上执行。

在上述`fetchData(from:completion:)`函数的例子中，闭包是在全局队列（一个后台线程）上被调用的，因此它会在后台线程上执行。

如果你想要在主线程上执行闭包（例如，你需要更新UI），你可以使用`DispatchQueue.main.async`：

```swift
fetchData(from: "https://example.com") { result in
    DispatchQueue.main.async {
        switch result {
        case .success(let data):
            print("获取到数据: \(data)")
            // 更新UI
        case .failure(let error):
            print("发生错误: \(error)")
            // 显示错误信息
        }
    }
}
```

在这个例子中，无论`fetchData(from:completion:)`函数在哪个线程上调用闭包，闭包中的代码都会在主线程上执行。

### Swift闭包的使用

在Swift中，闭包是一种自包含的函数代码块，可以在代码中被传递和使用。闭包可以捕获和存储其所在上下文中任何常量和变量的引用。

以下是一个简单的闭包的示例：

```swift
let greetingClosure: () -> Void = {
    print("Hello, World!")
}

greetingClosure() // Prints "Hello, World!"
```

在这个示例中，`greetingClosure`是一个没有参数也没有返回值的闭包。它的类型是`() -> Void`，表示这是一个没有参数并且没有返回值的函数。闭包的内容在花括号中定义，这个闭包打印一条消息。

闭包也可以接受参数和返回值。以下是一个接受两个`Int`参数并返回它们的和的闭包的示例：

```swift
let additionClosure: (Int, Int) -> Int = { num1, num2 in
    return num1 + num2
}

let sum = additionClosure(5, 3) // sum is 8
```

在这个示例中，`additionClosure`是一个接受两个`Int`参数并返回一个`Int`的闭包。它的类型是`(Int, Int) -> Int`。闭包的参数在`in`关键字之前定义，闭包的主体在`in`关键字之后定义。

闭包在Swift中被广泛使用，例如在数组的`map`、`filter`和`reduce`方法中，以及在异步API中作为完成处理器。


### 逃逸闭包和普通闭包的区别

在 Swift 中，闭包分为逃逸闭包（escaping closure）和非逃逸闭包（non-escaping closure），它们的主要区别在于闭包的生命周期和作用域。以下是这两种闭包的详细区别：

**非逃逸闭包**

非逃逸闭包（non-escaping closure）是在函数执行期间被调用的闭包。默认情况下，闭包参数是非逃逸的。它们不会脱离函数作用域被使用，也就是说，函数执行完毕后，非逃逸闭包就被释放。

  

```swift
func getRoomGameList(completion: (Result<Any, Error>) -> Void) {

    // 在函数体内部调用闭包

    completion(.success("Game list"))

}

  

// 调用 getRoomGameList

getRoomGameList { result in

    switch result {

    case .success(let gameList):

        print("游戏列表: \(gameList)")

    case .failure(let error):

        print("错误: \(error.localizedDescription)")

    }

}
```

**逃逸闭包**

逃逸闭包（escaping closure），即使用 ﻿@escaping 关键字标记的闭包，一般在异步操作中使用。此类闭包在函数返回之后仍然可能被调用。因此，逃逸闭包可以在函数作用域之外被使用，并在某个时间点触发。

  

```swift
func getRoomGameList(completion: @escaping (Result<Any, Error>) -> Void) {

    // 模拟异步操作，例如网络请求

    DispatchQueue.global().async {

        // 在异步操作完成后调用闭包

        completion(.success("Game list"))

    }

}

  

// 调用 getRoomGameList

getRoomGameList { result in

    switch result {

    case .success(let gameList):

        print("游戏列表: \(gameList)")

    case .failure(let error):

        print("错误: \(error.localizedDescription)")

    }

}
```

**主要区别**

1. **生命周期**：

▪ 非逃逸闭包在函数执行期间被调用，函数结束后闭包不会再被保留。

▪ 逃逸闭包可能在函数返回后被调用，生命周期延长。

2. **内存管理**：

▪ 非逃逸闭包的内存管理较为简单，因为它们不会在函数之外使用。

▪ 逃逸闭包可能导致循环引用（retain cycles），需要特别注意使用 ﻿weak 或 ﻿unowned 来避免内存泄漏。

3. **使用场景**：

▪ 非逃逸闭包适用于同步操作。

▪ 逃逸闭包适用于异步操作，如网络请求、动画等。

通过理解和区分这两种闭包，可以更有效地管理闭包的生命周期和内存。



---
# Swift的并发


## 异步函数与闭包

在 Swift 中，异步函数和闭包是处理异步操作的两种常见方式。它们有一些共同点，但也有显著的区别。以下是它们的共同点和区别的详细分析。

### 共同点

1. **处理异步操作**：
   - 异步函数和闭包都可以用于处理异步操作，例如网络请求、文件读写等。

2. **非阻塞**：
   - 它们都不会阻塞主线程，可以在后台执行耗时操作，然后在完成后通知主线程。

3. **回调机制**：
   - 它们都使用回调机制来处理操作完成后的结果。

### 区别

#### 1. 语法和使用方式

- **异步函数**：
  - Swift 5.5 引入了 `async`/`await` 语法，使异步代码更易读和编写。
  - 异步函数使用 `async` 关键字声明，并且在调用时使用 `await` 关键字。
  - 例子：

    ```swift
    func fetchData() async throws -> Data {
        // 异步操作
    }

    // 使用异步函数
    Task {
        do {
            let data = try await fetchData()
            // 使用数据
        } catch {
            // 处理错误
        }
    }
    ```

- **闭包**：
  - 闭包是一种可以捕获和存储其所在上下文中变量的代码块。
  - 闭包通常作为参数传递给函数，作为回调使用。
  - 例子：

    ```swift
    func fetchData(completion: @escaping (Result<Data, Error>) -> Void) {
        // 异步操作
    }

    // 使用闭包
    fetchData { result in
        switch result {
        case .success(let data):
            // 使用数据
        case .failure(let error):
            // 处理错误
        }
    }
    ```

#### 2. 可读性和可维护性

- **异步函数**：
  - `async`/`await` 语法使异步代码看起来像同步代码，提升了代码的可读性和可维护性。
  - 错误处理更加简洁，使用 `try` 和 `catch` 处理错误。

- **闭包**：
  - 闭包可能导致回调地狱（callback hell），使代码变得难以阅读和维护。
  - 错误处理通常通过回调参数处理，代码可能变得冗长。

#### 3. 错误处理

- **异步函数**：
  - 错误处理使用 `throws` 和 `try` 关键字，结合 `async`/`await` 语法，使错误处理更加直观。

- **闭包**：
  - 错误处理通常通过回调参数传递，使用 `Result` 类型或其他方式处理错误。

### 示例对比

#### 异步函数

```swift
func fetchData() async throws -> Data {
    // 假设这是一个异步网络请求
    let url = URL(string: "https://example.com/data")!
    let (data, _) = try await URLSession.shared.data(from: url)
    return data
}

Task {
    do {
        let data = try await fetchData()
        print("Data received: \(data)")
    } catch {
        print("Error: \(error)")
    }
}
```

#### 闭包

```swift
func fetchData(completion: @escaping (Result<Data, Error>) -> Void) {
    let url = URL(string: "https://example.com/data")!
    URLSession.shared.dataTask(with: url) { data, response, error in
        if let error = error {
            completion(.failure(error))
            return
        }
        if let data = data {
            completion(.success(data))
        }
    }.resume()
}

fetchData { result in
    switch result {
    case .success(let data):
        print("Data received: \(data)")
    case .failure(let error):
        print("Error: \(error)")
    }
}
```

### 总结

- **异步函数** 提供了更简洁和易读的语法，适合处理复杂的异步流程。
- **闭包** 是传统的异步处理方式，灵活但容易导致回调地狱。

选择哪种方式取决于具体的需求和代码风格。对于新的代码和项目，推荐使用 `async`/`await` 语法，因为它提供了更好的可读性和错误处理机制。

https://onevcat.com/2021/07/swift-concurrency/

## 1.  [ 什么是并发：](https://c.biancheng.net/view/9835.html)
按最简单、最基本的程度理解，并发（concurrency）是两个或多个同时独立进行的活动。并发现象遍布日常生活，我们可以边走路边说话，左右手同时做出不一样的动作，诸如此类。
## 2. 多线程
多线程是指程序中包含两个或多个并行运行的线程，每个线程都在处理不同的任务。在多线程环境中，CPU可以在多个线程之间进行切换，以实现并行处理。多线程可以提高程序的执行效率，但也会带来一些复杂性，比如线程同步和数据竞争等问题。

## 3. 同步与异步：
异步是指程序不必等待某个长时间运行的任务完成，而是在这个任务运行的同时，可以继续执行其他任务。异步操作可以在单线程或多线程环境中进行。在单线程环境中，异步操作通常通过事件循环和回调函数实现。在多线程环境中，异步操作可以通过创建新的线程来实现。
在我们说到线程的执行方式时，同步 (synchronous) 和异步 (asynchronous) 是这个话题中最基本的一组概念。**同步操作**意味着在操作完成之前，运行这个操作的线程都将被占用，直到函数最终被抛出或者返回。Swift 5.5 之前，所有的函数都是同步函数，我们简单地使用 `func` 关键字来声明这样一个同步函数：

```swift
var results: [String] = []<br>func addAppending(_ value: String, to string: String) {<br>    results.append(value.appending(string))<br>}
```

`addAppending` 是一个同步函数，在它返回之前，运行它的线程将无法执行其他操作，或者说它不能被用来运行其他函数，必须等待当前函数执行完成后这个线程才能做其他事情。

![](https://onevcat.com/assets/images/2021/sync-func.png)

在 iOS 开发中，我们使用的 UI 开发框架，也就是 UIKit 或者 SwiftUI，不是线程安全的：对用户输入的处理和 UI 的绘制，必须在与主线程绑定的 main runloop 中进行。假设我们希望用户界面以每秒 60 帧的速率运行，那么主线程中每两次绘制之间，所能允许的处理时间最多只有 16 毫秒 (1 / 60s)。当主线程中要同步处理的其他操作耗时很少时 (比如我们的 `addAppending`，可能耗时只有几十纳秒)，这不会造成什么问题。但是，如果这个同步操作耗时过长的话，主线程将被阻塞。它不能接受用户输入，也无法向 GPU 提交请求去绘制新的 UI，这将导致用户界面掉帧甚至卡死。这种“长耗时”的操作，其实是很常见的：比如从网络请求中获取数据，从磁盘加载一个大文件，或者进行某些非常复杂的加解密运算等。

下面的 `loadSignature` 从某个网络 URL 读取字符串：如果这个操作发生在主线程，且耗时超过 16ms (这是很可能发生的，因为通过握手协议建立网络连接，以及接收数据，都是一系列复杂操作)，那么主线程将无法处理其他任何操作，UI 将不会刷新。

```swift
// 从网络读取一个字符串
func loadSignature() throws -> String? {
// someURL 是远程 URL，比如 https://example.com  
let data = try Data(contentsOf: someURL)  return String(data: data, encoding: .utf8)
}
```

![](https://onevcat.com/assets/images/2021/sync-func-block-ui.png)

`loadSignature` 最终的耗时超过 16 ms，对 UI 的刷新或操作的处理不得不被延后。在用户观感上，将表现为掉帧或者整个界面卡住。这是客户端开发中绝对需要避免的问题之一。

Swift 5.5 之前，要解决这个问题，最常见的做法是将耗时的同步操作转换为**异步操作**：把实际长时间执行的任务放到另外的线程 (或者叫做后台线程) 运行，然后在操作结束时提供运行在主线程的回调，以供 UI 操作之用：

```swift
func loadSignature(
  _ completion: @escaping (String?, Error?) -> Void
)
{
  DispatchQueue.global().async {
    do {
      let d = try Data(contentsOf: someURL)
      DispatchQueue.main.async {
        completion(String(data: d, encoding: .utf8), nil)
      }
    } catch {
      DispatchQueue.main.async {
        completion(nil, error)
      }
    }
  }
}
```

![](https://onevcat.com/assets/images/2021/sync-func-dispatch.png)

`DispatchQueue.global` 负责将任务添加到全局后台派发队列。在底层，[GCD 库](https://en.wikipedia.org/wiki/Grand_Central_Dispatch) (Grand Central Dispatch) 会进行线程调度，为实际耗时繁重的 `Data.init(contentsOf:)` 分配合适的线程。耗时任务在主线程外进行处理，完成后再由 `DispatchQueue.main` 派发回主线程，并按照结果调用 `completion` 回调方法。这样一来，主线程不再承担耗时任务，UI 刷新和用户事件处理可以得到保障。

异步操作虽然可以避免卡顿，但是使用起来存在不少问题，最主要包括：

- 错误处理隐藏在回调函数的参数中，无法用 `throw` 的方式明确地告知并强制调用侧去进行错误处理。
- 对回调函数的调用没有编译器保证，开发者可能会忘记调用 `completion`，或者多次调用 `completion`。
- 通过 `DispatchQueue` 进行线程调度很快会使代码复杂化。特别是如果线程调度的操作被隐藏在被调用的方法中的时候，不查看源码的话，在 (调用侧的) 回调函数中，几乎无法确定代码当前运行的线程状态。
- 对于正在执行的任务，没有很好的取消机制。

除此之外，还有其他一些没有列举的问题。它们都可能成为我们程序中潜在 bug 的温床，在之后关于异步函数的章节里，我们会再回顾这个例子，并仔细探讨这些问题的细节。

需要进行说明的是，虽然我们将运行在后台线程加载数据的行为称为**异步操作**，但是接受回调函数作为参数的 `loadSignature(_:)` 方法，其本身依然是一个**同步函数**。这个方法在返回前仍旧会占据主线程，只不过它现在的执行时间非常短，UI 相关的操作不再受影响。

Swift 5.5 之前，Swift 语言中并没有真正异步函数的概念，我们稍后会看到使用 `async` 修饰的异步函数是如何简化上面的代码的。

## 4. 串行和并行

另外一组重要的概念是串行和并行。对于通过同步方法执行的同步操作来说，这些操作一定是以串行方式在同一线程中发生的。“做完一件事，然后再进行下一件事”，是最常见的、也是我们人类最容易理解的代码执行方式：

```swift
if let signature = try loadSignature() {  addAppending(signature, to: "some data")}
print(results)
```

`loadSignature`，`addAppending` 和 `print` 被顺次调用，它们在同一线程中按严格的先后顺序发生。这种执行方式，我们将它称为**串行 (serial)**。

![](https://onevcat.com/assets/images/2021/serial-sync.png)

**同步方法执行的同步操作**，是串行的充分但非必要条件。异步操作也可能会以串行方式执行。假设除了 `loadSignature(_:)` 以外，我们还有一个从数据库里读取一系列数据的函数，它使用类似的方法，把具体工作放到其他线程异步执行：

```swift
func loadFromDatabase(  _ completion: @escaping ([String]?, Error?) -> Void){  // ...<br>}
```

如果我们先从数据库中读取数据，在完成后再使用 `loadSignature` 从网络获取签名，最后将签名附加到每一条数据库中取出的字符串上，可以这么写：

```
loadFromDatabase { (strings, error) in

if let strings = strings {

loadSignature { signature, error in

if let signature = signature {

strings.forEach {

strings.forEach {

strings.forEach {

addAppending(signature, to: $0)

}

} else {

print("Error")

}

}

} else {

print("Error.")

}

}
```

虽然这些操作是**异步**的，但是它们 (从数据库读取 `[String]`，从网络下载签名，最后将签名添加到每条数据中) 依然是**串行**的，加载签名必定发生在读取数据库完成之后，而最后的 `addAppending` 也必然发生在 `loadSignature` 之后：

![](https://onevcat.com/assets/images/2021/serial-async.png)

> 虽然图中把 `loadFromDatabase` 和 `loadSignature` 画在了同一个线程里，但事实上它们有可能是在不同线程执行的。不过在上面代码的情况下，它们的先后次序依然是严格不变的。

事实上，虽然最后的 `addAppending` 任务同时需要原始数据和签名才能进行，但 `loadFromDatabase` 和 `loadSignature` 之间其实并没有依赖关系。如果它们能够一起执行的话，我们的程序有很大机率能变得更快。这时候，我们会需要更多的线程，来同时执行两个操作：

// loadFromDatabase { (strings, error) in<br>//     ...<br>//     loadSignature { signature, error in {<br>//     ...<br><br>// 可以将串行调用替换为：<br><br>loadFromDatabase { (strings, error) in<br>    //...<br>}<br><br>loadSignature { signature, error in<br>    //...<br>}|

> 为了确保在 `addAppending` 执行时，从数据库加载的内容和从网络下载的签名都已经准备好，我们需要某种手段来确保这些数据的可用性。在 GCD 中，通常可以使用 `DispatchGroup` 或者 `DispatchSemaphore` 来实现这一点。但是我们并不是一本探讨 GCD 的书籍，所以这部分内容就略过了。

两个 `load` 方法同时开始工作，理论上资源充足的话 (足够的 CPU，网络带宽等)，现在它们所消耗的时间会小于串行时的两者之和：

![](https://onevcat.com/assets/images/2021/parallel-async.png)

这时候，`loadFromDatabase` 和 `loadSignature` 这两个异步操作，在不同的线程中同时执行。对于这种拥有多套资源同时执行的方式，我们就将它称为**并行 (parallel)**。

## Swift 并发是什么

在有了这些基本概念后，最后可以谈谈关于并发 (concurrency) 这个名词了。在计算机科学中，并发指的是多个计算同时执行的特性。并发计算中涉及的**同时执行**，主要是若干个操作的开始和结束时间之间存在重叠。它并不关心具体的执行方式：我们可以把同一个线程中的多个操作交替运行 (这需要这类操作能够暂时被置于暂停状态) 叫做并发，这几个操作将会是分时运行的；我们也可以把在不同处理器核心中运行的任务叫做并发，此时这些任务必定是并行的。

而当 Apple 在定义“Swift 并发”是什么的时候，和上面这个经典的计算机科学中的定义实质上没有太多不同。Swift 官方文档给出了这样的解释：

> Swift 提供内建的支持，让开发者能以结构化的方式书写异步和并行的代码，… 并发这个术语，指的是异步和并行这一常见组合。

所以在提到 Swift 并发时，它指的就是**异步和并行代码的组合**。这在语义上，其实是传统并发的一个子集：它限制了实现并发的手段就是异步代码，这个限定降低了我们理解并发的难度。在本书中，如果没有特别说明，我们在提到 Swift 并发时，指的都是“异步和并行代码的组合”这个简化版的意义，或者专指 Swift 5.5 中引入的这一套处理并发的语法和框架。

除了定义方式稍有不同之外，Swift 并发和其他编程语言在处理同样问题时所面临的挑战几乎一样。从戴克斯特拉 (Edsger W. Dijkstra) 提出信号量 (semaphore) 的概念起，到东尼・霍尔爵士 (Tony Hoare) 使用 [CSP](https://zh.wikipedia.org/wiki/%E4%BA%A4%E8%AB%87%E5%BE%AA%E5%BA%8F%E7%A8%8B%E5%BC%8F) 描述和尝试解决[哲学家就餐问题](https://zh.wikipedia.org/wiki/%E5%93%B2%E5%AD%A6%E5%AE%B6%E5%B0%B1%E9%A4%90%E9%97%AE%E9%A2%98)，再到 actor 模型或者通道模型 (channel model) 的提出，并发编程最大的困难，以及这些工具所要解决的问题大致上只有两个：

1. 如何确保不同运算运行步骤之间的交互或通信可以按照正确的顺序执行
2. 如何确保运算资源在不同运算之间被安全地共享、访问和传递

第一个问题负责并发的逻辑正确，第二个问题负责并发的内存安全。在以前，开发者在使用 GCD 编写并发代码时往往需要很多经验，否则难以正确处理上述问题。Swift 5.5 设计了**异步函数**的书写方法，在此基础上，利用**结构化并发**确保运算步骤的交互和通信正确，利用 **actor 模型**确保共享的计算资源能在隔离的情况下被正确访问和操作。它们组合在一起，提供了一系列工具让开发者能简单地编写出稳定高效的并发代码。我们接下来，会浅显地对这几部分内容进行瞥视，并在后面对各个话题展开探究。

> 戴克斯特拉还发表了著名的《GOTO 语句有害论》(Go To Statement Considered Harmful)，并和霍尔爵士一同推动了结构化编程的发展。霍尔爵士在稍后也提出了对 null 的反对，最终促成了现代语言中普遍采用的 `Optional` (或者叫别的名称，比如 `Maybe` 或 null safety 等) 设计。如果没有他们，也许我们今天在编写代码时还在处理无尽的 goto 和 null 检查，会要辛苦很多。


## 异步函数

为了更容易和优雅地解决上面两个问题，Swift 需要在语言层面引入新的工具：第一步就是添加异步函数的概念。在函数声明的返回箭头前面，加上 `async` 关键字，就可以把一个函数声明为异步函数：

func loadSignature() async throws -> String {<br>  fatalError("暂未实现")<br>}

异步函数的 `async` 关键字会帮助编译器确保两件事情：

1. 它允许我们在函数体内部使用 `await` 关键字；
2. 它要求其他人在调用这个函数时，使用 `await` 关键字。

这和与它处于类似位置的 `throws` 关键字有点相似。在使用 `throws` 时，它允许我们在函数内部使用 `throw` 抛出错误，并要求调用者使用 `try` 来处理可能的抛出。`async` 也扮演了这样一个角色，它要求在特定情况下对当前函数进行标记，这是对于开发者的一种明确的提示，表明这个函数有一些特别的性质：`try/throw` 代表了函数可以被抛出，而 `await` 则代表了函数在此处可能会**放弃当前线程**，它是程序的**潜在暂停点**。

放弃线程的能力，意味着异步方法可以被“暂停”，这个线程可以被用来执行其他代码。如果这个线程是主线程的话，那么界面将不会卡顿。被 `await` 的语句将被底层机制分配到其他合适的线程，在执行完成后，之前的“暂停”将结束，异步方法从刚才的 `await` 语句后开始，继续向下执行。

关于异步函数的设计和更多深入内容，我们会在随后的相关章节展开。在这里，我们先来看看一个简单的异步函数的使用。Foundation 框架中已经为我们提供了很多异步函数，比如使用 `URLSession` 从某个 `URL` 加载数据，现在也有异步版本了。在由 `async` 标记的异步函数中，我们可以调用其他异步函数：

```swift
func loadSignature() async throws -> String? {  let (data, _) = try await URLSession.shared.data(from: someURL)  return String(data: data, encoding: .utf8)}
```

> 这些 Foundation，或者 AppKit 或 UIKit 中的异步函数，有一部分是重写和新添加的，但更多的情况是由相应的 Objective-C 接口转换而来。满足一定条件的 Objective-C 函数，可以直接转换为 Swift 的异步函数，非常方便。在后一章我们也会具体谈到。

如果我们把 `loadFromDatabase` 也写成异步函数的形式。那么，在上面串行部分，原本的嵌套式的异步操作代码：

```swift
loadFromDatabase { (strings, error) in
  if let strings = strings {
    loadSignature { signature, error in
      if let signature = signature {
        strings.forEach { 
                strings.forEach { 
        strings.forEach { 
          addAppending(signature, to: $0)
        }
      } else {
        print("Error")
      }
    }
  } else {
    print("Error.")
  }
}
```

就可以非常简单地写成这样的形式：

```swift
let strings = try await loadFromDatabase()
if let signature = try await loadSignature() {
  strings.forEach { 
    addAppending(signature, to: $0)
  }
} else {
  throw NoSignatureError()
}
```
不用多说，单从代码行数就可以一眼看清优劣了。异步函数极大简化了异步操作的写法，它避免了内嵌的回调，将异步操作按照顺序写成了类似“同步执行”的方法。另外，这种写法允许我们使用 try/throw 的组合对错误进行处理，编译器会对所有的返回路径给出保证，而不必像回调那样时刻检查是不是所有的路径都进行了处理。

## Task

在 Swift 中，`Task` 是 Swift 5.5 中引入的新特性，它是并发编程的一部分。`Task` 闭包通常用于异步操作。

以下是一个基本的 `Task` 闭包的使用示例：

```swift
Task {
    do {
        let data = try await fetchDataFromServer()
        process(data)
    } catch {
        print("Failed to fetch data: \(error)")
    }
}
```

在这个例子中，我们创建了一个新的 `Task`，并在其中执行异步操作。`fetchDataFromServer` 是一个异步函数，它可能会抛出错误，所以我们使用 `try await` 来调用它，并处理可能的错误。

注意，`Task` 闭包必须在支持并发的环境中使用，例如在 SwiftUI 的 `onAppear` 方法中，或者在你自己的并发代码中。


在 Swift 中，`Task {}` 是 Swift 5.5 引入的新特性，它是用于并发编程的一种新方式。`Task {}` 创建一个新的轻量级任务，这个任务可以在后台并发地执行一些工作。

`Task {}` 中的代码是异步的，这意味着它可以在等待某些操作完成（例如网络请求）时让出控制权，而不会阻塞当前的线程。这使得你可以在不阻塞 UI 线程的情况下执行一些耗时的操作，从而提高应用的响应性。

以下是一个 `Task {}` 的例子：

```swift
Task {
    do {
        let data = try await fetchDataFromNetwork()
        process(data)
    } catch {
        print("Failed to fetch data: \(error)")
    }
}
```

在这个例子中，`fetchDataFromNetwork()` 是一个异步函数，它可能需要一些时间来完成。通过将这个函数放在 `Task {}` 中，我们可以在等待这个函数完成时让出控制权，从而避免阻塞当前的线程。

请注意，`Task {}` 只能在支持并发的环境中使用，例如在 Swift 5.5 或更高版本的环境中，以及在支持并发的平台（例如 iOS 15 或更高版本）上。

**Task是在后台线程执行吗？**

Swift 中的 `Task` 并不直接关联到具体的线程。它们是在 Swift 的新并发模型中运行的，这个模型是基于协程的，而不是基于线程的。

当你创建一个 `Task` 时，它的执行可能会跨越多个线程。例如，一个任务可能在一个线程开始，然后在等待一个异步操作（如网络请求）完成时让出控制权，然后在另一个线程上继续执行。这个过程是由 Swift 的运行时系统自动管理的，你不需要（也不能）直接控制它。

然而，你可以认为 `Task` 是在后台执行的，因为它们不会阻塞当前的线程。这使得你可以在不阻塞 UI 线程的情况下执行一些耗时的操作，从而提高应用的响应性。

## await
在 Swift 中，`await` 关键字用于等待一个异步操作完成。`await` 只能在 `async` 函数或方法中使用。

在你的代码中，`saveImagesToPhotoAlbum` 是一个异步函数，这意味着它可能会花费一些时间来完成，例如，它可能需要从网络下载图片，或者将图片保存到照片库。在这种情况下，你需要使用 `await` 关键字来等待操作完成。

以下是如何在另一个异步函数中使用 `await` 来调用 `saveImagesToPhotoAlbum` 的示例：

```swift
func processImages() async {
    let images = [UIImage(named: "image1")!, UIImage(named: "image2")!]
    await saveImagesToPhotoAlbum(images: images)
}
```

在这个例子中，我们在 `processImages` 函数中调用 `saveImagesToPhotoAlbum` 函数，并使用 `await` 关键字等待它完成。注意，因为 `await` 只能在 `async` 函数中使用，所以 `processImages` 函数也必须被声明为 `async`。

## 结构化并发

文章出处：[https://www.bilibili.com/read/cv25781780/]


> [!定义] 『即使进行并发操作，也要保证控制流路径的单一入口和单一出口。程序可以产生多个控制流来实现并发，但是所有的并发路径在出口时都应该处于完成 (或取消) 状态，并合并到一起。』 

好处是：使抽象层得以有效运作。在这一结构下编码时要可以拍着胸脯保证代码不会跳转到结构外，是严格『自包含』的。 

同步 synchronous
异步 asynchronous

UIKit和SwiftUI都不是线程安全的：

    对于用户输入的处理和UI的绘制，必须在与主线程绑定的main runloop中进行。

为避免长耗时操作将主线程堵塞导致用户输入无响应、UI卡顿，最常见的应对办法是将同步操作转换成异步操作：

    开辟后台线程运行长耗时操作，然后在操作结束时提供运行在主线程的回调 
    并发编程的困难大致上有两个：

 如何确保顺序执行；————逻辑正确性

 如何确保运算资源调度、访问不冲突。————内存安全性

异步函数
为了化解并发编程的如上两个困难，引入异步函数

``` swift
func loadSignature() async throws -> String {

    fatalError("暂未实现")

}
```



在返回箭头前加上 async 关键字就可以把函数声明为异步函数。

与 throw 关键字类似地，该关键字帮助编译器确保两件事：

 它允许在函数体内部（正确地）使用 await 关键字；

 它要求其他来源在调用这个函数时，使用 await 关键字。

await 代表了函数在此处可能会放弃当前线程，它是程序的潜在暂停点。

Task 任务
对于同步函数来说，线程决定了它的执行环境。

对于异步函数来说，任务决定了它的执行环境。

『Swift 并发编程中，结构化并发需要依赖异步函数，而异步函数又必须运行在某个任务上下文中，因此可以说，想要进行结构化并发，必须具有任务上下文。

实际上，Swift 结构化并发就是以任务为基本要素进行组织的。』

简单地使用 Task.init 就可以让我们获取一个任务执行的上下文环境，它接受 `async` 标记的闭包。而且能继承当前任务上下文的优先级等特性，创建一个新的任务树的根节点。我们可以在其中使用异步函数，用法类似于 Task { 异步代码 } 。



> Task的要点

> 创建、组织、检查和取消任务

> 一个任务具有它自己的优先级和取消标识，它可以拥有若干个子任务并在其中执行异步函数。

> 无论是正常完成还是抛出错误，子任务会将结果向上报告给父任务，在所有子任务完成之前 (不论是正常结束还是抛出)，父任务是不会完成的。

> 当一个父任务被取消时，这个父任务的取消标识将被设置，并向下传递到所有的子任务中去。

Task Group 任务组
在任务运行上下文中，或具体来说——

在某个异步函数中，我们可以通过await withTaskGroup 为当前的任务添加一组结构化的并发子任务。

这些子任务在被添加后立刻开始执行，最终在离开group的作用域时再汇集到一起。

async let 异步绑定
类似于 let 地， async let 定义一条局部的不变变量，并通过等号右侧的表达式来初始化该不变变量。

不同的是，该初始化表达式必须是异步函数的调用，通过将其绑定到该不变变量上，在当前 Task 上下文创建一道并发执行的子任务并立刻加以执行。

async let 赋值之后将立刻执行，即使在 await 之前执行就已经完成，其结果依然可以等到 await 语句时再进行求值。

和 Task.init 新建一个任务根节点不同，async let 所创建的子任务是任务树上的叶子节点。

任务组和异步绑定的对比
async let 可以理解成任务组如 withTaskGroup 的语法糖，但是异步绑定并不能动态地表达任务的数量。

『一个大致的使用原则是，如果我们需要比较「严肃地」界定结构化并发的起始，那么用任务组 Task Group 的闭包将它限制起来，并发的结构会显得更加清晰；

而如果我们只是想要快速地并发开始少数几个任务，并减少其他模板代码的干扰，那么使用 async let 进行异步绑定，会让代码更简洁易读。』 作者：甜菜根战士骆驼驼背 https://www.bilibili.com/read/cv25781780/ 出处：bilibili


## 并发安全

Swift中的并发安全性是通过以下两种方式来保证的：

1. 互斥锁（Mutex）：Swift提供了一些线程安全的数据结构，如DispatchQueue、DispatchGroup和OperationQueue，这些结构在内部使用了互斥锁来确保只有一个线程可以访问它们的数据。通过使用这些数据结构来管理并发任务的执行，可以有效地避免并发访问导致的数据竞争和数据损坏。

2. 值类型（Value Types）：Swift中的值类型（如结构体和枚举）是并发安全的，因为它们在多个线程之间可以安全地进行复制和传递，而不会造成数据竞争。相比之下，引用类型（如类）在多个线程中共享时需要通过互斥锁来确保并发访问的安全性。

通过使用互斥锁和值类型，Swift可以保证并发操作的安全性，从而避免数据竞争和其他并发访问带来的问题。

---
# swift的属性

介绍：在Swift中，属性可以分为实例属性和类型属性。实例属性是属于特定类型实例的属性，而类型属性是属于类型本身的属性。

实例属性可以进一步分为**存储属性**和**计算属性**。存储属性存储常量和变量值，计算属性则提供一个getter和一个可选的setter来间接获取和设置其他属性和值。

类型属性可以是变量属性（用关键字`static`标记）或常量属性（用关键字`static let`标记）。类型属性是延迟初始化的，它们只会在第一次访问时初始化，并且只会初始化一次。

以下是Swift中的实例属性和类型属性的示例：

```swift
struct SomeStructure {
    // 存储实例属性
    var storedInstanceProperty = "Some value"
    // 计算实例属性
    var computedInstanceProperty: Int {
        return 1
    }
    
    // 类型属性
    static var storedTypeProperty = "Some value"
    static var computedTypeProperty: Int {
        return 6
    }
}

// 访问实例属性
let someInstance = SomeStructure()
print(someInstance.storedInstanceProperty)  // 输出 "Some value"
print(someInstance.computedInstanceProperty)  // 输出 "1"

// 访问类型属性
print(SomeStructure.storedTypeProperty)  // 输出 "Some value"
print(SomeStructure.computedTypeProperty)  // 输出 "6"
```

在Swift中，没有所谓的"动态属性"。如果你是指能够在运行时改变的属性，那么这可以通过存储属性或计算属性来实现，因为它们的值可以在运行时改变。

## `static` 静态属性(类属性)


在Swift中，`static`关键字用于定义类的静态成员。静态成员是属于类本身的，而不是类的实例的。这意味着你可以直接通过类来访问这些成员，而不需要创建类的实例。

例如，如果你有一个名为`MyClass`的类，它有一个静态方法`myMethod`，你可以直接通过`MyClass.myMethod()`来调用这个方法，而不需要先创建`MyClass`的实例。

同样，你也可以定义静态属性。静态属性的值是共享的，所有的类实例都会看到相同的值。

需要注意的是，`static`关键字在类（class）中定义的静态成员不能被子类重写。如果你想允许子类重写父类的静态成员，你应该使用`class`关键字代替`static`。但是，`class`关键字只能用于类的方法，不能用于属性或者下标。

静态属性是属于一个类的属性，而不是属于这个类的实例的属性。你可以直接通过类名来访问静态属性，而不需要创建类的实例。在Swift中，你可以使用`static`关键字来定义静态属性。

这是一个例子：

```swift
class MyClass {
    static var myStaticProperty = "Hello, world!"
}

print(MyClass.myStaticProperty) // 输出 "Hello, world!"
```

在这个例子中，`myStaticProperty`是一个静态属性。你可以直接通过`MyClass.myStaticProperty`来访问它，而不需要创建`MyClass`的实例。

静态属性在所有的类实例之间是共享的。这意味着，如果你在一个地方更改了静态属性的值，那么在其他地方访问这个静态属性时，你会看到这个更改。

在你的`MainViewModel`中，`shared`是一个静态属性。这意味着，无论你在哪里访问`MainViewModel.shared`，你都会得到同一个`MainViewModel`实例。这就是为什么你可以在一个地方更改`.photos`属性，然后在其他地方看到这个更改的原因。

在Swift中，静态属性是指属于类型本身，而不是类型实例的属性。它们被所有的实例共享。静态属性可以是变量（用`static`关键字标记）或常量（用`static let`关键字标记）。

静态属性是延迟初始化的，也就是说，直到第一次访问它们时，它们才会被初始化。并且，一旦被初始化，它们就不会再次初始化。

以下是一个Swift静态属性的示例：

```swift
struct SomeStructure {
    // 静态存储属性
    static var storedTypeProperty = "Some value"
    // 静态计算属性
    static var computedTypeProperty: Int {
        return 6
    }
}

// 访问静态属性
print(SomeStructure.storedTypeProperty)  // 输出 "Some value"
print(SomeStructure.computedTypeProperty)  // 输出 "6"
```

在这个例子中，`storedTypeProperty`和`computedTypeProperty`都是静态属性。它们属于`SomeStructure`类型，而不是`SomeStructure`的任何实例。因此，我们可以直接通过类型名来访问这些属性，而不需要创建类型的实例。


## Swift计算属性


==解释==

在Swift中，计算属性并不直接存储值，而是提供一个getter和一个可选的setter来间接获取和设置其他属性或变量的值。

计算属性可以用于类（Class）、结构体（Struct）和枚举（Enum）。它们的定义方式如下：

```swift
struct Rectangle {
    var width = 0.0, height = 0.0
    var area: Double {
        get {
            return width * height
        }
        set(newArea) {
            width = sqrt(newArea)
            height = sqrt(newArea)
        }
    }
}
```

在这个例子中，`area`就是一个计算属性。当你获取这个属性的值时，它会返回`width * height`的结果。当你设置这个属性的值时，它会同时更新`width`和`height`的值。

注意，setter的参数`newArea`是可选的，如果你不提供，那么可以使用默认的参数名`newValue`。同时，如果你的计算属性只有getter，没有setter，那么这个属性就是只读的，你可以省略`get`关键字，直接返回一个值，如下：

```swift
struct Rectangle {
    var width = 0.0, height = 0.0
    var area: Double {
        return width * height
    }
}
```

在这个例子中，`area`就是一个只读的计算属性。

 转载

[mb5fe559d8b9ae4](https://blog.51cto.com/u_15067227)2016-10-11 09:58:00

**_文章标签_[初始化](https://blog.51cto.com/search/result?q=%E5%88%9D%E5%A7%8B%E5%8C%96)[封装](https://blog.51cto.com/topic/fengzhuang.html)[运算符](https://blog.51cto.com/search/result?q=%E8%BF%90%E7%AE%97%E7%AC%A6)[显式](https://blog.51cto.com/search/result?q=%E6%98%BE%E5%BC%8F)[5e](https://blog.51cto.com/topic/5e.html)****_文章分类_[代码人生](https://blog.51cto.com/nav/code)****_阅读数_**72****

除存储属性外，类、结构体和枚举可以定义_计算属性_，计算属性不直接存储值，而是提供一个 getter 来获取值，一个可选的 setter 来间接设置其他属性或变量的值。

```swift
struct Point {
    var x = 0.0, y = 0.0
}
struct Size {
    var width = 0.0, height = 0.0
}
struct Rect {
    var origin = Point()
    var size = Size()
    var center: Point {
    get {
        let centerX = origin.x + (size.width / 2)
        let centerY = origin.y + (size.height / 2)
        return Point(x: centerX, y: centerY)
    }
    set(newCenter) {
        origin.x = newCenter.x - (size.width / 2)
        origin.y = newCenter.y - (size.height / 2)
    }
    }
}
var square = Rect(origin: Point(x: 0.0, y: 0.0),
    size: Size(width: 10.0, height: 10.0))
let initialSquareCenter = square.center
square.center = Point(x: 15.0, y: 15.0)
println("square.origin is now at (\(square.origin.x), \(square.origin.y))")
// 输出 "square.origin is now at (10.0, 10.0)”
```

这个例子定义了 3 个几何形状的结构体：

- `Point`封装了一个`(x, y)`的坐标
- `Size`封装了一个`width`和`height`
- `Rect`表示一个有原点和尺寸的矩形

`Rect`也提供了一个名为`center`的计算属性。一个矩形的中心点可以从原点和尺寸来算出，所以不需要将它以显式声明的`Point`来保存。`Rect`的计算属性`center`提供了自定义的 getter 和 setter 来获取和设置矩形的中心点，就像它有一个存储属性一样。

例子中接下来创建了一个名为`square`的`Rect`实例，初始值原点是`(0, 0)`，宽度高度都是`10`。如图所示蓝色正方形。

`square`的`center`属性可以通过点运算符(`square.center`)来访问，这会调用 getter 来获取属性的值。跟直接返回已经存在的值不同，getter 实际上通过计算然后返回一个新的`Point`来表示`square`的中心点。如代码所示，它正确返回了中心点`(5, 5)`。

`center`属性之后被设置了一个新的值`(15, 15)`，表示向右上方移动正方形到如图所示橙色正方形的位置。设置属性`center`的值会调用 setter 来修改属性`origin`的`x`和`y`的值，从而实现移动正方形到新的位置。

![Swift计算属性_封装](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Art/computedProperties_2x.png)

### 便捷 setter 声明

如果计算属性的 setter 没有定义表示新值的参数名，则可以使用默认名称`newValue`。下面是使用了便捷 setter 声明的`Rect`结构体代码：

```swift
struct AlternativeRect {
    var origin = Point()
    var size = Size()
    var center: Point {
    get {
        let centerX = origin.x + (size.width / 2)
        let centerY = origin.y + (size.height / 2)
        return Point(x: centerX, y: centerY)
    }
    set {
        origin.x = newValue.x - (size.width / 2)
        origin.y = newValue.y - (size.height / 2)
    }
    }
}
```

### 只读计算属性

只有 getter 没有 setter 的计算属性就是_只读计算属性_。只读计算属性总是返回一个值，可以通过点运算符访问，但不能设置新的值。

<<<<<<< HEAD

>   
> 注意：
> 
> #### 必须使用`var`关键字定义计算属性，包括只读计算属性，因为他们的值不是固定的。`let`关键字只用来声明常量属性，表示初始化后再也无法修改的值。
> 
> 注意：
> 
> 必须使用`var`关键字定义计算属性，包括只读计算属性，因为它们的值不是固定的。`let`关键字只用来声明常量属性，表示初始化后再也无法修改的值。
> 
> > > > > > > a516af6a531a104ec88da0d236ecf389a5ec72af  
> > > > > > >  

只读计算属性的声明可以去掉`get`关键字和花括号：

```swift
struct Cuboid {
    var width = 0.0, height = 0.0, depth = 0.0
    var volume: Double {
    return width * height * depth
    }
}
let fourByFiveByTwo = Cuboid(width: 4.0, height: 5.0, depth: 2.0)
println("the volume of fourByFiveByTwo is \(fourByFiveByTwo.volume)")
// 输出 "the volume of fourByFiveByTwo is 40.0"
```

这个例子定义了一个名为`Cuboid`的结构体，表示三维空间的立方体，包含`width`、`height`和`depth`属性，还有一个名为`volume`的只读计算属性用来返回立方体的体积。设置`volume`的值毫无意义，因为通过`width`、`height`和`depth`就能算出`volume`。然而，`Cuboid`提供一个只读计算属性来让外部用户直接获取体积是很有用的。

## SwiftUI中的计算属性

是的，`var body: some View` 在 SwiftUI 中是一个计算属性。这个属性负责定义视图的内容和布局。

`body` 是一个==只读的计算属性==，你只需要提供一个 getter，不需要提供 setter。当 SwiftUI 需要渲染视图或者视图的状态发生改变时，就会访问这个属性。

例如，下面是一个简单的 SwiftUI 视图，它有一个 `body` 计算属性：

```swift
struct ContentView: View {
    var body: some View {
        Text("Hello, world!")
            .padding()
    }
}
```

在这个例子中，`body` 属性返回一个 `Text` 视图，这个视图显示了 "Hello, world!" 并且有一些内边距。


## swift中计算属性与存储属性的关系

是的，Swift中的存储属性默认有getter和setter（除非它是一个常量存储属性，常量存储属性只有getter，没有setter，因为它的值不能被改变）。

你可以直接访问或修改存储属性的值，就像它是一个普通的变量或常量一样。例如：

```swift
struct Car {
    var color: String
}

var myCar = Car(color: "Red")
print(myCar.color) // 输出 "Red"

myCar.color = "Blue"
print(myCar.color) // 输出 "Blue"
```

在这个例子中，`color`是一个存储属性。你可以通过`.`语法来获取或设置它的值。

虽然存储属性有默认的getter和setter，但你不能提供自定义的getter和setter。如果你需要在获取或设置属性的值时执行一些自定义的操作，你应该使用计算属性。

---

# 多线程与异步
多线程和异步是两个在并发编程中经常被提到的概念，它们之间有一定的关系，但也有区别。

1. 多线程：多线程是指程序中包含两个或多个并行运行的线程，每个线程都在处理不同的任务。在多线程环境中，CPU可以在多个线程之间进行切换，以实现并行处理。多线程可以提高程序的执行效率，但也会带来一些复杂性，比如线程同步和数据竞争等问题。

2. 异步：异步是指程序不必等待某个长时间运行的任务完成，而是在这个任务运行的同时，可以继续执行其他任务。异步操作可以在单线程或多线程环境中进行。在单线程环境中，异步操作通常通过事件循环和回调函数实现。在多线程环境中，异步操作可以通过创建新的线程来实现。

多线程和异步的关系是：多线程是实现异步的一种方式，但并不是唯一的方式。异步操作可以在单线程环境中通过非阻塞 I/O 和事件驱动编程实现，也可以在多线程环境中通过线程创建和管理实现。


在 Swift 5.5 及更高版本中，`async` 关键字用于定义异步函数。异步函数是一种可以在等待某些操作完成时释放其执行上下文的函数，这样其他函数或任务就可以在等待时执行。

以下是一个简单的异步函数的例子：

```swift
func fetchUser() async -> User {
    // 模拟网络请求
    await sleep(2)
    return User(name: "John Doe")
}
```

在这个例子中，`fetchUser` 是一个异步函数，它返回一个 `User`。`await sleep(2)` 是一个异步操作，它会暂停 `fetchUser` 的执行，直到 `sleep(2)` 完成。在等待 `sleep(2)` 期间，`fetchUser` 的执行上下文被释放，这样其他函数或任务就可以执行。

请注意，你只能在异步上下文中调用异步函数，例如在另一个异步函数中，或者在使用 `Task` API 创建的任务中。例如，你可以这样调用 `fetchUser`：

```swift
Task {
    let user = await fetchUser()
    print(user.name)
}
```

在这个例子中，我们使用 `Task` API 创建了一个新的任务，并在这个任务中调用了 `fetchUser`。

## 多线程与同步，异步的概念

同步、异步、线程这三个概念在编程中都非常重要，它们之间的关系可以从以下几个方面来理解：

1. **同步与异步**：这两个概念主要描述的是程序的执行流程。同步意味着程序的执行必须按照一定的顺序，一个任务必须完成后，下一个任务才能开始。异步则意味着程序的执行不需要按照一定的顺序，一个任务的开始不需要等待上一个任务完成，可以并行执行。

2. **线程**：线程是操作系统能够进行运算调度的最小单位。它被包含在进程之中，是进程中的实际运作单位。一条线程指的是进程中一个单一顺序的控制流，一个进程中可以并发多个线程，每条线程并行执行不同的任务。

3. **同步、异步与线程的关系**：同步和异步主要描述的是任务的执行方式，而线程是实现这两种执行方式的一种手段。在单线程环境中，如果我们希望多个任务能够并行执行，那么就需要使用异步。在多线程环境中，我们可以通过创建多个线程来让多个任务并行执行，这既可以是同步的，也可以是异步的，取决于具体的实现。

例如，在 Swift 中，我们可以使用 `DispatchQueue` API 来在后台线程上执行任务，这可以是同步的，也可以是异步的。我们也可以使用 `async/await` 语法来编写异步代码，这种情况下，任务的执行可能会跨越多个线程，取决于具体的调度策略。



## 四种多线程的区别

-   
    pthread：运用C语言，是一套通用的API，可跨平台Unix/Linux/Windows。线程的生命周期由程序员管理。
- NSThread：面向对象，可直接操作线程对象。线程的生命周期由程序员管理。
- GCD：代替NSThread，可以充分利用设备的多核，自动管理线程生命周期。
- NSOperation：底层是GCD，比GCD多了一些方法，更加面向对象，自动管理线程生命周期。

## GCD
在Swift中，你可以使用`DispatchQueue`来在另一个线程上执行函数。这是一个例子：

```swift
DispatchQueue.global().async {
    // 在这里执行你的函数
}
```

在这个例子中，我们使用`DispatchQueue.global().async`来在全局队列的一个后台线程上执行函数。全局队列是并发的，所以你的函数可能会在任何一个可用的线程上执行。

如果你想在主线程上执行函数，你可以使用`DispatchQueue.main.async`：

```swift
DispatchQueue.main.async {
    // 在这里执行你的函数
}
```

在这个例子中，我们使用`DispatchQueue.main.async`来在主线程上执行函数。你应该在主线程上执行所有的UI更新，因为UI更新不是线程安全的。

注意，`async`方法是异步的，所以它不会阻塞当前线程。如果你想要阻塞当前线程，直到函数执行完成，你可以使用`sync`方法。但是，你应该避免在主线程上使用`sync`方法，因为这可能会导致你的应用程序冻结。
在Swift中，你可以使用`DispatchQueue`的`async`方法来设置任务的优先级。你可以通过`qos`参数来设置优先级。这是一个例子：

```swift
DispatchQueue.global(qos: .userInitiated).async {
    // 在这里执行你的函数
}
```

在这个例子中，我们使用`DispatchQueue.global(qos: .userInitiated).async`来在全局队列的一个后台线程上执行函数，并设置了任务的优先级为`.userInitiated`。这意味着这个任务是由用户直接发起的，所以它应该尽快执行。

这是所有可用的优先级：

- `.userInteractive`: 这个优先级用于需要立即发生的任务，如UI更新。
- `.userInitiated`: 这个优先级用于由用户发起并需要立即知道结果的任务。
- `.default`: 这个优先级用于普通的任务。这是默认的优先级。
- `.utility`: 这个优先级用于不需要立即知道结果的任务，如下载文件。
- `.background`: 这个优先级用于用户不直接知道的任务，如索引数据库。

你可以根据你的需求来选择合适的优先级。

在Swift中，你可以使用`DispatchQueue`来创建一个新的线程，并在这个线程上执行异步任务。以下是如何修改你的`saveImagesToPhotoAlbum`函数来使用GCD执行异步任务：

```swift
func saveImagesToPhotoAlbum(images: [UIImage]) {
    DispatchQueue.global(qos: .background).async {
        for image in images  {
            UIImageWriteToSavedPhotosAlbum(image, self, #selector(self.image(_:didFinishSavingWithError:contextInfo:)), nil)
        }
    }
}
```

在这个例子中，`DispatchQueue.global(qos: .background).async`创建了一个新的后台线程，并在这个线程上执行闭包中的代码。`qos: .background`参数表示这个线程的优先级是后台级别，也就是说，它不会阻塞用户界面或者其他更重要的操作。

### sleep
在Swift中，你可以使用`Thread.sleep(forTimeInterval:)`或者`usleep()`函数来让当前线程暂停一段时间。

以下是使用`Thread.sleep(forTimeInterval:)`的示例，这个函数的参数是以秒为单位的时间间隔：

```swift
Thread.sleep(forTimeInterval: 1.0) // 暂停1秒
```

以下是使用`usleep()`的示例，这个函数的参数是以微秒为单位的时间间隔（1秒等于1,000,000微秒）：

```swift
usleep(1000000) // 暂停1秒
```

请注意，让线程暂停是一种阻塞操作，它会阻止线程执行其他任务。在主线程上使用这些函数可能会导致你的应用程序界面无响应。你应该尽量避免在主线程上使用这些函数，或者只在后台线程上使用它们。

---
# 响应式编程

#什么是响应式编程？

简介：

响应式编程是一种处理异步数据流的编程范式。在响应式编程中，数据被视为在时间上发生变化的流，你可以对这些流进行各种操作，比如过滤、转换、组合等。

响应式编程的核心是观察者模式。你可以创建一个可观察的数据源（通常被称为Observable），然后添加观察者（Observer）来监听这个数据源。当数据源发生变化时，所有的观察者都会收到通知。

响应式编程的一个主要优点是它可以简化异步编程。在传统的异步编程中，你可能需要使用回调、事件、线程等来处理异步操作，这可能会导致代码复杂且难以理解。而在响应式编程中，你可以使用统一的API来处理所有的异步操作，这可以让你的代码更加简洁、易读、易维护。

响应式编程在很多现代的编程语言和框架中都有应用，比如JavaScript的RxJS、Swift的RxSwift和Combine、Android的RxJava等。



## Combine

### `@ObservedObject, @StateObject, @EnromentObject` 和`ObservableObject`



在 SwiftUI 中，`@EnvironmentObject` 是一种属性包装器，它可以让你在视图层次结构的任何地方共享数据。这是一种依赖注入的方式，允许数据在视图之间流动。

首先，你需要有一个遵循 `ObservableObject` 协议的类。这个类的某些属性需要用 `@Published` 标记，这样当这些属性的值改变时，任何使用这些属性的视图都会更新。

```swift
class UserSettings: ObservableObject {
    @Published var username = "User"
}
```

然后，你可以在视图层次结构的顶部将这个类的一个实例作为环境对象注入：

```swift
let settings = UserSettings()

var body: some View {
    ContentView()
        .environmentObject(settings)
}
```

最后，你可以在任何需要这个数据的视图中使用 `@EnvironmentObject` 属性包装器：

```swift
struct ContentView: View {
    @EnvironmentObject var settings: UserSettings

    var body: some View {
        Text("Hello, \(settings.username)!")
    }
}
```

这样，无论 `ContentView` 在视图层次结构中的哪个地方，只要 `settings.username` 改变，`ContentView` 就会更新。

### OnReceive

在 SwiftUI 中，`onReceive` 是一个非常有用的方法，它允许你监听一个发布者，并在发布者发出新的值时执行一些操作。

`onReceive` 方法接受两个参数：一个发布者和一个闭包。当发布者发出新的值时，这个闭包会被调用，并接收到这个新的值。

以下是一个例子：

```swift
struct ContentView: View {
    @State private var time = Date()

    let timer = Timer.publish(every: 1, on: .main, in: .common).autoconnect()

    var body: some View {
        Text("\(time)")
            .onReceive(timer) { time in
                self.time = time
            }
    }
}
```

在这个例子中，我们首先创建了一个 `@State` 属性 `time` 和一个 `Timer` 发布者 `timer`。然后，我们在 `Text` 视图上调用了 `onReceive` 方法，监听 `timer` 发布者。当 `timer` 发布者每秒发出新的时间时，我们将 `time` 属性更新为这个新的时间，这会导致 `Text` 视图重新渲染。

总的来说，`onReceive` 方法是一个非常强大的工具，它允许你在 SwiftUI 视图中响应异步事件。

要实现这个功能，你需要在 `viewModel.progress` 发生变化时更新 `progressHUD`。你可以通过将 `progressHUD` 设置为 `ContentView` 的一个属性，并在 `viewModel.progress` 发生变化时更新 `progressHUD` 来实现这个功能。

以下是一个例子：

```swift
import SwiftUI
import MBProgressHUD

class ViewModel: ObservableObject {
    @Published var progress: Float = 0.0
}

struct ContentView: View {
    @ObservedObject var viewModel = ViewModel()
    @State private var progressHUD: MBProgressHUD?

    var body: some View {
        VStack {
            Button("Show Progress") {
                showProgress()
            }
        }
        .onReceive(viewModel.$progress) { _ in
            updateProgress()
        }
    }

    func showProgress() {
        guard let window = UIApplication.shared.windows.first else { return }
        progressHUD = MBProgressHUD(view: window)
        window.addSubview(progressHUD!)
        progressHUD?.mode = .determinateHorizontalBar
        progressHUD?.show(animated: true)
    }

    func updateProgress() {
        progressHUD?.label.text = String(viewModel.progress)
        progressHUD?.progress = Float(viewModel.progress/100)
    }
}
```

在这个例子中，我们首先创建了一个 `@State` 属性 `progressHUD`。然后，我们在 `showProgress` 方法中初始化 `progressHUD`，并在 `updateProgress` 方法中更新 `progressHUD`。

我们使用 `.onReceive` 方法来监听 `viewModel.progress` 的变化。当 `viewModel.progress` 发生变化时，`updateProgress` 方法会被调用，`progressHUD` 会被更新。

请注意，由于 SwiftUI 是声明式的，你不能在视图的 body 中直接调用 `showProgress` 或 `updateProgress` 方法。你需要在某个事件发生时（例如，一个按钮被点击，或者一个属性的值发生变化）调用这些方法。在这个例子中，我们在按钮被点击时调用 `showProgress` 方法，而在 `viewModel.progress` 的值发生变化时调用 `updateProgress` 方法。


## RxSwift

中文课程： https://boxueio.com/series/rxswift-101

[RxSwift](https://github.com/ReactiveX/RxSwift)是一个用于在Swift编程语言中进行响应式编程的库。响应式编程是一种处理异步数据流的编程范式。

在响应式编程中，你可以把数据看作是在时间上发生变化的流。你可以监听这个流，然后对流中的数据进行各种操作，比如过滤、转换、组合等。

RxSwift提供了一种统一的、简洁的API来处理各种异步操作，包括网络请求、用户输入、系统通知等。它可以让你的代码更加简洁、易读、易维护。

RxSwift的核心是`Observable`和`Observer`。`Observable`代表一个可以在时间上发生变化的数据流，`Observer`则是监听这个数据流的变化。当`Observable`中的数据发生变化时，所有订阅这个`Observable`的`Observer`都会收到通知。

总的来说，RxSwift是一种强大的工具，它可以帮助你更好地处理异步操作和复杂的数据流。


---

# 延时处理

你可以使用 `DispatchQueue` 的 `asyncAfter(deadline:execute:)` 方法来实现延时处理。以下是一个例子：

```swift
func updateProgress(_ progress: Float) {
    if progress == 1 {
        progressHUD?.label.text = "传输成功"
        progressHUD?.hide(animated: true)
    } else {
        progressHUD?.label.text = "传输中\(Int(progress*100))%"
        progressHUD?.progress = progress

        // Cancel any existing timer
        timer?.cancel()

        // Start a new timer
        timer = DispatchWorkItem {
            self.progressHUD?.label.text = "传输错误"
            self.progressHUD?.hide(animated: true)
        }

        // Schedule the timer to run after 1 minute
        DispatchQueue.main.asyncAfter(deadline: .now() + 60, execute: timer!)
    }
}

// Store the timer as a property of your class
var timer: DispatchWorkItem?
```

在这个例子中，我们首先创建了一个 `DispatchWorkItem`，这个 `DispatchWorkItem` 将在 1 分钟后执行。然后，我们使用 `DispatchQueue.main.asyncAfter(deadline:execute:)` 方法来安排这个 `DispatchWorkItem` 在 1 分钟后执行。

当 `updateProgress(_:)` 方法被调用时，我们首先取消任何已经存在的定时器，然后开始一个新的定时器。这样，如果 `updateProgress(_:)` 在 1 分钟内被多次调用，我们只会在最后一次调用后的 1 分钟后显示错误。

请注意，你需要将 `timer` 存储为你的类的一个属性，这样你才能在 `updateProgress(_:)` 方法中访问它。



---

# swift 错误处理

## try

在Swift中，`try`关键字用于调用可能会抛出错误的函数或方法。在Swift中，错误处理是一种重要的编程模式，它允许程序在错误发生时有恰当的响应。

以下是`try`关键字的三种形式：

1. `try`：如果一个表达式抛出一个错误，该错误会被传递到周围的作用域，直到它被一个`catch`子句处理。

```swift
do {
    try someThrowingFunction()
} catch {
    // Handle error here
}
```

2. `try?`：通过将错误转换为可选值来处理错误。如果一个表达式抛出一个错误，那么该表达式的值就是`nil`。

```swift
if let result = try? someThrowingFunction() {
    // Use the result
} else {
    // Handle the failure
}
```


3. `try!`：当你确定表达式不会抛出错误时使用。如果表达式确实抛出错误，你将得到一个运行时错误。

```swift
let result = try! someThrowingFunction() // Will crash if an error is thrown
```

总的来说，`try`关键字是Swift错误处理的一部分，它允许你编写能够抛出、捕获和处理错误的代码。


## do{ }catch{ }

1. 介绍
在Swift中，`do-catch`语句用于处理可能会抛出错误的代码。这是一个强大的错误处理模式，允许你捕获和处理错误。

`do-catch`语句的基本结构如下：

```swift
do {
    // 尝试执行可能会抛出错误的代码
    try someFunctionThatMayThrowAnError()
} catch {
    // 如果上面的代码抛出了错误，这里就会捕获并处理错误
    print("An error occurred: \(error)")
}
```

在`do`块中，你可以执行可能会抛出错误的代码。这些代码需要使用`try`关键字来标记。

如果`do`块中的代码抛出了错误，控制流将立即转移到最近的`catch`块，你可以在`catch`块中处理错误。

在`catch`块中，你可以访问一个名为`error`的自动变量，这个变量包含了被抛出的错误。

你也可以定义多个`catch`块来处理不同类型的错误，或者对错误进行更详细的分类。例如：

```swift
do {
    try someFunctionThatMayThrowAnError()
} catch SomeSpecificError {
    // 处理特定类型的错误
} catch {
    // 处理所有其他类型的错误
}
```

在这个例子中，第一个`catch`块只会捕获`SomeSpecificError`类型的错误，其他类型的错误将被第二个`catch`块捕获。





---


# 数据的编码，解码
## 将UIImage编码或解码

你可以使用 `NSKeyedArchiver` 和 `NSKeyedUnarchiver` 来将 `[UIImage]` 转化为 `Data`，以及将 `Data` 转化回 `[UIImage]`。以下是一个示例：

```swift
// 编码器：将 [UIImage] 转化为 Data
func encodeImages(images: [UIImage]) -> Data? {
    return try? NSKeyedArchiver.archivedData(withRootObject: images, requiringSecureCoding: false)
}

// 解码器：将 Data 转化回 [UIImage]
func decodeImages(data: Data) -> [UIImage]? {
    return try? NSKeyedUnarchiver.unarchiveTopLevelObjectWithData(data) as? [UIImage]
}
```

在这个示例中，`encodeImages(images:)` 函数接受一个 `[UIImage]` 参数，然后使用 `NSKeyedArchiver.archivedData(withRootObject:requiringSecureCoding:)` 方法将其转化为 `Data`。如果转化成功，函数返回转化后的 `Data`；如果转化失败，函数返回 `nil`。

`decodeImages(data:)` 函数接受一个 `Data` 参数，然后使用 `NSKeyedUnarchiver.unarchiveTopLevelObjectWithData(_:)` 方法将其转化回 `[UIImage]`。如果转化成功，函数返回转化后的 `[UIImage]`；如果转化失败，函数返回 `nil`。

请注意，这个示例假设你的 `[UIImage]` 可以成功地通过 `NSKeyedArchiver` 和 `NSKeyedUnarchiver` 进行编码和解码。如果你的 `[UIImage]` 包含不能被 `NSKeyedArchiver` 或 `NSKeyedUnarchiver` 编码或解码的对象，那么你可能需要自定义你的编码和解码逻辑。

**解释：**
`NSKeyedUnarchiver` 是一个类，它是 Foundation 框架中的一部分，用于从归档对象（也就是已经被编码为 `Data` 类型的对象）中解码和恢复原始的对象。

归档和解档是一种序列化和反序列化的过程，它们使得你可以将对象转换为二进制数据，然后再从二进制数据中恢复对象。这对于数据的存储和传输非常有用。

例如，你可以使用 `NSKeyedArchiver` 将对象编码（归档）为 `Data`，然后将这个 `Data` 存储到磁盘上，或者通过网络发送给其他设备。然后，你可以使用 `NSKeyedUnarchiver` 将这个 `Data` 解码（解档）回原始的对象。

`NSKeyedUnarchiver` 的使用通常与 `NSKeyedArchiver` 配合，因为 `NSKeyedArchiver` 是用于编码对象的，而 `NSKeyedUnarchiver` 是用于解码对象的。


 **将UIImage 转化为data的注意事项：**

你的代码中有一些小错误。在 Swift 中，我们不能直接将 UIImage 对象转换为 Data 对象，需要使用 `UIImagePNGRepresentation` 或 `UIImageJPEGRepresentation` 函数。同样，我们也不能直接将 Data 对象转换为 UIImage 对象，需要使用 `UIImage(data:)` 构造器。以下是修正后的代码：

```swift
@Field.Coded(
    "photo",
    coder: {
        encode: { UIImage.pngData($0)() },
        decode: { UIImage(data: $0) }
    }
)
var photo: UIImage?
```

在这个修正后的代码中，`encode: { UIImage.pngData($0)() }` 将 `UIImage` 对象转换为 PNG 格式的 `Data` 对象，`decode: { UIImage(data: $0) }` 将 `Data` 对象转换为 `UIImage` 对象。

请注意，这个示例假设你的 `UIImage` 对象可以被成功转换为 PNG 格式。如果你的 `UIImage` 对象不能被成功转换为 PNG 格式，`UIImage.pngData($0)()` 将返回 `nil`，这可能会导致问题。你可能需要根据你的实际情况对这个示例进行一些修改。


---

# 文件的压缩与解压

## 1. 第三方库`ZIPFoundation` 

第三方库：
 https://github.com/weichsel/ZIPFoundation

用法：
https://qiita.com/john-rocky/items/7c3c8701646c8b9ab5ed

1. 引入`zipFoundation` 库
2. `import ZIPFoundation`
3. 压缩：
``` swift
do {
    try FileManager.default.zipItem(at: sourceURL, to: destinationURL) // destinationURLは拡張子が.zip
} catch {
    print("Creation of ZIP archive failed with error:\(error)")
}

```

4. 解压
``` swift
do {
    try FileManager.default.createDirectory(at: destinationURL, withIntermediateDirectories: true, attributes: nil)
    try FileManager.default.unzipItem(at: sourceURL, to: destinationURL, skipCRC32: true)
   } catch {
    print("Extraction of ZIP archive failed with error:\(error)")
   }

```


---

# URL

选择的文件的 URL 包含以下信息：

1. **Scheme**：URL 的开头部分，表示 URL 的类型。对于文件，这通常是 "file"。

2. **Host**：对于文件 URL，这通常是空的。

3. **Path**：文件在文件系统中的路径。这包括目录和文件名。

4. **Query**：URL 的可选部分，用于提供额外的参数。对于文件 URL，这通常是空的。

5. **Fragment**：URL 的可选部分，用于指定资源的特定部分。对于文件 URL，这通常是空的。

例如，一个文件 URL 可能看起来像这样：`file:///Users/username/Documents/myfile.txt`。在这个例子中，"file" 是 scheme，"/Users/username/Documents/myfile.txt" 是 path。

你可以使用 `URL` 类的属性来访问这些信息。例如，`url.scheme`、`url.host`、`url.path`、`url.query` 和 `url.fragment`。

注意，由于沙盒限制，你的应用只能访问用户通过 `UIDocumentPickerViewController` 明确选择的文件，或者你的应用的沙盒目录中的文件。你不能访问其他目录中的文件。

## 获取URL文件大小
如果你的 URL 是从文件系统获取的，而不是通过 `FileManager`，你可以使用 `URL` 的 `resourceValues(forKeys:)` 方法来获取文件的大小。这个方法返回一个 `URLResourceValues` 对象，其中包含了文件的各种属性，包括其大小。

以下是一个函数，它接受一个 `URL` 参数，返回该 URL 指向的文件的大小：

```swift
import Foundation

func getFileSize(url: URL) -> Int64? {
    do {
        let resourceValues = try url.resourceValues(forKeys: [.fileSizeKey])
        return resourceValues.fileSize
    } catch {
        print("Failed to get file size: \(error)")
        return nil
    }
}
```

在这个函数中，我们首先使用 `resourceValues(forKeys:)` 方法获取 URL 的资源值。然后，我们从资源值中获取文件大小，并返回它。如果获取资源值或文件大小失败，我们打印一个错误消息，并返回 `nil`。

你可以在你的 `HStack` 中使用这个函数来显示文件的大小，如下所示：

```swift
HStack{
    Text("\(url.pathExtension)") // 文件类型
    Text("\(url.lastPathComponent)")// 文件名称
    if let fileSize = getFileSize(url: url) {
        Text("Size: \(fileSize) bytes")
    }
}
```

在 Swift 中，你可以使用 `FileManager` 的 `attributesOfItem(atPath:)` 方法来获取文件的大小。这个方法返回一个字典，其中包含了文件的各种属性，包括其大小。

以下是一个函数，它接受一个 `URL` 参数，返回该 URL 指向的文件的大小：

```swift
import Foundation

func getFileSize(url: URL) -> UInt64? {
    let filePath = url.path
    let fileManager = FileManager.default

    do {
        let attributes = try fileManager.attributesOfItem(atPath: filePath)
        if let fileSize = attributes[.size] as? UInt64 {
            return fileSize
        } else {
            print("Failed to get file size")
            return nil
        }
    } catch {
        print("Failed to get file attributes: \(error.localizedDescription)")
        return nil
    }
}
```

在这个函数中，我们首先获取 URL 的路径，然后使用 `FileManager` 获取该路径的文件属性。然后，我们从属性字典中获取文件大小，并返回它。如果获取文件属性或文件大小失败，我们打印一个错误消息，并返回 `nil`。

你可以在你的 `HStack` 中使用这个函数来显示文件的大小，如下所示：

```swift
HStack{
    Text("\(url.pathExtension)") // 文件类型
    Text("\(url.lastPathComponent)")// 文件名称
    if let fileSize = getFileSize(url: url) {
        Text("Size: \(fileSize) bytes")
    }
}
```


---



---

# mvvm和mvc区别

MVVM和MVC的区别主要在于==**数据绑定和通信方式的不同**==，MVVM是双向数据绑定，而MVC是单向数据绑定。1234567

MVVM模式中，视图(View)和模型(Model)之间通过视图模型(ViewModel)进行交互，视图模型负责将数据绑定到视图上，并处理视图相关的逻辑，同时，视图模型也能监听视图的变化，并更新数据，这种双向数据绑定的特性使得数据和视图之间的同步更加简单和高效。

MVC模式中，视图和模型之间通过控制器(Controller)进行交互，控制器负责协调模型和视图之间的逻辑和流程，在MVC中，视图的变化会直接影响模型，而在MVVM中，视图的变化不会直接影响到模型，这种设计思想更加符合单向数据流的思想。

总的来说，MVVM模式在数据绑定、视图与模型之间的解耦、开发效率和用户体验方面优于MVC模式。

---

# 实例化对象

实例化一个对象在内存中干了三件事
1:开辟存储空间
2:初始化成员变量
3:返回指针地址

---

# if DEBUG

在Objective-C中，你可以使用`#else`预处理指令来在`#if`和`#endif`之间添加一个"else"块。如果`#if`的条件不满足（在这个例子中，如果`DEBUG`宏没有被定义），那么"else"块的代码会被包含在编译的代码中。

以下是一个例子：

```objective-c
#if DEBUG
    NSLog(@"This is a debug message.");
#else
    NSLog(@"This is a production message.");
#endif
```

在这个例子中，如果`DEBUG`宏被定义，那么会输出"This is a debug message."。如果`DEBUG`宏没有被定义，那么会输出"This is a production message."。

---


# swift类与OC的区别

**Swift的类内存结构是**：

- 前8个字节放元类型（metadata，元数据）相关，
- 后8个字节放指针相关，后⾯再放成员变量信息。
- 如果继承于NSObject，内存信息就变成了：前8个字节放isa指针相关，后⾯再放成员变量信息。

---

# @avaiable 与 #avaiable


在编程中，`@`和`#`的含义取决于你使用的编程语言。然而，`@available`和`#available`通常在Swift语言中使用，用于平台和版本检查。

- `@available`：这是一个属性修饰符，用于指示函数、方法、类等在特定平台和语言版本中的可用性。例如，如果一个函数在iOS 10及以上版本中可用，你可以这样标记：

```swift
@available(iOS 10, *)
func myFunction() {
    // Function body
}
```

- `#available`：这是一个条件语句，用于在代码中检查运行代码的平台版本。例如，如果你有一段只在iOS 10及以上版本运行的代码，你可以这样写：

```swift
if #available(iOS 10, *) {
    // Use iOS 10 APIs
} else {
    // Fallback on earlier versions
}
```

总的来说，`@available`和`#available`都是用于处理不同平台和版本间的兼容性问题。

---

# 路由

https://blog.csdn.net/weixin_42786992/article/details/83273008

## 1. 路由是什么

路由是一种在软件应用中导航和管理页面或视图之间跳转的机制。在Web开发中，路由通常用于根据URL的不同来显示不同的内容。在移动应用开发中，路由用于管理和导航不同的屏幕或视图。

例如，当你在浏览器中输入一个URL并按下回车键时，浏览器会根据URL的路径来决定显示哪个页面，这就是路由的一个例子。

在iOS开发中，路由可以通过多种方式实现，包括使用UINavigationController进行堆栈式的导航，使用TabBarController进行标签式的导航，或者使用自定义的URL Scheme进行应用内部的跳转等。

路由的主要目的是提供一种方式来管理和组织应用的不同部分，使用户可以方便地在应用的不同部分之间进行导航。


## 2. 在Swift中使用URL Scheme来进行应用内部的跳转

在Swift中，你可以使用`UIApplication`的`openURL:`方法来打开一个URL。如果这个URL是你应用的自定义URL Scheme，那么你的应用就可以根据这个URL来进行内部的跳转。

首先，你需要在你的应用的Info.plist文件中注册你的自定义URL Scheme。你可以添加一个叫做`URL types`的项，然后在这个项中添加你的URL Scheme。

然后，你可以在你的应用中任何需要的地方使用下面的代码来打开一个URL：

```swift
if let url = URL(string: "yourapp://yourpath") {
    UIApplication.shared.open(url, options: [:], completionHandler: nil)
}
```

当你的应用接收到一个URL时，`UIApplicationDelegate`的`application:openURL:options:`方法会被调用。你可以在这个方法中解析URL，然后根据URL的内容来决定要跳转到哪个视图。

```swift
func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool {
    // 解析URL，然后根据URL的内容来决定要跳转到哪个视图
    // ...
    return true
}
```

请注意，这只是一种基本的实现方式，你可能需要根据你的应用的具体需求来进行修改和扩展。


在Swift中，处理自定义URL Scheme的回调通常在`UIApplicationDelegate`的`application(_:open:options:)`方法中进行。当你的应用通过URL Scheme被其他应用打开时，这个方法会被调用。

以下是一个基本的处理自定义URL Scheme回调的例子：

```swift
func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool {
    // 获取URL的scheme
    let scheme = url.scheme
    
    // 获取URL的host
    let host = url.host
    
    // 获取URL的path
    let path = url.path
    
    // 获取URL的query参数
    let query = url.query
    
    // 根据scheme, host, path和query来决定如何处理这个URL
    if scheme == "yourapp" && host == "yourhost" {
        // 这是你的应用的自定义URL Scheme，你可以在

这

里进行相应的处理
        // ...
    }
    
    return true
}
```

在这个例子中，我们首先获取了URL的scheme、host、path和query，然后根据这些信息来决定如何处理这个URL。

请注意，这只是一种基本的实现方式，你可能需要根据你的应用的具体需求来进行修改和扩展。

## 3. 使用路由打开其他app
在Swift中，你可以使用`UIApplication`的`open(_:options:completionHandler:)`方法来打开一个URL。如果这个URL是其他应用的自定义URL Scheme，那么这个应用将会被打开。

以下是一个基本的例子：

```swift
if let url = URL(string: "otherapp://path") {
    UIApplication.shared.open(url, options: [:], completionHandler: nil)
}
```

在这个例子中，`otherapp://path`是其他应用的自定义URL Scheme。当这段代码执行时，如果用户的设备上安装了能处理这个URL Scheme的应用，那么这个应用将会被打开。

请注意，你只能打开用户设备上已经安装了的能处理这个URL Scheme的应用。如果没有安装能处理这个URL Scheme的应用，那么`open(_:options:completionHandler:)`方法将不会做任何事情。

此外，为了保护用户的隐私，从iOS 9开始，你需要在你的应用的Info.plist文件中添加一个`LSApplicationQueriesSchemes`项，然后在这个项中列出你的应用需要打开的所有其他应用的URL Scheme。





---

# 检查枚举类型的case数量

在Swift中，你可以通过`CaseIterable`协议来获取枚举的case数量。当你的枚举遵循`CaseIterable`协议时，你可以通过`allCases`属性来获取所有的case。然后，你可以使用`count`属性来获取case的数量。以下是一个例子：

```swift
enum SomeEnum: CaseIterable {
    case case1
    case case2
    case case3
}

let caseCount = SomeEnum.allCases.count
print(caseCount)  // 输出：3
```

在这个例子中，`SomeEnum`有3个case，所以`caseCount`的值是3。

---

# 语法

## `components(separatedBy:)`

在 Swift 中，你可以使用 `components(separatedBy:)` 方法来将字符串分段。这个方法会返回一个数组，数组中的每个元素都是原始字符串中的一个段。

以下是一个例子：

```swift
let str = "Hello, World, Swift"
let segments = str.components(separatedBy: ", ")
```

在这个例子中，`str` 是一个包含多个段的字符串，每个段之间都由一个逗号和一个空格分隔。`components(separatedBy: ", ")` 方法将 `str` 分割成多个段，并将这些段作为一个数组返回。所以，`segments` 是一个数组，它包含了 `str` 中的每个段。

在这个例子中，`segments` 的值将是 `["Hello", "World", "Swift"]`。


## `prefix(_:)` 和 `suffix(_:)`

在 Swift 中，你可以使用字符串的 `prefix(_:)` 和 `suffix(_:)` 方法来从中间分割一个 4 位字符串。以下是一个例子：

```swift
let str = "1234"
let firstPart = str.prefix(2)
let secondPart = str.suffix(2)
```

在这个例子中，`str` 是一个 4 位字符串。`prefix(2)` 方法返回 `str` 的前两个字符，`suffix(2)` 方法返回 `str` 的后两个字符。所以，`firstPart` 的值将是 `"12"`，`secondPart` 的值将是 `"34"`。

请注意，`prefix(_:)` 和 `suffix(_:)` 方法返回的是 `Substring`，而不是 `String`。如果你需要 `String`，你可以使用 `String` 的初始化方法来将 `Substring` 转换为 `String`，如下所示：

```swift
let firstPartStr = String(firstPart)
let secondPartStr = String(secondPart)
```



---

# map和compactMap

在 Swift 中，`map` 和 `compactMap` 是两个用于处理数组的高阶函数。

`map 函数遍历数组中的每个元素，并对每个元素执行一个你提供的转换函数（闭包）。它返回一个新的数组，这个数组包含了转换后的元素。例如：

```swift
let numbers = [1, 2, 3, 4, 5]
let squaredNumbers = numbers.map { $0 * $0 } // 结果是 [1, 4, 9, 16, 25]
```

在这个例子中，`map` 函数遍历 `numbers` 数组中的每个元素，并对每个元素执行闭包 `{ $0 * $0 }`，这个闭包计算每个元素的平方。

`compactMap` 函数类似于 `map`，但它会自动过滤掉转换函数返回的 `nil` 值。这在你的转换函数可能返回 `nil` 时非常有用。例如：

```swift
let strings = ["1", "2", "three", "4", "5"]
let numbers = strings.compactMap { Int($0) } // 结果是 [1, 2, 4, 5]
```

在这个例子中，`compactMap` 函数遍历 `strings` 数组中的每个元素，并对每个元素执行闭包 `{ Int($0) }`，这个闭包尝试将每个元素转换为整数。对于不能转换为整数的元素（例如 "three"），闭包返回 `nil`，`compactMap` 函数会自动过滤掉这些 `nil` 值。




---

# `NavigationBar`编辑按钮

## UIKit

在 UIKit 中，你可以使用 `UIBarButtonItem` 来在导航栏上添加编辑按钮。以下是一个简单的示例：

```swift
let editButton = UIBarButtonItem(barButtonSystemItem: .edit, target: self, action: #selector(editButtonTapped))
navigationItem.rightBarButtonItem = editButton
```

在这个示例中，我们首先创建了一个 `UIBarButtonItem`，并设置了它的样式为 `.edit`，这将使得按钮显示为一个编辑图标。然后，我们设置了按钮的 `target` 和 `action`，这意味着当按钮被点击时，`editButtonTapped` 方法将会被调用。最后，我们将这个按钮设置为导航栏的右侧按钮。

`editButtonTapped` 方法可能看起来像这样：

```swift
@objc func editButtonTapped() {
    // 在这里处理按钮点击事件
}
```

请注意，你需要将这些代码放在一个继承自 `UIViewController` 的类中，并且这个视图控制器需要被嵌入在一个导航控制器 (`UINavigationController`) 中。

## swiftUI

```swift
struct ContentView: View {
	var body: some View {
		Vstack{
		//...
		}
		.naviigationBartitle()// 导航栏
		.toolBar{} // 编辑按钮
	}
}
```


---

# 修改json键值

在Swift中，你可以使用`JSONSerialization`类来解析和修改JSON文件。以下是一个简单的步骤：

1. 读取JSON文件并将其转换为`Data`对象。
2. 使用`JSONSerialization.jsonObject(with:options:)`方法将`Data`对象转换为可变字典。
3. 修改字典中的键值。
4. 使用`JSONSerialization.data(withJSONObject:options:)`方法将修改后的字典转换回`Data`对象。
5. 将修改后的`Data`对象写回文件。

以下是具体的代码示例：

```swift
import Foundation

do {
    // 1. 读取JSON文件并将其转换为Data对象
    let url = URL(fileURLWithPath: "/path/to/your/json/file.json")
    let data = try Data(contentsOf: url)
    
    // 2. 将Data对象转换为可变字典
    if var jsonObject = try JSONSerialization.jsonObject(with: data, options: .mutableContainers) as? [String: Any] {
        // 3. 修改字典中的键值
        jsonObject["key1"] = "newValue1"
        jsonObject["key2"] = "newValue2"
        
        // 4. 将修改后的字典转换回Data对象
        let newData = try JSONSerialization.data(withJSONObject: jsonObject, options: .prettyPrinted)
        
        // 5. 将修改后的Data对象写回文件
        try newData.write(to: url)
    }
} catch {
    print("Error: \(error)")
}
```

请将`/path/to/your/json/file.json`替换为你的JSON文件的实际路径，将`key1`和`key2`替换为你想要修改的键，将`newValue1`和`newValue2`替换为新的值。

注意：这个代码示例假设你的JSON文件包含一个字典。如果你的JSON文件包含一个数组或其他结构，你可能需要稍微修改这个代码。

例子：
首先，你需要读取`dial_config.json`文件，然后解析`dial_datas`字段以获取`itemArray`数组。然后，你可以根据用户的设置来修改数组中的第二个和第三个对象的颜色和位置。以下是具体的步骤和代码：

1. 读取`dial_config.json`文件。
2. 解析`dial_datas`字段以获取`itemArray`数组。
3. 根据用户的设置来修改数组中的第二个和第三个对象的颜色和位置。

```swift
import Foundation

// 1. 读取dial_config.json文件
guard let path = Bundle.main.path(forResource: "dial_config", ofType: "json") else {
    print("dial_config.json file not found")
    return
}

do {
    // 2. 解析dial_datas字段以获取itemArray数组
    let data = try Data(contentsOf: URL(fileURLWithPath: path), options: .mappedIfSafe)
    let jsonResult = try JSONSerialization.jsonObject(with: data, options: .mutableLeaves)
    if let jsonResult = jsonResult as? Dictionary<String, AnyObject>, let dialDatas = jsonResult["dial_datas"] as? [Any] {
        var itemArray = dialDatas
        // 3. 根据用户的设置来修改数组中的第二个和第三个对象的颜色和位置
        if itemArray.count > 3 {
            if var item2 = itemArray[1] as? [String: Any], var item3 = itemArray[2] as? [String: Any] {
                item2["color"] = "newColor" // 替换为用户设置的颜色
                item2["x"] = "newX" // 替换为用户设置的x位置
                item2["y"] = "newY" // 替换为用户设置的y位置

                item3["color"] = "newColor" // 替换为用户设置的颜色
                item3["x"] = "newX" // 替换为用户设置的x位置
                item3["y"] = "newY" // 替换为用户设置的y位置

                itemArray[1] = item2
                itemArray[2] = item3
            }
        }
    }
} catch {
    print("Unable to parse dial_config.json: \(error)")
}
```

请注意，你需要将`"newColor"`, `"newX"`和`"newY"`替换为用户设置的实际值。


---

# swift的函数

## 1. 标记

在Swift中，函数可以有以下几种标记：

1. `throws`：这个标记表示函数可能会抛出错误。如果一个函数被标记为`throws`，那么它必须使用`throw`语句来抛出一个错误，而调用这个函数的代码必须使用`try`、`try?`或`try!`来调用它。

2. `rethrows`：这个标记表示函数接受一个抛出错误的函数作为参数，并且它自己可能会抛出这个参数函数抛出的错误。`rethrows`函数只能抛出它的参数函数抛出的错误。

3. `@escaping`：这个标记表示函数的参数是一个逃逸闭包。逃逸闭包是在函数返回后才被调用的闭包，例如存储为全局变量或者异步执行的闭包。

4. `@autoclosure`：这个标记表示函数的参数是一个自动闭包。自动闭包是一种自动创建的闭包，用于包装传递给函数的表达式。这允许延迟表达式的执行。

5. `@discardableResult`：这个标记表示函数的返回值可以被忽略。如果一个函数被标记为`@discardableResult`，那么调用这个函数时可以不使用它的返回值，而不会产生警告。

6. `@available`：这个标记表示函数在特定平台和语言版本的可用性。你可以使用它来标记函数在某个版本被引入、被弃用或者被废弃。

7. `@objc`：这个标记表示函数被暴露给Objective-C代码。这允许Objective-C代码调用Swift函数，但是可能会有一些限制，例如不能使用Swift的某些特性。

8. `@inlinable`：这个标记表示函数的实现对于模块外部是可见的，这允许编译器在模块外部内联这个函数。

9. `@nonobjc`：这个标记表示函数不会被暴露给Objective-C代码，即使它满足Objective-C的要求。

这些标记提供了很大的灵活性，允许你精确地控制函数的行为和使用方式。


### `throw`

在Swift中，`throws`关键字用于标记一个函数可能会抛出错误。这是Swift的错误处理模型的一部分，它允许你编写能够抛出、捕获和处理错误的代码。

使用`throws`标记函数有以下几个原因：

1. 明确性：`throws`关键字明确地表明了函数可能会失败，并且会抛出错误。这使得调用者知道他们需要处理可能的错误。

2. 安全性：在Swift中，你必须使用`try`、`try?`或`try!`来调用可能抛出错误的函数。这强制你处理可能的错误，从而提高了代码的安全性。

3. 灵活性：`throws`关键字允许你抛出任何遵循`Error`协议的类型。这意味着你可以创建自定义的错误类型，以提供更多的错误信息。

4. 结构化错误处理：Swift的错误处理模型允许你使用`do-catch`语句来捕获和处理错误。这使得你可以编写结构化的错误处理代码，而不是依赖于例如返回错误码或错误对象的方式。

总的来说，使用`throws`标记函数是一种明确、安全、灵活且结构化的方式来处理可能的错误。

## 2. 函数的访问（public）
在Swift中，你可以使用`public`关键字来定义一个公开的函数。公开的函数可以在任何地方被访问，包括不同的模块和框架。以下是一个例子：

```swift
public func myPublicFunction() {
    // 函数体
}
```

在这个例子中，`myPublicFunction`是一个公开的函数，可以在定义它的模块外部被访问。

需要注意的是，`public`函数在其他模块中可以被访问和重写，但不能被继承。如果你想让一个函数在其他模块中可以被继承，你需要使用`open`关键字：

```swift
open func myOpenFunction() {
    // 函数体
}
```

在这个例子中，`myOpenFunction`是一个开放的函数，可以在定义它的模块外部被访问、重写和继承。


---

# swift的同步与异步，多线程 `async`

相关文章：

https://juejin.cn/post/7048912537709969416

深层的：(很好的文章，讲Swift的同步异步与线程)
https://onevcat.com/2021/07/swift-concurrency/

### 同步和异步


---

# KVO

[key-value observing](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/KeyValueObserving/KeyValueObserving.html) (KVO)


# Swift的宏

https://cloud.tencent.com/developer/article/2410406





---

# swift中的JSON字符串

在 Swift 中，JSON 字符串通常以字符串字面量的形式表示。具体来说，可以使用单行字符串或多行字符串字面量来表示 JSON 数据。以下是两种表示方式的示例：

### 单行字符串字面量

如果 JSON 数据较短，可以使用单行字符串字面量：

```swift
let jsonString = "{\"key1\":\"value1\",\"key2\":2,\"key3\":true}"
```

### 多行字符串字面量

对于较长的 JSON 数据，使用多行字符串字面量会更方便和清晰。多行字符串字面量使用三个双引号 `"""` 包围字符串内容：

```swift
let jsonString = """
{
  "personalitySignatureUnAudit" : "",
  "servicePrice" : 300,
  "isCalling" : false,
  "headPictureUrl" : "https://aliyuncdn.yingtaoliao.com/vidoechatfiles/cf12457a-16ea-4ce2-86ce-6da55e3041bb.png",
  "userId" : 9000684,
  "doNotPickAudio" : 0,
  "nickname" : "yy",
  "doNotDisturbMode" : 0,
  "video_avatar" : {
    "width" : 2160,
    "user_video_avatar_audit_status" : false,
    "height" : 3840,
    "video_avatar_url" : "https://aliyuncdn.yingtaoliao.com/trend/ae7420e5-c562-4947-be2a-c03aadf186f3.mp4",
    "video_avatar_picture_url" : "https://aliyuncdn.yingtaoliao.com/trend/310b610b-b42a-40bf-8b25-1ead19cb1bd7.png"
  },
  "real_certify_status" : 1,
  "gender" : "女",
  "age" : 33,
  "sound_introduction" : {
    "status" : 1,
    "update_time" : "2024-06-20 11:54:15",
    "id" : 190,
    "media_len" : 10,
    "create_time" : "2024-06-18 18:43:31",
    "user_id" : 9000684,
    "auditor" : "耿家琪",
    "media_url" : "https://aliyuncdn.yingtaoliao.com/trend/4fd4a833-6ff4-4498-af26-1897aa8d1b60.mp3"
  },
  "personalitySignature" : "",
  "recentOnlineTime" : "2024-06-20 00:10:38",
  "doNotPickVideo" : 0,
  "audioServicePrice" : 100
}
"""
```

### 使用多行字符串字面量的优点

1. **可读性**：多行字符串字面量使得长字符串（如 JSON 数据）更易读和维护。
2. **格式保持**：保留了原始 JSON 数据的格式，包括换行和缩进。

### 在 Swift 中处理 JSON 字符串

在 Swift 中，处理 JSON 字符串通常涉及以下步骤：

1. **将 JSON 字符串转换为 `Data` 对象**：
   ```swift
   let jsonData = jsonString.data(using: .utf8)!
   ```

2. **将 `Data` 对象解析为 Swift 对象**（如字典或自定义结构体）：
   ```swift
   do {
       if let jsonObject = try JSONSerialization.jsonObject(with: jsonData, options: []) as? [String: Any] {
           // 处理解析后的 JSON 对象
           print(jsonObject)
       }
   } catch {
       print("JSON 解析失败: \(error)")
   }
   ```

### 完整示例

以下是一个完整的示例，展示了如何将 JSON 字符串保存到文件中，并在 Xcode 控制台中打印文件路径：

```swift
import Foundation

let jsonString = """
{
  "personalitySignatureUnAudit" : "",
  "servicePrice" : 300,
  "isCalling" : false,
  "headPictureUrl" : "https://aliyuncdn.yingtaoliao.com/vidoechatfiles/cf12457a-16ea-4ce2-86ce-6da55e3041bb.png",
  "userId" : 9000684,
  "doNotPickAudio" : 0,
  "nickname" : "yy",
  "doNotDisturbMode" : 0,
  "video_avatar" : {
    "width" : 2160,
    "user_video_avatar_audit_status" : false,
    "height" : 3840,
    "video_avatar_url" : "https://aliyuncdn.yingtaoliao.com/trend/ae7420e5-c562-4947-be2a-c03aadf186f3.mp4",
    "video_avatar_picture_url" : "https://aliyuncdn.yingtaoliao.com/trend/310b610b-b42a-40bf-8b25-1ead19cb1bd7.png"
  },
  "real_certify_status" : 1,
  "gender" : "女",
  "age" : 33,
  "sound_introduction" : {
    "status" : 1,
    "update_time" : "2024-06-20 11:54:15",
    "id" : 190,
    "media_len" : 10,
    "create_time" : "2024-06-18 18:43:31",
    "user_id" : 9000684,
    "auditor" : "耿家琪",
    "media_url" : "https://aliyuncdn.yingtaoliao.com/trend/4fd4a833-6ff4-4498-af26-1897aa8d1b60.mp3"
  },
  "personalitySignature" : "",
  "recentOnlineTime" : "2024-06-20 00:10:38",
  "doNotPickVideo" : 0,
  "audioServicePrice" : 100
}
"""

// 获取文档目录路径
let fileManager = FileManager.default
if let documentsDirectory = fileManager.urls(for: .documentDirectory, in: .userDomainMask).first {
    // 创建文件路径
    let fileURL = documentsDirectory.appendingPathComponent("output.json")
    
    do {
        // 将 JSON 字符串写入文件
        try jsonString.write(to: fileURL, atomically: true, encoding: .utf8)
        // 打印文件路径
        print("JSON 文件已保存到: \(fileURL.path)")
    } catch {
        print("无法保存文件: \(error)")
    }
}
```

这样，你就可以在 Swift 中使用 JSON 字符串，并将其保存到文件中。


---

# Swift的访问控制

在 Swift 中，访问控制用于限制代码中不同部分的访问权限。Swift 提供了几种访问级别标记：`private`、`fileprivate`、`internal`、`public` 和 `open`。其中，`private` 和 `fileprivate` 都用于限制访问权限，但它们有不同的作用范围。以下是对这两种标记的详细解释：

### `private`

`private` 访问级别限制声明只能在其定义的作用域内（即同一个类、结构体、枚举或扩展）访问。它是最严格的访问级别，通常用于保护实现细节，防止外部访问。

示例：

```swift
class MyClass {
    private var privateVariable = 0
    
    private func privateMethod() {
        print("This is a private method.")
    }
    
    func publicMethod() {
        privateVariable += 1
        privateMethod()
    }
}

let myClass = MyClass()
// myClass.privateVariable // 错误：'privateVariable' 是私有的
// myClass.privateMethod() // 错误：'privateMethod' 是私有的
myClass.publicMethod() // 正确：可以访问公共方法
```

在上面的例子中，`privateVariable` 和 `privateMethod` 只能在 `MyClass` 的内部访问，外部无法访问它们。

### `fileprivate`

`fileprivate` 访问级别允许声明在同一个源文件中访问。它比 `private` 更宽松，可以用于需要在同一个文件的多个类型或扩展中共享代码的情况。

示例：

```swift
class MyClass {
    fileprivate var fileprivateVariable = 0
    
    fileprivate func fileprivateMethod() {
        print("This is a fileprivate method.")
    }
}

extension MyClass {
    func publicMethod() {
        fileprivateVariable += 1
        fileprivateMethod()
    }
}

let myClass = MyClass()
myClass.fileprivateVariable // 正确：可以在同一个文件中访问
myClass.fileprivateMethod() // 正确：可以在同一个文件中访问
myClass.publicMethod() // 正确：可以访问公共方法
```

在上面的例子中，`fileprivateVariable` 和 `fileprivateMethod` 可以在同一个文件中的任何地方访问，包括类的扩展。

### `internal`

`internal` 是默认的访问级别，如果你不显式指定访问级别，Swift 会默认将其设置为 `internal`。`internal` 允许在同一个模块内访问（通常是一个应用程序或框架）。

示例：

```swift
class MyClass {
    var internalVariable = 0 // 默认是 internal
    
    func internalMethod() {
        print("This is an internal method.")
    }
}

let myClass = MyClass()
myClass.internalVariable // 正确：可以在同一个模块中访问
myClass.internalMethod() // 正确：可以在同一个模块中访问
```

### `public` 和 `open`

`public` 和 `open` 允许在模块外部访问，但有一些区别：

- `public`：可以在模块外部访问，但不能在模块外部继承或重写。
- `open`：不仅可以在模块外部访问，还可以在模块外部继承和重写。

示例：

```swift
public class PublicClass {
    public var publicVariable = 0
    
    public func publicMethod() {
        print("This is a public method.")
    }
}

open class OpenClass {
    open var openVariable = 0
    
    open func openMethod() {
        print("This is an open method.")
    }
}

let publicClass = PublicClass()
publicClass.publicVariable // 正确：可以在模块外部访问
publicClass.publicMethod() // 正确：可以在模块外部访问

let openClass = OpenClass()
openClass.openVariable // 正确：可以在模块外部访问
openClass.openMethod() // 正确：可以在模块外部访问
```

### 总结

- `private`：限制声明只能在其定义的作用域内访问。
- `fileprivate`：限制声明只能在同一个源文件中访问。
- `internal`：限制声明只能在同一个模块内访问（默认访问级别）。
- `public`：允许在模块外部访问，但不能继承或重写。
- `open`：允许在模块外部访问，并且可以继承和重写。

选择合适的访问级别可以帮助你保护代码的实现细节，控制代码的可访问性，从而提高代码的安全性和可维护性。

---

# Swift的引用

在 Swift 中，闭包会捕获并保留其上下文中的所有变量，包括 `self`。如果 `self` 是一个类实例，并且闭包对 `self` 有强引用，而 `self` 也对闭包有强引用，就会导致循环引用（也称为强引用循环或引用周期），从而导致内存泄漏。

为了避免这种情况，通常在闭包中使用捕获列表（capture list）来声明对 `self` 的弱引用或无主引用。以下是如何在闭包中使用捕获列表的示例：

### 使用弱引用

```swift
imagePickerVc?.navLeftBarButtonSettingBlock = { [weak self] (leftButton: UIButton) in
    guard let self = self else { return }
    leftButton.setImage(UIImage(named: "icon_nav_back"), for: .normal)
    leftButton.imageEdgeInsets = UIEdgeInsets(top: 0, left: -15, bottom: 0, right: 0)
}
```

在这个示例中，`[weak self]` 声明了对 `self` 的弱引用。这样，如果 `self` 被释放，闭包中的 `self` 也会变为 `nil`，从而打破循环引用。使用 `guard let self = self else { return }` 确保在闭包执行时 `self` 仍然存在。

### 使用无主引用

如果你确定在闭包执行期间 `self` 一定不会被释放，可以使用无主引用：

```swift
imagePickerVc?.navLeftBarButtonSettingBlock = { [unowned self] (leftButton: UIButton) in
    leftButton.setImage(UIImage(named: "icon_nav_back"), for: .normal)
    leftButton.imageEdgeInsets = UIEdgeInsets(top: 0, left: -15, bottom: 0, right: 0)
}
```

在这个示例中，`[unowned self]` 声明了对 `self` 的无主引用。无主引用不会增加 `self` 的引用计数，但如果在闭包执行时 `self` 已经被释放，程序会崩溃。

### 选择合适的捕获方式

- **使用弱引用**：当你不确定 `self` 是否会在闭包执行期间被释放时，使用弱引用是更安全的选择。
- **使用无主引用**：当你确定 `self` 在闭包执行期间一定不会被释放时，可以使用无主引用。

在大多数情况下，使用弱引用是更安全的选择，因为它可以防止潜在的崩溃。

### 示例代码

结合前面的代码示例，使用弱引用来避免循环引用：

```swift
imagePickerVc?.navLeftBarButtonSettingBlock = { [weak self] (leftButton: UIButton) in
    guard let self = self else { return }
    leftButton.setImage(UIImage(named: "icon_nav_back"), for: .normal)
    leftButton.imageEdgeInsets = UIEdgeInsets(top: 0, left: -15, bottom: 0, right: 0)
}
```

通过这种方式，你可以确保闭包中的 `self` 不会导致循环引用，从而避免内存泄漏。


## 几种引用的区别

在 Swift 中，引用类型（如类实例）可以通过不同的方式进行引用：强引用（strong reference）、弱引用（weak reference）和无主引用（unowned reference）。它们的主要区别在于它们如何影响对象的生命周期以及它们在内存管理中的作用。

### 强引用（Strong Reference）

**默认情况下，所有引用都是强引用。**

- **作用**：增加对象的引用计数。
- **生命周期管理**：只要有强引用存在，对象就不会被释放。
- **使用场景**：大多数情况下，默认的强引用是合适的，尤其是当你希望对象在整个生命周期内都存在时。

```swift
class Person {
    var name: String
    init(name: String) {
        self.name = name
    }
}

var person1 = Person(name: "Alice")
var person2 = person1  // person2 是对 person1 的强引用
```

### 弱引用（Weak Reference）

**弱引用不会增加对象的引用计数。**

- **作用**：不会增加对象的引用计数。
- **生命周期管理**：如果对象的所有强引用都被释放，对象会被释放，即使还有弱引用存在。弱引用在对象被释放后会自动变为 `nil`。
- **使用场景**：适用于可能导致循环引用的情况，例如在委托（delegate）模式中，或者在闭包中引用 `self` 时。

```swift
class Person {
    var name: String
    init(name: String) {
        self.name = name
    }
}

class Apartment {
    weak var tenant: Person?
}

var person: Person? = Person(name: "Alice")
var apartment = Apartment()
apartment.tenant = person  // tenant 是对 person 的弱引用

person = nil  // person 被释放，apartment.tenant 变为 nil
```

### 无主引用（Unowned Reference）

**无主引用不会增加对象的引用计数，并且在对象被释放后不会自动变为 `nil`。**

- **作用**：不会增加对象的引用计数。
- **生命周期管理**：如果对象被释放，无主引用会指向一个无效的内存地址，访问它会导致程序崩溃。
- **使用场景**：适用于对象在整个生命周期中总是存在的情况，例如在两个对象互相引用且一个对象的生命周期完全包含在另一个对象的生命周期内时。

```swift
class Person {
    var name: String
    init(name: String) {
        self.name = name
    }
}

class Apartment {
    unowned var tenant: Person
    init(tenant: Person) {
        self.tenant = tenant
    }
}

var person: Person? = Person(name: "Alice")
var apartment: Apartment? = Apartment(tenant: person!)

person = nil  // person 被释放，apartment 仍然持有无效的 tenant 引用，这会导致崩溃
```

### 选择合适的引用类型

- **强引用**：默认情况下使用，适用于需要确保对象在整个生命周期内存在的情况。
- **弱引用**：适用于可能导致循环引用的情况，尤其是在闭包中引用 `self` 或在委托模式中。
- **无主引用**：适用于对象在整个生命周期中总是存在的情况，通常用于两个对象互相引用且一个对象的生命周期完全包含在另一个对象的生命周期内。

通过理解这些引用类型的区别和使用场景，可以更好地管理内存，避免内存泄漏和崩溃。


---

# swiftData
SwiftData 是 Apple 在 WWDC 2023 上发布的一种新的数据持久化框架。它旨在简化开发者在 Swift 语言中处理持久化数据的工作。SwiftData 提供了现代化的 API，支持声明式语法和类型安全，允许开发者以更直观和简洁的方式定义和管理数据模型。

### SwiftData 的主要特点

1. **声明式语法**：使用 SwiftData，可以以声明式的方式定义数据模型。这使得代码更加简洁和易读。

2. **类型安全**：SwiftData 充分利用了 Swift 的类型系统，确保在编译时捕获错误，减少运行时错误的可能性。

3. **自动化管理**：SwiftData 提供了许多自动化功能，例如自动生成的 CRUD 操作（创建、读取、更新和删除），简化了数据管理的复杂性。

4. **与 SwiftUI 集成**：SwiftData 与 SwiftUI 紧密集成，允许开发者轻松地将数据绑定到 UI 组件，使得数据驱动的用户界面开发更加顺畅。

### 基本用法

以下是一个使用 SwiftData 的简单示例：

```swift
import SwiftData

// 定义数据模型
@Model
class Task {
    @Attribute(.primaryKey) var id: UUID
    @Attribute var title: String
    @Attribute var isCompleted: Bool
    
    init(title: String, isCompleted: Bool = false) {
        self.id = UUID()
        self.title = title
        self.isCompleted = isCompleted
    }
}

// 创建数据上下文
let context = DataContext()

// 创建新任务
let newTask = Task(title: "Learn SwiftData")
context.insert(newTask)

// 保存上下文
context.save()

// 查询任务
let tasks = context.fetch(Task.self)
for task in tasks {
    print("\(task.title) - Completed: \(task.isCompleted)")
}
```

### 与 SwiftUI 的集成

SwiftData 可以与 SwiftUI 无缝集成，使得数据驱动的 UI 开发更加便捷。例如：

```swift
import SwiftUI
import SwiftData

struct TaskListView: View {
    @Environment(\.dataContext) private var context: DataContext
    @FetchRequest(entity: Task.entity(), sortDescriptors: [NSSortDescriptor(keyPath: \Task.title, ascending: true)]) var tasks: FetchedResults<Task>
    
    var body: some View {
        List {
            ForEach(tasks) { task in
                Text(task.title)
            }
        }
    }
}

@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            TaskListView()
                .environment(\.dataContext, DataContext())
        }
    }
}
```

### 总结

SwiftData 是 Apple 为 Swift 开发者提供的一种现代化数据持久化解决方案。它简化了数据模型的定义和管理，并与 SwiftUI 紧密集成，使得数据驱动的应用开发更加直观和高效。通过使用 SwiftData，开发者可以更轻松地处理复杂的数据持久化需求，同时保持代码的简洁和可维护性。

---

# 包管理
## CocoaPods, SPM,Carthage

![[f7dd8aca06b241698df35f4d43b2b997.png]]



SPM

https://www.jiansh\u.com/p/2f0d5794c7e2

## CocoaPods和SPM的区别

1. CocoaPods是中心化的，SPM是去中心化的
2. CocoaPods的项目入侵比较严重

- [CocoaPods](https://blog.csdn.net/u014600626/article/details/102922568)、[Carthage](https://www.jianshu.com/p/42118918177b)、[SPM](https://zhuanlan.zhihu.com/p/103197303)对比

![[f7dd8aca06b241698df35f4d43b2b997.png]]

主要区别：
1. 原理
2. 项目入侵性，源码是否可见


---

# Swift常用关键词术语表

[Swift编程术语表 --- Glossary of terms for Swift programming](https://www.hackingwithswift.com/glossary)

---

# 手动创建Swift - OC桥接文件

https://www.cnblogs.com/wangkejia/p/7891374.html


---

# Swift的extension

在 Swift 中，`extension`、继承和直接在类中新增功能都有其特定的用途和场景。理解它们之间的区别有助于更有效地设计和组织代码。

### 1. Extension（扩展）

#### 功能
- **扩展现有类型**：可以为现有的类、结构体、枚举或协议添加新功能，而无需访问原始源代码。
- **分离关注点**：可以将类的功能分成多个部分，使代码更清晰和可维护。
- **添加协议一致性**：可以通过扩展为现有类型添加协议一致性。

#### 优点
- **组织代码**：可以将相关功能分组到扩展中，使代码更具可读性和可维护性。
- **修改不可变代码**：可以为你没有源代码的类（例如系统类）添加功能。
- **避免子类化**：可以在不创建子类的情况下扩展类的功能。

#### 示例

```swift
extension String {
    func reversedString() -> String {
        return String(self.reversed())
    }
}

let original = "hello"
print(original.reversedString())  // 输出: "olleh"
```

### 2. Inheritance（继承）

#### 功能
- **创建子类**：可以创建一个类的子类，并继承父类的属性和方法。
- **重写功能**：可以重写父类的方法和属性，提供新的实现。
- **多态性**：允许使用父类类型的引用来指向子类对象。

#### 优点
- **代码重用**：通过继承，可以重用父类的代码，而不必重新实现相同的功能。
- **多态性**：允许通过父类引用调用子类的重写方法，实现更灵活的代码设计。

#### 示例

```swift
class Animal {
    func sound() {
        print("Some sound")
    }
}

class Dog: Animal {
    override func sound() {
        print("Bark")
    }
}

let myDog = Dog()
myDog.sound()  // 输出: "Bark"
```

### 3. 在 Class 中新增功能

#### 功能
- **直接在类中新增功能**：可以直接在类的定义中添加属性和方法。

#### 优点
- **直接可见**：所有功能都在一个地方定义，容易查看。
- **简单明了**：适用于简单的类，不需要额外的结构。

#### 示例

```swift
class Cat {
    func meow() {
        print("Meow")
    }
}

let myCat = Cat()
myCat.meow()  // 输出: "Meow"
```

### 选择使用的场景

- **Extension**：当你需要为现有类型添加新功能，或者将类的功能分组以提高代码可读性和可维护性时。
- **Inheritance**：当你需要创建一个类的子类，并希望重用父类的功能或重写父类的方法时。
- **直接在类中新增功能**：当你在定义一个新的类时，并且所有功能都可以直接在类中实现时。

### 总结

- **扩展（Extension）** 适用于为现有类型添加功能、分离关注点和增强代码组织。
- **继承（Inheritance）** 适用于重用代码和实现多态性。
- **直接在类中新增功能** 适用于简单类的定义和实现。

根据具体需求选择合适的方法，可以帮助你编写更清晰、可维护和高效的代码。


---

在Swift中，使用闭包初始化属性的方式（如下所示）并不是懒加载：

```swift
private let callingAgreement: CFJumpLinkLabel = {
    let label = CFJumpLinkLabel(frame: .zero, preText: "拨打通话即表示同意", linkText: "用户通话协议", jumpUrl: CFPublicInstance.shareInstance().sealingControl().communicationProtocolLink())
    return label
}()
```

这种方式是立即初始化，即在对象创建时就会初始化这些属性。虽然代码看起来简洁，但它并不是懒加载。

懒加载在Swift中通常使用`lazy var`来实现。`lazy var`属性在第一次访问时才会被初始化。以下是使用`lazy var`实现懒加载的示例：

```swift
private lazy var callingAgreement: CFJumpLinkLabel = {
    let label = CFJumpLinkLabel(frame: .zero, preText: "拨打通话即表示同意", linkText: "用户通话协议", jumpUrl: CFPublicInstance.shareInstance().sealingControl().communicationProtocolLink())
    return label
}()
```

在这种情况下，`callingAgreement`属性只有在第一次被访问时才会被创建和初始化，这样可以节省资源并提高性能。

### 总结

- 使用闭包初始化属性的方式（`let`声明）是立即初始化，不是懒加载。
- 使用`lazy var`声明属性可以实现懒加载，属性只有在第一次访问时才会被初始化。

如果你的目标是实现懒加载，请使用`lazy var`。



使用闭包初始化属性在Swift中有几个主要的优点：

### 1. 简洁和可读性
闭包初始化属性可以将初始化代码封装在一个地方，使代码更加简洁和易读。例如：

```swift
private let callingAgreement: CFJumpLinkLabel = {
    let label = CFJumpLinkLabel(frame: .zero, preText: "拨打通话即表示同意", linkText: "用户通话协议", jumpUrl: CFPublicInstance.shareInstance().sealingControl().communicationProtocolLink())
    return label
}()
```

这种方式将初始化逻辑包裹在一个闭包中，使得属性声明和初始化逻辑紧密结合，代码更具可读性。

### 2. 设置复杂的默认值
对于一些需要复杂初始化逻辑的属性，闭包初始化提供了一种清晰的方式来设置默认值。例如：

```swift
private let customView: UIView = {
    let view = UIView()
    view.backgroundColor = .red
    view.layer.cornerRadius = 10
    view.layer.shadowColor = UIColor.black.cgColor
    view.layer.shadowOpacity = 0.5
    return view
}()
```

这种方式允许你在初始化时执行多步配置，而不是在初始化后再进行配置。

### 3. 避免`init`方法中的冗长代码
将属性的初始化逻辑放在闭包中，可以减少`init`方法中的代码量，使得`init`方法更加简洁。例如：

```swift
class MyViewController: UIViewController {
    private let label: UILabel = {
        let label = UILabel()
        label.text = "Hello, World!"
        label.textColor = .black
        return label
    }()
    
    override func viewDidLoad() {
        super.viewDidLoad()
        view.addSubview(label)
    }
}
```

### 4. 提供默认值
闭包初始化属性可以用于提供默认值，这在某些情况下非常有用。例如：

```swift
private let dateFormatter: DateFormatter = {
    let formatter = DateFormatter()
    formatter.dateStyle = .medium
    formatter.timeStyle = .none
    return formatter
}()
```

### 5. 延迟计算
虽然闭包初始化属性不是懒加载，但它们可以用于延迟计算属性的初始值，直到对象被创建时才计算。例如：

```swift
private let computedProperty: Int = {
    return someExpensiveComputation()
}()
```

### 总结

闭包初始化属性在Swift中被广泛使用，因为它们提供了一种简洁、可读和灵活的方式来初始化属性。它们特别适合用于需要复杂初始化逻辑的属性，或在属性声明时就需要设置默认值的情况。尽管它们不是懒加载，但在很多情况下，它们提供了足够的延迟计算能力。对于需要懒加载的情况，`lazy var`是更合适的选择。

---

# 宏 Macro 


---
# 泛型 Generics
泛型（Generics）是一种编程特性，允许开发者在定义类、接口、方法或函数时使用类型参数，从而实现类型的抽象化和复用。通过泛型，开发者可以编写与特定数据类型无关的代码，这样可以在不同的上下文中使用相同的逻辑，而不必重复编写代码。

### 泛型的主要概念

1. **类型参数**:
   泛型使用类型参数来代表将要使用的具体类型。类型参数通常用尖括号（`<T>`）表示，其中 `T` 是一个占位符，可以是任何有效的类型。

   ```swift
   func swap<T>(a: inout T, b: inout T) {
       let temp = a
       a = b
       b = temp
   }
   ```

2. **类型安全**:
   泛型提供了类型安全性。在编译时，编译器会检查类型的一致性，从而避免在运行时出现类型错误。这有助于减少运行时错误，提高代码的可靠性。

3. **代码复用**:
   泛型允许开发者编写通用的算法和数据结构，能够处理多种数据类型。例如，泛型集合类（如数组、列表、字典）可以存储任何类型的元素，而不需要为每种类型实现不同的集合类。

4. **约束**:
   泛型可以通过约束来限制类型参数的类型。例如，可以指定类型参数必须遵循某个协议或继承自某个类。这使得泛型能够更加灵活和强大。

   ```swift
   func printValue<T: CustomStringConvertible>(value: T) {
       print(value.description)
   }
   ```

5. **性能优化**:
   泛型可以帮助提高性能，因为编译器可以在编译时生成针对特定类型的高效代码，而不需要在运行时进行类型检查和转换。

### 泛型的应用场景

- **数据结构**: 泛型广泛应用于数据结构的实现，如链表、栈、队列等，使得这些数据结构可以存储任何类型的元素。
  
- **算法**: 泛型算法可以在不同类型的数据上运行，例如排序、查找等。

- **API 设计**: 在设计库和框架时，使用泛型可以提供更灵活和可重用的 API。

### 示例

以下是一个简单的泛型函数示例，演示如何使用泛型交换两个值：

```swift
func swap<T>(a: inout T, b: inout T) {
    let temp = a
    a = b
    b = temp
}

// 使用泛型函数
var x = 5
var y = 10
swap(&x, &y)  // x 现在是 10，y 现在是 5
```

### 总结

泛型是一种强大的编程特性，允许开发者编写灵活、可重用和类型安全的代码。通过使用泛型，开发者可以创建通用的算法和数据结构，提高代码的可读性和维护性，同时减少重复代码的数量。



## 泛型函数

你可以定义一个泛型函数，该函数可以处理任何类型的数据。以下是一个简单的泛型函数示例：

```swift
func swapTwoValues<T>(_ a: inout T, _ b: inout T) {
    let temporaryA = a
    a = b
    b = temporaryA
}

var x = 5
var y = 10
swapTwoValues(&x, &y)
print("x: \(x), y: \(y)")  // 输出: x: 10, y: 5

var str1 = "Hello"
var str2 = "World"
swapTwoValues(&str1, &str2)
print("str1: \(str1), str2: \(str2)")  // 输出: str1: World, str2: Hello
```

在这个示例中，`swapTwoValues` 函数可以交换任何类型的两个值，因为它是泛型函数。`T` 是一个占位符类型，它将在函数被调用时由实际类型替换。

## 泛型类型

你还可以定义泛型类型，例如泛型类、结构体和枚举。以下是一个简单的泛型结构体示例：

```swift
struct Stack<Element> {
    var items: [Element] = []

    mutating func push(_ item: Element) {
        items.append(item)
    }

    mutating func pop() -> Element {
        return items.removeLast()
    }
}

var intStack = Stack<Int>()
intStack.push(1)
intStack.push(2)
print(intStack.pop())  // 输出: 2

var stringStack = Stack<String>()
stringStack.push("Hello")
stringStack.push("World")
print(stringStack.pop())  // 输出: World
```

在这个示例中，`Stack` 结构体是一个泛型类型，可以存储任何类型的元素。`Element` 是一个占位符类型，它将在实例化 `Stack` 时由实际类型替换。

## 泛型约束

有时候，你可能希望对泛型类型施加一些限制。你可以使用泛型约束来指定泛型类型必须符合某些协议或继承自某个类。以下是一个示例：

```swift
func findIndex<T: Equatable>(of valueToFind: T, in array: [T]) -> Int? {
    for (index, value) in array.enumerated() {
        if value == valueToFind {
            return index
        }
    }
    return nil
}

let numbers = [1, 2, 3, 4, 5]
if let index = findIndex(of: 3, in: numbers) {
    print("Index of 3 is \(index)")  // 输出: Index of 3 is 2
}

let words = ["apple", "banana", "cherry"]
if let index = findIndex(of: "banana", in: words) {
    print("Index of banana is \(index)")  // 输出: Index of banana is 1
}
```

在这个示例中，`findIndex` 函数使用了泛型约束 `T: Equatable`，这意味着 `T` 必须符合 `Equatable` 协议。这样可以确保我们在函数内部可以使用 `==` 运算符来比较数组中的元素。

## 关联类型

在定义协议时，你可以使用关联类型来定义泛型占位符。以下是一个示例：

```swift
protocol Container {
    associatedtype Item
    mutating func append(_ item: Item)
    var count: Int { get }
    subscript(i: Int) -> Item { get }
}

struct IntStack: Container {
    var items: [Int] = []

    mutating func push(_ item: Int) {
        items.append(item)
    }

    mutating func pop() -> Int {
        return items.removeLast()
    }

    // 遵循 Container 协议
    mutating func append(_ item: Int) {
        push(item)
    }

    var count: Int {
        return items.count
    }

    subscript(i: Int) -> Int {
        return items[i]
    }
}
```

在这个示例中，`Container` 协议定义了一个关联类型 `Item`。`IntStack` 结构体遵循 `Container` 协议，并将 `Item` 关联类型指定为 `Int`。

### 总结

Swift 的泛型为开发者提供了强大的工具，可以编写灵活且可重用的代码。通过泛型函数、泛型类型、泛型约束和关联类型，你可以创建适用于多种类型的通用代码，而不必牺牲类型安全性。泛型使得代码更加模块化、可维护，并且减少了重复代码。




## Swift的泛型与SwiftUI

是的，Apple 在 SwiftUI 中大量使用了泛型。泛型是 Swift 语言的一个核心特性，它允许开发者编写灵活且可重用的代码。SwiftUI 作为一个声明式的 UI 框架，利用泛型来实现多种功能，主要体现在以下几个方面：

### 1. **视图的类型安全**

SwiftUI 中的视图（`View`）协议是一个泛型协议。许多 SwiftUI 组件和视图使用泛型来确保类型安全。例如，`NavigationLink` 和 `List` 等组件都接受泛型视图作为其内容。这使得开发者可以在不同的上下文中使用不同类型的视图，而不需要牺牲类型安全性。

```swift
struct ContentView: View {
    var body: some View {
        NavigationView {
            NavigationLink(destination: Text("Detail View")) {
                Text("Go to Detail")
            }
        }
    }
}
```

### 2. **组合和重用**

SwiftUI 的设计鼓励视图的组合和重用。通过泛型，开发者可以创建通用的视图结构，比如自定义的 `ViewModifier` 或者 `ViewBuilder`，这些结构可以接受不同类型的视图并进行操作。

例如，下面是一个简单的自定义视图，它接受任何类型的视图：

```swift
struct CustomView<Content: View>: View {
    var content: () -> Content

    var body: some View {
        VStack {
            Text("Header")
            content()  // 调用传入的视图
            Text("Footer")
        }
    }
}
```

### 3. **类型推断和简化代码**

使用泛型可以减少代码的重复性，使代码更加简洁。例如，SwiftUI 的 `ForEach` 结构使用泛型来处理不同类型的集合：

```swift
struct ItemListView: View {
    let items: [String]

    var body: some View {
        List {
            ForEach(items, id: \.self) { item in
                Text(item)
            }
        }
    }
}
```

### 4. **协议和扩展**

SwiftUI 中的许多协议和扩展也使用了泛型。例如，`View` 协议本身就是一个泛型协议，允许开发者定义符合该协议的自定义视图。此外，许多 SwiftUI 组件和功能都使用了泛型扩展来增强功能。

### 5. **性能优化**

泛型在 Swift 中也可以帮助优化性能。通过在编译时确定类型，Swift 可以生成更高效的代码，减少运行时的类型检查和转换。

### 总结

总的来说，泛型在 SwiftUI 中是一个重要的设计理念，帮助开发者创建灵活、可重用和类型安全的代码。通过泛型，SwiftUI 能够提供强大的功能，同时保持简洁和易于理解的 API。这也是 Swift 语言的一大优势，使得开发者能够以更高效的方式构建复杂的用户界面。

---

# inout关键字

在 Swift 中，`inout` 关键字用于标记函数参数，使得该参数可以在函数内部被修改，并且这些修改会影响到函数外部的变量。通常情况下，函数参数是常量，意味着在函数内部对参数的修改不会影响到原始变量。然而，使用 `inout` 关键字后，参数可以被视为变量，允许在函数内部进行修改。

### 使用 `inout` 的特点

1. **传递引用**: 使用 `inout` 时，参数实际上是通过引用传递的，这意味着对参数的修改会影响到传入的变量。

2. **需要使用 `&` 符号**: 在调用带有 `inout` 参数的函数时，必须在传入的变量前加上 `&` 符号，以指示该变量是以引用的方式传递的。

3. **不能是常量**: 传入的变量必须是可变的（即声明为 `var`），因为 `inout` 参数需要能够被修改。

### 示例

以下是一个使用 `inout` 的简单示例，演示如何交换两个变量的值：

```swift
func swapValues(a: inout Int, b: inout Int) {
    let temp = a
    a = b
    b = temp
}

var x = 5
var y = 10

// 使用 & 符号传递变量
swapValues(a: &x, b: &y)

print("x: \(x), y: \(y)")  // 输出: x: 10, y: 5
```

### 解释示例

- 在函数 `swapValues` 中，参数 `a` 和 `b` 被标记为 `inout`，这意味着它们可以在函数内部被修改。
- 在调用函数时，使用 `&x` 和 `&y` 将变量 `x` 和 `y` 作为引用传递给函数。
- 函数内部的操作会直接修改 `x` 和 `y` 的值，因此在函数调用后，`x` 和 `y` 的值被交换。

### 总结

`inout` 关键字在 Swift 中非常有用，特别是在需要修改传入参数并希望这些修改反映到原始变量时。它使得函数能够在不返回值的情况下直接影响外部变量，从而提供了一种灵活的参数传递方式。