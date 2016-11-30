# PHP核心课程

标签（空格分隔）： 未分类

---

## web开发的介绍

web开发分为
1. 静态web开发（html页面）
如果我们的一个页面，始终是一成不变的，则就是属于静态web开发，一般讲用html技术就可以了。
2. 动态web开发
我们需要发帖，发邮件等需要进行数据交互，这时需要动态web开发。

常用的动态web技术：php、jsp、asp--->asp.net、cgi




1. 一台机器可以有1-65535号端口

2. netstat -an   来查看机器有哪些端口在监听，如果有一场端口在监听，则我们可以关闭该端口。

netstat -anb
 通过该命令我们可以发现是哪个程序在监听该端口，从而关闭

3. 如果一台机器的80端口被apache监听，则该端口不能再被其他的应用程序监听

4. 端口号分为有名端口 1-1024号，其它端口可以自己分配。


apache如何去配置端口
1. 我们的Apache软件配置在hpptd.conf文件中配置，该文件在Apache安装目录下的conf。
在hpptd.conf文件中我们修改端口：
listen 81

修改完成后，一定要重新启动Apache

Apache目录结构：
bin目录：用来存放Apache常用的命令，比如hpptd。
cgi-bin:该目录用来存放Linux下的常用命令。
conf：该目录用来存放配置文件。httpd.conf.
error:apache的错误记录。
htdocs:存放我们的站点的文件。（默认情况下）如果有多个站点，可以通过文件夹来分类。
icons：存放图标。
logs:记录apache的相关日志。
manual:手册
modules：apache模块






虚拟目录：

问题：我们的apache安装在c盘，但是出现c盘没有空间，d盘有更多空间，能不能把d盘的一个文件夹下的网页html，php当做网站管理。


解决办法：

配置虚拟目录在apache的conf目录下的hpptd.conf中的`<IfModule dir_module>`节点后添加如下代码：


1. 添加虚拟目录的节点

    ```html
    #配置虚拟目录
    <IfModule dir_module>
        #Directory相当于欢迎页面
        DirectoryIndex index.html index.htm index.php
        #你的站点别名
        Alias /myblog "D:/myblog"
        <Directory d:/myblog>
        #访问权限设置
        Order allow,deny
        Allow from all
        </Directory>
    </IfModule>
    ```
2. 注销documentroot路径

    `#Documentroot "C:/Program Files/Apache Software Foundation/Apache2.2/htdocs"`

3. 测试
        http://localhost/myblog/news.html

4. 如何设置欢迎页面

5. 关于apache访问权限的讲解

    ```html
      <Directory d:/myblog>//表示对d:/myblog文件权限设置
        #访问权限设置
        Order allow,deny //先允许所有的IP访问 deny表示拒绝所有
        Allow from all //先看看allow设置，许可所有ip
        </Directory>
    ```

例题：

    order deny，allow 
    allow from 218.20.253.2
    deny from 218.20
    
    
    
    
配置虚拟主机的步骤如下：

1. 启用 httpd-vhosts.conf
在httpd.conf文件中
`#Virtual host`虚拟主机 
Include conf/extra/gttpd-vhosts.conf

2. 在 httpd-vhosts.conf文件中做配置

    ```html
    #配置我们自己的虚拟主机
    <VirtualHost 127.0.0.1:80>
        DocumentRoot "d:/myblog"
        #Directory相当于欢迎页面
        DirectoryIndex index.html index.htm index.php
        #你的站点别名
        #Alias /myblog "D:/myblog"
        <Directory d:/myblog>
        Options FollowSymLinks
        #不许可别人修改我们的页面 
        AllowOverride None
        #访问权限设置
        Order allow,deny
        Allow from all
        </Directory>
    </VirtualHost>
    ```
3. 修改hosts文件 








字符串细节：
1. 理论上，我们对字符串大小没有限制，即只要不超过内存就可以。
2. 我们定义字符串的时候，

如果



数据类型自动转换


### php的表达式
表达式是php最重要的基石。在php中，几乎所写的任何东西都是一个表达式。简单但确最精确的定义一个表达式的方式就是"任何有值得东西"。    
$a=67;

### 算数运算符
php中常用的是：
加
减
乘
除
取模







### 函数

完成 某一功能的程序指令（语句）的集合， 称为函数。

在PHP中

##### 自定函数的基本语法结构

//参数列表用处是接受数据的
function 函数名(参数列表){
    语句；//方法(函数)主体（必须有）
    return 返回值;//返回值（可以没有）

}
 



require 和 require_once细节
一般放在php页面的最前面。php在执行前，就先读入require所引入的文件，一旦出现错误，则退出程序。
这两个区别为，前者遇到即包含文件，后者会判断是否已经包含过了，如果包含过了，则不再包含文件。一可以节省资源，二可以避免重复定义的错误。


include 和 include_once细节

可以放在php页面的调用函数前，当php执行到时，才会读入include所引入的php页面，如果出现错误，程序不会退出，会继续执行