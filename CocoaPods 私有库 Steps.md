# `CocoaPods`私有库`Steps` 

## 1.创建私有仓库
先`coding.net`、`OSChina`、`GitHub`或者自己搭建的`Git`服务器上创建一个私有仓库，然后在本地添加仓库

```ruby
pod repo add LYSpecs https://git.coding.net/CodingZero/LYSpecs.git
```

## 2.创建私有库
创建私有库模板

```ruby
pod lib create VenderName
```

* 第一个问题是问你选择`Swift`还是`Objc`构建项目。`eg: ObjC `

 ```ruby
hat language do you want to use?? [ Swift / ObjC ]
 > ObjC
 ```
* 第二个问题问你是否需要创建一个Demo项目`eg: Yes`

 ```ruby
Would you like to include a demo application with your library? [ Yes / No ]
 > Yes
 ```
* 第三个问题让你是否选择一个测试框架`eg: None`

 ```ruby
 Which testing frameworks will you use? [ Specta / Kiwi / None ]
 > None
 ```
* 第四个问题是否基于View测试`eg: No`

 ```ruby
 Would you like to do view based testing? [ Yes / No ]
 > No
 ```
 
* 第五个问题是询问 类的前缀`eg: LY`
 
  ```ruby
  What is your class prefix?
 > LY
  ```

## 3.更新发布私有库
* 提交代码
 
 ```ruby
 git add -A && git commit -m "Release 1.0.0"
 ```
 
* 打`tag`
 
 ```ruby
 git tag '1.0.0'
 ```

* 把`tag`推到远程仓库

 ```ruby
 git push --tags
 ```
 
* 将本地的`master`分支推送到远程仓库

 ```ruby
 git push origin master
 ```
 
* 提交到私有仓库

 ```ruby
 pod repo push LYSpecs VenderName.podspec --allow-warnings --verbose
// --allow-warnings : 允许 警告，有一些警告是代码自身带的。
// --use-libraries  : 私有库、静态库引用的时候加上
// —verbose ： lint显示详情
 ```
 
## 4.使用私有库
* 用的时候需要在`Podfile`里添加源

 ```ruby
 // GitHub地址
source 'https://github.com/CocoaPods/Specs.git'
# ...相关库
// 私有库地址
source 'https://git.coding.net/CodingZero/LYSpecs.git'
# ...私有库
 ```
 
* 用的时候在Podfile里引用

 ```ruby
 pod 'VenderName'
 ```
 
* 开发模式下测试Pod库的代码

 ```ruby
 pod 'VenderName', :path => '../' # 指定路径
 ```
 然后在Example工程目录下执行`pod update`命令安装依赖，打开项目工程，可以看到库文件都被加载到`Pods`子项目中了
不过它们并没有在`Pods`目录下，而是跟测试项目一样存在于`Development Pods/VenderName `中，这是因为我们是在本地测试，而没有把`podspec`文件添加到`Spec Repo`中的缘故。

## 5.`podspec`文件配置说明

```ruby
#
# Be sure to run `pod lib lint VenderName.podspec' to ensure this is a
# valid spec before submitting.
#
# Any lines starting with a # are optional, but their use is encouraged
# To learn more about a Podspec see http://guides.cocoapods.org/syntax/podspec.html
#

Pod::Spec.new do |s|
  #名称
  s.name             = 'VenderName'
  #版本号
  s.version          = '0.1.0'
  #简介
  s.summary          = '这个是我的私有库项目Demo.'

# This description is used to generate tags and improve search results.
#   * Think: What does it do? Why did you write it? What is the focus?
#   * Try to keep it short, snappy and to the point.
#   * Write the description between the DESC delimiters below.
#   * Finally, don't worry about the indent, CocoaPods strips it!

  s.description      = <<-DESC
  这个是教程的 私有库项目 学习Demo. （主要：比s.ummary要长）
                       DESC
  #主页,这里要填写可以访问到的地址，不然验证不通过
  s.homepage         = 'https://coding.net/CodingZero/VenderName'

  # s.screenshots     = 'www.example.com/screenshots_1', 'www.example.com/screenshots_2'

  #开源协议

  s.license          =   { :type => 'MIT', :file => 'LICENSE' }

  #作者
  s.author           = { 'DeveloperLY' => 'coderyliu@gmail.com' }

  #项目地址，这里不支持ssh的地址，验证不通过，只支持HTTP和HTTPS，最好使用HTTPS。
  #这里的s.source须指向存放源代码的链接地址，而不是托管spec文件的repo地址
  s.source           = { :git => 'https://coding.net/CodingZero/VenderName.git', :tag => "0.1.0" }

  #s.social_media_url = 'http://weibo.com/lycoder'

  #支持的平台及版本
  s.ios.deployment_target = '7.0'

  #代码源文件地址，**/*表示Classes目录及其子目录下所有文件，如果有多个目录下则
  #用逗号分开，如果需要在项目中分组显示，这里也要做相应的设置

  s.source_files = "VenderName/Classes/**/*"

  #资源文件地址
  # s.resource_bundles = {
  #   'MyLib' => ['VenderName/Assets/*.png']
  # }

  #公开头文件地址
  #s.public_header_files = 'VenderName/Classes/**/*.h'

  #所需的framework，多个用逗号隔开
  s.frameworks = 'UIKit'

  #依赖关系，该项目所依赖的其他库，如果有多个需要填写多个s.dependency
  # s.dependency 'AFNetworking', '~> 2.3'
end
```