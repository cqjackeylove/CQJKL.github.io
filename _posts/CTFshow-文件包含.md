---
layout: post
title: CTFshow_文件包含
---    

### 知识点

#### 运用
服务器执行PHP文件时，可以通过文件包含函数加载另一个文件中的PHP代码并执行，这样能够为开发者节约许多时间。

#### 起因
1·代码传入文件，从而解析PHP代码   
2·通常文件包含漏洞产生于文件包含函数的使用  

#### 类别
1·LFI：Local File Inclusion,本地文件包含漏洞，大部分情况下所遇到的文件包含漏洞都是LFI  
2·RFI：Remote File Inclusion,远程文件包含漏洞，要求allow_url_fopen=On(默认)，规定是否允许用户从远程服务器或者网站检索数据；allow_url_include=On(php5.2之后默认为Off)，规定是否允许include/require远程文件   

#### 文件包含函数  
`require()//在包含的过程中遇到错误，直接报错并且退出`  
`require_once()//同require，但是对包含过的文件不在包含`
`include()//在包含的过程中遇到错误，抛出警告并且继续执行`
`include_once()//同include，但是对包含过的文件不在包含`

#### CTF中常用的伪协议
一·php://filter		//访问本地文件的协议   
  可以获取指定的源码。与包含函数结合时，php://filter流被当作php文件执行   
//所以我们一般对其进行编码，让其不执行，从而实现任意文件读取。    
  php://filter/resource=flag.php   
  php://filter/read=convert.base64-encode/resource=flag.php   

二·php://input	要求(allow_url_include=On)    
  //可以访问请求的原始数据的只读流，将post请求的数据当作php代码执行。   
  //当传入的参数作为文件名打开时，可以将参数设为php://input，同时post内容，   
  //php执行时会将post的内容当作文件内容，从而实现任意代码执行   
  遇到file_get_contents()要想到用php://input绕过   
使用：   
  php://input   
  post:****   
三·data://text/plain		//要求allow_url_fopen=On,allow_url_include=On    
  使用：    
    data://text/plain,<?php phpinfo();?>   
    data:text/plain;base64,PD9waHAgcGhwaW5mbygpOz8%2b   
    //加号+的url编码为%2b，PD9waHAgcGhwaW5mbygpOz8+的base64解码为：<?php phpinfo();?>     
     