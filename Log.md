
# DDLog

是的，﻿DDLog 是 CocoaLumberjack 框架中的核心类，广泛用于 iOS 和 macOS 开发中进行日志记录。CocoaLumberjack 是一个功能强大、灵活且高性能的日志库，支持多种日志级别和目标。

**安装 CocoaLumberjack**

您可以通过 CocoaPods 或 Swift Package Manager 来安装 CocoaLumberjack。

**CocoaPods**

在 Podfile 中添加：

```
pod 'CocoaLumberjack/Swift'
```


然后运行 `pod install`﻿。

**Swift Package Manager**

可以在 Xcode 中通过 Package 管理器添加：

```
.package(url: "https://github.com/CocoaLumberjack/CocoaLumberjack.git", from: "3.7.5")
```


**基本用法**

**引入框架**

Objective-C:

```objc
#import <CocoaLumberjack/CocoaLumberjack.h>
```


Swift:

```swift
import CocoaLumberjack

import CocoaLumberjackSwift
```


**配置日志**

配置 CocoaLumberjack 以输出日志到控制台、文件或其他目标。

Objective-C:

```objc
[DDLog addLogger:[DDTTYLogger sharedInstance]]; // TTY = Xcode console

[DDLog addLogger:[DDASLLogger sharedInstance]]; // ASL = Apple System Logs
```



```objc
// 示例：将日志保存到文件

DDFileLogger *fileLogger = [[DDFileLogger alloc] init];

fileLogger.rollingFrequency = 60 * 60 * 24; // 24 hour rolling

fileLogger.logFileManager.maximumNumberOfLogFiles = 7;

[DDLog addLogger:fileLogger];
```


Swift:


```swift
DDLog.add(DDTTYLogger.sharedInstance) // TTY = Xcode console

DDLog.add(DDASLLogger.sharedInstance) // ASL = Apple System Logs

  

// 示例：将日志保存到文件

let fileLogger: DDFileLogger = DDFileLogger()

fileLogger.rollingFrequency = TimeInterval(60 * 60 * 24) // 24 hours rolling

fileLogger.logFileManager.maximumNumberOfLogFiles = 7

DDLog.add(fileLogger)
```


**记录日志**

使用 CocoaLumberjack 提供的不同级别函数来记录日志消息。

Objective-C:

```objc
DDLogError(@"Error message");   // 错误信息

DDLogWarn(@"Warning message");  // 警告信息

DDLogInfo(@"Info message");     // 信息

DDLogDebug(@"Debug message");   // 调试信息

DDLogVerbose(@"Verbose message"); // 详细信息
```


Swift:

```swift
DDLogError("Error message")      // 错误信息

DDLogWarn("Warning message")     // 警告信息

DDLogInfo("Info message")        // 信息

DDLogDebug("Debug message")      // 调试信息

DDLogVerbose("Verbose message")  // 详细信息
```


**日志级别**

CocoaLumberjack 提供了多种日志级别，可以根据需要进行过滤：

• ﻿DDLogError

• ﻿DDLogWarn

• ﻿DDLogInfo

• ﻿DDLogDebug

• ﻿DDLogVerbose

**自定义日志格式**

您还可以定义自定义的日志格式，确保日志输出符合您的需求。使用 ﻿DDLogFormatter 协议来自定义日志格式。

Objective-C:

```objc

@interface CustomLogFormatter : NSObject <DDLogFormatter>

@end

  

@implementation CustomLogFormatter

-  (NSString *)formatLogMessage:(DDLogMessage *)logMessage {

    NSString *logLevel;

    switch (logMessage.flag) {

        case DDLogFlagError   : logLevel = @"[ERROR]"; break;

        case DDLogFlagWarning : logLevel = @"[WARN]"; break;

        case DDLogFlagInfo    : logLevel = @"[INFO]"; break;

        case DDLogFlagDebug   : logLevel = @"[DEBUG]"; break;

        default               : logLevel = @"[VERBOSE]"; break;

    }

    return [NSString stringWithFormat:@"%@ %@", logLevel, logMessage.message];

}

@end

  

DDTTYLogger.sharedInstance.logFormatter = [[CustomLogFormatter alloc] init];
```


Swift:

 
```swift
 

class CustomLogFormatter: NSObject, DDLogFormatter {

    public func format(message logMessage: DDLogMessage) -> String? {

        let logLevel: String

        switch logMessage.flag {

        case .error:   logLevel = "[ERROR]"

        case .warning: logLevel = "[WARN]"

        case .info:    logLevel = "[INFO]"

        case .debug:   logLevel = "[DEBUG]"

        default:       logLevel = "[VERBOSE]"

        }

        return "\(logLevel) \(logMessage.message)"

    }

}

  

DDTTYLogger.sharedInstance.logFormatter = CustomLogFormatter()
```


通过这些步骤，您可以在 iOS 或 macOS 应用中高效地使用 CocoaLumberjack 进行日志记录。

## DDLog介绍

`DDLog` 是 `CocoaLumberjack` 库中的一个类，`CocoaLumberjack` 是一个强大且灵活的日志框架，通常用于 iOS 和 macOS 应用程序中。它提供了高性能的日志记录功能，并支持多种日志目标（如文件、控制台等）。

### 主要特点

1. **高性能**：`CocoaLumberjack` 经过优化，可以在高负载下高效地记录日志。
2. **灵活性**：你可以配置多个日志目标（如控制台、文件、远程服务器等），并为每个目标设置不同的日志级别。
3. **线程安全**：`CocoaLumberjack` 是线程安全的，适合多线程环境。
4. **支持多种日志级别**：包括 `verbose`、`debug`、`info`、`warn`、`error` 等。

### 安装

你可以使用 CocoaPods 或 Swift Package Manager 来安装 `CocoaLumberjack`。

#### CocoaPods

在你的 `Podfile` 中添加：

```ruby
pod 'CocoaLumberjack/Swift'
```

然后运行 `pod install`。

#### Swift Package Manager

在你的 `Package.swift` 文件中添加：

```swift
dependencies: [
    .package(url: "https://github.com/CocoaLumberjack/CocoaLumberjack.git", from: "3.7.0")
]
```

然后运行 `swift build`。

### 使用

以下是一个简单的示例，展示如何使用 `DDLog` 进行日志记录：

```swift
import CocoaLumberjackSwift

// 配置日志记录器
DDLog.add(DDOSLogger.sharedInstance) // 使用 OS Logger

// 设置日志级别
dynamicLogLevel = .all

// 记录日志
DDLogVerbose("Verbose message")
DDLogDebug("Debug message")
DDLogInfo("Info message")
DDLogWarn("Warning message")
DDLogError("Error message")
```

### 配置文件日志

如果你想将日志记录到文件中，可以添加一个文件日志记录器：

```swift
let fileLogger: DDFileLogger = DDFileLogger() // 默认的文件日志记录器
fileLogger.rollingFrequency = TimeInterval(60*60*24) // 每24小时滚动一次日志文件
fileLogger.logFileManager.maximumNumberOfLogFiles = 7 // 保留最近7天的日志文件
DDLog.add(fileLogger)
```

### 日志级别

你可以使用以下日志级别：

- `DDLogVerbose`
- `DDLogDebug`
- `DDLogInfo`
- `DDLogWarn`
- `DDLogError`

这些日志级别可以帮助你过滤和管理不同重要性的日志信息。

### 自定义日志格式

你可以创建自定义的日志格式器来格式化日志输出：

```swift
class CustomLogFormatter: NSObject, DDLogFormatter {
    let dateFormatter = DateFormatter()
    
    override init() {
        super.init()
        dateFormatter.dateFormat = "yyyy/MM/dd HH:mm:ss:SSS"
    }
    
    func format(message logMessage: DDLogMessage) -> String? {
        let dateAndTime = dateFormatter.string(from: logMessage.timestamp)
        return "\(dateAndTime) [\(logMessage.level)] \(logMessage.message)"
    }
}

let customFormatter = CustomLogFormatter()
DDOSLogger.sharedInstance.logFormatter = customFormatter
```

通过这种方式，你可以根据需要自定义日志输出格式。

`CocoaLumberjack` 提供了许多功能和配置选项，可以满足大多数应用程序的日志需求。详细的文档和更多功能可以参考 [CocoaLumberjack 的 GitHub 仓库](https://github.com/CocoaLumberjack/CocoaLumberjack)。

---
# OSlog

`@avaiable iOS14`