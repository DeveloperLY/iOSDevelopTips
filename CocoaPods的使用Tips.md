# CocoaPods 的使用Tips
-- 
## 问题1：
在团队开发中，由于团队成员使用的是不同的`cocoapods gem`的安装版本，当有成员执行`pod install`命令时，其他成员更新代码就会报错。

解决方案：使用`Gemfile`指定`cocoapods gem`的使用版本

```ruby
	ruby
	source 'https://rubygems.org' # 在大天朝使用'https://gems.ruby-china.org'
	gem 'cocoapods', '1.2.0'
```
当更新了`Gemfile`文件并且自动安装了正确的`gem`后，确保团队每个成员都运行一次`bundle install`。

此后，只需要运行`bundle exec pod install`命令安装新的`CocoaPods`--这将会通过`Gemfile`文件中指定`cocoapods gem`的版本安装`pods`。

## 问题2：
ERROR: While executing gem ... (Gem::Exception) Unable to require openssl, install OpenSSL and rebuild ruby (preferred) or use non-HTTPS sources

```ruby
	sudo gem update --system -n/usr/local/bin
	sudo gem install -n /usr/local/bin cocoapods
	pod setup
```

## 问题3：
编译出现找不到`libPods.a`
在`Build Setting` > `Other Linker Flag`:
将所有`$(TARGET_BUILD_DIR)` 改成 `$(BUILT_PRODUCTS_DIR)`即可

## 问题4：
出现`error: RPC failed; result=52, HTTP code = 0`

```ruby
更新pod:
$ pod setup
更新gem到最新版本：
$ sudo gem update --system 
检查ping到github：
$ ping github.com
查看pob repo list：
$ pod repo list
结果显示0 repos，说明没有安装成功；
删除.cocoapods目录，重新下载pod更新：
$ cd ~/.cocoapods/
$ sudo -rm -rf ~/.cocoapods/
重新执行 $ pod setup

现在pod intall指令就能用啦
```

## 问题5：
报错: [!] Unable to add a source with url `https://github.com/CocoaPods/Specs.git` named `master-1`.
You can try adding it manually in `~/.cocoapods/repos` or via `pod repo add`.

解决方法：这是因为电脑里安装了另外一个Xcode导致cocoapods找不到路径了
在终端执行 `sudo xcode-select -switch /Applications/Xcode.app` 即可


# Tips
## CocoaPods：在多target中安装相同pod的优雅解决方案

```ruby
# Podfile

platform :ios, '9.0'

use_frameworks!

# My other pods

def testing_pods
    pod 'Quick', '0.5.0'
    pod 'Nimble', '2.0.0-rc.1'
end

target 'MyTests' do
    testing_pods
end

target 'MyUITests' do
    testing_pods
end
```
