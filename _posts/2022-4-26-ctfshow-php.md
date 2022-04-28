---
layout: post
title: ctfshow-php
---
>**web89**
![89](/assets/images/imgshow/8900.png)
首先，我们应该先搞懂intval这个函数     
intval() 函数用于获取变量的整数值。     
intval() 函数通过使用指定的进制 base 转换（默认是十进制），返回变量 var 的 integer 数值。 intval() 不能用于 object，否则会产生 E_NOTICE 错误并返回 1     
intval() 函数作为数组的话空数组返回0，非空则返回1；    
因此，我们可以传一个非空数组让if条件成立，返回flag    
![89](/assets/images/8901.png)    

>**web90**   
![90](/assets/images/imgshow/9000.png)    
因为有===    
所以我们可以利用num=4476.0，当intval读到符号时返回值   
![90](/assets/images/imgshow/9001.png)    
还可以利用十六进制和八进制    
num=010574（八进制）   
num=0x117（十进制）    
或者num=4475a   
![90](/assets/images/imgshow/9002.png)  

>**web91**  
![91](/assets/images/imgshow/9100.png)   
这里是个正则匹配^开头   $结尾  
这里的意思是说第一个if要以php开头，第二个if不能以php开头结尾     
并且这里i是不区分大小写，m是多行匹配   
就因为这两个if相差m，所以我们可以用%0a换行来匹配    
![91](/assets/images/imgshow/9101.png)     

>**web92**     
![92](/assets/images/imgshow/9200.png)     
考察了一个==弱类型比较  
可以试着用八进制和十六进制直接绕过==  
![92](/assets/images/imgshow/9101.png)
![92](/assets/images/imgshow/9102.png)
或者利用科学计数法构造第一个if绕过，第二个if遇到字母就结束   
payload：num=4476e123     

>**web93**  
![93](/assets/images/imgshow/9300.png)    
同上题一样只是过滤了十六进制   

>**web94**
![94](/assets/images/imgshow/9400.png)     
pos是截取当前字符串第一个  
因此可以利用空格%20绕过   
或者+4476 绕过   
利用===构造4476.1     

>**web95**   
![95](/assets/images/imgshow/9500.png)   
这次多过滤了小数点，所以用空格加八进制过滤就行    

>**web96**
![96](/assets/images/imgshow/9600.png)   
这是一道路劲问题因为有highlight_file这个函数   
?u=/var/www/html/flag.php              绝对路径        
?u=./flag.php                          相对路径     
?u=php://filter/resource=flag.php      php伪协议     
![96](/assets/images/imgshow/9601.png)   

>**web97**   
![97](/assets/images/imgshow/9700.png)    
这里有md5，用到了md5强碰撞    
所以利用数组返回NULL   
?a[]=1&b[]=2   
![97](/assets/images/imgshow/9701.png)   

>**web98**   
![98](/assets/images/imgshow/9800.png)   
这道题运用了三元运算   
第一个是如果get传参，下一次就会把get变成post方式   
中间两个COOKIE 和 SERVER跟没没用，不用管它   
于是只用完成最后一个highlight_file三元运算就行了   
![98](/assets/images/imgshow/9801.png)   

>**web99**  
![99](/assets/images/imgshow/9900.png) 
rand会生成随机数  
in——array是延用了==弱类型比较  
所以payload：
get:n=1.php  POST: content=<?php eval($_POST[a]); ?> 
在打开1.php  POST:a=system('ls')    
发现了flag36d.php  在打开即可得到flag   

>**web100** 
![100](/assets/images/imgshow/10000.png)   
$v0=is_numeric($v1) and is_numeric($v2) and is_numeric($v3);   
重点理解这句话，这句话是关键   
首先我们应该补给一下知识   
优先权 && > = > and   
|| > = > or  
因此这句话只用满足v1为数字即可   
第二部分     
反射类的具体使用方法可参考php官网文档,简单来说反射类就是存放了类里的所有东西。     
最简单的方法直接输出这个类即可，也就是构造出 echo new ReflectionClass('ctfshow');     
payload:?v1=1&v2=echo new ReflectionClass&v3=;  

