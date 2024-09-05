# 小组件

https://juejin.cn/post/7292696857163612171


### 小组件尺寸

目前小组件支持设置基础的三个尺寸，即：小、中、大。

设置方式是在 `Widget` 上添加 `supportedFamilies` 属性：

less

复制代码

```swift
import Foundation
import SwiftUI
import WidgetKit

struct MyWidget: Widget {
    let kind: String = "MyWidget" // 唯一标识
    var body: some WidgetConfiguration {
        StaticConfiguration(kind: kind, provider: Provider()) { entry in             MyWidgetEntryView(entry: entry)         }         .configurationDisplayName("这是小组件的名称")
            .description("这是小组件的描述.")
            .supportedFamilies([.systemSmall, .systemMedium, .systemLarge]) // 支持小、中、大尺寸
    }
}
```
  

---

# iOS小组件widget（@avaiable on iOS14）

**教程**

https://zhuanlan.zhihu.com/p/661980240

https://zhuanlan.zhihu.com/p/661980685

**注意事项**

1. app与widget是两个target，最低target版本要保持一致



## 小组件基本知识

### 文件结构
![[Pasted image 20240322164304.png]]

- `MyWidgetBundle` 是小组件的代码入口文件  
    
- `MyWidget` 是主要的小组件代码文件  
    
- `Assets` 存放小组件需要用的资源

![](https://pic2.zhimg.com/80/v2-cd90549bb124c23ecadabbf834c07bd1_720w.webp)

  

然后打开 `MyWidget.swift` 文件，这个文件中总共分为 5 个部分：

- `struct Provider` 负责为小组件提供数据  
    
- `struct SimpleEntry` 小组件的数据模型  
    
- `struct MyWidgetEntryView` 小组件的视图  
    
- `struct MyWidget` 小组件的配置部分  
    
- `struct MyWidget_Previews` 提供小组件在 Xcode 中的预览  
    

### Provider

这个结构体中有三个方法：

- `placeholder(in: )` 在首次显示小组件，没有数据时使用占位  
    
- `getSnapshot(in: , completion: )` 获取小组件的快照，例如在小组件库中预览时会调用  
    
- `getTimeline(in: , completion: )` 这个方法来获取当前时间和（可选）未来时间的时间线的小组件数据以更新小部件。也就是说你在这个方法中设置在什么时间显示什么内容。  
    

### SimpleEntry

这个结构体是小组件的数据模型，默认情况下只有 `let date: Date` 一个属性，后续如果你需要展示更多的数据，可以在这里增加你想要的数据属性。

### MyWidgetEntryView

这个就是小组件的入口视图了，它包含一个 `SimpleEntry` 的数据模型，和一个 `View`。

### MyWidget

这个文件包含小组件的一些配置，`kind` 是这个小组件的唯一标识，可以随便填，以后当你的 App 有多个小组件，为了识别某个小组件时会用得上。

`WidgetConfiguration` 可以针对小组件做一些配置，比如名称、描述、支持的类型等等：

```SWIFT
struct MyWidget: Widget {
    let kind: String = "MyWidget" // 唯一标识

    var body: some WidgetConfiguration {
        StaticConfiguration(kind: kind, provider: Provider()) { entry in
            MyWidgetEntryView(entry: entry)
        }
        .configurationDisplayName("这是小组件的名称")
        .description("这是小组件的描述.")
        .supportedFamilies([.systemSmall, .systemMedium, .systemLarge])
    }
}
```

### MyWidget_Previews

这个结构体提供小组件预览，一般来说默认就行了，当然你也可以调整其中的预览代码。

  

![](https://pic2.zhimg.com/80/v2-832ac6066c5f209752a41dcfce201c75_720w.webp)


## 时间线


时间线是小组件刷新数据的机制，简单来说就是让你告诉系统，你需要小组件什么时间展示什么内容。

刷新**时间和内容**被封装在 `TimelineEntry` 对象中：

```text
struct SimpleEntry: TimelineEntry {
    let date: Date
    // 自定义的其他数据...
}
```

我们可以把它称为**时间线条目**，方便后文描述，每个条目都可以指定更新小组件内容的日期和时间。
举个例子，比如，9 点刷新一次，9 点半刷新一次，10:05 刷新一次，大概是下面这个图：

  

![](https://pic3.zhimg.com/80/v2-44c382b538216eb9d513acdcbf12f062_720w.jpg)





---