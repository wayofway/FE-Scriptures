# 服务器端内嵌(SSI)

SSI全称是Server Side Includes，即服务器端包含，是一种基于服务器端的网页制作技术。

SSI是嵌入HTML页面中的指令，在页面被提供时由服务器进行运算，以对现有HTML页面增加动态生成的内容，而无须通过CGI程序提供其整个页面，或者使用其他动态技术。

> 基本原理：**SSI在HTML文件中，可以通过注释行调用命令或指针，即允许通过在HTML页面注入脚本或远程执行任意代码。**

## 01 主要用途

1. 显示服务器端环境变量<#echo>
2. 将文本内容直接插入到文档中<#include>
3. 显示WEB文档相关信息<#flastmod #fsize> (如文件制作日期/大小等)
4. 直接执行服务器上的各种程序<#exec>(如CGI或其他可执行程序)
5. 设置SSI信息显示格式<#config>(如文件制作日期/大小显示方式)

## 02 SHTML文件

SHTML即Server-Parsed HTML。

shtml文件（还有stm、shtm文件）就是应用了SSI技术的html文件，所以在.shtml页面返回到客户端前，页面中的SSI指令将被服务器解析。可以使用SSI指令将其它文件、图片包含在页面中，也可以将其它的CGI程序包含在页面中，如.aspx文件。在给客户端返回的页面中不会包含SSI指令。如果SSI指令不能被解析，则浏览器会将其做为普通的HTML注释处理。

## 03 SSI基本语法

在SHTML文件中SSI标签使用的几种基本语法如下，必须注意的是其语法格式必须是以html的注释符`<!--`开头、且后面紧接#符号和SSI命令，它们期间不能存在空格：

**1、显示服务器端环境变量`<#echo>`**

本文档名称：`<!--#echo var="DOCUMENT_NAME"-->`

现在时间：`<!--#echo var="DATE_LOCAL"-->`

显示IP地址：`<!--#echo var="REMOTE_ADDR"-->`

**2、将文本内容直接插入到文档中`<#include>`**

```
<!--#include file="文件名称"-->
<!--#include virtual="index.html" -->
<!--#include virtual="文件名称"–>
<!--#include virtual="/www/footer.html" -->
```

注：file包含文件可以在同一级目录或其子目录中，但不能在上一级目录中，virtual包含文件可以是Web站点上的虚拟目录的完整路径。

**3、显示WEB文档相关信息`<#flastmod><#fsize>`(如文件制作日期/大小等)**

文件最近更新日期：`<!--#flastmod file="文件名称"-–>`

文件的长度：`<!--#fsize file="文件名称"-->`

**4、直接执行服务器上的各种程序`<#exec>`(如CGI或其他可执行程序)**

```
<!–#exec cmd="文件名称"–>
<!--#exec cmd="cat /etc/passwd"--
<!–#exec cgi="文件名称"–>
<!--#exec cgi="/cgi-bin/access_log.cgi"–>
```

将某一外部程序的输出插入到页面中。可插入CGI程序或者是常规应用程序的输入，这取决于使用的参数是cmd还是CGI。

**5、设置SSI信息显示格式`<#config>`(如文件制作日期/大小显示方式)**

**6、高级SSI可设置变量使用if条件语句**

```php+HTML
<!--#if expr=”$SERVER_NAME=/”hoyi.zb169.net/””-->

欢迎光临好易CGI工厂在淄博热线的分站http://hoyi.zb169.net。

<!--#elif expr=”$SERVER_NAME=/”linux.cqi.com.cn/”” -->

欢迎光临好易CGI工厂在太阳城的分站http://linux.cqi.com.cn/~hoy。

<!--#else-->

欢迎光临好易CGI工厂！

<!--#endif”-->

```

注意：用于前面指令中的反斜杠，是用来代换内部的引号，以便它们不会被解释为结束表达式。不可省略。

## 04 Web服务启动SSI

#### Nginx

在Nginx中，开启SSI只需在配置文件中添加如下几项：

```
ssi on;
ssi_silent_errors off;
ssi_types text/shtml;
```

如：

```
server{
	listen 80;
	server_name www.hello.com
	# 配置SSL
	ssi on; # 开启SSI支持
	ssi_silent_errors on; # 默认为off，设置为on则在处理SSI文件出错时不输出错误信息
	ssi_types text/html; # 需要支持的shtml 默认是 text/html
	
	location / {
		root html;
		index index.html index.htm;
	}
}
```

#### Apache

修改Apache配置文件httpd.conf：

1、确认加载include.so模块，将注释去掉：

```
LoadModule include_module libexec/apache2/mod_include.so
```

2、AddType部分去掉这两段注释：

```
AddType text/html .shtml
AddOutputFilter INCLUDES .shtml
```

3、Directory目录权限里面找到`Options Indexes FollowSymLinks`，并增加Includes修改为`Options Indexes FollowSymLinks Includes`；

4、重新启动Apache；

## 05 SSI注入漏洞

SSI注入全称Server-Side Includes Injection，即服务端包含注入。在stm、shtm、shtml等Web页面中，如果用户可以从外部输入SSI标签，而输入的内容会显示到上述后缀的Web页面时，就导致可以远程在Web应用中注入脚本来执行代码。

简单点说就是攻击者可以通过外部输入SSI标签到Web页面（stm、shtm、shtml文件）来动态执行代码。

SSI注入允许远程在Web应用中注入脚本来执行代码。简单点说就是攻击者可以通过外部输入SSI语句到Web页面来动态执行代码。

### 防御方法

- 若非必须，尽量关闭服务器的SSI功能；
- 对用户的输入进行严格的过滤，过滤相关SSI特殊字符（`<,>,#,-,",'`）；

## 参考

[SSI注入漏洞总结](https://www.mi1k7ea.com/2019/09/28/SSI注入漏洞总结/)

[SSI技术详解](https://blog.csdn.net/blue_sky2008/article/details/1501376)

