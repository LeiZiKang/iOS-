# app显示名字`BundleDisplayName`

在Xcode中，如果你想改变Info.plist中的应用程序名称，你可以编辑Info.plist文件中的CFBundleDisplayName键。这个键定义了应用程序在用户界面上显示的名称。
以下是具体步骤：
在Xcode项目导航器中，选择你的项目文件（通常是带有你的项目名称的.xcodeproj文件）。
展开你的目标项目，然后选择你想要更改的Info.plist文件。
查看属性列表的内容，找到CFBundleDisplayName键。
双击CFBundleDisplayName键，输入你想要显示的新名称。
如果CFBundleDisplayName不存在，你可以选择在列表中右键点击，然后选择"Add Row"，并添加新的键，将其命名为CFBundleDisplayName，然后设置其值为你的新应用程序名称。
保存Info.plist文件的更改。
注意：如果你的项目是作为workspace的一部分，确保你选择的是正确的项目文件，并且操作是在该项目的上下文中进行的。
这将改变应用程序在iOS设备上显示的名称，以及在App Store和其他地方，除非你的代码或其他配置文件中有其他地方硬编码了旧的应用程序名称。


---

#  iOS系统分享

## ShareExtension

原生分享插件与自定义的区别：
https://www.jianshu.com/p/ee998ed20df3


## `UIActivityViewController`

在SwiftUI中，你可以使用`Button`和`UIActivityViewController`来实现点击按钮调出分享扩展。以下是一个例子：

```swift
import SwiftUI

struct ContentView: View {
    @State private var showShareSheet = false

    var body: some View {
        Button(action: {
            showShareSheet = true
        }) {
            Text("分享")
        }
        .sheet(isPresented: $showShareSheet) {
            ShareSheet(activityItems: ["分享内容"])
        }
    }
}

struct ShareSheet: UIViewControllerRepresentable {
    let activityItems: [Any]
    var applicationActivities: [UIActivity]? = nil

    func makeUIViewController(context: Context) -> UIActivityViewController {
        let controller = UIActivityViewController(activityItems: activityItems, applicationActivities: applicationActivities)
        return controller
    }

    func updateUIViewController(_ uiViewController: UIActivityViewController, context: Context) {}
}
```

在这个例子中，当用户点击"分享"按钮时，会弹出一个`ShareSheet`视图，这个视图是一个`UIActivityViewController`的封装。你可以将"分享内容"替换为你想要分享的任何内容，比如文本、图片、URL等。

---

# 保存图片到相册

[NSPhotoLibraryAddUsageDescription](https://link.jianshu.com/?t=https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW73)

在iOS11后如果不在info.plist中增加[NSPhotoLibraryAddUsageDescription](https://link.jianshu.com/?t=https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW73)，用户在保存图片到相册时会崩溃

1.iOS11之后

使用UIImageWriteToSavedPhotosAlbum(nil,nil,nil,nil);这种方法保存图片到相册,在原来的增加[NSPhotoLibraryUsageDescription](https://link.jianshu.com/?t=https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW17)的基础上需要增加权限：[NSPhotoLibraryAddUsageDescription](https://link.jianshu.com/?t=https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW73)。

[NSPhotoLibraryAddUsageDescription](https://link.jianshu.com/?t=https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW73)这个权限只有在保存图片到相册的时候才会触发，在iOS11之前[NSPhotoLibraryUsageDescription](https://link.jianshu.com/?t=https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW17)包括用户的读写权限，iOS11后[NSPhotoLibraryUsageDescription](https://link.jianshu.com/?t=https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW17)只有读的权限，[NSPhotoLibraryAddUsageDescription](https://link.jianshu.com/?t=https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW73)有写的权限。  

但是使用

```swift
[[PHPhotoLibrarysharedPhotoLibrary]performChanges:^{

PHAssetChangeRequest*photoAsset = [PHAssetChangeRequestcreationRequestForAssetFromImage:image];

}completionHandler:^(BOOLsuccess,NSError*_Nullableerror) {

if(success) {

}else{

}  

}];
```

则不需要增加权限

---

# 剪切板

UITextField、UITextView组件系统原生就支持文字的复制，但有时我们需要让其他的一些组件也能实现复制功能，比如点击复制UILabel上的文字、UIImageView中的图片、UITableView里单元格的内容、或者点击按钮把文字或图片自动复制到粘贴板中等等。

这些我们借助 UIPasteboard 就可以实现。

一，将内容写入到剪贴板中

1，复制字符串

|   |   |
|---|---|
|1|`UIPasteboard``.general.string =` `"欢迎访问 hangge.com"`|

2，复制字符串数组

|   |   |
|---|---|
|1|`UIPasteboard``.general.strings = [``"hellow"``,` `"hangge.com"``]`|

3，复制图片

|   |   |
|---|---|
|1<br><br>2|`let` `image =` `UIImage``(named:` `"logo.png"``)`<br><br>`UIPasteboard``.general.image = image`|

4，复制二进制数据（Data）

|   |   |
|---|---|
|1<br><br>2<br><br>3<br><br>4|`let` `path =` `Bundle``.main.path(forResource:` `"logo"``, ofType:` `"png"``)!`<br><br>`let` `url =` `URL``(fileURLWithPath: path)`<br><br>`let` `fileData = try!` `Data``(contentsOf: url)`<br><br>`UIPasteboard``.general.setData(fileData, forPasteboardType:` `"public.png"``)`|

注：从剪贴板获取二进制数据（Data）

|     |                                                                                     |
| --- | ----------------------------------------------------------------------------------- |
| 1   | `let` `myData =` `UIPasteboard``.general.data(forPasteboardType:` `"public.png"``)` |


在 iOS 14 及以上版本中，当应用程序尝试访问剪贴板时，系统会自动弹出一个提示框，告诉用户应用程序正在尝试访问剪贴板。这是由系统自动处理的，开发者无需手动请求权限。

但是，如果你的应用需要在后台访问剪贴板，你需要在 Info.plist 文件中添加 `NSPasteboardReadingOptionsKey` 键，并设置其值为 `NSPasteboardReadingAsData` 或 `NSPasteboardReadingAsString`。

请注意，频繁访问剪贴板可能会引起用户的不满，因此最好只在必要时才访问剪贴板。

这是一个例子：

```xml
<key>NSPasteboardReadingOptionsKey</key>
<string>NSPasteboardReadingAsString</string>
```

在你的代码中，你可以使用以下方式来访问剪贴板：

```swift
let pasteboard = UIPasteboard.general
if let string = pasteboard.string {
    print("剪贴板内容：", string)
}
```

这段代码会尝试从剪贴板中读取字符串。如果剪贴板中有字符串，它将被打印出来。

https://blog.csdn.net/gf771115/article/details/112307980

---
# 压缩文件的方法

## 1. 第三方库`ZIPFoundation` 

第三方库：
 https://github.com/weichsel/ZIPFoundation

用法：
https://qiita.com/john-rocky/items/7c3c8701646c8b9ab5ed

## 2. 原生
iOS只提供压缩单个文件的APi，不提供压缩整个文件夹的Api



---
# 数据库
## CoreData

## CoreData的数据类型

### 1.URI
在 CoreData 中，每个托管对象都有一个与之关联的 URI，称为 URI 表示形式（URI representation）。这个 URI 是一个唯一标识托管对象的标识符，它包含了托管对象的实体名称、托管对象所在的托管对象上下文，以及托管对象的对象 ID。

URI 表示形式的格式如下：

```
x-coredata://<UUID>/<EntityName>/p<PrimaryKey>
```

其中：

- `<UUID>` 是托管对象所在的持久化存储协调器的 UUID。
- `<EntityName>` 是托管对象的实体名称。
- `<PrimaryKey>` 是托管对象的主键，它是一个唯一标识托管对象的数字。

例如，一个 URI 表示形式可能是这样的：

```
x-coredata://3F2504E0-4F89-11D3-9A0C-0305E82C3301/Person/p1
```

在这个例子中，`3F2504E0-4F89-11D3-9A0C-0305E82C3301` 是持久化存储协调器的 UUID，`Person` 是实体名称，`1` 是主键。

你可以通过 `NSManagedObject` 的 `objectID` 属性获取对象 ID，然后通过 `NSManagedObjectID` 的 `uriRepresentation` 方法获取 URI 表示形式。例如：

```swift
let uri = managedObject.objectID.uriRepresentation()
```

### 2. Binary Data

在 CoreData 中，`Binary Data` 是一种属性类型，它用于存储二进制数据。在 Swift 中，这种类型的属性通常被映射为 `Data` 类型。

所以，`Binary Data` 和 `Data` 之间实际上没有区别。`Binary Data` 是 CoreData 中的一个数据类型，用于在数据库中存储二进制数据，而 `Data` 是 Swift 中的一个数据类型，用于在代码中处理二进制数据。

当你在 CoreData 模型中为某个实体创建一个 `Binary Data` 类型的属性时，你可以在你的 Swift 代码中使用 `Data` 类型的变量来访问和操作这个属性。例如，如果你有一个名为 `photo` 的 `Binary Data` 类型的属性，你可以像这样在你的 Swift 代码中使用它：

```swift
let photoData: Data = person.photo
```

在这个例子中，`photoData` 是一个 `Data` 类型的变量，它包含了 `person` 的 `photo` 属性的值。


### 3.对URL类型的存储

在 CoreData 中，你不能直接存储 `URL` 类型的数据。但是，你可以将 `URL` 转换为 `String` 或 `Data`，然后存储转换后的数据。

以下是一个例子，展示了如何将 `URL` 转换为 `String`，然后存储转换后的数据：

首先，在你的 CoreData 模型中，为你的实体添加一个新的属性，并将其类型设置为 `String`。例如，你可能有一个名为 `Person` 的实体，你可以为它添加一个名为 `website` 的 `String` 类型的属性。

然后，在你的代码中，你可以像这样存储 `URL` 对象：

```swift
let person = NSEntityDescription.insertNewObject(forEntityName: "Person", into: context) as! Person
person.website = yourURL.absoluteString
```

在这个例子中，首先创建了一个 `Person` 的实例 `person`，然后将 `URL` 对象 `yourURL` 的绝对字符串存储在 `person` 的 `website` 属性中。

最后，别忘了保存你的上下文：

```swift
do {
    try context.save()
} catch {
    print("Failed saving")
}
```

这将把你的更改保存到持久化存储中。

请注意，这个示例假设你已经有了一个名为 `Person` 的实体，它有一个名为 `website` 的 `String` 类型的属性，以及一个名为 `context` 的 `NSManagedObjectContext` 对象。你可能需要根据你的实际情况对这个示例进行一些修改。

## CoreStore错误

```
❗ [CoreStore: Fatal Error] XcodeDataModelSchema.swift:57 from(modelName:bundle:migrationChain:)
  ↪︎ Could not find "FileTransferAssistant.momd" from the bundle "LeiZikang.FileTransferAssistant". Other model files in bundle: 1 item(s) [
    0 = "FileTransferAssitant.momd";
]
```

删掉xcdatamodeld后重新添加即可

---
# 音频
## 音频的访问权限与后台播放

在iOS中，播放声音并不需要特殊的权限。你可以使用AVFoundation框架中的AVAudioPlayer类来播放音频，而不需要请求用户的权限。

但是，如果你想访问用户的音乐库，或者你想在后台播放音频，那么你需要请求相应的权限。

1. 访问用户的音乐库：你需要在你的Info.plist文件中添加一个对应的键值对，键为`NSAppleMusicUsageDescription`，值为你的请求理由。

```xml
<key>NSAppleMusicUsageDescription</key>
<string>We need access to your music library for...</string>
```

2. 后台播放音频：你需要在你的Info.plist文件中添加一个对应的键值对，键为`UIBackgroundModes`，值为一个数组，其中包含一个字符串`audio`。

```xml
<key>UIBackgroundModes</key>
<array>
    <string>audio</string>
</array>
```

请注意，你应该尽量减少对用户权限的请求，只有当你真正需要这些权限时，才应该请求。并且，你应该在请求权限时向用户清楚地解释为什么需要这些权限。


## AVFoundation

在Objective-C中，我们可以使用AVFoundation库中的AVPlayer类来实现在线音频播放。以下是一个简单的示例：

```objective-c
#import <AVFoundation/AVFoundation.h>

@interface CFSoundRequest()

@property (nonatomic, strong) AVPlayer *onlinePlayer;

@end

@implementation CFSoundRequest

// 在线资源播放器
- (AVPlayer *)onlinePlayer {
    if (!_onlinePlayer) {
        _onlinePlayer = [[AVPlayer alloc] init];
    }
    return _onlinePlayer;
}

// 播放在线资源
- (void)playOnlineAudioWithURL:(NSString *)url {
    if (!url.isValidString) {
        return;
    }
    self.playingOnlineUrl = url;
    NSURL *audioURL = [NSURL URLWithString:url];
    AVPlayerItem *playerItem = [AVPlayerItem playerItemWithURL:audioURL];
    [self.onlinePlayer replaceCurrentItemWithPlayerItem:playerItem];
    [self.onlinePlayer play];
}

// 停止播放在线资源
- (void)stopOnlineAudioPlay {
    [self.onlinePlayer pause];
}

@end
```

这段代码首先导入了AVFoundation库，然后在CFSoundRequest类中添加了一个AVPlayer类型的属性onlinePlayer。在onlinePlayer的getter方法中，如果onlinePlayer不存在，就创建一个新的AVPlayer实例。

在playOnlineAudioWithURL:方法中，首先检查传入的url是否有效，如果有效，就创建一个NSURL实例，并使用这个NSURL实例创建一个AVPlayerItem实例，然后使用replaceCurrentItemWithPlayerItem:方法将onlinePlayer当前的播放项替换为新创建的AVPlayerItem实例，并调用play方法开始播放。

在stopOnlineAudioPlay方法中，调用onlinePlayer的pause方法来停止播放。

## AudioKit
对于iOS开发，一个很受欢迎且功能强大的第三方库用于播放在线和本地音频是 **AudioKit**。

### AudioKit 简介
AudioKit 是一个强大的音频合成、处理和分析库。它支持iOS、macOS 和 tvOS，是基于 Swift 和 C++ 构建的。AudioKit 允许开发者非常简单地实现复杂的音频功能，比如合成声音、添加效果、进行音频分析等。

### AudioKit 主要特性
- **广泛的音频支持**：支持播放本地音频文件以及流式传输在线音频。
- **音频合成**：可以创建虚拟乐器，合成独特的声音。
- **音频效果**：内置多种音频效果，如混响、延时、失真等。
- **音频分析**：提供工具进行实时音频分析，如频谱分析、节拍检测等。

### 如何使用 AudioKit 播放音频
以下是一个简单的示例，展示如何使用 AudioKit 播放本地音频文件：

```swift
import AudioKit
import AVFoundation

class AudioPlayer {
    var player: AKPlayer?
    
    init() {
        AKSettings.playbackWhileMuted = true
        do {
            try AKSettings.setSession(category: .playback)
        } catch {
            AKLog("Could not set session category.")
        }
        AKManager.output = player
        do {
            try AKManager.start()
        } catch {
            AKLog("AudioKit did not start!")
        }
    }
    
    func play(fileUrl: URL) {
        let file = try? AKAudioFile(forReading: fileUrl)
        if let audioFile = file {
            player = AKPlayer(audioFile: audioFile)
            player?.isLooping = true
            player?.play()
        }
    }
    
    func stop() {
        player?.stop()
    }
}
```

这段代码初始化了一个 `AudioPlayer` 类，它有播放和停止音频的方法。`play(fileUrl:)` 方法接受一个文件URL，用来播放该文件。

### 安装
要在你的项目中使用 AudioKit，你可以通过 CocoaPods 来安装：

```ruby
pod 'AudioKit', '~> 5.0'
```

确保在你的 `Podfile` 中添加了上述内容，然后运行 `pod install` 来集成到你的项目中。

### 结论
AudioKit 是一个非常强大且灵活的库，适用于需要高级音频功能的iOS应用。不仅仅是播放音频，你还可以探索它的合成和音频处理功能来丰富你的应用。


---

# 网络图片

https://github.com/onevcat/Kingfisher



---

# 设备信息

## 获取当前语言

在iOS中，你可以通过`Locale`类来获取设备的当前语言设置。以下是如何获取设备语言的Swift代码：

```swift
let languageCode = Locale.current.languageCode
print("Device language: \(languageCode ?? "unknown")")
```

在这段代码中，`Locale.current`返回一个表示设备当前区域设置的`Locale`实例。`languageCode`属性是一个可选的字符串，表示这个区域的语言代码。如果设备的语言设置无法获取，`languageCode`将为`nil`，在这种情况下，我们打印"unknown"。

你可以通过检查`Locale.current.languageCode`的值来判断设备的语言设置。以下是如何判断设备是否设置为中文、英语或意大利语的Swift代码：

```swift
let languageCode = Locale.current.languageCode

switch languageCode {
case "zh":
    print("设备语言设置为中文")
case "en":
    print("Device language is set to English")
case "it":
    print("La lingua del dispositivo è impostata su italiano")
default:
    print("Device language is not Chinese, English, or Italian")
}
```

在这段代码中，我们使用`switch`语句来检查`languageCode`的值。如果值为"zh"，则设备语言设置为中文；如果值为"en"，则设备语言设置为英语；如果值为"it"，则设备语言设置为意大利语。如果`languageCode`的值不是这三种之一，我们打印一条消息表示设备语言不是中文、英语或意大利语。


---

# 通知中心`NotificationCenter`

在iOS中，通知是一种强大的解耦工具，允许不同的应用组件之间进行通信，而不需要直接的引用。这是通过`NotificationCenter`类实现的。

以下是如何在Swift中使用通知的基本步骤：

1. **定义通知名**：首先，你需要定义一个通知的名字。这通常是一个静态的字符串，可以定义在`Notification.Name`的扩展中。

```swift
extension Notification.Name {
    static let myNotification = Notification.Name("myNotification")
}
```

2. **发送通知**：你可以使用`NotificationCenter`的`post`方法来发送通知。

```swift
NotificationCenter.default.post(name: .myNotification, object: nil)
```

在这里，`object`参数可以用来传递与通知相关的任何数据。如果你不需要传递任何数据，你可以设置它为`nil`。

3. **监听通知**：你可以使用`NotificationCenter`的`addObserver`方法来监听通知。

```swift
NotificationCenter.default.addObserver(self, selector: #selector(handleMyNotification), name: .myNotification, object: nil)
```

在这里，`selector`参数是一个方法，当通知被接收时，这个方法将被调用。`object`参数可以用来指定你只想接收哪个对象发送的通知。如果你想接收所有对象发送的通知，你可以设置它为`nil`。

4. **处理通知**：你需要定义一个方法来处理通知。

```swift
@objc func handleMyNotification(notification: NSNotification) {
    // 处理通知
}
```

5. **移除通知监听器**：当你不再需要监听通知时，你应该移除通知监听器，以避免内存泄漏。

```swift
NotificationCenter.default.removeObserver(self, name: .myNotification, object: nil)
```

通常，你会在对象的`deinit`方法中移除通知监听器。


---

# iOS的响应式编程

iOS中的响应式编程框架主要有以下几种：

1. RxSwift：这是ReactiveX API的Swift版本，它是一个强大的响应式编程库，可以帮助你更容易地编写动态、响应式的代码。

2. ReactiveCocoa：这是一个Objective-C的响应式编程框架，它提供了一种声明式的方式来处理数据流和事件传播。

3. Combine：这是Apple在iOS 13中引入的新框架，它提供了一种声明式的方式来处理异步事件。

哪一个框架最好用，这主要取决于你的具体需求和你的团队的技术栈。如果你的项目是用Swift编写的，并且需要支持iOS 13以上的版本，那么Combine可能是一个不错的选择，因为它是Apple官方提供的，与Swift和其他Apple框架的集成性很好。如果你的项目需要支持iOS 13以下的版本，或者你的团队已经熟悉了RxSwift或ReactiveCocoa，那么选择这两个框架也是一个不错的选择。

RxSwift、ReactiveCocoa和Combine都是响应式编程框架，但它们之间存在一些关键的区别：

1. **RxSwift**：RxSwift是ReactiveX API的Swift实现，它是一个跨平台的响应式编程库，可以在iOS、Android等多个平台上使用。RxSwift提供了一套丰富的操作符，可以帮助你更容易地处理异步事件和数据流。

2. **ReactiveCocoa**：ReactiveCocoa最初是为Objective-C设计的，后来也增加了对Swift的支持。ReactiveCocoa提供了一套强大的函数式编程和响应式编程工具，但它的API和RxSwift有一些不同，学习曲线可能会比RxSwift更陡峭。

3. **Combine**：Combine是Apple在iOS 13中引入的新框架，它提供了一种声明式的方式来处理异步事件。Combine与Swift和其他Apple框架的集成性很好，但它只能在iOS 13及以上版本的系统中使用。

总的来说，哪个框架最适合你，主要取决于你的具体需求和你的团队的技术栈。如果你的项目需要支持iOS 13以下的版本，或者你的团队已经熟悉了RxSwift或ReactiveCocoa，那么选择这两个框架可能是一个不错的选择。如果你的项目是用Swift编写的，并且需要支持iOS 13及以上版本的系统，那么Combine可能是一个更好的选择。

---


# UITableView

`UItableView`的`section`必须`return` `1`不能为空或`0`


---


# 系统相机界面

系统相机界面通常是由`UIImagePickerController`类来实现的。`UIImagePickerController`是一个视图控制器，它可以让用户从用户的图库中选择图片，或者使用相机拍摄新的图片。当你创建一个`UIImagePickerController`实例并将其`sourceType`属性设置为`.camera`时，它就会显示系统相机界面。

---

# Xcode的`.bundle` 文件

Xcode中的 ﻿.bundle 文件是一个目录结构，它被用于收集和组织应用程序的资源文件。﻿.bundle 文件可以包含如下资源：

• 图像

• 音频文件

• 视频文件

• NIB/XIB 文件（用于定义用户界面）

• 文件的本地化版本

• 自定义的任意文件（如动态库、文本文档等）

﻿.bundle 文件的结构和用途类似于单个文件，但实际上是一个目录，并且被系统当作一个单独的资源文件来管理和加载。

**主要功能和用途**

1. **资源组织**：

﻿.bundle 可以用来将资源文件组织在一起，使得项目结构更清晰、维护更方便。开发者可以将特定的资源按照功能模块分开存放在不同的 ﻿.bundle 中。

2. **本地化支持**：

在使用多语言的应用中，可以在 ﻿.bundle 文件夹中存放不同语言版本的资源文件，系统会根据用户的语言设置自动加载相应的资源。

3. **动态加载**：

应用程序在运行时可以动态地加载和使用 ﻿.bundle 内的资源。这种动态加载的能力让应用更具灵活性，尤其适用于插件架构或者模块化开发。

4. **切分项目**：

对于大型项目，可以通过 ﻿.bundle 文件将资源和代码分割开来，便于项目的模块化管理和开发。

**如何创建和使用** ﻿.bundle **文件**

**创建** ﻿.bundle **文件**

1. **在 Xcode 中创建** ﻿.bundle **文件**：

▪ 右键点击项目中的某个组（group），选择 ﻿New File...。

▪ 在 ﻿Resource 选项卡下选择 ﻿Bundle 文件模板，创建一个新的 ﻿.bundle 文件，并命名它。

2. **将资源添加到** ﻿.bundle **文件中**：

▪ 将资源文件（如图片、音频、视频等）拖放到已经创建的 ﻿.bundle 目录中。

**使用代码加载** ﻿.bundle **文件中的资源**

假设你已经在项目中添加了一个名为 ﻿MyResources.bundle 的资源包，并且在里面存放了一张图片 ﻿exampleImage.png。

  

```swift
import UIKit

  

// 获取自定义 .bundle 文件的 URL

if let bundleURL = Bundle.main.url(forResource: "MyResources", withExtension: "bundle"),

   let resourceBundle = Bundle(url: bundleURL) {

    // 从 .bundle 文件中加载图片资源

    if let imageURL = resourceBundle.url(forResource: "exampleImage", withExtension: "png"),

       let image = UIImage(contentsOfFile: imageURL.path) {

        // 这里可以使用 image 对象

        let imageView = UIImageView(image: image)

        imageView.frame = CGRect(x: 0, y: 0, width: 200, height: 200)

        // 将 imageView 添加到视图

    }

}
```

**注意事项**

• **路径问题**：在加载资源时，确保路径和文件名必须完全匹配，包括大小写。

• **依赖管理**：如果你在 ﻿.bundle 中存放资源，如NIB/XIB文件，确保这些文件所依赖的资源也包含在同一个 ﻿.bundle 中。

• **打包和发布**：在打包应用时，确保所有 ﻿.bundle 文件及其内容都包含在应用的最终发布包中。Xcode通常会自动处理这部分，但检查一下以确保没有遗漏。

**示例**

以下是一个更复杂的示例，演示了如何加载不同类型的资源：

  

``` swift
import UIKit

import AVFoundation

  

class ViewController: UIViewController {

  

    override func viewDidLoad() {

        super.viewDidLoad()

        // 加载图片资源

        if let bundleURL = Bundle.main.url(forResource: "MyResources", withExtension: "bundle"),

           let resourceBundle = Bundle(url: bundleURL),

           let imageURL = resourceBundle.url(forResource: "exampleImage", withExtension: "png"),

           let image = UIImage(contentsOfFile: imageURL.path) {

            let imageView = UIImageView(image: image)

            imageView.frame = CGRect(x: 0, y: 0, width: 200, height: 200)

            self.view.addSubview(imageView)

        }

        // 加载视频资源

        if let bundleURL = Bundle.main.url(forResource: "MyResources", withExtension: "bundle"),

           let resourceBundle = Bundle(url: bundleURL),

           let videoURL = resourceBundle.url(forResource: "exampleVideo", withExtension: "mp4") {

            let player = AVPlayer(url: videoURL)

            let playerViewController = AVPlayerViewController()

            playerViewController.player = player

            self.present(playerViewController, animated: true) {

                player.play()

            }

        }

    }

}
```

通过使用 ﻿.bundle 文件，你可以更加有效地管理资源，并提升项目的组织性和可维护性。


---

# UIButton

如果 ﻿UIImageView 的父视图本身就是 ﻿UIButton，我们可以通过多种方式确保点击 ﻿UIImageView 触发 ﻿UIButton 的点击事件。以下是一些简化的实现方法：

**方法一：使用透明按钮覆盖** ﻿UIImageView

在 ﻿UIImageView 上添加一个透明的 ﻿UIButton，并将事件转发给父视图（即实际的 ﻿UIButton）。

  

```swift
// 假设 button 是你的 UIButton 实例

let button = UIButton(type: .system)

button.frame = CGRect(x: 50, y: 50, width: 200, height: 200)

  

// 设置按钮其他属性，比如背景色

button.backgroundColor = .lightGray

  

// 创建并添加 UIImageView 到 UIButton

let imageView = UIImageView(image: UIImage(named: "yourImage"))

imageView.frame = CGRect(x: 50, y: 50, width: 100, height: 100)

button.addSubview(imageView)

  

// 添加一个透明覆盖按钮

let overlayButton = UIButton(frame: imageView.bounds)

overlayButton.backgroundColor = .clear

imageView.addSubview(overlayButton)

  

// 将透明按钮的事件转发给父视图按钮 （即图片父视图的 UIButton）

overlayButton.addTarget(button, action: #selector(button.sendActions(for: .touchUpInside)), for: .touchUpInside)

  

// 添加按钮到视图中

self.view.addSubview(button)

  

// 为 UIButton 添加点击事件处理

button.addTarget(self, action: #selector(buttonTapped), for: .touchUpInside)

  

@objc func buttonTapped() {

    print("UIButton clicked!")

}
```

**方法二：确保用户交互启用并不会遮挡点击事件**

确保 ﻿UIImageView 的 ﻿isUserInteractionEnabled 属性设置为 ﻿false，这样点击事件会直接传递给父视图 ﻿UIButton。

  

```swift
// 假设 button 是你的 UIButton 实例

let button = UIButton(type: .system)

button.frame = CGRect(x: 50, y: 50, width: 200, height: 200)

  

// 设置按钮其他属性，比如背景色

button.backgroundColor = .lightGray

  

// 创建并添加 UIImageView 到 UIButton

let imageView = UIImageView(image: UIImage(named: "yourImage"))

imageView.frame = CGRect(x: 50, y: 50, width: 100, height: 100)

imageView.isUserInteractionEnabled = false // 确保 UIImageView 不接收用户交互

button.addSubview(imageView)

  

// 添加按钮到视图中

self.view.addSubview(button)

  

// 为按钮添加点击事件处理

button.addTarget(self, action: #selector(buttonTapped), for: .touchUpInside)

  

@objc func buttonTapped() {

    print("UIButton clicked!")

}
```

**方法三：通过覆盖按钮的** ﻿hitTest(_:with:) **方法**

这种方法允许你更灵活地处理点击事件，确保即使点击了子视图（比如 ﻿UIImageView），事件仍然会传递给父视图（﻿UIButton）。

  

```swift
class CustomButton: UIButton {

    override func hitTest(_ point: CGPoint, with event: UIEvent?) -> UIView? {

        if let imageView = self.subviews.first(where: { $0 is UIImageView }),

           imageView.frame.contains(point) {

            return self

        }

        return super.hitTest(point, with: event)

    }

}

  

// 创建你的 CustomButton 实例

let button = CustomButton(type: .system)

button.frame = CGRect(x: 50, y: 50, width: 200, height: 200)

button.backgroundColor = .lightGray

  

// 创建并添加 UIImageView 到 CustomButton

let imageView = UIImageView(image: UIImage(named: "yourImage"))

imageView.frame = CGRect(x: 50, y: 50, width: 100, height: 100)

button.addSubview(imageView)

  

// 添加按钮到视图中

self.view.addSubview(button)

  

// 为按钮添加点击事件处理

button.addTarget(self, action: #selector(buttonTapped), for: .touchUpInside)

  

@objc func buttonTapped() {

    print("UIButton clicked!")

}
```

任选一种方法，根据你的具体场景来实现 ﻿UIImageView 点击触发 ﻿UIButton 的点击事件。

---

# UserDefaults

在 Swift 中，可以使用 ﻿`UserDefaults` 来存储和读取用户数据。以下是一些如何处理不同数据类型的示例：

**存储数据到** ﻿`UserDefaults`

1. **存储字符串**:

  

```swift
let defaults = UserDefaults.standard

defaults.set("Hello, World!", forKey: "myStringKey")
```

2. **存储整数**:

  

let defaults = UserDefaults.standard

defaults.set(42, forKey: "myIntegerKey")

3. **存储布尔值**:

  

```swift
let defaults = UserDefaults.standard

defaults.set(true, forKey: "myBoolKey")
```

4. **存储浮点数**:

  
```swift

let defaults = UserDefaults.standard

defaults.set(3.14159, forKey: "myFloatKey")
```

5. **存储数组**:

  

```swift
let defaults = UserDefaults.standard

let myArray = ["item1", "item2", "item3"]

defaults.set(myArray, forKey: "myArrayKey")
```

6. **存储字典**:

  

```swift
let defaults = UserDefaults.standard

let myDict: [String: Any] = ["name": "John", "age": 30]

defaults.set(myDict, forKey: "myDictKey")
```

7. **存储自定义对象**:

自定义对象需要实现 ﻿Codable 协议，并且需要先将对象编码为 ﻿Data 类型。

  

```swift
struct User: Codable {

    var name: String

    var age: Int

}
```

  

```swift
let user = User(name: "John", age: 30)

let defaults = UserDefaults.standard

  

if let encodedUser = try? JSONEncoder().encode(user) {

    defaults.set(encodedUser, forKey: "myUserKey")

}
```

  

**从** ﻿UserDefaults **读取数据**

1. **读取字符串**:

  

```swift
let defaults = UserDefaults.standard

let myString = defaults.string(forKey: "myStringKey")
```

2. **读取整数**:

  

```swift
let defaults = UserDefaults.standard

let myInteger = defaults.integer(forKey: "myIntegerKey")
```

3. **读取布尔值**:

  

```swift
let defaults = UserDefaults.standard

let myBool = defaults.bool(forKey: "myBoolKey")
```

4. **读取浮点数**:

  

```swift
let defaults = UserDefaults.standard

let myFloat = defaults.double(forKey: "myFloatKey")
```

5. **读取数组**:

  

```swift
let defaults = UserDefaults.standard

let myArray = defaults.array(forKey: "myArrayKey") as? [String]
```

6. **读取字典**:

  

```swift
let defaults = UserDefaults.standard

let myDict = defaults.dictionary(forKey: "myDictKey")
```

7. **读取自定义对象**:

  

```swift
struct User: Codable {

    var name: String

    var age: Int

}
```

  

```swift
let defaults = UserDefaults.standard

if let savedUserData = defaults.data(forKey: "myUserKey") {

    let decoder = JSONDecoder()

    if let loadedUser = try? decoder.decode(User.self, from: savedUserData) {

        print("User name: \(loadedUser.name), age: \(loadedUser.age)")

    }

}
```

  

**使用示例**

一个完整的示例，展示如何存储和读取自定义对象：

  

```swift
struct User: Codable {

    var name: String

    var age: Int

}
```

  

```swift
let user = User(name: "John", age: 30)

let defaults = UserDefaults.standard

  

// 存储用户对象

if let encodedUser = try? JSONEncoder().encode(user) {

    defaults.set(encodedUser, forKey: "myUserKey")

}

  

// 读取用户对象

if let savedUserData = defaults.data(forKey: "myUserKey") {

    let decoder = JSONDecoder()

    if let loadedUser = try? decoder.decode(User.self, from: savedUserData) {

        print("User name: \(loadedUser.name), age: \(loadedUser.age)")

    }

}
```

﻿UserDefaults 是一种简单有效的方式来存储小型数据，如设置、首选项和一些较小的用户数据。对于更复杂的数据存储需求，可能需要考虑其他方式，例如 Core Data 或文件存储。


---

# 循环引用

## objc

在 Objective-C 和 Swift 中，强引用（strong reference）和弱引用（weak reference）是内存管理中的两个重要概念，主要用于管理对象的生命周期和防止内存泄漏。

### 强引用（Strong Reference）

**强引用**是默认的引用类型。当一个对象被另一个对象强引用时，这个被引用的对象的引用计数（retain count）会增加。只要引用计数大于零，对象就不会被释放。

#### 特点：
- 持有对象的强引用会阻止该对象被释放。
- 对象的引用计数增加。
- 默认情况下，所有的对象引用都是强引用。

#### 示例：
```objective-c
@property (nonatomic, strong) MyClass *strongReference;
```

```swift
var strongReference: MyClass? = MyClass()
```

在上述示例中，`strongReference` 是一个强引用，只要 `strongReference` 持有对 `MyClass` 实例的引用，该实例就不会被释放。

### 弱引用（Weak Reference）

**弱引用**不会增加对象的引用计数。使用弱引用时，即使有其他对象持有该对象的强引用，当这些强引用被移除后，该对象会被释放。弱引用通常用于避免强引用循环（retain cycle），这是内存泄漏的一个常见原因。

#### 特点：
- 不会增加对象的引用计数。
- 当对象被释放时，弱引用会自动设置为 `nil`。
- 常用于委托（delegate）模式和闭包（closure）中，避免强引用循环。

#### 示例：
```objective-c
@property (nonatomic, weak) MyClass *weakReference;
```

```swift
weak var weakReference: MyClass? = MyClass()
```

在上述示例中，`weakReference` 是一个弱引用，不会增加 `MyClass` 实例的引用计数。当没有其他强引用持有 `MyClass` 实例时，该实例会被释放，并且 `weakReference` 会自动设置为 `nil`。

### 强引用循环（Retain Cycle）

强引用循环是指两个或多个对象互相持有对方的强引用，导致它们的引用计数都无法降为零，从而无法释放，造成内存泄漏。

#### 示例：
```objective-c
@interface MyClassA : NSObject
@property (nonatomic, strong) MyClassB *objectB;
@end

@interface MyClassB : NSObject
@property (nonatomic, strong) MyClassA *objectA;
@end
```

在上述示例中，`MyClassA` 和 `MyClassB` 互相持有对方的强引用，形成强引用循环，导致它们都无法被释放。

### 解决强引用循环

使用弱引用可以解决强引用循环的问题：

```objective-c
@interface MyClassA : NSObject
@property (nonatomic, strong) MyClassB *objectB;
@end

@interface MyClassB : NSObject
@property (nonatomic, weak) MyClassA *objectA;
@end
```

在上述示例中，将 `MyClassB` 对 `MyClassA` 的引用改为弱引用，避免了强引用循环。

### 总结

- **强引用**：增加对象的引用计数，防止对象被释放。
- **弱引用**：不增加对象的引用计数，当对象被释放时，弱引用会自动设置为 `nil`。
- 使用弱引用可以避免强引用循环，从而防止内存泄漏。



## swift

在 Swift 中，循环引用（也称为强引用循环）通常发生在两个或多个对象相互持有对方的强引用，导致它们无法被释放，从而造成内存泄漏。为了打破这种循环引用，Swift 提供了两种解决方案：弱引用（weak references）和无主引用（unowned references）。

### 1. 弱引用（weak）

弱引用不会增加引用计数，因此它不会阻止对象的释放。弱引用必须声明为可选类型，因为对象可能会在任何时候被释放，导致引用变为 `nil`。

```swift
class Person {
    let name: String
    var apartment: Apartment?
    
    init(name: String) {
        self.name = name
    }
    
    deinit {
        print("\(name) is being deinitialized")
    }
}

class Apartment {
    let unit: String
    weak var tenant: Person?
    
    init(unit: String) {
        self.unit = unit
    }
    
    deinit {
        print("Apartment \(unit) is being deinitialized")
    }
}

var john: Person? = Person(name: "John")
var unit4A: Apartment? = Apartment(unit: "4A")

john?.apartment = unit4A
unit4A?.tenant = john

john = nil
unit4A = nil

// 当 john 和 unit4A 都被设为 nil 时，它们会被正确地释放，因为 weak 引用不会造成强引用循环。
```

### 2. 无主引用（unowned）

无主引用也不会增加引用计数，但与弱引用不同，无主引用是非可选的，并且在对象被释放后，继续访问无主引用会导致运行时错误。因此，无主引用适用于引用在对象的生命周期中总是有值的情况。

```swift
class Customer {
    let name: String
    var card: CreditCard?
    
    init(name: String) {
        self.name = name
    }
    
    deinit {
        print("\(name) is being deinitialized")
    }
}

class CreditCard {
    let number: UInt64
    unowned let customer: Customer
    
    init(number: UInt64, customer: Customer) {
        self.number = number
        self.customer = customer
    }
    
    deinit {
        print("Card #\(number) is being deinitialized")
    }
}

var john: Customer? = Customer(name: "John")
john?.card = CreditCard(number: 1234_5678_9012_3456, customer: john!)

john = nil

// 当 john 被设为 nil 时，CreditCard 实例也会被正确地释放，因为 unowned 引用不会造成强引用循环。
```

### 选择 weak 还是 unowned

- **weak**：当引用可能变为 `nil` 时使用。适用于引用周期中可能会变为 `nil` 的情况。
- **unowned**：当引用在对象的生命周期中总是有值时使用。适用于引用周期中不应该变为 `nil` 的情况。

通过合理使用弱引用和无主引用，您可以有效地避免循环引用，确保对象在不再需要时能够正确释放，从而避免内存泄漏。

---

# 布局

## frame

frame会直接给定视图的所有信息，包括位置和宽高，相对布局的frame是动态调整的，不会马上到获取到，需要layOutIfNeeded为true，绝对布局（frame）包括bounds等元素，尽量不要混合使用，因为绝对布局会获取不到frame

## snapKit等



---

#  UTC 时间标准

UTC（协调世界时，Coordinated Universal Time）是一种时间标准，用于全球时间同步和协调。它是国际上最广泛使用的时间标准，通常被用作时间和日期的基准。以下是关于UTC的一些关键点：

1. **定义和来源**：
   - UTC是基于原子时间（TAI，International Atomic Time）和地球自转时间（UT1，Universal Time 1）的混合时间标准。
   - 它通过原子钟的高精度时间测量来保持时间的稳定性，同时通过闰秒调整来保持与地球自转时间的同步。

2. **闰秒调整**：
   - 由于地球自转速度并不恒定，UTC会定期加入或减少一秒（称为闰秒）以保持与地球自转时间的同步。这些调整由国际地球自转服务（IERS）决定和实施。

3. **用途**：
   - UTC用于全球时间同步，如互联网、卫星导航系统（如GPS）、航空和航海等领域。
   - 在日常生活中，许多国家和地区的标准时间都是基于UTC的某个偏移量（如UTC+8:00为中国标准时间）。

4. **表示方式**：
   - UTC时间通常以24小时制表示，后面可能会附加“Z”表示零时区（如：12:00Z表示UTC时间的正午12点）。
   - 时间偏移量表示某地时间相对于UTC的偏移（如：UTC+1:00表示比UTC时间快1小时）。

5. **与其他时间标准的关系**：
   - UTC与格林尼治标准时间（GMT，Greenwich Mean Time）在定义上略有不同，但在实际使用中常常被视为等同。
   - UTC取代了GMT成为现代的时间标准，因为它基于原子时间，提供了更高的精度和稳定性。

总之，UTC是一个全球统一的时间标准，用于确保全球各地时间的一致性和协调性。

---

# 内存泄漏

在 iOS 开发中，内存泄漏（Memory Leak）通常是由对象未能正确释放导致的。这些对象在不再需要时仍然占用内存，从而导致应用程序的内存使用不断增加，最终可能导致应用程序崩溃或性能下降。以下是一些常见的导致内存泄漏的原因：

### 1. 强引用循环（Retain Cycles）
这是最常见的内存泄漏原因之一。当两个对象相互持有对方的强引用时，导致它们都无法被释放。

#### 示例：
```swift
class A {
    var b: B?
}

class B {
    var a: A?
}

let a = A()
let b = B()
a.b = b
b.a = a
```

在这个例子中，`A` 和 `B` 相互持有对方的强引用，导致它们都无法被释放。

#### 解决办法：
使用 `weak` 或 `unowned` 关键字来打破强引用循环。

```swift
class A {
    var b: B?
}

class B {
    weak var a: A?
}

let a = A()
let b = B()
a.b = b
b.a = a
```

### 2. 闭包中的强引用
当闭包捕获了 `self` 并且闭包被 `self` 强引用时，会导致强引用循环。

#### 示例：
```swift
class MyClass {
    var closure: (() -> Void)?
    
    func setupClosure() {
        closure = {
            print(self)
        }
    }
}
```

#### 解决办法：
使用捕获列表 `[weak self]` 或 `[unowned self]` 来打破循环引用。

```swift
class MyClass {
    var closure: (() -> Void)?
    
    func setupClosure() {
        closure = { [weak self] in
            guard let self = self else { return }
            print(self)
        }
    }
}
```

### 3. NSTimer
`NSTimer` 对其目标对象持有强引用，可能会导致目标对象无法被释放。

#### 示例：
```swift
class MyClass {
    var timer: Timer?
    
    func startTimer() {
        timer = Timer.scheduledTimer(withTimeInterval: 1.0, repeats: true) { _ in
            print(self)
        }
    }
}
```

#### 解决办法：
使用 `weak` 引用或在 `deinit` 中无效化定时器。

```swift
class MyClass {
    var timer: Timer?
    
    func startTimer() {
        timer = Timer.scheduledTimer(withTimeInterval: 1.0, repeats: true) { [weak self] _ in
            guard let self = self else { return }
            print(self)
        }
    }
    
    deinit {
        timer?.invalidate()
    }
}
```

### 4. 代理模式中的强引用
如果代理对象对其委托者持有强引用，可能会导致内存泄漏。

#### 示例：
```swift
protocol MyDelegate: AnyObject {
    func doSomething()
}

class MyClass {
    var delegate: MyDelegate?
}

class ViewController: UIViewController, MyDelegate {
    var myClass = MyClass()
    
    override func viewDidLoad() {
        super.viewDidLoad()
        myClass.delegate = self
    }
    
    func doSomething() {}
}
```

#### 解决办法：
将代理声明为 `weak`。

```swift
class MyClass {
    weak var delegate: MyDelegate?
}
```

### 5. Core Foundation 对象
使用 Core Foundation 框架时，忘记释放对象可能会导致内存泄漏。

#### 示例：
```swift
let cfObject = CFStringCreateWithCString(nil, "Hello, World!", CFStringBuiltInEncodings.UTF8.rawValue)
```

#### 解决办法：
使用 `CFRelease` 释放对象，或在 Swift 中使用 `Unmanaged` 来管理 Core Foundation 对象。

```swift
let cfObject = CFStringCreateWithCString(nil, "Hello, World!", CFStringBuiltInEncodings.UTF8.rawValue)
CFRelease(cfObject)
```

### 6. 其他常见原因
- **通知中心**：添加观察者后未能移除。
- **KVO**：注册观察者后未能移除。
- **URLSession**：未能正确处理回调或取消任务。

### 总结
内存泄漏主要是由于对象之间的强引用循环导致的。通过使用 `weak` 或 `unowned` 关键字、注意闭包的捕获列表、正确管理定时器和代理对象等方法，可以有效地防止内存泄漏。定期使用 Xcode 的 Instruments 工具中的 Leaks 和 Allocations 仪器来检测和分析内存泄漏问题也是一个好习惯。

---

# APP启动与生命周期

App 冷启动（Cold Start）是指应用程序从完全退出状态重新启动的过程。在冷启动时，应用程序没有在内存中运行，需要从头开始加载所有资源和初始化所有必要的组件。与之相对的是“热启动”（Warm Start），即应用程序已经在后台运行，此时重新启动不需要重新加载所有资源和初始化组件，启动速度会更快。

### 冷启动的具体步骤

1. **应用程序进程启动**：
   - 操作系统创建一个新的进程来运行应用程序。

2. **加载应用程序代码**：
   - 操作系统将应用程序的代码和资源从存储加载到内存中。

3. **初始化应用程序**：
   - 应用程序的入口点（通常是 `main` 函数或 `@UIApplicationMain` 注解标记的类）开始执行。
   - 初始化应用程序的全局状态和配置。

4. **创建 UI**：
   - 创建应用程序的主窗口和根视图控制器。
   - 加载和渲染初始的用户界面。

5. **准备运行**：
   - 完成最后的初始化步骤，应用程序准备好响应用户输入。

### 冷启动的优化

由于冷启动涉及到加载大量的资源和初始化步骤，通常需要更多的时间。因此，优化冷启动时间对于提升用户体验非常重要。以下是一些常见的优化策略：

1. **减少启动时的工作量**：
   - 将不必要的初始化和资源加载延迟到应用程序启动后进行。

2. **减少应用程序包大小**：
   - 优化资源文件（如图片、视频等）的大小和数量，减少应用程序包的体积，从而加快加载速度。

3. **优化代码执行**：
   - 避免在启动时进行复杂的计算和操作，优化代码路径。

4. **使用并行加载**：
   - 利用多线程技术并行加载资源和初始化组件，减少单线程的阻塞时间。

5. **缓存数据**：
   - 使用缓存技术保存经常使用的数据，减少冷启动时的数据加载时间。

### 冷启动与热启动的区别

- **冷启动**：
  - 应用程序完全退出，需要从头开始加载和初始化。
  - 启动时间较长。

- **热启动**：
  - 应用程序在后台运行，重新启动时不需要重新加载所有资源和初始化组件。
  - 启动时间较短。

通过理解和优化冷启动过程，可以显著提升应用程序的启动速度和用户体验。


## TabView

TabView在APP启动后，TabView中的几个视图APP会一直持有，不会delloc

---
# 支付跳转
## 跳转微信支付宝

要在 iOS 应用中处理从 H5 页面接收到的购买链接，并跳转到微信或支付宝进行支付，你可以按照以下步骤实现：

### 1. 接收并处理购买链接

首先，确保你已经正确设置了 `WKWebView` 和 `WKScriptMessageHandler`，并能够接收 H5 页面发送的消息。假设你已经有一个方法来接收消息并提取购买链接。

### 2. 检查并跳转到微信或支付宝

根据接收到的购买链接，判断应该跳转到微信还是支付宝，并使用 `UIApplication` 的 `open(_:options:completionHandler:)` 方法进行跳转。

以下是一个示例代码：

```swift
import UIKit
import WebKit

class ViewController: UIViewController, WKScriptMessageHandler {
    
    var webView: WKWebView!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        // 配置 WKWebView
        let contentController = WKUserContentController()
        contentController.add(self, name: "jumpHandler")
        
        let config = WKWebViewConfiguration()
        config.userContentController = contentController
        
        webView = WKWebView(frame: self.view.bounds, configuration: config)
        self.view.addSubview(webView)
        
        // 加载 H5 页面
        if let url = URL(string: "https://your-h5-page-url.com") {
            webView.load(URLRequest(url: url))
        }
    }
    
    // 实现 WKScriptMessageHandler 协议的方法
    func userContentController(_ userContentController: WKUserContentController, didReceive message: WKScriptMessage) {
        if message.name == "jumpHandler", let messageBody = message.body as? [String: Any] {
            handleJumpMessage(messageBody)
        }
    }
    
    // 处理 jump 消息
    func handleJumpMessage(_ messageBody: [String: Any]) {
        if let urlString = messageBody["url"] as? String, let url = URL(string: urlString) {
            openURL(url)
        }
    }
    
    // 打开指定的 URL
    func openURL(_ url: URL) {
        let urlScheme = url.scheme?.lowercased()
        
        switch urlScheme {
        case "weixin":
            // 跳转到微信
            if UIApplication.shared.canOpenURL(url) {
                UIApplication.shared.open(url, options: [:], completionHandler: nil)
            } else {
                showAlert("无法打开微信")
            }
        case "alipay":
            // 跳转到支付宝
            if UIApplication.shared.canOpenURL(url) {
                UIApplication.shared.open(url, options: [:], completionHandler: nil)
            } else {
                showAlert("无法打开支付宝")
            }
        default:
            // 处理其他情况
            showAlert("不支持的 URL Scheme")
        }
    }
    
    // 显示提示框
    func showAlert(_ message: String) {
        let alert = UIAlertController(title: nil, message: message, preferredStyle: .alert)
        alert.addAction(UIAlertAction(title: "确定", style: .default, handler: nil))
        present(alert, animated: true, completion: nil)
    }
}
```

### 解释

1. **接收并处理购买链接**：
   - 在 `userContentController(_:didReceive:)` 方法中，检查消息的名称是否为 `jumpHandler`，并提取消息体中的 URL。
   - 调用 `handleJumpMessage(_:)` 方法来处理接收到的 URL。

2. **打开指定的 URL**：
   - 在 `openURL(_:)` 方法中，根据 URL 的 Scheme 判断应该跳转到微信还是支付宝。
   - 使用 `UIApplication.shared.canOpenURL(url)` 检查设备上是否安装了对应的应用。
   - 使用 `UIApplication.shared.open(url, options: [:], completionHandler: nil)` 方法打开对应的应用。
   - 如果无法打开应用，显示一个提示框。

3. **显示提示框**：
   - 使用 `UIAlertController` 显示提示信息，告知用户无法打开对应的应用。

### 配置 URL Schemes

为了确保你的应用能够检测并打开微信和支付宝，你需要在你的 Xcode 项目中配置 URL Schemes。

1. 打开你的 Xcode 项目。
2. 选择你的项目目标（Target）。
3. 选择 `Info` 标签。
4. 展开 `URL Types` 部分。
5. 点击 `+` 按钮添加新的 URL Scheme。
6. 添加微信和支付宝的 URL Scheme，例如 `weixin` 和 `alipay`。

通过这种方式，你可以在接收到 H5 页面发送的购买链接后，跳转到微信或支付宝进行支付。

---

# iOS的根视图

在 iOS 开发中，获取根视图控制器（Root View Controller）通常是指获取应用程序窗口的根视图控制器。根视图控制器是应用程序启动时设置的第一个视图控制器，它是视图控制器层次结构的起点。

### 获取根视图控制器

你可以通过 `UIApplication` 的 `delegate` 属性来访问应用程序的 `UIWindow`，然后获取其 `rootViewController` 属性。以下是一个示例：

#### Swift

```swift
if let window = UIApplication.shared.delegate?.window {
    if let rootViewController = window?.rootViewController {
        // 现在你可以使用 rootViewController
    }
}
```

#### Objective-C

```objc
UIWindow *window = [UIApplication sharedApplication].delegate.window;
UIViewController *rootViewController = window.rootViewController;
// 现在你可以使用 rootViewController
```

### 处理 SwiftUI

如果你使用的是 SwiftUI，获取根视图控制器的方式有些不同，因为 SwiftUI 的应用结构和 UIKit 不完全相同。以下是一个在 SwiftUI 中获取根视图控制器的示例：

#### Swift

```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        Button("Get Root View Controller") {
            if let rootViewController = UIApplication.shared.windows.first?.rootViewController {
                // 现在你可以使用 rootViewController
                print("Root view controller: \(rootViewController)")
            }
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

### 获取当前显示的视图控制器

有时候，你可能需要获取当前显示的视图控制器，而不仅仅是根视图控制器。以下是一个递归函数示例，用于获取当前显示的视图控制器：

#### Swift

```swift
func getCurrentViewController() -> UIViewController? {
    if let rootViewController = UIApplication.shared.windows.first?.rootViewController {
        return getVisibleViewController(rootViewController)
    }
    return nil
}

func getVisibleViewController(_ viewController: UIViewController) -> UIViewController? {
    if let presentedViewController = viewController.presentedViewController {
        return getVisibleViewController(presentedViewController)
    }
    
    if let navigationController = viewController as? UINavigationController {
        return getVisibleViewController(navigationController.visibleViewController ?? navigationController)
    }
    
    if let tabBarController = viewController as? UITabBarController {
        if let selectedViewController = tabBarController.selectedViewController {
            return getVisibleViewController(selectedViewController)
        }
    }
    
    return viewController
}
```

#### Objective-C

```objc
- (UIViewController *)getCurrentViewController {
    UIWindow *window = [UIApplication sharedApplication].delegate.window;
    UIViewController *rootViewController = window.rootViewController;
    return [self getVisibleViewControllerFrom:rootViewController];
}

- (UIViewController *)getVisibleViewControllerFrom:(UIViewController *)viewController {
    if (viewController.presentedViewController) {
        return [self getVisibleViewControllerFrom:viewController.presentedViewController];
    }
    
    if ([viewController isKindOfClass:[UINavigationController class]]) {
        UINavigationController *nav = (UINavigationController *)viewController;
        return [self getVisibleViewControllerFrom:nav.visibleV...
```


---
# APP的生命周期
## SceneDelegate

注意： 需要iOS13.0以上

在iOS 13及更高版本中引入了`SceneDelegate`，它是一个新的应用程序生命周期管理类，用于管理应用程序中的不同场景（Scenes）。在之前的iOS版本中，应用程序通常只有一个主窗口（Window），而在iOS 13及更高版本中引入了多窗口支持，每个窗口可以包含一个或多个场景。  
  
`SceneDelegate`主要负责以下几个方面：  
  
1. **管理场景生命周期**：`SceneDelegate`负责管理应用程序中的不同场景（Scenes）的生命周期，包括创建、连接、断开和销毁场景。  
  
2. **设置场景的界面**：`SceneDelegate`可以设置每个场景的界面和根视图控制器。  
  
3. **响应场景间的切换**：当应用程序需要切换到另一个场景时，`SceneDelegate`会负责处理场景之间的切换逻辑。  
  
通过引入`SceneDelegate`，开发人员可以更好地管理应用程序中的多个场景，例如在iPad上支持多任务处理（Multitasking）时，每个应用程序场景可以在不同的分屏中独立运行。这为开发人员提供了更大的灵活性和控制权，使他们能够更好地适应不同设备和使用场景。

#### 纯代码实现
> [!NOTE] Title
> 如果你想在使用纯代码实现启动页的同时使用`SceneDelegate`，你可以在`SceneDelegate.swift`文件中创建并管理启动页的场景。以下是一个示例代码，演示如何在应用程序启动时通过`SceneDelegate`显示一个简单的启动页：

```swift
import UIKit

class SceneDelegate: UIResponder, UIWindowSceneDelegate {

    var window: UIWindow?

    func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
        guard let windowScene = (scene as? UIWindowScene) else { return }

        // 创建启动页界面
        let launchScreenView = UIView(frame: windowScene.coordinateSpace.bounds)
        launchScreenView.backgroundColor = UIColor.white

        let label = UILabel(frame: CGRect(x: 0, y: 0, width: 200, height: 50))
        label.center = launchScreenView.center
        label.text = "My App Launching..."
        label.textAlignment = .center
        launchScreenView.addSubview(label)

        // 显示启动页界面
        window = UIWindow(windowScene: windowScene)
        window?.rootViewController = UIViewController()
        window?.rootViewController?.view = launchScreenView
        window?.makeKeyAndVisible()

        // 模拟应用程序加载过程
        DispatchQueue.main.asyncAfter(deadline: .now() + 2) {
            // 应用程序加载完成后，显示主界面
            self.showMainAppScreen()
        }
    }

    func showMainAppScreen() {
        // 创建并显示应用程序的主界面
        let mainViewController = UIViewController()
        mainViewController.view.backgroundColor = UIColor.lightGray
        window?.rootViewController = mainViewController
    }
}
```

在上面的示例中，`SceneDelegate`的`scene(_:willConnectTo:options:)`方法创建了一个简单的启动页界面，并在应用程序加载完成后切换到应用程序的主界面。你可以根据需要自定义启动页的界面和显示逻辑。

通过在`SceneDelegate`中管理启动页的场景，你可以在应用程序启动时显示自定义的启动页，并在加载完成后切换到应用程序的主界面。

---

# APP启动页

在iOS开发中，你可以通过设置启动画面（Launch Screen）来实现应用程序显示启动页。启动画面是在应用程序启动过程中显示的界面，用于提供应用程序的初始视图，直到应用程序完全加载并准备好显示主界面。  
  
以下是实现显示启动页的步骤：  
  
1. **创建启动画面文件**：  
- 在Xcode中，选择你的项目文件。  
- 在Targets列表中选择你的应用程序目标。  
- 在General选项卡中，找到"App Icons and Launch Images"部分。  
- 在"Launch Screen File"下拉菜单中选择一个启动画面文件，或者创建一个新的启动画面文件。  
  
2. **设计启动画面**：  
- 打开创建的启动画面文件（通常是一个`.storyboard`文件）。  
- 在启动画面文件中，设计你想要显示的启动页界面。你可以添加图片、标签、视图等元素来自定义启动页的外观。  
  
3. **设置启动画面文件**：  
- 在Xcode中，选择你的项目文件。  
- 在Targets列表中选择你的应用程序目标。  
- 在General选项卡中，确保你选择的启动画面文件在"Launch Screen File"下拉菜单中被正确设置。  
  
4. **运行应用程序**：  
- 编译并运行你的应用程序。  
- 当你启动应用程序时，系统会显示你设计的启动画面，直到应用程序准备好显示主界面。  
  
通过设置启动画面，你可以为你的应用程序提供一个专业和个性化的启动体验，同时在应用程序启动过程中展示重要的信息或品牌元素。

 [[iOS#纯代码实现]]

---

# 获取根视图

在 iOS 中，`UIApplication.shared.keyWindow` 在某些情况下可能会返回 `nil`，主要原因如下：

1. **多窗口支持**：
   - 从 iOS 13 开始，iOS 支持多窗口应用（尤其是在 iPad 上）。在这种情况下，应用可能有多个窗口（`UIWindow`），而 `keyWindow` 并不总是指向当前活动的窗口。

2. **窗口层级变化**：
   - 当应用有多个窗口时，窗口层级（window hierarchy）可能会发生变化，导致 `keyWindow` 不是当前需要的窗口。

3. **应用状态**：
   - 在应用启动初期，`keyWindow` 可能还没有被设置。这种情况通常发生在应用还没有完全初始化或在应用刚刚启动时。

4. **场景支持**：
   - 从 iOS 13 开始，Apple 引入了 `UISceneDelegate`，每个场景（scene）都有自己的窗口。使用 `UIScene`，应用可能有多个场景，每个场景有自己的 `UIWindow`，这使得 `keyWindow` 的概念更加复杂。

为了更可靠地获取当前活动的根视图控制器，可以使用以下方法，遍历所有连接的场景并获取它们的根视图控制器：

```swift
import UIKit

extension UIApplication {
    func getRootViewController() -> UIViewController {
        // 尝试从当前活动场景中获取根视图控制器
        if #available(iOS 13.0, *) {
            if let scene = self.connectedScenes.first(where: { $0.activationState == .foregroundActive }) as? UIWindowScene {
                return scene.windows.first(where: { $0.isKeyWindow })?.rootViewController ?? UIViewController()
            }
        }
        
        // 如果无法从当前活动场景中获取，尝试从 keyWindow 中获取根视图控制器
        if let rootViewController = self.keyWindow?.rootViewController {
            return rootViewController
        }
        
        // 如果以上方法都未获取到根视图控制器，则尝试从 AppDelegate 的 window 中获取
        if let rootViewController = self.delegate?.window??.rootViewController {
            return rootViewController
        }
        
        // 如果以上方法都未获取到根视图控制器，则返回一个默认的视图控制器
        return UIViewController()
    }
}

// 使用示例
let rootViewController = UIApplication.shared.getRootViewController()
// 现在你可以使用 rootViewController
```

### 解释

1. **iOS 13 及以上版本**：
   - 如果应用运行在 iOS 13 及以上版本，首先尝试从当前活动的 `UIWindowScene` 中获取根视图控制器。
   - 使用 `connectedScenes` 属性获取所有连接的场景，并找到当前处于前台活动状态的场景。
   - 从该场景的窗口中找到 `isKeyWindow` 为 `true` 的窗口，并返回其根视图控制器。

2. **iOS 13 以下版本**：
   - 如果应用运行在 iOS 13 以下版本，或者上述方法未能获取到根视图控制器，则尝试从 `keyWindow` 中获取根视图控制器。

3. **AppDelegate 的 window**：
   - 如果 `keyWindow` 也未能获取到根视图控制器，则尝试从 `AppDelegate` 的 `window` 中获取根视图控制器。

4. **默认视图控制器**：
   - 如果以上方法都未能获取到根视图控制器，则返回一个默认的 `UIViewController` 实例，以确保返回值非 `nil`。
   
> [!Notice]
>  iOS开发中，无法保证 `window.rpptViewController` 一定时存在的，当要实现某个视图添加到根视图控制器获取从根视图出现时建议使用 `currentVC.present(VC, animate: false)` 或 `YourView.sheet()` 



---

# 一些系统组件

## ImagePicker
### 1. ImagePicker(可多选)

 **swiftUI实现：**

在 SwiftUI 中，你可以使用 `PHPickerViewController` 来实现多张照片的选择。以下是一个示例：

首先，创建一个遵循 `UIViewControllerRepresentable` 协议的 `ImagePicker` 视图：

```swift
import SwiftUI
import PhotosUI

struct ImagePicker: UIViewControllerRepresentable {
    @Binding var images: [UIImage]
    @Environment(\.presentationMode) var presentationMode

    func makeUIViewController(context: Context) -> PHPickerViewController {
        var configuration = PHPickerConfiguration()
        configuration.selectionLimit = 0 // 0 表示无限制
        configuration.filter = .images
        let picker = PHPickerViewController(configuration: configuration)
        picker.delegate = context.coordinator
        return picker
    }

    func updateUIViewController(_ uiViewController: PHPickerViewController, context: Context) {}

    func makeCoordinator() -> Coordinator {
        Coordinator(self)
    }

    class Coordinator: NSObject, PHPickerViewControllerDelegate {
        let parent: ImagePicker

        init(_ parent: ImagePicker) {
            self.parent = parent
        }

        func picker(_ picker: PHPickerViewController, didFinishPicking results: [PHPickerResult]) {
            parent.presentationMode.wrappedValue.dismiss()

            for result in results {
                result.itemProvider.loadObject(ofClass: UIImage.self) { (object, error) in
                    if let image = object as? UIImage {
                        DispatchQueue.main.async {
                            self.parent.images.append(image)
                        }
                    }
                }
            }
        }
    }
}
```

然后，你可以在你的 SwiftUI 视图中使用 `ImagePicker`：

```swift
struct ContentView: View {
    @State private var images: [UIImage] = []
    @State private var isImagePickerPresented = false

    var body: some View {
        VStack {
            ForEach(images, id: \.self) { image in
                Image(uiImage: image)
                    .resizable()
                    .scaledToFit()
            }
            Button("选择照片") {
                isImagePickerPresented = true
            }
        }
        .sheet(isPresented: $isImagePickerPresented) {
            ImagePicker(images: $images)
        }
    }
}
```

在这个示例中，我们创建了一个 `ImagePicker` 视图，并将其绑定到一个 `@State` 变量 `images`。当用户点击 "选择照片" 按钮时，`ImagePicker` 视图将被显示，用户可以选择多张照片。选择的照片将被添加到 `images` 数组中，并在 `ContentView` 中显示。

### 2. ImagePicker（单选）

**UIKit实现**

在UIKit中，你可以通过以下步骤来实现点击按钮弹出UIImagePickerController：

1. 首先，你需要创建一个按钮并设置其点击事件。
2. 在点击事件中，创建一个UIImagePickerController实例。
3. 设置UIImagePickerController的代理和源类型。
4. 最后，使用present方法将UIImagePickerController显示出来。

以下是具体的代码实现：

```swift
import UIKit

class ViewController: UIViewController, UIImagePickerControllerDelegate, UINavigationControllerDelegate {

    override func viewDidLoad() {
        super.viewDidLoad()
        
        let button = UIButton(frame: CGRect(x: 100, y: 100, width: 100, height: 50))
        button.backgroundColor = .blue
        button.setTitle("Open Picker", for: .normal)
        button.addTarget(self, action: #selector(openImagePicker), for: .touchUpInside)
        
        self.view.addSubview(button)
    }

    @objc func openImagePicker() {
        if UIImagePickerController.isSourceTypeAvailable(.photoLibrary) {
            let picker = UIImagePickerController()
            picker.delegate = self
            picker.sourceType = .photoLibrary
            self.present(picker, animated: true, completion: nil)
        }
    }

    // UIImagePickerControllerDelegate
    func imagePickerController(_ picker: UIImagePickerController, didFinishPickingMediaWithInfo info: [UIImagePickerController.InfoKey : Any]) {
        picker.dismiss(animated: true, completion: nil)
        if let image = info[.originalImage] as? UIImage {
            // 使用选中的图片
        }
    }

    func imagePickerControllerDidCancel(_ picker: UIImagePickerController) {
        picker.dismiss(animated: true, completion: nil)
    }
}
```

这段代码首先创建了一个按钮，并设置了其点击事件为`openImagePicker`。在`openImagePicker`方法中，我们检查是否可以访问图片库，如果可以，则创建一个UIImagePickerController实例，设置其代理和源类型，然后将其显示出来。当用户选择了图片或取消选择时，我们会调用相应的代理方法。


---

# 线程进程

当然，以下是使用 Swift 代码来解释主线程和子线程的概念及其使用方法。

### 主线程和子线程概念

- **主线程**：负责处理所有的 UI 更新和用户交互。所有与 UI 相关的操作必须在主线程上执行。
- **子线程**：用于执行耗时的任务，如网络请求、文件读写和数据处理，以避免阻塞主线程，从而保持应用的响应性。

### 使用 GCD (Grand Central Dispatch)

#### 在主线程上执行任务

```swift
DispatchQueue.main.async {
    // 在主线程上执行的代码
    self.label.text = "Updated on main thread"
}
```

#### 在子线程上执行任务

```swift
DispatchQueue.global(qos: .default).async {
    // 在子线程上执行的代码
    let data = self.loadDataFromNetwork()
    
    // 回到主线程更新 UI
    DispatchQueue.main.async {
        self.label.text = "Data loaded"
    }
}
```

### 使用 Operation 和 OperationQueue

`Operation` 和 `OperationQueue` 提供了更高级的并发控制，支持依赖关系和优先级等特性。

#### 创建并添加操作到队列

```swift
let operationQueue = OperationQueue()

let operation = BlockOperation {
    // 在子线程上执行的代码
    let data = self.loadDataFromNetwork()
    
    // 回到主线程更新 UI
    OperationQueue.main.addOperation {
        self.label.text = "Data loaded"
    }
}

operationQueue.addOperation(operation)
```

### 示例：网络请求和 UI 更新

以下是一个示例，展示如何在子线程上执行网络请求，并在完成后更新 UI。

```swift
DispatchQueue.global(qos: .background).async {
    // 在子线程上执行网络请求
    guard let url = URL(string: "https://example.com/api") else { return }
    
    do {
        let data = try Data(contentsOf: url)
        let json = try JSONSerialization.jsonObject(with: data, options: []) as? [String: Any]
        
        // 回到主线程更新 UI
        DispatchQueue.main.async {
            if let json = json, let value = json["key"] as? String {
                self.label.text = value
            }
        }
    } catch {
        print("Error: \(error.localizedDescription)")
    }
}
```

### 线程安全

在多线程编程中，确保线程安全非常重要。可以使用同步机制如 `DispatchQueue` 提供的同步工具来保护共享资源。

#### 使用 DispatchQueue 的同步机制

```swift
let queue = DispatchQueue(label: "com.example.myQueue")

queue.sync {
    // 线程安全的代码
}
```

#### 使用 NSLock

```swift
let lock = NSLock()

lock.lock()
// 线程安全的代码
lock.unlock()
```

### 完整示例：网络请求和 UI 更新

以下是一个完整的示例，展示如何在子线程上执行网络请求，并在完成后更新 UI，同时确保线程安全。

```swift
import UIKit

class ViewController: UIViewController {

    @IBOutlet weak var label: UILabel!
    let lock = NSLock()

    override func viewDidLoad() {
        super.viewDidLoad()
        fetchData()
    }

    func fetchData() {
        DispatchQueue.global(qos: .background).async {
            // 在子线程上执行网络请求
            guard let url = URL(string: "https://example.com/api") else { return }
            
            do {
                let data = try Data(contentsOf: url)
                let json = try JSONSerialization.jsonObject(with: data, options: []) as? [String: Any]
                
                // 回到主线程更新 UI
                DispatchQueue.main.async {
                    self.lock.lock()
                    if let json = json, let value = json["key"] as? String {
                        self.label.text = value
                    }
                    self.lock.unlock()
                }
            } catch {
                print("Error: \(error.localizedDescription)")
            }
        }
    }
}
```

通过这些方法，你可以在 Swift 中有效地管理主线程和子线程，从而实现高效的并发编程。如果你有更多问题或需要进一步的帮助，欢迎继续提问。


---

 iOS 应用开发中，实现更新用户界面（UI）和加载用户头像的功能通常涉及到以下几个方面：

1. **获取用户数据**：从数据源（如服务器或本地存储）获取用户数据。
2. **处理用户数据**：根据业务逻辑处理用户数据，决定显示哪些信息。
3. **更新UI控件**：使用UIKit或SwiftUI更新UI控件，如UIImageView。

---
要使应用打包最小化，可以采用以下几种技术和策略：

### 1. 使用On-Demand Resources (ODR)
**On-Demand Resources (ODR)** 是苹果提供的一种技术，允许你将资源文件（如视频、图像等）按需加载，而不是在应用安装时全部下载。这种方式可以显著减小初始应用包的大小。

#### 配置ODR的步骤：
1. **在Xcode中配置ODR**：
   - 打开你的Xcode项目。
   - 在项目导航器中，选择你的项目文件。
   - 在项目设置的“General”标签页，找到“On-Demand Resources”部分。
   - 点击“+”按钮添加新的资源标签，并将资源文件拖放到标签中。

2. **在代码中按需加载资源**：
   ```swift
   import UIKit
   import AVKit
   import AVFoundation

   class VideoViewController: UIViewController {
       var playerViewController: AVPlayerViewController!
       
       override func viewDidLoad() {
           super.viewDidLoad()
           playerViewController = AVPlayerViewController()
           self.addChild(playerViewController)
           self.view.addSubview(playerViewController.view)
           playerViewController.view.frame = self.view.frame
           loadVideoResource()
       }
       
       func loadVideoResource() {
           let tag = "exampleVideoTag" // ODR标签
           let resourceRequest = NSBundleResourceRequest(tags: [tag])
           resourceRequest.beginAccessingResources { error in
               if let error = error {
                   print("Failed to load resource: \(error.localizedDescription)")
                   return
               }
               guard let url = Bundle.main.url(forResource: "exampleVideo", withExtension: "mp4") else {
                   print("Video resource not found")
                   return
               }
               let player = AVPlayer(url: url)
               self.playerViewController.player = player
               player.play()
           }
       }
   }
   ```

### 2. 使用App Thinning
**App Thinning** 是苹果提供的另一种技术，旨在根据设备类型生成不同的应用包，以减小每个设备上安装的应用包大小。App Thinning包括以下几个部分：

- **Slicing**：根据设备类型生成不同的应用包，确保每个包只包含该设备所需的资源。
- **Bitcode**：上传Bitcode到App Store，苹果会根据不同设备重新编译应用，提高应用效率。
- **On-Demand Resources (ODR)**：如上所述，按需加载资源。

### 3. 使用外部存储和动态加载
将视频资源存储在云端（如AWS S3、Google Cloud Storage），在应用运行时动态加载。这种方式可以确保视频资源不会占用应用包的空间。

#### 示例：
```swift
import UIKit
import AVKit
import AVFoundation

class VideoViewController: UIViewController {
    var playerViewController: AVPlayerViewController!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        playerViewController = AVPlayerViewController()
        self.addChild(playerViewController)
        self.view.addSubview(playerViewController.view)
        playerViewController.view.frame = self.view.frame
        loadVideoFromURL()
    }
    
    func loadVideoFromURL() {
        guard let url = URL(string: "https://example.com/path/to/video.mp4") else {
            print("Invalid URL")
            return
        }
        let player = AVPlayer(url: url)
        playerViewController.player = player
        player.play()
    }
}
```

### 4. 视频压缩与优化
使用高效的视频编码格式（如H.264或H.265）压缩视频文件，减小文件大小。选择高效的文件格式（如MP4）来存储视频，并根据实际需求适当降低视频的分辨率和比特率。

### 总结
在上述方法中，**On-Demand Resources (ODR)** 和 **外部存储与动态加载** 是最有效的减少应用包大小的技术。ODR适合需要在应用内按需加载资源的情况，而外部存储和动态加载适合资源文件较大且需要频繁更新的情况。结合App Thinning技术，可以进一步优化应用包大小。

---

# APP运行状态

`UIApplicationState` 枚举表示 iOS 应用程序的当前运行状态。它有三个可能的值：

1. **`UIApplicationStateActive`**：应用程序当前正在前台运行并接收事件。
2. **`UIApplicationStateInactive`**：应用程序在前台运行，但没有接收事件。通常发生在应用程序过渡到其他状态（如进入后台或从后台返回到前台）时。
3. **`UIApplicationStateBackground`**：应用程序当前在后台运行，且不在屏幕上显示。

### 详细解释

#### 1. `UIApplicationStateActive`

- **描述**：应用程序处于活动状态，正在前台运行并接收用户事件。
- **示例场景**：用户正在使用应用程序，点击按钮、滑动屏幕等操作都可以被处理。
- **典型用途**：大多数应用逻辑和用户交互都在这个状态下进行。

#### 2. `UIApplicationStateInactive`

- **描述**：应用程序在前台运行，但没有接收事件。这个状态通常是暂时的，发生在应用程序状态的过渡期间。
- **示例场景**：
  - 用户刚刚按下 Home 键，应用程序即将进入后台。
  - 用户刚刚从后台返回到前台，但还没有完全进入活动状态。
  - 用户接收到电话或短信通知时，应用程序短暂地变为非活跃状态。
- **典型用途**：处理过渡状态，保存当前状态或暂停某些操作。

#### 3. `UIApplicationStateBackground`

- **描述**：应用程序在后台运行，不在屏幕上显示。应用程序在这种状态下的执行能力有限。
- **示例场景**：
  - 用户按下 Home 键或切换到其他应用程序，当前应用程序进入后台。
  - 应用程序在后台执行下载任务。
- **典型用途**：完成有限的后台任务，如下载数据、处理推送通知等。

### 使用示例

你可以通过 `UIApplication` 的 `applicationState` 属性来检查应用程序的当前状态：

```swift
import UIKit

func checkAppState() {
    let state = UIApplication.shared.applicationState
    
    switch state {
    case .active:
        print("App is in the foreground and receiving events.")
    case .inactive:
        print("App is in the foreground but not receiving events.")
    case .background:
        print("App is in the background.")
    @unknown default:
        print("A new state that we need to handle.")
    }
}
```

### 状态变化的通知

你可以通过监听通知来处理应用程序状态的变化：

- **`UIApplicationDidBecomeActiveNotification`**：应用程序变为活跃状态。
- **`UIApplicationWillResignActiveNotification`**：应用程序将变为非活跃状态。
- **`UIApplicationDidEnterBackgroundNotification`**：应用程序进入后台。
- **`UIApplicationWillEnterForegroundNotification`**：应用程序将进入前台。

```swift
NotificationCenter.default.addObserver(self, selector: #selector(appDidBecomeActive), name: UIApplication.didBecomeActiveNotification, object: nil)
NotificationCenter.default.addObserver(self, selector: #selector(appWillResignActive), name: UIApplication.willResignActiveNotification, object: nil)
NotificationCenter.default.addObserver(self, selector: #selector(appDidEnterBackground), name: UIApplication.didEnterBackgroundNotification, object: nil)
NotificationCenter.default.addObserver(self, selector: #selector(appWillEnterForeground), name: UIApplication.willEnterForegroundNotification, object: nil)

@objc func appDidBecomeActive() {
    print("App did become active")
}

@objc func appWillResignActive() {
    print("App will resign active")
}

@objc func appDidEnterBackground() {
    print("App did enter background")
}

@objc func appWillEnterForeground() {
    print("App will enter foreground")
}
```

通过这些状态和通知，你可以更好地管理应用程序的生命周期，确保在不同状态下正确处理任务和资源。


---

# `UIImageWriteToSavedPhotosAlbum`保存照片到相册

在iOS中，你可以使用`UIImageWriteToSavedPhotosAlbum`函数将`UIImage`对象保存到用户的相册。这个函数需要一个`UIImage`对象，一个目标对象，一个完成选择器和一个上下文信息对象。

以下是一个简单的示例，展示了如何将`UIImage`数组中的每个图像保存到相册：

```swift
import Photos

func saveImagesToPhotoAlbum(images: [UIImage]) {
    for image in images {
        UIImageWriteToSavedPhotosAlbum(image, self, #selector(image(_:didFinishSavingWithError:contextInfo:)), nil)
    }
}

@objc func image(_ image: UIImage, didFinishSavingWithError error: Error?, contextInfo: UnsafeRawPointer) {
    if let error = error {
        // 我们在这里得到了一个错误!
        print("Error: \(error.localizedDescription)")
    } else {
        // 图片保存成功
        print("Image saved successfully!")
    }
}
```

请注意，你需要在你的应用的Info.plist文件中添加`NSPhotoLibraryAddUsageDescription`键，并提供一个描述，解释为什么你的应用需要这个权限。

---

# Mutipeer Connectivity 多点连接

`sendResource(at:withName:toPeer:withCompletionHandler:)` 和 `send(_:toPeers:with:)` 是 MultipeerConnectivity 框架中的两种发送数据的方式，它们的主要区别在于发送的数据类型和发送方式。

1. `sendResource(at:withName:toPeer:withCompletionHandler:)`：这个方法用于发送文件资源，例如图片、音频、视频等。这个方法会返回一个 `Progress` 对象，你可以使用这个对象来跟踪发送进度。这个方法是异步的，当资源发送完成时，会调用提供的完成处理器。

2. `send(_:toPeers:with:)`：这个方法用于发送小量的数据，例如文本、数字、小的数据对象等。这个方法不会返回 `Progress` 对象，你不能直接跟踪发送进度。这个方法是同步的，当方法返回时，数据已经被发送。

总的来说，如果你需要发送的是文件资源，并且需要跟踪发送进度，你应该使用 `sendResource(at:withName:toPeer:withCompletionHandler:)` 方法。如果你需要发送的是小量的数据，并且不需要跟踪发送进度，你可以使用 `send(_:toPeers:with:)` 方法。

---


# `QLPreviewController`预览文件
在SwiftUI中，你可以使用`QLPreviewController`来预览文档，包括PDF。但是，`QLPreviewController`是UIKit的一部分，所以你需要创建一个`UIViewControllerRepresentable`的实现来在SwiftUI中使用它。

以下是一个示例，展示了如何创建一个可以预览PDF的`QLPreviewController`：

```swift
import SwiftUI
import QuickLook

struct DocumentPreview: UIViewControllerRepresentable {
    var url: URL

    func makeUIViewController(context: Context) -> QLPreviewController {
        let controller = QLPreviewController()
        controller.dataSource = context.coordinator
        return controller
    }

    func updateUIViewController(_ uiViewController: QLPreviewController, context: Context) {}

    func makeCoordinator() -> Coordinator {
        Coordinator(self)
    }

    class Coordinator: NSObject, QLPreviewControllerDataSource {
        var parent: DocumentPreview

        init(_ parent: DocumentPreview) {
            self.parent = parent
        }

        func numberOfPreviewItems(in controller: QLPreviewController) -> Int {
            return 1
        }

        func previewController(_ controller: QLPreviewController, previewItemAt index: Int) -> QLPreviewItem {
            return parent.url as QLPreviewItem
        }
    }
}
```

你可以像这样使用`DocumentPreview`：

```swift
DocumentPreview(url: URL(fileURLWithPath: "/path/to/your/document.pdf"))
```

请注意，你需要将`/path/to/your/document.pdf`替换为你的文档的实际路径。

---

# `UIActivityViewController` 分享

在SwiftUI中，你可以使用`Button`和`UIActivityViewController`来实现点击按钮调出分享扩展。以下是一个例子：

```swift
import SwiftUI

struct ContentView: View {
    @State private var showShareSheet = false

    var body: some View {
        Button(action: {
            showShareSheet = true
        }) {
            Text("分享")
        }
        .sheet(isPresented: $showShareSheet) {
            ShareSheet(activityItems: ["分享内容"])
        }
    }
}

struct ShareSheet: UIViewControllerRepresentable {
    let activityItems: [Any]
    var applicationActivities: [UIActivity]? = nil

    func makeUIViewController(context: Context) -> UIActivityViewController {
        let controller = UIActivityViewController(activityItems: activityItems, applicationActivities: applicationActivities)
        return controller
    }

    func updateUIViewController(_ uiViewController: UIActivityViewController, context: Context) {}
}
```

在这个例子中，当用户点击"分享"按钮时，会弹出一个`ShareSheet`视图，这个视图是一个`UIActivityViewController`的封装。你可以将"分享内容"替换为你想要分享的任何内容，比如文本、图片、URL等。


---


# Picker

https://blog.csdn.net/lingjunjie/article/details/136739051

https://www.jianshu.com/p/812967bcf4d0


# HEXColor

SwiftUI本身并不直接支持十六进制颜色。但是，你可以通过扩展`Color`结构体来添加这个功能。以下是一个如何添加这个功能的例子：

```swift
import SwiftUI

extension Color {
    init(hex: String) {
        let hex = hex.trimmingCharacters(in: CharacterSet.alphanumerics.inverted)
        var int: UInt64 = 0
        Scanner(string: hex).scanHexInt64(&int)
        let a, r, g, b: UInt64
        switch hex.count {
        case 3: // RGB (12-bit)
            (a, r, g, b) = (255, (int >> 8) * 17, (int >> 4 & 0xF) * 17, (int & 0xF) * 17)
        case 6: // RGB (24-bit)
            (a, r, g, b) = (255, int >> 16, int >> 8 & 0xFF, int & 0xFF)
        case 8: // ARGB (32-bit)
            (a, r, g, b) = (int >> 24, int >> 16 & 0xFF, int >> 8 & 0xFF, int & 0xFF)
        default:
            (a, r, g, b) = (1, 1, 1, 0)
        }
        self.init(
            .sRGB,
            red: Double(r) / 255,
            green: Double(g) / 255,
            blue:  Double(b) / 255,
            opacity: Double(a) / 255
        )
    }
}
```

现在，你可以使用十六进制颜色来创建`Color`实例，如下所示：

```swift
Color(hex: "ff6347")
```

这将创建一个代表番茄色的`Color`实例。


在Swift中，枚举不能有基类，因为它们不是类。然而，你可以使用协议来定义共享的行为。在你的例子中，所有的枚举都遵循了`RawRepresentable`，`CaseIterable`和`Identifiable`协议。你可以定义一个自定义协议，包含这些协议，并让你的枚举遵循这个新的协议。

以下是如何定义和使用这个新协议的例子：

```swift
protocol CustomEnum: RawRepresentable, CaseIterable, Identifiable where Self.RawValue == String, Self.AllCases: BidirectionalCollection {
    var id: Self { get }
}

extension CustomEnum {
    var id: Self { self }
}

enum DisplayPosition: String, CustomEnum {
    case invalid = "invalid"
    // other cases...
}

enum HiddenDisplay: String, CustomEnum {
    case showAll, hideChildControls
}

enum Icontype: String, CustomEnum {
    case weekOrdate, numberOfSteps, distance, calorie, heartRate, battery
}

enum Colors: String, CustomEnum {
    case white = "#FFFFFF"
    // other cases...
}
```

在这个例子中，我们定义了一个新的协议`CustomEnum`，它包含了`RawRepresentable`，`CaseIterable`和`Identifiable`协议，并添加了一个约束，要求遵循这个协议的类型的原始值类型必须是`String`，并且它的所有案例必须是一个双向集合。然后，我们为`CustomEnum`添加了一个默认的`id`实现。最后，我们让你的所有枚举遵循这个新的协议。


在Swift中，`any`关键字用于创建类型擦除的包装器。在你的代码中，你试图创建一个`any SetCloudDail`类型的变量，这是不正确的。你应该使用`AnyHashable`来包装你的`SetCloudDail`类型。

---


# 渐变色

在SwiftUI中，`LinearGradient`，`RadialGradient`和`AngularGradient`都是用来创建渐变色的。

1. `LinearGradient`：线性渐变，颜色沿直线方向逐渐改变。它有两个关键参数：`gradient`和`startPoint`，`endPoint`。`gradient`定义了渐变的颜色和位置，`startPoint`和`endPoint`定义了渐变的方向。

```swift
LinearGradient(gradient: Gradient(colors: [.red, .blue]), startPoint: .top, endPoint: .bottom)
```

2. `RadialGradient`：径向渐变，颜色从一个中心点向外逐渐改变。它有三个关键参数：`gradient`，`center`和`startRadius`，`endRadius`。`gradient`定义了渐变的颜色和位置，`center`定义了渐变的中心点，`startRadius`和`endRadius`定义了渐变的半径范围。

```swift
RadialGradient(gradient: Gradient(colors: [.red, .blue]), center: .center, startRadius: 0, endRadius: 200)
```

3. `AngularGradient`：角度渐变，颜色沿圆周方向逐渐改变。它有两个关键参数：`gradient`和`center`。`gradient`定义了渐变的颜色和位置，`center`定义了渐变的中心点。

```swift
AngularGradient(gradient: Gradient(colors: [.red, .blue]), center: .center)
```

	以上都是创建渐变色的基本方法，你可以根据需要调整参数来创建不同的渐变效果。


---


# UIImage保存到文件app（HEIC形式）
在 iOS 11 及更高版本中，你可以使用 `AVAssetWriter` 和 `AVAssetWriterInputPixelBufferAdaptor` 将 `UIImage` 数组保存为 HEIC 格式的文件。以下是一个示例：

```swift
import AVFoundation
import UIKit

func saveImages(_ images: [UIImage], toFile file: String) {
    let fileURL = URL(fileURLWithPath: file)
    let assetWriter = try! AVAssetWriter(outputURL: fileURL, fileType: AVFileType.heic)
    let outputSettings: [String: Any] = [
        AVVideoCodecKey: AVVideoCodecType.heic,
        AVVideoWidthKey: NSNumber(value: Float(images[0].size.width)),
        AVVideoHeightKey: NSNumber(value: Float(images[0].size.height))
    ]
    let assetWriterInput = AVAssetWriterInput(mediaType: .video, outputSettings: outputSettings)
    let adaptor = AVAssetWriterInputPixelBufferAdaptor(assetWriterInput: assetWriterInput, sourcePixelBufferAttributes: nil)
    assetWriter.add(assetWriterInput)

    assetWriter.startWriting()
    assetWriter.startSession(atSourceTime: CMTime.zero)

    let context = CIContext()
    for (i, image) in images.enumerated() {
        let buffer = context.createPixelBuffer(for: image.cgImage!)!
        adaptor.append(buffer, withPresentationTime: CMTime(value: Int64(i), timescale: 1))
    }

    assetWriterInput.markAsFinished()
    assetWriter.finishWriting {}
}
```

在这个示例中，我们首先创建了一个 `AVAssetWriter`，并设置了输出文件的类型为 HEIC。然后，我们创建了一个 `AVAssetWriterInput`，并设置了输出的宽度和高度。接着，我们创建了一个 `AVAssetWriterInputPixelBufferAdaptor`，并将 `AVAssetWriterInput` 添加到 `AVAssetWriter` 中。

然后，我们开始写入会话，并遍历图像数组。对于每个图像，我们创建一个像素缓冲区，并将其添加到 `AVAssetWriterInputPixelBufferAdaptor` 中。

最后，我们标记 `AVAssetWriterInput` 为已完成，并结束写入。

请注意，这个函数将图像保存为一个 HEIC 文件，而不是多个文件。每个图像都被保存为文件中的一个帧。

---

# 使用sheet实现全屏显示（iOS15以下）

```swift
struct DemoCompatibleFullScreen: View {
    @State private var activateFullScreen = false
    var body: some View {
        Button("Toggle") { self.activateFullScreen.toggle() }
            .compatibleFullScreen(isPresented: $activateFullScreen) {
                Text("I'm in Full Screen!")
            }
    }
}

extension View {
    func compatibleFullScreen<Content: View>(isPresented: Binding<Bool>, @ViewBuilder content: @escaping () -> Content) -> some View {
        self.modifier(FullScreenModifier(isPresented: isPresented, builder: content))
    }
}

struct FullScreenModifier<V: View>: ViewModifier {
    let isPresented: Binding<Bool>
    let builder: () -> V

    @ViewBuilder
    func body(content: Content) -> some View {
        if #available(iOS 14.0, *) {
            content.fullScreenCover(isPresented: isPresented, content: builder)
        } else {
            content.sheet(isPresented: isPresented, content: builder)
        }
    }
}
```

好像对iOS14以下没有什么屌用

---
# Coredata和FileManager

`FileManager`和`CoreData`是两种不同的数据存储方式，它们各有优势，适用于不同的场景。

`FileManager`是一个用于文件和目录管理的类，它可以用于读写文件，创建和删除目录等。如果你需要存储的数据是大量的非结构化数据，如图片、音频、视频等，那么使用`FileManager`可能会更高效。

`CoreData`是一个强大的对象图和持久化框架，它可以用于管理应用程序的模型层对象、追踪它们的更改以及持久化到磁盘。如果你需要存储的数据是结构化的、需要进行复杂查询的，那么使用`CoreData`可能会更高效。

总的来说，`FileManager`和`CoreData`的存储和读写效率取决于你的具体需求。在选择使用哪种方式时，你应该考虑你的数据类型、数据量、以及你对数据的操作需求。

---
# iPhone尺寸大全

https://uiiiuiii.com/screen/

---

# 使用日志记录BUG

在iOS开发中，可以使用os.log来记录日志信息。以下是一个简单的例子，展示如何使用os.log记录日志信息：
首先，需要导入os.log库：
```swift
import os.log
```
然后，定义一个日志信息的类别，这样可以更好地过滤和组织日志信息：
```swift
private let log = OSLog(subsystem: "com.yourcompany.yourapp", category: "general")
```
接着，使用os_log函数记录日志信息：
```swift
os_log("This is a log message", log: log, type: .info)
```
如果需要记录变量或者格式化的信息，可以使用如下方式：
```swift
let username = "JohnDoe"
os_log("User logged in: %{public}s", log: log, type: .info, username)
```
在这个例子中，`%{public}s`是一个格式说明符，它告诉os_log接下来的参数是一个字符串（s代表字符串），public表示这个字符串是公开的，可以被第三方的日志查看工具访问。
为了捕获BUG，可以在代码中合适的地方添加日志记录，例如在异常处理或者重要的代码路径中。
```swift
do {
    // 尝试执行某些操作
} catch {
    os_log("An error occurred: %{public}@", log: log, type: .error, error.localizedDescription)
    // 处理错误
}
```
使用os.log可以在Xcode的调试区域查看日志输出，或者通过查看设备的系统日志来获取。这是一个基本的日志记录方法，对于更复杂的日志需求，可以考虑使用其他日志库或框架，如CocoaLumberjack或SwiftLog。

---


# 略缩图`QLThumbnailProvider`
在Swift中，你可以使用`QLThumbnailProvider`来获取文件的缩略图。这需要导入`QuickLookThumbnailing`框架。以下是一个简单的示例：

```swift
import QuickLookThumbnailing

func getThumbnail(for fileURL: URL, completion: @escaping (UIImage?) -> Void) {
    let size = CGSize(width: 60, height: 60)
    let scale = UIScreen.main.scale
    let request = QLThumbnailGenerator.Request(fileAt: fileURL, size: size, scale: scale, representationTypes: .thumbnail)

    QLThumbnailGenerator.shared.generateBestRepresentation(for: request) { (thumbnail, error) in
        DispatchQueue.main.async {
            if let thumbnail = thumbnail {
                completion(UIImage(cgImage: thumbnail.cgImage))
            } else {
                print("Error generating thumbnail: \(error?.localizedDescription ?? "Unknown error")")
                completion(nil)
# UIKit与swiftUI的视图结构

## swiftUI的视图

在 SwiftUI 中，视图的结构是由多个小的、可重用的视图组合而成的。这些小的视图可以是 SwiftUI 提供的，如 `Text`、`Image`、`Button` 等，也可以是自定义的视图。

视图可以嵌套在其他视图中，形成一个视图树。例如，你可以将多个视图放在 `VStack`（垂直堆栈）或 `HStack`（水平堆栈）中。你也可以使用 `ZStack` 来创建重叠的视图。

以下是一个简单的 SwiftUI 视图结构的例子：

```swift
struct ContentView: View {
    var body: some View {
        VStack {
            Text("Hello, World!")
            HStack {
                Button(action: {
                    print("Button tapped")
                }) {
                    Text("Tap me")
                }
                Image(systemName: "star.fill")
            }
        }
    }
}
```

这个函数接受一个文件URL和一个回调函数作为参数。它创建一个`QLThumbnailGenerator.Request`，指定文件URL、缩略图的大小、屏幕的比例和表示类型。然后，它使用`QLThumbnailGenerator`来生成缩略图。当缩略图生成完成时，它在主线程上调用回调函数，并传入生成的UIImage。如果在生成缩略图时发生错误，它会打印错误信息，并调用回调函数，传入nil。

注意，这个函数是异步的，因为生成缩略图可能需要一些时间。你应该在回调函数中处理生成的UIImage，例如将其显示在UIImageView中。
在这个例子中，`ContentView` 是一个 `VStack`，它包含一个 `Text` 视图和一个 `HStack`。`HStack` 又包含一个 `Button` 和一个 `Image`。这就形成了一个视图树，从 `ContentView` 到 `VStack`，再到 `Text`、`HStack`，最后到 `Button` 和 `Image`。

SwiftUI 是 Apple 的一种声明式 UI 框架，用于构建跨 Apple 平台的用户界面。在 SwiftUI 中，视图是用户界面的基本构建块。

在 SwiftUI 中，每个视图都是一个结构体，实现了 `View` 协议。这个协议只有一个要求，那就是一个名为 `body` 的计算属性，其返回值也是一个视图。

例如，下面是一个简单的 SwiftUI 视图：

```swift
struct ContentView: View {
    var body: some View {
        Text("Hello, World!")
    }
}
```

在这个例子中，`ContentView` 是一个视图，它的 `body` 属性返回一个 `Text` 视图，显示 "Hello, World!"。

SwiftUI 视图是不可变的，这意味着一旦创建，就不能更改它们的属性。要更新视图，需要创建一个新的视图。SwiftUI 会负责比较新旧视图，并有效地更新 UI。

此外，SwiftUI 视图可以组合在一起，创建更复杂的视图。例如，可以使用 `VStack`、`HStack` 和 `ZStack` 等布局视图来组合多个视图。

在 SwiftUI 中，视图的层级结构是由多个视图组合而成的，形成一个视图树。这些视图可以是 SwiftUI 提供的，如 `Text`、`Image`、`Button` 等，也可以是自定义的视图。

以下是一个简单的 SwiftUI 视图层级结构的例子：

```swift
struct ContentView: View {
    var body: some View {
        VStack { // 顶层视图
            Text("Hello, World!") // 子视图
            HStack { // 子视图
                Button(action: { // 子视图的子视图
                    print("Button tapped")
                }) {
                    Text("Tap me") // Button 的子视图
                }
                Image(systemName: "star.fill") // HStack 的另一个子视图
            }
        }
    }
}
```

在这个例子中，`ContentView` 是顶层视图，它包含一个 `VStack`。`VStack` 是一个垂直堆栈视图，它有两个子视图：一个 `Text` 和一个 `HStack`。`HStack` 是一个水平堆栈视图，它有两个子视图：一个 `Button` 和一个 `Image`。`Button` 又有一个子视图，即 `Text`。

这就形成了一个视图树，从 `ContentView` 到 `VStack`，再到 `Text`、`HStack`，最后到 `Button` 和 `Image`。

---


## UIKit的视图结构

（1）UIApplication对象是应用程序的象征，一个UIApplication对象就代表一个应用程序。

（2）每一个应用都有自己的UIApplication对象，而且是单例的，如果试图在程序中新建一个UIApplication对象，那么将报错提示。
（3）通过[UIApplicationsharedApplication]可以获得这个单例对象
（4） 一个iOS程序启动后创建的第一个对象就是UIApplication对象，且只有一个（通过代码获取两个UIApplication对象，打印地址可以看出地址是相同的）。
（5）利用UIApplication对象，能进行一些应用级别的操作

一、使用步骤
1.main函数
2.UIApplicationMain
创建UIApplication对象
创建UIApplication的delegate对象
3.加载视图
（1）delegate对象开始处理(监听)系统事件(没有storyboard)

程序启动完毕的时候, 就会调用代理的application:didFinishLaunchingWithOptions:方法
在application:didFinishLaunchingWithOptions:中创建UIWindow
创建和设置UIWindow的rootViewController
显示窗口
（2）根据Info.plist获得最主要storyboard的文件名,加载最主要的storyboard(有storyboard)

创建UIWindow
创建和设置UIWindow的rootViewController
显示窗口
二、基本属性
1）设置应用程序图标右上角的红色提醒数字（如QQ消息的时候，图标上面会显示1，2，3条新信息等。）
@property(nonatomic) NSInteger applicationIconBadgeNumber;

2）设置联网指示器的可见性
@property(nonatomic,getter=isNetworkActivityIndicatorVisible) BOOL networkActivityIndicatorVisible;

3）管理状态栏
从iOS7开始，系统提供了2种管理状态栏的方式
如果状态栏的样式只设置一次，那就用UIApplication来进行管理
如果状态栏是否隐藏，样式不一样那就用控制器进行管理
UIApplication来进行管理有额外的好处，可以提供动画效果

a.通过UIViewController管理（每一个UIViewController都可以拥有自己不同的状态栏）.

在iOS7中，默认情况下，状态栏都是由UIViewController管理的，UIViewController实现下列方法就可以轻松管理状态栏的可见性和样式
状态栏的样式　　 - (UIStatusBarStyle)preferredStatusBarStyle;
状态栏的可见性　　-(BOOL)prefersStatusBarHidden;

b.通过UIApplication管理（一个应用程序的状态栏都由它统一管理）

如果想利用UIApplication来管理状态栏，首先得修改Info.plist的设置

4）openURL:方法
UIApplication有个功能十分强大的openURL:方法
- (BOOL)openURL:(NSURL*)url;
openURL:方法的部分功能有
打电话 UIApplication *app = [UIApplicationsharedApplication]; [app openURL:[NSURLURLWithString:@”tel://10086”]];
发短信 [app openURL:[NSURLURLWithString:@”sms://10086”]];
发邮件 [app openURL:[NSURLURLWithString:@”mailto://12345@qq.com”]];
打开一个网页资源 [app openURL:[NSURLURLWithString:@”http://ios.itcast.cn“]];
打开其他app程序 openURL方法，可以打开其他APP。

5.UIAppDelegate生命周期
在app受到干扰时，会产生一些系统事件，这时UIApplication会通知它的delegate对象，让delegate代理来处理这些系统事件。当被打断的时候，通知代理进入到后台。


---

# UIImage存入filemanager

在Swift中，你可以使用以下步骤将一组UIImage存入FileManager：

1. 将UIImage转换为Data对象
2. 使用FileManager的write方法将Data对象写入文件

以下是具体的代码实现：

```swift
import UIKit

func saveImages(images: [UIImage], directory: String) {
    let fileManager = FileManager.default
    let directoryURL = fileManager.urls(for: .documentDirectory, in: .userDomainMask)[0].appendingPathComponent(directory)

    do {
        try fileManager.createDirectory(at: directoryURL, withIntermediateDirectories: true, attributes: nil)

        for (index, image) in images.enumerated() {
            if let data = image.pngData() {
                let filename = directoryURL.appendingPathComponent("\(index).png")
                try data.write(to: filename)
            }
        }
    } catch {
        print("Error saving images: \(error)")
    }
}
```

这个函数接受一个UIImage数组和一个目录名作为参数。它首先获取到文档目录的URL，然后在这个URL下创建一个新的目录。然后，它遍历每个UIImage，将其转换为PNG数据，并将这些数据写入到新目录下的文件中。每个文件的名字是其在数组中的索引。如果在任何地方发生错误，它会打印出错误信息。

---

# 模拟器


`~/Library/Developer/CoreSimulator/Images` 目录通常用于存储 iOS 模拟器的磁盘镜像。这些镜像包含了模拟器运行所需的 iOS 系统和预装应用。

每个模拟器都有一个对应的磁盘镜像，这个镜像包含了模拟器的文件系统。当你在模拟器中安装应用或修改设置时，这些更改会保存到磁盘镜像中。

请注意，这个目录通常是隐藏的，你需要在 Finder 中使用 "前往文件夹" 命令，或在终端中使用 `cd` 命令才能访问它。你不应该直接修改这个目录中的文件，因为这可能会破坏你的模拟器。如果你需要重置模拟器，你可以在 Xcode 的 "Devices and Simulators" 窗口中删除和重新创建模拟器。



# 裁剪图片

https://github.com/TimOliver/TOCropViewController?tab=readme-ov-file


# hex颜色

```swift
let colorList: [Int] = [0xffffff, 0x000000, 0xde4371, 0xde4343,
                        0xde7143, 0xdba85c, 0xdbcf60, 0xb7c96b,
                        0xa8e36d, 0x85e36d, 0x6de379, 0x6de39c,
                        0x6de3c0, 0x6de3e3, 0x6dc0e3, 0x6d9ce3,
                        0x6d79e3, 0x856de3, 0xa86de3, 0xcb6de3,
                        0xe36dd7, 0xe36db4]

let swiftUIColors = colorList.map { (colorInt) -> Color in
    let red = Double((colorInt >> 16) & 0xFF) / 255.0
    let green = Double((colorInt >> 8) & 0xFF) / 255.0
    let blue = Double(colorInt & 0xFF) / 255.0
    return Color(red: red, green: green, blue: blue)
}
```

---


# HEXColor

在 Swift 中，构造器不能返回一个可选值，所以你不能在构造器中使用 `return` 关键字。你应该直接使用参数来初始化 `self`。这是修改后的代码：

```swift
extension Color {
    init(hexStr: String) {
        let hex = hexStr.trimmingCharacters(in: CharacterSet.alphanumerics.inverted)
        var int: UInt64 = 0
        Scanner(string: hex).scanHexInt64(&int)
        let a, r, g, b: UInt64
        switch hex.count {
        case 3: // RGB (12-bit)
            (a, r, g, b) = (255, (int >> 8) * 17, (int >> 4 & 0xF) * 17, (int & 0xF) * 17)
        case 6: // RGB (24-bit)
            (a, r, g, b) = (255, int >> 16, int >> 8 & 0xFF, int & 0xFF)
        case 8: // ARGB (32-bit)
            (a, r, g, b) = (int >> 24, int >> 16 & 0xFF, int >> 8 & 0xFF, int & 0xFF)
        default:
            (a, r, g, b) = (1, 1, 1, 0)
        }
        self.init(
            .sRGB,
            red: Double(r) / 255,
            green: Double(g) / 255,
            blue:  Double(b) / 255,
            opacity: Double(a) / 255
        )
    }
    
    init(hexInt: Int) {
        let red = Double((hexInt >> 16) & 0xFF) / 255.0
        let green = Double((hexInt >> 8) & 0xFF) / 255.0
        let blue = Double(hexInt & 0xFF) / 255.0
        self.init(red: red, green: green, blue: blue)
    }
}
```

在 `init(hexInt:)` 构造器中，我移除了 `return` 关键字，并直接使用 `self.init(red:green:blue:)` 来初始化 `Color`。这样，你就可以使用一个十六进制整数来创建一个 `Color` 对象了。

---


# iOS中的模版图像

**什么是模版图片：**
没有颜色信息的图像通常被称为模板图像或者蒙版图像。这些图像只包含透明度信息，不包含颜色信息。换句话说，这些图像只有黑白两种颜色，没有灰度或者其他颜色。

在 iOS 中，系统图标就是模板图像的一个例子。这些图标通常是单色的，它们的颜色可以通过代码来改变。例如，你可以使用 `foregroundColor(_:)` 方法来改变一个 `Image` 视图的颜色，如果这个视图显示的是一个模板图像。

你可以使用 `withRenderingMode(_:)` 方法来将一个 `UIImage` 转换为模板图像：

```swift
let image = UIImage(named: "example")?.withRenderingMode(.alwaysTemplate)
```

在这个例子中，我们加载了一个名为 "example" 的图像，然后使用 `withRenderingMode(_:)` 方法将它转换为模板图像。现在，我们可以使用 `foregroundColor(_:)` 方法来改变这个图像的颜色。

请注意，不是所有的图像都可以转换为模板图像。如果一个图像包含多种颜色或者灰度，那么转换为模板图像可能会丢失一些信息。在实际的项目中，你可能需要根据你的具体需求来选择是否使用模板图像。

在 SwiftUI 中，你可以使用 `foregroundColor(_:)` 方法来设置 `Image` 的颜色。这个方法会改变图像的前景色，也就是图像非透明部分的颜色。

这是一个例子：

```swift
Image(systemName: "star.fill")
    .foregroundColor(.red)
```

在这个例子中，我们创建了一个系统图像，并使用 `foregroundColor(_:)` 方法将它的颜色设置为红色。

请注意，这个方法只适用于模板图像，也就是那些只有透明度信息，没有颜色信息的图像。对于彩色图像，这个方法可能不会产生预期的效果。如果你需要改变彩色图像的颜色，你可能需要使用其他的方法，如使用 `CGImage` 的 `applyingFilter(_:parameters:)` 方法来应用一个颜色滤镜。

在 SwiftUI 中，你可以使用 `renderingMode(_:)` 方法来将 `Image` 视图设置为模板模式。这样，图像就会忽略其原有的颜色信息，只保留透明度信息，然后使用前景色作为其颜色。

---

# SpringBoard

SpringBoard是iOS和iPadOS操作系统中的主屏幕管理程序。它负责启动和切换应用程序，以及管理设备的主屏幕。这包括显示应用图标，处理壁纸，以及响应设备的物理按钮。

当你按下设备的Home按钮或者滑动屏幕解锁设备时，你看到的就是SpringBoard。所有的应用图标，文件夹，壁纸，Dock，状态栏，以及锁屏界面，都是由SpringBoard管理的。

SpringBoard也负责处理一些系统级的操作，比如显示弹出窗口，处理设备旋转，以及显示应用切换器。

请注意，虽然SpringBoard是iOS和iPadOS的一个重要组成部分，但是作为开发者，你通常不能直接与它交互。大部分与SpringBoard相关的功能，比如启动应用，都是通过iOS SDK提供的API来实现的。

---

# CoreStore实现实时UI更新

要实现这个需求，你可以使用 CoreStore 的 `ListPublisher`。首先，你需要创建一个 `ListPublisher` 来监视 `Person` 对象的变化。然后，你可以使用 `@ListState` 属性包装器来订阅这个 `ListPublisher` 的更新。

以下是一个简单的示例：

```swift
import SwiftUI
import CoreStore

struct PersonView: View {
    @ListState
    var people: ListSnapshot<Person>

    init() {
        let listPublisher = CoreStoreDefaults.dataStack.publisher(
            From<Person>(),
            OrderBy(.ascending(\.name))
        )
        self._people = .init(listPublisher)
    }

    var body: some View {
        List {
            ForEach(objectIn: self.people) { objectSnapshot in
                Text(objectSnapshot.name)
            }
        }
        .animation(.default)
    }
}
```

在这个示例中，我们首先创建了一个 `ListPublisher` 来监视 `Person` 对象的变化。我们使用 `From<Person>()` 来指定我们想要监视的对象类型，使用 `OrderBy(.ascending(\.name))` 来指定我们想要的排序方式。

然后，我们使用 `@ListState` 属性包装器来订阅这个 `ListPublisher` 的更新。当 `Person` 对象发生变化时，`ListPublisher` 会发布一个新的 `ListSnapshot`，并更新 `people` 属性。这会触发视图的重新渲染。

在 `body` 属性中，我们使用 `ForEach` 视图来遍历 `people` 中的每一个对象，并为每一个对象创建一个 `Text` 视图。当 `people` 发生变化时，`ForEach` 视图会自动更新。

请注意，这个示例假设你已经正确配置了 CoreStore 和 CoreData。你可能需要根据你的实际情况对这个示例进行一些修改。

## CoreStore的排序

`OrderBy(.ascending(\.name))` 这段代码的作用是指定查询结果的排序方式。

在这个例子中，`OrderBy(.ascending(\.name))` 表示你希望查询结果按照 `Person` 对象的 `name` 属性的升序排列。换句话说，`name` 属性值较小的 `Person` 对象会排在前面，`name` 属性值较大的 `Person` 对象会排在后面。

`OrderBy` 是 CoreStore 库中的一个类，它用于指定查询结果的排序方式。`.ascending(\.name)` 是一个 `OrderBy` 的实例，它表示升序排序。

如果你希望查询结果按照 `name` 属性的降序排列，你可以使用 `OrderBy(.descending(\.name))`。

---
# 使用其他app打开文件

在 Swift 中，你可以使用 `UIDocumentInteractionController` 来实现使用其他 app 打开一个文件。以下是一个例子：

```swift
import UIKit

func openFileWithOtherApp(url: URL) {
    let documentController = UIDocumentInteractionController(url: url)
    documentController.presentOpenInMenu(from: .zero, in: view, animated: true)
}
```

在这个例子中，我们首先创建了一个 `UIDocumentInteractionController` 实例，然后调用 `presentOpenInMenu(from:in:animated:)` 方法来显示一个菜单，用户可以从这个菜单中选择一个 app 来打开文件。

请注意，你需要在一个 `UIViewController` 中调用这个函数，因为 `presentOpenInMenu(from:in:animated:)` 方法需要一个视图来显示菜单。你也需要确保文件的 URL 是有效的，否则 `UIDocumentInteractionController` 将无法打开文件。

此外，你还需要在你的 app 的 Info.plist 文件中添加一个 `LSApplicationQueriesSchemes` 键，并列出你想要打开的其他 app 的 URL schemes，否则你的 app 将无法打开这些 app。

---

# 点击屏幕隐藏键盘

### 在UIKit中隐藏键盘的方法

1. `textField.resignFirstResponder()`
2. `view.endEditing(true)`

本质上是需要获取到承载键盘的视图

SwiftUI添加方法
SwiftUI 没有之前 View 的概念了，但是同样可以获取到整个 App 的 window，从而调用 endEditing。
给 UIApplication 增加 Extension

```swift
// MARK: - 全局点击隐藏键盘分类
extension UIApplication {
    
    public func addTapHideKeyBoardGesture() {
        guard let window = windows.first else { return }
        
        let tapGesture = UITapGestureRecognizer(target: window, action: #selector(UIView.endEditing))
        tapGesture.requiresExclusiveTouchType = false
        tapGesture.cancelsTouchesInView = false
        tapGesture.delegate = self
        window.addGestureRecognizer(tapGesture)
    }
}
```

```swift
extension UIApplication: UIGestureRecognizerDelegate {
    public func gestureRecognizer(_ gestureRecognizer: UIGestureRecognizer, shouldRecognizeSimultaneouslyWith otherGestureRecognizer: UIGestureRecognizer) -> Bool {
        return true // 可以同时响应多个手势
    }
}
```

requiresExclusiveTouchType：默认为 true。这个属性是指是否允许多种手势输入，这里的多种包含触摸、遥控器、触控笔等，所以可以配置成 false
cancelsTouchesInView：默认为 true。这里设置为 false，主要为了不影响其他手势的识别。当前的 tap 手势被识别出来之后，也不会触发 UITouch 的 cancel 方法，因此就不会中断 UITouch 的传递。

最后加上手势识别

```swift
.onAppear(perform: UIApplication.shared.addTapHideKeyBoardGesture)
```

原文链接：
https://blog.csdn.net/guoxulieying/article/details/132869730

SwiftUI中几种关闭键盘的方式


在国内大多数app的操作中都有在带有输入框视图的页面中点击其他部分关闭键盘，因此给用户形成了一个操作习惯，于是在开发者自己开发的app中也需能够点击其他部分关闭键盘，不然会给用户造成困扰，在SwiftUI中，关闭弹出的键盘有几种常用的方式：

使用UIApplication.shared.sendAction方法：这是一种通用的方法，可以在任何地方使用。你只需要调用UIApplication.shared.sendAction并发送一个隐藏键盘的命令。

``` swift
UIApplication.shared.sendAction(#selector(UIResponder.resignFirstResponder), to: nil, from: nil, for: nil)
```
1
这行代码的工作原理如下：
UIApplication.shared:
UIApplication.shared是对当前应用实例的引用。它提供了许多控制和配置应用行为的方法。
sendAction(_:to:from:for:)方法:
sendAction(_:to:from:for:)是一个发送动作或事件的方法。这个方法可以用来触发特定的行为或命令。
#selector(UIResponder.resignFirstResponder):
#selector(UIResponder.resignFirstResponder)是一个选择器，指向resignFirstResponder方法。resignFirstResponder是UIResponder类的一个方法，用于放弃响应者状态，通常意味着隐藏键盘。在iOS中，当一个控件（如文本框）成为第一响应者时，键盘会显示。当它放弃第一响应者状态时，键盘会隐藏。
to: nil, from: nil, for: nil:
这些参数定义了动作发送的目标、来源和上下文。在这种情况下，它们都被设置为nil，意味着不指定特定的目标或来源，而是允许应用自动确定应该响应此动作的对象。
通过执行这段代码，应用会查找当前成为第一响应者的UI元素（通常是一个激活的文本字段）并让它放弃其第一响应者状态，从而导致键盘被隐藏。
这种方法的优点是它在SwiftUI中非常通用，不依赖于特定的UI组件或视图结构。然而，需要注意的是，这种方法使用了UIKit的API，这在纯SwiftUI的环境中可能不是最理想的选择。随着SwiftUI的不断发展，可能会出现更多纯SwiftUI的解决方案。
使用@FocusState属性（iOS 15及以上）：@FocusState是iOS 15引入的一个属性，允许你管理特定视图的焦点状态。你可以使用它来控制哪个输入字段应该是活动的，并相应地显示或隐藏键盘。

```swift
@FocusState private var isInputActive: Bool
```

```swift
// 在某个视图上
TextField("输入点什么", text: $text)
    .focused($isInputActive)

// 然后可以设置isInputActive为false来隐藏键盘
isInputActive = false
```

使用dismiss方法：在某些情况下，例如在Form或Sheet中，你可以直接使用dismiss方法来关闭键盘。
原文链接：https://blog.csdn.net/weixin_63783406/article/details/134504721


---
