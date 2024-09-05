下载地址：
https://developer.apple.com/download/all/?q=xcode

---
# Xcode代码索引原理
https://cloud.tencent.com/developer/article/2204613?areaSource=102001.18&traceId=EI_rLraLXoc6jzEs8CZlN




---

# xcode注释

https://blog.csdn.net/weixin_38633659/article/details/104019028

1、#pragma mark
#pragma mark -
#pragma mark - TableViewDelegate
从技术角度讲，以 #pragma 开头的代码是一条编译器指令，一个特定于程序或编译器的指令。它们不一定适用于其它编译器或其它环境。如果编译器不能识别该指令，则会将其忽略。
其作用是，告诉Xcode编译器，要在编辑器窗格顶部的方法和函数弹出菜单中将代码分隔开，如下图所示：


其他特殊注释，这些一般比较少用，一般在特殊情况下使用，而且用完之后尽量及时的清除，使得代码更加规范：

2、其他注释【TODO、FIXME、!!!、???、MARK】：
方法一（系统自带功能）：

当你需要标记部分代码以供将来参考，比如: 优化，改进，可能的更改，要讨论的问题等。通常我们会在代码中加入如下的标记表示待办：

```
///TODO:标示处有功能代码待编写
///FIXME:标示处代码需要修正
///!!!:标示处代码需要注意
///???:标示处代码有疑问
///MARK:标记，和#pragma mark效果相同
```


使用示例：

#pragma mark TODO:  标示处有功能代码待编写
#pragma mark FIXME: 标示处代码需要修正
#pragma mark !!!:  标示处代码需要注意
#pragma mark ???:  标示处代码有疑问
#pragma mark MARK:  标记，和#pragma mark效果相同

方法二（脚本实现）：

1、直接先上脚本：

TAGS="XXX:|!!!:|MARK:|TODO:|FIXME:|#WARNING:"
ERRORTAG="#ERROR:"
find "${SRCROOT}" \( -name "*.h" -or -name "*.m" -or -name "*.swift" \) -print0 | xargs -0 egrep --with-filename --line-number --only-matching "($TAGS).*\$|($ERRORTAG).*\$" | perl -p -e "s/($TAGS)/ warning: \$1/" | perl -p -e "s/($ERRORTAG)/ error: \$1/"
1
2
3
2、将脚本加到这个位置


3、这样加上//TODO:等的注释，编译的时候就会有警告提示了



应用总结：
1、不管是系统方法还是脚本实现，这些标记对项目的开发维护只是起到锦上添花的作用,但是要规范代码，它们将不可或缺。
2、针对项目而言，一定要记得定期处理这些的标记（除MARK标记外），不然时间越长，垃圾代码就越多了。
3、Xcode对这些标记的实现和写法做了点细节调整，但是感觉起来会更加性感，至于想使用图一还是使用最后一张图的写法，主要看个人的习惯。个人来说，还是喜欢和【#pragma mark 】配合使用，这样会醒目一点。
4、个人感觉唯一美中不足的地方是，和【#pragma mark - 】配合只实现分行作用，没能展示对应的小图标。–> 总想着能尽善尽美😆。
5、脚本实现的方法，感觉太抢眼，对拥有警告强迫症的人来说，简直就是噩梦般的存在，针对那些必须要尽快修改的地方可以加上😺。

使用方法汇总：

#pragma mark TODO:  标示处有功能代码待编写
#pragma mark FIXME: 标示处代码需要修正
#pragma mark !!!:  标示处代码需要注意
#pragma mark ???:  标示处代码有疑问
#pragma mark MARK:  标记，和#pragma mark效果相同

///TODO:标示处有功能代码待编写
///FIXME:标示处代码需要修正
///!!!:标示处代码需要注意
///???:标示处代码有疑问
///MARK:标记，和#pragma mark效果相同
推荐博客：
1、如何让自己的代码更整洁
2、iOS开发:#pragma的应用
3、ios面向切面编程：强大的AOP
4、Swift与OC的混编
5、OC与Swift的数据传输


在 Xcode 中，可以使用快捷键生成注释块来提高开发效率。以下是一些常用的快捷键和方法：

### 1. 单行注释
- **快捷键**：`Command + /`
- **效果**：将当前行或选中的多行代码注释或取消注释。

### 2. 多行注释块
Xcode 没有直接的快捷键来生成多行注释块，但你可以手动添加多行注释，或者使用 Xcode 的“代码片段”功能来快速插入自定义注释块。

#### 手动添加多行注释
```swift
/*
 This is a multi-line comment.
 It can span multiple lines.
*/
```

### 3. 代码片段（Code Snippets）
你可以创建自定义的代码片段来快速插入注释块。

#### 创建自定义代码片段
1. **打开代码片段库**：按 `Command + Shift + L` 或者点击右侧的代码片段库图标。
2. **创建新的代码片段**：
   - 在代码编辑器中输入你的注释块模板，例如：
     ```swift
     /*
      * <#Description#>
      *
      * - Parameters:
      *   - <#parameter#>: <#description#>
      * - Returns: <#return value#>
      */
     ```
   - 选中这段代码并将其拖动到代码片段库中。
3. **设置代码片段属性**：
   - 在出现的弹窗中，给代码片段命名，并设置触发器（Completion Shortcut），例如 `commentblock`。
   - 选择适用的语言（Language），如 Swift 或 Objective-C。
   - 设置完成后，点击“完成”按钮。

#### 使用自定义代码片段
1. **输入触发器**：在代码编辑器中，输入你设置的触发器（如 `commentblock`）。
2. **触发代码片段**：按下 `Return` 键，Xcode 会自动插入你的自定义注释块。

### 4. 文档注释（Documentation Comment）
对于 Swift 和 Objective-C 代码，可以使用文档注释来生成带格式的注释，方便生成文档。

#### Swift 文档注释
- **快捷键**：`Option + Command + /`
- **效果**：在函数、类、属性等声明的上一行生成文档注释模板。

```swift
/// <#Description#>
/// - Parameters:
///   - <#parameter#>: <#description#>
/// - Returns: <#return value#>
func exampleFunction(parameter: Int) -> String {
    // Function implementation
}
```

#### Objective-C 文档注释
- **快捷键**：`Option + Command + /`
- **效果**：在方法或属性声明的上一行生成文档注释模板。

```objc
/**
 * <#Description#>
 * @param parameter <#description#>
 * @return <#return value#>
 */
- (NSString *)exampleMethodWithParameter:(NSInteger)parameter {
    // Method implementation
}
```

通过这些快捷键和技巧，你可以在 Xcode 中更高效地生成和管理注释块。

---

# Xcode包管理工具

## CocoaPods, SPM与Carthage

![[f7dd8aca06b241698df35f4d43b2b997.png]]



### SPM

https://www.jianshu.com/p/2f0d5794c7e2


---
# Instruments

## Time Profiler

Time Profiler
https://cloud.tencent.com/developer/article/1782272

---
# Xcode15新功能文档预览（可以实现预览markdown代码）

https://zhuanlan.zhihu.com/p/640931284


---

# 错误：`SDK does not contain 'libarclite' at the path '/Applications/Xcode15.0.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/lib/arc/libarclite_iphoneos.a'; try increasing the minimum deployment target`

解决方案：
https://blog.csdn.net/u013712343/article/details/134262640

找到文件路径，新建arc文件夹，下载:[https://github.com/kamyarelyasi/Libarclite-Files](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fkamyarelyasi%2FLibarclite-Files "https://github.com/kamyarelyasi/Libarclite-Files") 放入对应文件

---

# 断点调试

https://blog.csdn.net/yunfeihope/article/details/131853764

Xcode如何在库工程中打断点?

![[Pasted image 20240419164329.png]]



# 解决Xcode的模拟器无法启动的问题

https://www.cnblogs.com/ficow/p/18090763



# 使用FastLane自动打包
https://blog.csdn.net/long4512524/article/details/129733908