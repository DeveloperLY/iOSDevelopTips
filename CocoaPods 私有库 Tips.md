# `CocoaPods`私有库`Tips` 

## 1.`pod lib lint` 和 `pod spec lint` 命令的区别
* `pod lib lint`是只从本地验证你的pod能否通过验证;
* `pod spec lint`是从本地和远程验证你的pod能否通过验证;

## 2.私有`pod`的验证
使用`pod spec lint`去验证私有库能否通过验证时应该要添加`--sources`选项，不然会出现找不到`repo`的错误:

```ruby
pod spec lint --sources='私有仓库repo地址,https://github.com/CocoaPods/Specs'
```

## 3.`subspec`
为了让自己的`Pod`被导入时显示出良好的文件层划分，`subspec`是必须的。
若`subspec`要依赖其它的`subspec`，则`subspec`的`dependency`后面接的不是目录路径，而是`specA/specB`这种`spec`关系；

## 4.私有库引用私有库的问题
在私有库引用了私有库的情况下，在验证和推送私有库的情况下都要加上所有的资源地址，不然`Pod`会默认从官方`repo`查询。

```ruby
pod spec lint --sources='私有仓库repo地址,https://github.com/CocoaPods/Specs'
pod repo push 本地repo名 podspec名 --sources='私有仓库repo地址,https://github.com/CocoaPods/Specs
```

## 5.引用自己或第三方的`framework`或`.a`文件时
在`podsepc`中应该这样写:

```ruby
s.ios.vendored_frameworks = "xxx/**/*.framework"
s.ios.vendored_libraries = "xxx/**/*.a”
```

## 6.引用静态库：`(.ios).library`。去掉头尾的`lib`，用”`,`”分割

```ruby
// 引用libxml2.lib和libz.lib.
spec.libraries =  'xml2', 'z'
```

## 7.引用公有framework：`(.ios).framework`. 用”`,`”分割. 去掉尾部的”`.framework`”

```ruby
spec.frameworks = 'UIKit','SystemConfiguration', 'Accelerate'
```

## 8.引用自己生成的framework：`(.ios).vendored_frameworks`。用”`,`”分割,路径写从`.podspec`所在目录为根目录的相对路径 ps:这个不要省略`.framework`

```ruby
spec.ios.vendored_frameworks = 'Pod/Assets/*.framework'
```

## 9.引用自己生成的`.a`文件, 添加到`Pod/Assets`文件夹里. Demo的Example文件夹里也需要添加一下, 不然找不到

```ruby
spec.ios.vendored_libraries = 'Pod/Assets/*.a'
```
在提交到私有仓库的时候需要加上`--use-libraries`
## 10.私有库中添加资源(图片、音视频等)
方法共有三种:

* 第一种

 ```ruby
 spec.resources = ["Images/*.png", "Sounds/*"]
 ```
但是这些资源会在打包的时候直接拷贝的`App`的`Bundle`中，这样说不定会和其它资源产生命名冲突；

* 第二种

 ```ruby
 spec.resource = "Resources/MyLibrary.bundle"
 ```
 把资源都放在`bundle`中，然后打包时候这个`bundle`会直接拷贝进`App`的`mainBundle`中。使用的时候在`mainBundle`中查找这个`bundle`然后再搜索具体资源:
 
 ```Objective-C
 NSURL *bundleURL = [[NSBundle mainBundle] URLForResource:@"MyLibrary" withExtension:@"bundle"];
  NSBundle *bundle = [NSBundle bundleWithURL:bundleURL];
  UIImage *imgage = [UIImage imageNamed:icon inBundle:bundle compatibleWithTraitCollection:nil];
 ```
 
* 第三种

 ```ruby
 spec.resource_bundles = {
		'MyLibrary' => ['Resources/*.png'],
	 	'OtherResources' => ['OtherResources/*.png']
 }
 ```
 
 这种方法利用`framework`的命名空间，有效防止了资源冲突。
使用方法是先拿到最外面的`bundle`，然后再去找下面指定名字的`bundle` 对象，再搜索具体资源:

 ```Objective-C
 NSBundle *bundle = [NSBundle bundleForClass:[self class]];
NSURL *bundleURL = [bundle URLForResource:@"MyLibrary" withExtension:@"bundle"];
NSBundle *resourceBundle = [NSBundle bundleWithURL: bundleURL];
UIImage *imgage = [UIImage imageNamed:icon inBundle:resourceBundle compatibleWithTraitCollection:nil];
 ```
 
## 11.如果私有库添加了静态库或者`dependency`用了静态库
那么执行`pod lib lint`还有`pod spec lint`时候需要加上`—user-libraries`选项,否则会出现`'The 'Pods' target has transitive dependencies`错误

## 12.如果私有库只引用其他库的`subspec`
只需要依赖想依赖的`subspec`，不用管主`spec`（因为依赖`subspec`必然要依赖主`spec`）

## 13.私有库已经通过验证并传到私有`repo`也能通过`pod search`，但是就是`pod install`失败
这时候只要执行`pod update`

## 14.提交到私有仓库的之前可以先验证一下, 有问题就修复它, 验证过了在提交

```ruby
pod spec lint VenderName.podspec --verbose
```
打好`tag`, 推到`Git`里去后, 才可以在测试的项目里的`Podfile`里引用这个库, 然后`pod update VenderName --no-repo-update`, 测试通过了, 在提交到私有仓库里

```ruby
pod 'VenderName', :podspec => 'VenderName.podspec的路径地址'
```

还可以指定引用某个分支的代码

```ruby
pod 'VenderName', :git => 'https://coding.net/CodingZero/VenderName.git', :branch => 'develop'
```

提交到私有仓库的时候还可以忽略警告类的错误, 愣是要提交. 在后面加上`--allow-warnings`

```ruby
pod repo push LYSpecs VenderName.podspec --allow-warnings
```
如果有添加新的文件, 需要更新下引索, `Demo`里才可以识别

```ruby
pod update VenderName --no-repo-update
```

## 15.使用的时候还可以通过直接指定地址 + `tag` or `分支` or `commit` 的方式来引入, 这样就可以不用走发布流程了. 也不需要添加源了.

```ruby
pod 'VenderName', :git => 'https://coding.net/CodingZero/VenderName.git', :tag => '0.8.1'

pod 'VenderName', :git => 'https://coding.net/CodingZero/VenderName.git', :branch => 'develop'

pod 'VenderName', :git => 'https://coding.net/CodingZero/VenderName.git', :commit => '0812fe81319af2411233'
```