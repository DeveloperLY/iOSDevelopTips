## iOS 返回到任意界面（控制器）
### 一、根据指定的类名返回
```
for (UIViewController *controller in self.navigationController.viewControllers) {
	if ([controller isKindOfClass:[要返回的类名 class]]) {
		[self.navigationController popToViewController:controller animated:YES];
    }
}
```

### 二、根据栈的索引返回
```
NSArray *temArray = self.navigationController.viewControllers;
[self.navigationController popToViewController:[temArray objectAtIndex:1] animated:YES];
```

### 三、类似方式一
```
NSArray *temArray = self.navigationController.viewControllers;
LYTestVC *testVC = [[LYTestVC alloc] init];
for (UIViewController *temVC in temArray) {
	if([temVC isKindOfClass:[test class]]) {
   		[self.navigationController popToViewController:temVC animated:YES];
    }
 }
```