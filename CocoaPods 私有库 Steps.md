# `CocoaPods`私有库`Steps` 

## 1.创建私有仓库
先`coding.net`、`OSChina`、`GitHub`或者自己搭建的`Git`服务器上创建一个私有仓库，然后在本地添加仓库

```ruby
pod repo add LYSpecs https://coding.net/CodingZero/LYSpecs.git
```

## 2.创建私有库
创建私有库模板

```ruby
pod lib create VenderName
```

创建模板的时候会问你要用什么语言(Swift/Objective-C), 要不要自带测试框架,使用前缀等.

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
 pod repo push PHSpecs VenderName.podspec --allow-warnings --verbose
// --allow-warnings : 允许 警告，有一些警告是代码自身带的。
// --use-libraries  : 私有库、静态库引用的时候加上
// —verbose ： lint显示详情
 ```
 
## 4.使用私有库
* 添加私有仓库

 ```ruby
 pod repo add LYSpecs https://coding.net/CodingZero/LYSpecs.git
 ```
 
* 用的时候需要在`Podfile`里添加源

 ```ruby
 // GitHub地址
source 'https://github.com/CocoaPods/Specs.git'
# ...相关库
// 私有库地址
source 'https://coding.net/CodingZero/LYSpecs.git'
# ...私有库
 ```
 
* 用的时候在Podfile里引用

 ```ruby
 pod 'VenderName'
 ```
