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
* 添加私有仓库

 ```ruby
 pod repo add LYSpecs https://git.coding.net/CodingZero/LYSpecs.git
 ```
 
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
