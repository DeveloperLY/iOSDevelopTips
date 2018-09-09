# 小技巧
* 视频提取音频（需要安装`ffmpeg `） `ffmpeg -i input.avi -b:a 128k output.mp3`

* 如何对NSMutableArray进行KVO
	官方为我们提供了这个方法
	`(NSMutableArray *)mutableArrayValueForKey:(NSString *)key`
 eg:
 
 ```
  // myltems是我们要进行KVO的一 个属性，它的定义如下：
	@property (nonatomic, strong) NSMutableArray *myltems;
 // 在它进行添加元素时，使用如下方法：
[[self mutableArrayValueForKey:@"myltems"] addObject:item];
```
 这样，便实现了对 NSMutableArray 的 KV0 .
 
* 两点之间的距离

 ```
 static __inline__ CGFloat CGPointDistanceBetweenTwoPoints(CGPoint point1, CGPoint point2) { 
 	CGFloat dx = point2.x - point1.x; 
 	CGFloat dy = point2.y - point1.y; 
 	return sqrt(dx*dx + dy*dy);
 }
 ```
 
* `UITableView`的`Group`样式下顶部空白处理

 ```
 // 分组列表头部空白处理
 UIView *view = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 0, 0.1)];
 self.tableView.tableHeaderView = view;
 
 ```

* 模态推出透明界面

 ```
 UIViewController *vc = [[UIViewController alloc] init]; 
 UINavigationController *na = [[UINavigationController alloc] initWithRootViewController:vc]; 
 if ([[[UIDevice currentDevice] systemVersion] floatValue] >= 8.0) { 
 na.modalPresentationStyle = UIModalPresentationOverCurrentContext; 
 } else { 
self.modalPresentationStyle = UIModalPresentationCurrentContext; 
} 
[self presentViewController:na animated:YES completion:nil];
 ```
 
* 打印全 NSLog 日志输出

 ```
 #define NSLog( s, ... ) printf("[ %s:(%d) ] %s :%s\n", [[[NSString stringWithUTF8String:__FILE__] lastPathComponent] UTF8String], __LINE__, __PRETTY_FUNCTION__, [[NSString stringWithFormat:(s), ##__VA_ARGS__] UTF8String])
 ```