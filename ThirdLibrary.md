# iOS开发中常用的库整理
## App框架
* [Nimbus](https://github.com/jverkoey/nimbus) 是一个开源的iOS框架，比起Three20，Nimbus的文档更为全面、丰富，能够实现很多非常炫的界面特效。因此，开发者可以借助Nimbus来降低项目设计的复杂度。
* [ReactiveCocoa](https://github.com/ReactiveCocoa/ReactiveCocoa) 受函数响应式编程激发。不同于使用可变的变量替换和就地修改，RAC提供Signals来捕获当前值和将来值。
* [samurai-native](https://github.com/hackers-painters/samurai-native) 是一个基于浏览器内核通过HTML+CSS 开发原生移动应用的iOS框架。
* [AsyncDisplayKit](https://github.com/facebook/AsyncDisplayKit) 异步界面渲染库,为极限优化View效果而生（同时提供 UIView bridge 接口） Smooth asynchronous user interfaces for iOS apps.

---

## UI相关
* [Material-Controls-For-iOS](https://github.com/fpt-software/Material-Controls-For-iOS) Many Google Material Design Controls for iOS native application
* [MJRefresh](https://github.com/CoderMJLee/MJRefresh) 仅需一行代码就可以为UITableView或者CollectionView加上下拉刷新或者上拉刷新功能。可以自定义上下拉刷新的文字说明。
* [XHRefreshControl](https://github.com/xhzengAIB/XHRefreshControl) 是一款高扩展性、低耦合度的下拉刷新、上提加载更多的组件。
* [YFStartView](https://github.com/yeziahehe/YFStartView) 动态的启动图
* [MBProgressHUD](https://github.com/jdg/MBProgressHUD) 非常赞 最多人用的loading。
* [SVProgressHUD](https://github.com/SVProgressHUD/SVProgressHUD) 非常赞 SVProgressHUD的loading，如果你需要定制化的等待提示器，这个就是了（也许是最好的）。
* [Toast](https://github.com/scalessec/Toast) An Objective-C category that adds toast notifications to the UIView object class.
* [REMenu](https://github.com/romaonthego/REMenu) 一个效果很好的弹出下拉框
* [iCarousel](https://github.com/nicklockwood/iCarousel) 旋转木马多种效果滚动图
* [CoreLock](https://github.com/CharlinFeng/CoreLock) 高仿支付宝解锁
* [IQKeyboardManager](https://github.com/hackiftekhar/IQKeyboardManager) 键盘遮挡解决方案，处理键盘事件强大的库，有OC和Swift版本，纯代码、Storyboard和Xib都适用。
* [JMHoledView](https://github.com/leverdeterre/JMHoledView) 用户第一次使用时，高亮显示某一部分，用于应用页面的某些强调说明（引导图层）
* [DZNEmptyDataSet](https://github.com/dzenbot/DZNEmptyDataSet) 非常赞 DZNEmptyDataSet算是一个很标准的iOS内建方式，适合用来处理空的tableview和collection view。会自动将collection view处理完善，并将用户消息以合适美观的方式显示出来。每个iOS项目都可以自动处理。
* [MMDrawerController](https://github.com/mutualmobile/MMDrawerController) 是个非常利于集成的左右侧滑动选择栏
* [GLCalendarView](http://tech.glowing.com/cn/glcalendarview-a-fully-customizable-date-range-picker/) GLOW团队开源的 GLCalendarView 日历
* [GDPerformanceView](https://github.com/dani-gavrilov/GDPerformanceView-Swift) 可以查看FPS、CPU使用率
* [LazyScrollView](https://github.com/alibaba/LazyScrollView) iOS 高性能异构滚动视图构建方案
* [JSQMessagesViewController](https://github.com/jessesquires/JSQMessagesViewController) 一个优秀的即时聊天UI库
* [HYNavBarHidden](https://github.com/HelloYeah/HYNavBarHidden) 导航条滚动透明，超简单好用的监听滚动,导航条渐隐的UI效果实现。
* [BLKFlexibleHeightBar](https://github.com/bryankeller/BLKFlexibleHeightBar) 是一个使导航栏高度可以动态变化的 UI 库。固定Header的效果库，一个拥有非常灵活高度的标题栏，可以为使用软件的用户提供更多的阅读和滑动空间，现在已经被众多app所采用。
* [EasyTipView](https://github.com/teodorpatras/EasyTipView) 弹出提示框类及演示示例。同样地，API 简单、易用。
* [PPCounter](https://github.com/jkpang/PPCounter) 一款简单实用的数字加减动画,支持UILabel、UIButton显示
* [PYSearch](https://github.com/iphone5solo/PYSearch) An elegant search controller for iOS.
* [SDCycleScrollView](https://github.com/gsdios/SDCycleScrollView) 无限循环自动图片轮播器(一步设置即可使用)。

---

## AutoLayout
* [Masonry](https://github.com/SnapKit/Masonry) 是一个轻量级的布局框架，拥有自己的描述语法，采用更优雅的链式语法封装自动布局，简洁明了并具有高可读性
* [PureLayout](https://github.com/PureLayout/PureLayout) 是 iOS & OS X Auto Layout 的终极 API——非常简单，又非常强大。PureLayout 通过一个全面的Auto Layout API 扩展了 UIView/NSView, NSArray 和 NSLayoutConstraint，仿照苹果自身的框架。
* [UITableView-FDTemplateLayoutCell](https://github.com/forkingdog/UITableView-FDTemplateLayoutCell) 是一个方便缓存 UITableViewCell 的高度的框架。
* [UIView-FDCollapsibleConstraints](https://github.com/forkingdog/UIView-FDCollapsibleConstraints) 一个AutoLayout辅助工具，最优雅的方式解决自动布局中子View的动态显示和隐藏的问题。第二个Demo模拟了一个经典的FlowLayout，任意一个元素隐藏时，底下的元素需要自动“顶”上来，配合这个扩展，你可以在IB里连一连，选一选，不用一行代码就能搞定。
* [SDAutoLayout](https://github.com/gsdios/SDAutoLayout) 一行代码搞定自动布局！支持Cell、Label和Tableview高度自适应，致力于做最简单易用的AutoLayout库。

---

## 网络相关
* [AFNetworking](https://github.com/AFNetworking/AFNetworking) ASI不升级以后，最多人用的网络连接开源库。
* [YTKNetwork](https://github.com/yuantiku/YTKNetwork) 是基于 AFNetworking 封装的 iOS网络库，提供了更高层次的网络访问抽象。相比AFNetworking，YTKNetwork提供了以下更高级的功能：按时间或版本号缓存网络请求内容、检查返回 JSON 内容的合法性、文件的断点续传、批量的网络请求发送、filter和插件机制等。
* [SDWebImage](https://github.com/rs/SDWebImage) 网络图片获取及缓存处理。
* [UIActivityIndicator-for-SDWebImage](https://github.com/JJSaccolo/UIActivityIndicator-for-SDWebImage) 为SDWebImage显示加载效果。
* [YYWebImage](https://github.com/ibireme/YYWebImage) 一个图片加载库，支持 APNG、WebP、GIF 播放，支持渐进式图片加载，更高性能的缓存，更多图像处理方法，可以替代 SDWebImage 等开源库。
* [CocoaAsyncSocket](https://github.com/robbiehanson/CocoaAsyncSocket) 在iOS开发中使用socket，一般都是用这个第三方库。

---

## 数据处理相关
* [MJExtension](https://github.com/CoderMJLee/MJExtension) 用于json转model进行使用，转换效率很高，使用也比较简单，只要前后台约定好，json直接就转成了model。
* [YYModel](https://github.com/ibireme/YYModel) High performance model framework for iOS/OSX.
* [FMDB](https://github.com/ccgus/fmdb) sqlite的工具，通过 fmdb 进行的数据库的 基本操作(增删改查 )查找是使用 UISearchBar 和UISearchDisplayController 进行混合使用。
* [RealmObjectEditor ](https://realm.io/docs/objc/latest/#getting-started) Realm Object Editor is a visual editor where you can create your Realm entities, attributes and relationships inside a nice user interface. Once you finish, you can save your schema document for later use and you can export your entities in Swift, Objective-C and Java.

---

## 富文本
* [YYText](https://github.com/ibireme/YYText) 兼容 UILabel 和 UITextView 的 API，支持异步排版与渲染、图文混排、自定义点击样式、自定义键盘、表情解析与输入、图片复制粘贴、容器形状控制、竖排版、文本变形、Markdown 等等功能，能够实现微博微信QQ等应用的全部文本需求。
* [Shimmer](https://github.com/facebook/Shimmer) BlingBling闪光效果，酷炫的Label的效果，可以用于加载等待提示。
* [TTTAttributedLabel](https://github.com/TTTAttributedLabel/TTTAttributedLabel) 一个文字视图开源组件，是UILabel的替代元件，可以以简单的方式展现渲染的属性字符串。另外，还支持链接植入，不管是手动还是使用UIDataDetectorTypes自动把电话号码、事件、地址以及其他信息变成链接。[用TTTAttributedLabel创建变化丰富的UILabel](http://blog.csdn.net/prevention/article/details/9998575) - 网易新闻iOS版使用。
* [MLEmojiLabel](https://github.com/molon/MLEmojiLabel) 自动识别网址、号码、邮箱、@、#话题#和表情的label。可以自定义自己的表情识别正则，和对应的表情图像。(默认是识别微信的表情符号)，继承自TTTAttributedLabel，所以可以像label一样使用。label的特性全都有，使用起来更友好更方便。
* [MarkdownTextView](https://github.com/indragiek/MarkdownTextView) 显示Markdown的TextView。
* [WordPress-Editor-iOS](https://github.com/wordpress-mobile/WordPress-Editor-iOS) 一个文本编辑器 简书和新浪博客都在用。


---

## 图表
* [PNChart](https://github.com/kevinzhow/PNChart) 动态的图表。
* [YOChartImageKit](https://github.com/yasuoza/YOChartImageKit) 支持在watchOS上绘制图表。


---

## 主题
* [LEETheme](https://github.com/lixiang1994/LEETheme) 优雅的主题管理库- 一行代码完成多样式切换。

---

## 综合
* [YYKit](https://github.com/ibireme/YYKit) 是一组功能丰富的 iOS 组件，用于构建大型、复杂的 iOS 应用