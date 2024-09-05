# Apple各平台开发框架介绍

UIKit并不是iOS平台专用的。它主要用于iOS，但也被扩展到其他Apple平台，如iPadOS、tvOS和watchOS。然而，macOS使用的是一个不同的框架叫做AppKit。

**各平台详细情况：**

1. **iOS/iPadOS**:

▪ UIKit是主要的用户界面框架，用于构建iPhone和iPad应用程序。

2. **tvOS**:

▪ UIKit也用于tvOS应用开发，有一些特定的调整和附加内容来适应电视显示和遥控器输入。

3. **watchOS**:

▪ UIKit的一些部分用于watchOS，用于构建用于Apple Watch的应用程序，但大多使用WatchKit，这是为小屏幕设备特别设计的。

4. **macOS**:

▪ macOS主要使用AppKit，这是为桌面应用程序提供更多功能和灵活性的框架。

▪ **注意**: 在macOS 10.15 Catalina及更高版本，Apple引入了Mac Catalyst（Project Catalyst），它允许开发者将iPad应用移植到macOS，并在macOS上运行iPad应用。在这种情况下，你可以使用UIKit在macOS上开发应用程序。

**UIKit 与 AppKit 对比**

• **UIKit**:

▪ 面向触摸屏设备（iOS, iPadOS）

▪ 设计为轻量级并适合移动设备的用户交互

▪ 使用单视图控制器（UIViewController）

• **AppKit**:

▪ 面向桌面设备（macOS）

▪ 支持更复杂的窗口和视图层次结构

▪ 使用窗口控制器（NSWindowController）和视图控制器（NSViewController）

**UIKit的跨平台扩展**

借助于Mac Catalyst，可使同一个iOS应用在macOS上运行，这样开发者可以实现跨平台共享代码，但要注意对一些特定平台进行调整和优化。

**总结**

虽然UIKit主要设计用于iOS和iPadOS，但它也被tvOS和watchOS使用，并通过Mac Catalyst允许在macOS上运行iPad应用。对于专门的macOS开发，AppKit仍然是首选框架。
---


在 SwiftUI 上制作一个可以点击复制文本到剪切板的 Mac 应用非常简单。你可以使用 ﻿NSPasteboard 类来管理剪切板内容，并在按钮点击时将文本复制到剪切板。

以下是一个SwiftUI示例，展示如何实现这一功能：

**示例代码**

1. 创建一个新的 SwiftUI Mac 应用程序项目。

2. 使用以下代码在 SwiftUI 视图中添加一个按钮，当点击时将文本复制到剪切板。

  

import SwiftUI

  

struct ContentView: View {

    var body: some View {

        VStack {

            Text("Click the button to copy text to clipboard!")

                .padding()

            Button(action: {

                copyToClipboard(text: "Hello, World!")

            }) {

                Text("Copy to Clipboard")

                    .padding()

                    .background(Color.blue)

                    .foregroundColor(.white)

                    .cornerRadius(8)

            }

        }

        .padding()

    }

  

    private func copyToClipboard(text: String) {

        let pasteboard = NSPasteboard.general

        pasteboard.clearContents()

        pasteboard.setString(text, forType: .string)

    }

}

  

@main

struct YourAppNameApp: App {

    var body: some Scene {

        WindowGroup {

            ContentView()

        }

    }

}

**解释**

1. **内容视图 (**﻿ContentView**)**：

▪ 使用 ﻿VStack 布局来垂直排列文本和按钮。

▪ ﻿Text 显示一段提示文字。

▪ ﻿Button 在点击时调用 ﻿copyToClipboard 函数，将指定文本复制到剪切板。

2. ﻿copyToClipboard **函数**：

▪ 创建一个 ﻿NSPasteboard 实例。

▪ 清除剪切板的现有内容。

▪ 将字符串设置为剪贴板的内容。

3. ﻿YourAppNameApp **应用程序入口**：

▪ ﻿@main 标记表示应用的入口点。

▪ ﻿WindowGroup 包裹了 ﻿ContentView，意味着这个视图将作为窗口内容显示。

**运行效果**

点击 "Copy to Clipboard" 按钮后，字符串 "Hello, World!" 将被复制到剪切板，你可以通过 ﻿Cmd+V 粘贴验证结果。

这个简单的示例展示了如何在 SwiftUI 中实现点击按钮将文本复制到剪切板的功能。这可以扩展使用在更多复杂场景，如复制动态生成的内容等。

---

# 支持MacOS提示的第三方库

https://github.com/elai950/AlertToast?tab=readme-ov-file#usage-example-with-regular-alert


任何纯SwiftUI编写的框架都可以用于iOS， MacOS


---

# MacOS 工具

如果你想在控制面板（控制台）中要求用户输入目录路径并使用这个路径来调用 ﻿listMFiles(in:) 函数，可以使用 ﻿readLine() 函数来获取用户输入。以下是一个示例代码，展示如何实现这个交互过程：

  

import Foundation

  

func listMFiles(in directory: String) {

    var mFiles = [String]()

    let fileManager = FileManager.default

    guard let enumerator = fileManager.enumerator(atPath: directory) else {

        print("Could not create enumerator for directory: \(directory)")

        return

    }

    for case let file as String in enumerator {

        if file.hasSuffix(".m") {

            let fullPath = (directory as NSString).appendingPathComponent(file)

            mFiles.append(fullPath)

        }

    }

    for file in mFiles {

        replaceChineseStrings(inFileAtPath: file)

    }

}

  

func replaceChineseStrings(inFileAtPath filePath: String) {

    // 这里可以实现对每个 .m 文件的处理逻辑

    print("Replacing Chinese strings in file: \(filePath)")

}

  

// 从控制台获取用户输入的目录路径

print("请输入要遍历的目录路径:")

if let directoryPath = readLine() {

    listMFiles(in: directoryPath)

} else {

    print("未输入有效的目录路径")

}

**代码说明：**

1. **定义** ﻿listMFiles(in:) **函数**:

▪ 实现文件遍历逻辑，找到并处理所有 ﻿.m 文件。

2. **定义** ﻿replaceChineseStrings(inFileAtPath:) **函数**:

▪ 示例中的处理逻辑仅打印处理文件的消息，你可以在这里实现具体的处理逻辑。

3. **从控制台获取用户输入**:

  

print("请输入要遍历的目录路径:")

if let directoryPath = readLine() {

    listMFiles(in: directoryPath)

} else {

    print("未输入有效的目录路径")

}

▪ 提示用户输入要遍历的目录路径。

▪ 使用 ﻿readLine() 获取用户输入。如果输入有效，则调用 ﻿listMFiles(in:) 函数进行处理。

通过这段代码，你可以在控制面板中要求用户输入目录路径，并使用输入的路径调用 ﻿listMFiles(in:) 函数，从而遍历并处理指定目录中的所有 ﻿.m 文件。

---

# 通知

在使用 SwiftUI 框架的 macOS 应用中，你可以通过 `UserNotifications` 框架来实现通知功能。以下是一个完整的示例，展示如何在 SwiftUI 中请求通知权限并发送通知。

### 请求通知权限

首先，在应用启动时请求用户的通知权限。可以在 `App` 结构体中进行权限请求。

```swift
import SwiftUI
import UserNotifications

@main
struct YourApp: App {
    @NSApplicationDelegateAdaptor(AppDelegate.self) var appDelegate

    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}

class AppDelegate: NSObject, NSApplicationDelegate {
    func applicationDidFinishLaunching(_ notification: Notification) {
        // 请求通知权限
        UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .sound, .badge]) { (granted, error) in
            if granted {
                print("Permission granted")
            } else if let error = error {
                print("Permission denied: \(error.localizedDescription)")
            }
        }
    }
}
```

### 发送通知

在 SwiftUI 视图中，可以通过按钮点击事件来发送通知：

```swift
import SwiftUI
import UserNotifications

struct ContentView: View {
    var body: some View {
        VStack {
            Button(action: sendNotification) {
                Text("Send Notification")
                    .padding()
                    .background(Color.blue)
                    .foregroundColor(.white)
                    .cornerRadius(8)
            }
        }
        .frame(width: 300, height: 200)
    }

    func sendNotification() {
        let content = UNMutableNotificationContent()
        content.title = "Hello"
        content.body = "This is a macOS notification."
        content.sound = UNNotificationSound.default

        let trigger = UNTimeIntervalNotificationTrigger(timeInterval: 1, repeats: false)
        let request = UNNotificationRequest(identifier: UUID().uuidString, content: content, trigger: trigger)

        UNUserNotificationCenter.current().add(request) { (error) in
            if let error = error {
                print("Error adding notification: \(error.localizedDescription)")
            }
        }
    }
}
```

### 完整示例

以下是完整的 SwiftUI 示例代码：

```swift
import SwiftUI
import UserNotifications

@main
struct YourApp: App {
    @NSApplicationDelegateAdaptor(AppDelegate.self) var appDelegate

    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}

class AppDelegate: NSObject, NSApplicationDelegate {
    func applicationDidFinishLaunching(_ notification: Notification) {
        // 请求通知权限
        UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .sound, .badge]) { (granted, error) in
            if granted {
                print("Permission granted")
            } else if let error = error {
                print("Permission denied: \(error.localizedDescription)")
            }
        }
    }
}

struct ContentView: View {
    var body: some View {
        VStack {
            Button(action: sendNotification) {
                Text("Send Notification")
                    .padding()
                    .background(Color.blue)
                    .foregroundColor(.white)
                    .cornerRadius(8)
            }
        }
        .frame(width: 300, height: 200)
    }

    func sendNotification() {
        let content = UNMutableNotificationContent()
        content.title = "Hello"
        content.body = "This is a macOS notification."
        content.sound = UNNotificationSound.default

        let trigger = UNTimeIntervalNotificationTrigger(timeInterval: 1, repeats: false)
        let request = UNNotificationRequest(identifier: UUID().uuidString, content: content, trigger: trigger)

        UNUserNotificationCenter.current().add(request) { (error) in
            if let error = error {
                print("Error adding notification: \(error.localizedDescription)")
            }
        }
    }
}
```

### 关键步骤

1. **请求通知权限**：
   - 在 `AppDelegate` 的 `applicationDidFinishLaunching` 方法中请求用户的通知权限。
   - 使用 `UNUserNotificationCenter.current().requestAuthorization(options:completionHandler:)` 方法。

2. **发送通知**：
   - 在 SwiftUI 视图中，创建一个按钮，并在按钮点击事件中发送通知。
   - 创建通知内容 `UNMutableNotificationContent`。
   - 设置通知触发条件 `UNTimeIntervalNotificationTrigger`。
   - 创建通知请求 `UNNotificationRequest`。
   - 将通知请求添加到通知中心 `UNUserNotificationCenter.current().add(request)`。

以上代码展示了如何在 SwiftUI 框架的 macOS 应用中使用通知。确保在实际应用中处理好用户权限和错误情况。