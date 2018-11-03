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

### 四、
```
AppDelegate *appDelegate = (AppDelegate *)[UIApplication sharedApplication].delegate;
if (appDelegate.window.rootViewController) 	appDelegate.window.rootViewController = nil;

LYTestVC *testVC = [[LYTestVC alloc]init];
appDelegate.window.rootViewController = [[LYNavigationController alloc] initWithRootViewController: testVC];

```

### 五、
```
LYTestVC * testVC = [[LYTestVC alloc] init];
[self.navigationController pushViewController: testVC animated:YES];
```

### 六、
```
// dissmiss 返回根部控制器
[self.presentingViewController.presentingViewController dismissViewControllerAnimated:NO completion:nil];
```

## 判断当前是否连接VPN
通过判断`tap` `tun` `ipsec` `ppp` 这些字段是否在`CFNetworkCopySystemProxySettings`里来判断`VPN`是否开启

代码：

```Obj-C
- (BOOL)isVPNOn { 
	BOOL flag = NO; 
	NSString *version = [UIDevice currentDevice].systemVersion; 
	// need two ways to judge this. 
	if (version.doubleValue >= 9.0) { 
		NSDictionary *dict = CFBridgingRelease(CFNetworkCopySystemProxySettings()); 
		NSArray *keys = [dict[@"__SCOPED__"] allKeys]; 
		for (NSString *key in keys) { 
			if ([key rangeOfString:@"tap"].location != NSNotFound || 
				[key rangeOfString:@"tun"].location != NSNotFound || 
				[key rangeOfString:@"ipsec"].location != NSNotFound || 
				[key rangeOfString:@"ppp"].location != NSNotFound) { 
				flag = YES; 
				break; 
			} 
		} 
	} else { 
		struct ifaddrs *interfaces = NULL; 
		struct ifaddrs *temp_addr = NULL; 
		int success = 0; 

		// retrieve the current interfaces - returns 0 on success 
		success = getifaddrs(&interfaces); 
		if (success == 0) { 
			// Loop through linked list of interfaces 
			temp_addr = interfaces; 
			while (temp_addr != NULL) {
				NSString *string = [NSString stringWithFormat:@"%s" , temp_addr->ifa_name]; 
				if ([string rangeOfString:@"tap"].location != NSNotFound || 
				 	[string rangeOfString:@"tun"].location != NSNotFound || 
				 	[string rangeOfString:@"ipsec"].location != NSNotFound || 
				 	[string rangeOfString:@"ppp"].location != NSNotFound) { 
				 	flag = YES; 
				 	break; 
				 } 
				 temp_addr = temp_addr->ifa_next; 
			} 
		} 

		// Free memory 
		freeifaddrs(interfaces); 
	} 
	return flag; 
}

```

这个是判断系统的`VPN`状态，还有一种是调起`vpnExtension`或着说`NEVPNManager`的时候的`vpn`状态可以通过实例化`NEVPNManager`，然后通过`manager.connection.status`来获取当前的`VPN`状态