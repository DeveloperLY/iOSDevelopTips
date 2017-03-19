# CocoaPods
-- 
## 小技巧一：
在团队开发中，由于团队成员使用的是不同的`cocoapods gem`的安装版本，当有成员执行`pod install`命令时，其他成员更新代码就会报错。

解决方案：使用`Gemfile`指定`cocoapods gem`的使用版本

```ruby
	ruby
	source 'https://rubygems.org' # 在大天朝使用'https://gems.ruby-china.org'
	gem 'cocoapods', '1.2.0'
```
当更新了`Gemfile`文件并且自动安装了正确的`gem`后，确保团队每个成员都运行一次`bundle install`。

此后，只需要运行`bundle exec pod install`命令安装新的`CocoaPods`--这将会通过`Gemfile`文件中指定`cocoapods gem`的版本安装`pods`。