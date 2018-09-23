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
* 快速定位使用`Masonry`布局时出现的约束警告
	* 把`View`的内存地址换成了具体的`View`，其实我们可以通过`Xcode`中的`【Debug View Hierarchy】`，根据约束警告的内存地址（比如：`0x147f56930`）找到内存地址对应的`View()`，把内存地址粘贴到搜索框，然后一样做替换操作，即可解决约束警告。
	* 使用`Masonry`自带的`MASAttachKeys`宏来给`View`添加`key`,然后有约束警告的话就会知道具体哪个`View`布局有问题。
	
	```
	UIButton *btn1 = [UIButton buttonWithType:UIButtonTypeCustom ]; 
	btn1.backgroundColor = [UIColor redColor];
	 MASAttachKeys(btn1); // Masonry 布局冲突快速定位，设置key必须在布局之前设置，否则无效！ 
	 [self.view addSubview:btn1]; 
	 [btn1 mas_makeConstraints:^(MASConstraintMaker *make) { 
	 make.left.top.offset(80); 
	 make.size.mas_equalTo(CGSizeMake(100, 100)); 
	 }]; 
	 // 制造约束冲突 
	 [btn1 mas_makeConstraints:^(MASConstraintMaker *make) { 
	 make.left.top.offset(100); 
	 make.size.mas_equalTo(CGSizeMake(100, 100)); 
	 }];

	```
	
* 实现控件周边的发散阴影

 ```
 UIImageView *image = [UIImageView new]; 
 image.frame = CGRectMake(100, 100, 300, 300);
 [self.view addSubview:image]; 
 self.image = image; 
 image.center = self.view.center; 
 image.image = [UIImage imageNamed:@"test.jpg"]; 
 
 // image.layer.cornerRadius = 15; 
 //偏移距离
 image.layer.shadowOffset = CGSizeMake(5, 5); 
 //透明度 
 image.layer.shadowOpacity = 0.8; 
 //阴影颜色 
 image.layer.shadowColor = [UIColor lightGrayColor].CGColor; 
 //阴影半径 
 image.layer.shadowRadius = 30; 
 UIBezierPath * path = [UIBezierPath bezierPathWithRoundedRect:CGRectMake(-20,-20, image.frame.size.width + 40, image.frame.size.height + 40) cornerRadius:1.0]; 
 //阴影路径 
 image.layer.shadowPath = path.CGPath;
 ```