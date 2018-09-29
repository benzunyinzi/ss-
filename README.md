# 一般的ss在终端设置代理：
export http_proxy=http://127.0.0.1:1080
export https_proxy=http://127.0.0.1:1080
这样是不起作用的。

# 原因是什么呢？
因为ss的代理是socks代理，而在goland之类的终端需要转成http才可以使用。
那么就需要一个工具进行转化，polipo。

# 安装过程如下：
brew install polipo
【如果过程中报关于xcode相关的错误，直接将xcode直接卸载】

vim ~/.polipo
编辑文件内容如下：
socksParentProxy = "127.0.0.1:1080"
socksProxyType = "socks5"
proxyAddress = "127.0.0.1"
proxyPort = 8123

开机启动：
ln -sfv /usr/local/opt/polipo/*.plist ~/Library/LaunchAgents/

加载：
launchctl load ~/Library/LaunchAgents/homebrew.mxcl.polipo.plist

Done,现在试试设置http代理,127.0.0.1 端口号 8123，看看能不能访问。
export http_proxy=http://127.0.0.1:8123
export https_proxy=http://127.0.0.1:8123

做个测试：
curl -I www.google.com
