# 74cms v4.2.126-因任意文件读取漏洞导致的任意用户密码修改漏洞

## 0x00 前言
厂商：74cms

下载地址：http://www.74cms.com/download/index.html

关于版本：

新版的74cms采用了tp3.2.3重构了，所以可知底层是tp，74cms新版升级是后台升级的，所以先将将升级方法。

注：此漏洞不用升级至最新版本也可使用。

0x01 74cms升级到最新版

1， 先去官网下载 骑士人才系统基础版(安装包)

2， 将下载好的包进行安装

3， 进入后台点击查看如果不是最新版的话，请点击升级！

4， 如果是本地环境的话，会提示 域名不合法升级失败，这个问题很好解决

5， 搜索文件74cms\upload\Application\Admin\Controller\ApplyController.class.php

6， 查找所有$_SERVER['HTTP_HOST'] 改为 http://baidu.com 即可

## 0x02
突突突突突突突

文件：

74cms\upload\Application\Home\Controller\ApiController.class.php

方法：members_edit(

![image](images/img22.png)

从这里看漏洞整体都很简单。没有过多的套路的，有的只是中规中矩。

那么就让我们直接利用试试。

先看看数据库现在的数据

![image](images/img23.png)

接着让我们来调接口看看

![image](images/img24.png)

文件： 74cms\upload\Application\Home\Controller\ApiController.class.php

方法：check_token(

![image](images/img25.png)

接口调用失败的原因是因为，上图的析构函数

调用了方法 check_token 进行了token验证

这些都没有问题，

$token 也是我们可以操控的。

现在的问题就是C('PWDHASH') 我们现在无法得到。

好在，我们还可以通过组合漏洞的形式来获取。

想要利用此漏洞，我的想法是先通过，任意读取漏洞，先把C('PWDHASH') 的值读取出来，然后在加密验证一下即可

而加密的代码其实我们不需要去看，因为这是全局通用的代码，所以我们正式环境中复制出来加密一下就可以利用了。

思路：

先下载此源码然后本地把此加密函数保存下来即可。（因为没人会没事去改加密函数）

然后在通过 “任意文件读取漏洞” 读取目标站点的C('PWDHASH') 的值，接着本地加密成token

这样漏洞就可以使用了

任意文件读取的小脚本下载

https://github.com/ianxtianxt/74cms_file_read

下载此文件以后

![image](images/img26.png)

设置成这样，然后执行一下

![image](images/img27.png)

接着把 PWDHASH 复制出来

我们这里看看加密的代码：

文件：74cms\upload\Application\Common\Common\function.php

函数：encrypt(

![image](images/img28.png)

然后加密一下

![image](images/img29.png)

![image](images/img30.png)

![image](images/img31.png)

![image](images/img32.png)

这时你就会发现虽然我们密码改了但是不知道用户名怎么办？

![image](images/img33.png)

好在我们可以这样利用！

人家登录是可以用户名，手机号登录的，所以我们就

![image](images/img34.png)

![image](images/img35.png)

当然如果你要修改用户名登录的话，也可以，看你自己喜欢了

![image](images/img36.png)

![image](images/img37.png)

## 0x03 利用小工具
为了方便大家，手工做这种事情是很累的，所以还是要写个小工具，可以方便的去利用。

利用工具:

https://github.com/ianxtianxt/74cms_file_read

![image](images/img38.png)

![image](images/img39.png)

## 四、参考链接
https://www.yuque.com/pmiaowu/bfgkkh/rymscc
