1.python环境
ubuntu16.04自带python的环境，不用进行python环境安装，在安装好环境的虚拟机中，提供了py2,py3,django_py2,tornado_py2,spider_py2,django_py3的虚拟环境

虚拟环境
升级python包管理工具pip
pip install --upgrade pip
备注：当你想升级一个包的时候 pip install --upgrade 包名
python虚拟环境安装
sudo apt-get install python-virtualenv
sudo easy_install virtualenvwrapper
上述工具装好后找不到mkvirtualenv命令，需要执行以下环境变量设置。
创建目录用来存放虚拟环境
mkdir $HOME/.virtualenvs
在~/.bashrc中添加行：
export WORKON_HOME=$HOME/.virtualenvs
source /usr/local/bin/virtualenvwrapper.sh
运行:
source ~/.bashrc
创建python虚拟环境
mkvirtualenv [虚拟环境名称]
workon [虚拟环境名称]
退出虚拟环境
deactivate
删除(慎用)
rmvirtualenv [虚拟环境名称]
python 2版本开发
创建python2的虚拟开发环境

mkvirtualenv -p /usr/bin/python2.7 py2
使用python2.7+django1.7.8环境，你应该安装如下环境：
(py2)python@ubuntu:~$ pip freeze list
pip==8.1.0
Django==1.7.8
ipdb==0.8.1
ipython==3.2.0
Pillow==2.8.2
把以上包名存储到package_py2.txt，在你的python虚拟环境中，运行:

pip install -r package_py2.txt
python 3版本开发 我们的课程基于Python2.7，因为很多第三方库还没有过度到python3系列。 创建python3的虚拟开发环境
mkvirtualenv -p /usr/bin/python3.4 py3
使用python3.4+django1.9.4环境，你应该安装如下环境：
(py3)python@ubuntu:~$ pip freeze list
pip==8.1.0
Django==1.9.4
ipdb==0.8.1
ipython==4.1.2
Pillow==2.8.2
把以上包名存储到package_py3.txt，在你的python虚拟环境中，运行:
pip install -r package_py3.txt
pip命令速查 查看已安装的包
pip show --files SomePackage
检查哪些包需要更新
pip list --outdated
升级包
pip install --upgrade SomePackage
卸载包
pip uninstall SomePackage
参数解释
pip --help


2.基础组件包安装
在我们提供的虚拟机中，都安装过了

mysql安装
sudo apt-get install mysql-server
sudo apt-get install libmysqlclient-dev
注意安装server端的时候会提示输入密码，记住这个密码。然后通过命令登入数据库，如图： !

redis安装
sudo apt-get install redis-server
通过redis-cli登入

mongoDB安装
详情请参考 http://blog.csdn.net/zgf19930504/article/details/52045600

postgresql安装
sudo apt-get install postgresql
sudo apt-get install libpq-dev
elasticsearch安装(django项目使用)
sudo apt-get install elasticsearch
其它依赖包
sudo apt-get install python-dev


3.django环境安装
我们将虚拟环境所需的包全部放在install.txt,以下是django_py3项目所需环境：

django==1.7.4
jsonfield
Pillow==2.8.2
celery
amqp==1.4.9
anyjson==0.3.3
billiard==3.3.0.23
celery==3.1.23
decorator==4.0.10
Django==1.7.8
django-haystack==2.5.0
django-redis-sessions==0.5.6
ipdb==0.8.1
ipython-genutils==0.1.0
jsonfield==1.0.3
kombu==3.0.35
psycopg2==2.6.2
pytz==2016.6.1
redis==2.10.5
setuptools==25.1.0
wheel==0.29.0
执行pip3 install -r instal.txt命令即可


4.tornado环境安装
在tornado_py2虚拟环境中安装：

ipython==4.2.0
ipython-genutils==0.1.0
pingpp==2.0.11
pycrypto==2.6.1
qiniu==7.0.7
redis==2.10.5
requests==2.10.0
tornado==4.3
MySQL-python==1.2.5
SQLAlchemy==1.0.14


5.spider环境安装
在spider_py2虚拟环境中安装：

attrs==16.0.0
backports-abc==0.4
backports.ssl-match-hostname==3.5.0.1
BeautifulSoup==3.2.1
beautifulsoup4==4.4.1
boto==2.38.0
certifi==2016.2.28
cffi==1.7.0
chardet==2.3.0
CherryPy==3.5.0
click==6.6
cryptography==1.4
cssselect==0.9.2
cssutils==1.0
Cython==0.24
decorator==4.0.6
Django==1.8.7
dnspython==1.12.0
easydict==1.6
enum34==1.1.6
feedparser==5.1.3
greenlet==0.4.10
html5lib==0.999
idna==2.1
ipaddress==1.0.16
ipython==2.4.1
jieba==0.38
jsonpath==0.54
lxml==3.5.0
Markdown==2.6.6
mechanize==0.2.5
motor==0.2
motorengine==0.9.0
mysqlclient==1.3.7
ndg-httpsclient==0.4.0
netifaces==0.10.4
nltk==3.2.1
parsel==1.0.2
pbr==1.9.1
pexpect==4.0.1
Pillow==3.3.0
pip==8.1.2
pkg-resources==0.0.0
poster==0.8.1
ptyprocess==0.5
pyasn1==0.1.9
pyasn1-modules==0.0.8
pybloomfilter==1.0
pybloomfiltermmap==0.3.12
pycparser==2.14
pycrypto==2.6.1
PyDispatcher==2.0.5
Pygments==2.1
pymongo==2.7
pyOpenSSL==16.0.0
python-dateutil==2.4.2
pytz==2014.10
PyYAML==3.11
queuelib==1.4.2
redis==2.10.5
repoze.lru==0.6
requests==2.10.0
Routes==2.2
rq==0.6.0
Scrapy==1.1.0
scrapy-redis==0.6.3
scrapyd==1.1.0
scrapyd-client==1.0.1
selenium==2.53.6
service-identity==16.0.0
setuptools==25.1.0
simplegeneric==0.8.1
singledispatch==3.4.0.3
six==1.10.0
sqlparse==0.1.18
stevedore==1.13.0
tornado==4.3
Twisted==16.2.0
urllib3==1.13.1
w3lib==1.14.2
WebOb==1.5.1
wheel==0.29.0
zope.interface==4.2.0




sublime text安装
进入提供的相关环境sublime Text目录，点击运行
调出installpackage界面
ctrl + shift + p
install package
常用工具包
AdvancedNewFile
Djaneiro
Emmet
less
sass
Git
Side Bar
HTML/CSS/JS Prettify
Python PEP8 Autoformat
SublimeCodeIntel
ColorPicker
OmniMarkupPreviewer
常用包使用说明
AdvancedNewFile 可以创建文件，也可以连目录和文件都创建 win+alt+n
Djaneiro django一些语法快速补齐功能，参考如下 https://packagecontrol.io/packages/Djaneiro
Emmet 快速缩写html,tab补齐,
代码简写扩展神器 ul#test>li*4 Ctrl+e展开上述指令
html:5    补齐html
p.foo     补齐class
p#foo     补齐id
>         子元素符号，表示嵌套的元素
+         同级标签符号
^         可以使该符号前的标签提升一行
Git 集成git ctrl+shift+p 输入git
Side Bar 折叠目录树 ctrl+k ctrl+b
HTML/CSS/JS Prettify 格式化代码 鼠标右键，从里面选
Python PEP8 Autoformat 格式化python代码 ctrl+shift+r
SublimeCodeIntel 自动匹配补全代码 ctrl+f3 调到变量定义的地方
ColorPicker 屏幕拾色器 ctrl+shift+c
ConvertToUTF8 直接在菜单栏中可以转，专为中文设计


在Ubuntu内安装软件，我们需要连接 Internet互联网！2.如果安装软件失败： 更换网易等国内服务器源： 设置 - 软件更新 - 更新管理器设置 - 选择上面的Ubuntu软件 – 点击下载自: 选择其他站点… - 选择 mirrors.aliyun.com – 选择服务器 – 关闭窗口

