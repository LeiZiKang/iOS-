https://www.swift.org/documentation/package-manager/

# 包

包分为3个关键部分，依赖(Dependency)，目标(target)，产品(product)


# 模块的访问控制

在Swift中，默认情况下，每个模块（包括通过Swift Package Manager（SPM）引入的包）都需要显式地通过`import`语句导入才能使用其内容。然而，通过一些技巧和配置，可以实现某些包全局可被访问而无需每次都显式导入。

### 方法一：创建Umbrella Module

一种常见的方法是创建一个“Umbrella Module”（伞模块），在这个模块中统一导入所有需要的模块，然后在项目中只导入这个伞模块。以下是具体步骤：

1. **创建一个新的Swift Package**：
   创建一个新的Swift Package，用于作为伞模块。

2. **在伞模块中导入其他模块**：
   编辑伞模块的`Sources`目录下的Swift文件（例如`UmbrellaModule.swift`），在其中导入所有需要的模块。

   ```swift
   // UmbrellaModule.swift
   @_exported import YourFirstModule
   @_exported import YourSecondModule
   // ... 导入其他模块
   ```

   这里使用了`@_exported import`，它不仅导入了模块，还将其重新导出，使得在任何导入伞模块的地方，这些模块也会被自动导入。

3. **在项目中使用伞模块**：
   在你的主项目中，只需要导入伞模块。

   ```swift
   import UmbrellaModule
   ```

### 方法二：修改Package.swift文件

你可以在`Package.swift`文件中配置你的伞模块，使其包含所有需要的依赖模块。

```swift
// swift-tools-version: 5.6
import PackageDescription

let package = Package(
    name: "UmbrellaModule",
    platforms: [
        .iOS(.v13),
        .macOS(.v10_15)
    ],
    products: [
        .library(
            name: "UmbrellaModule",
            targets: ["UmbrellaModule"]),
    ],
    dependencies: [
        .package(url: "https://github.com/your/first-module.git", from: "1.0.0"),
        .package(url: "https://github.com/your/second-module.git", from: "1.0.0"),
        // ... 添加其他依赖包
    ],
    targets: [
        .target(
            name: "UmbrellaModule",
            dependencies: [
                "YourFirstModule",
                "YourSecondModule",
                // ... 添加其他依赖包
            ]),
        .testTarget(
            name: "UmbrellaModuleTests",
            dependencies: ["UmbrellaModule"]),
    ]
)
```

### 方法三：使用Precompiled Framework

如果你希望避免在每个文件中都显式导入，可以考虑将你的SPM包编译成一个预编译的框架（framework），然后将其集成到你的项目中。这个方法稍微复杂一些，涉及到手动编译和配置，但是可以达到类似的效果。

### 总结

最常见和推荐的方法是通过创建一个伞模块（Umbrella Module），在其中统一导入并重新导出所有需要的模块。这样在你的主项目中只需要导入这个伞模块即可。这种方法简单且有效，能够很好地管理和组织你的依赖。

---
\
# 指定Swift版本

在使用Swift Package Manager时，Swift的版本是通过在你的包的Package.swift文件中指定swiftLanguageVersions属性来设置的。这个属性允许你指定你的包能够与哪些版本的Swift编译器兼容。

下面是一个Package.swift文件的示例，其中设置了Swift语言的版本：

```swift
// swift-tools-version:5.3
// The swift-tools-version declares the minimum version of Swift required to build this package.
 
import PackageDescription
 
let package = Package(
    name: "MyPackage",
    products: [
        // Define your products here.
    ],
    dependencies: [
        // Dependencies declare other packages that this package depends on.
    ],
    targets: [
        // Targets are the basic building blocks of a package. A target can define a module or a test suite.
        // Targets can depend on other targets in this package, and on products in packages this package depends on.
        .target(
            name: "MyTarget",
            dependencies: [],
            swiftSettings: [.version("5")] // 指定Swift版本为5
        ),
        .testTarget(
            name: "MyTargetTests",
            dependencies: ["MyTarget"],
            swiftSettings: [.version("5")] // 指定Swift版本为5
        )
    ]
)
```

在上面的代码中，swiftSettings的.version选项被用来指定Swift的版本。在这个例子中，我们指定了版本为5。你可以根据需要更改版本号。注意，指定的版本需要与你的包能够兼容。

请确保你的swift-tools-version声明与你在Package.swift文件中指定的Swift版本相匹配。这行声明告诉Swift Package Manager你的包需要的最低Swift工具版本。