---
layout: post
title: ctfshow-php
---
>**web89**
![89](/assets/images/8900.png)
首先，我们应该先搞懂intval这个函数     
intval() 函数用于获取变量的整数值。     
intval() 函数通过使用指定的进制 base 转换（默认是十进制），返回变量 var 的 integer 数值。 intval() 不能用于 object，否则会产生 E_NOTICE 错误并返回 1     
intval() 函数作为数组的话空数组返回0，非空则返回1；    
因此，我们可以传一个非空数组让if条件成立，返回flag    
![89](/assets/images/8901.png)    

>**web90**   
![90](/assets/images/9000.png)    
因为有===    
所以我们可以利用num=4476.0，当intval读到符号时返回值   
![90](/assets/images/9001.png)    
还可以利用十六进制和八进制    
num=010574（八进制）   
num=0x117（十进制）    
或者num=4475a   
![90](/assets/images/9002.png)  

>**web91**  
![91](/assets/images/9100.png)   
这里是个正则匹配^开头   $结尾  
这里的意思是说第一个if要以php开头，第二个if不能以php开头结尾     
并且这里i是不区分大小写，m是多行匹配   
就因为这两个if相差m，所以我们可以用%0a换行来匹配    
![91](/assets/images/9101.png)     
