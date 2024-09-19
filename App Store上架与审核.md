# app一直卡在正在等待审核

案例：
https://www.jianshu.com/p/8d894380eb6e
https://www.jianshu.com/p/8d894380eb6e

可能的原因：

info-list的隐私描述不完整

申诉： [developer.apple.com/contact/cn/](http://developer.apple.com/contact/cn/)
![[Pasted image 20240415100209.png]]


---

# 什么是马甲包

马甲包又称之为APP分身、影子APP、APP矩阵，是APP主包的克隆版，安卓应用市场和App Store都有马甲APP的身影。通常马甲APP在应用名称、副标题、icon、应用截图、包名、Bundle ID、关键词、开发者账号等方面与主APP不一样。

https://zhuanlan.zhihu.com/p/62725375

[Your app transfer request was accepted.](message:%3C318191746.88703564.1714571513044@email.apple.com%3E)


---

# APPStore新规 privacyInfo

要求开发者报告使用的SDK有没有收集用户信息

编写xcprivacy：
https://juejin.cn/post/7360928627631931418

隐私清单生成：
https://wemakeapps.net/manifest-maker

介绍：
https://zhuanlan.zhihu.com/p/649662474


----

# Xcode上传appStore时要求验证

退出Xcode重新登陆即可


---
# ITMS-90714
Xcode打包上传到appStoreConnect后显示：
ITMS-90714:Invalid binary- The app containsone or more corrupted binaries. Please rebuildthe app and resubmit.

移除 `Other Linker Flag / -Xlinker -interposable` 

来源：
https://forums.developer.apple.com/forums/thread/751400

