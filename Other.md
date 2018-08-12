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