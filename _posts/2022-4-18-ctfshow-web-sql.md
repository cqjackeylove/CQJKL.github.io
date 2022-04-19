---
layout: post
title: ctfshow_web入门sql
---
今天只有熬夜写wp了  
先从sqlmap这几道题写着走吧   
>**201**  
先上payload          
![201](/assets/images/201.png)        
这道题是想教我们学会sqlmap使用ua和referer注入      
我最开始倒腾了半天不知道为什么一直注不出来,后来去问了别的大佬一语指出来我的错误,因为我在api/后加了sqlmap.php没有删掉,导致我一直注不出来，我还以为是后面写错了       
![2011](/assets/images/2011.png)    

>**202**        
这道题是想让我们通过post方式传参数      
![202](/assets/images/202.png)          
反正把格式注意到就好了    
![2022](/assets/images/2022.png)       
  
>**203**   
此题是想让我们用PUT的请求方式传参，因此要加一个Content-Type
![203](/assets/images/203.png)   
然后跑出flag   
![203](/assets/images/2033.png)    

>**204**   
提示了我们要用cookie，就在后面导入就是，注意此题cooki里的两个都要导入进来哦   
![204](/assets/images/204.png)   
![2044](/assets/images/2044.png)    

>**205**    
api要鉴权所以加这个   
![205](/assets/images/205.png)   
![205](/assets/images/2055.png)    

>**206**    
注意看传参的id有(""""),因此尝试去闭合   
![206](/assets/images/206.png)    
![206](/assets/images/2066.png)    

>**207**   
提示我们要使用temper,看了wp视频，要引用space2comment的脚本把空格换成/* */进行逃逸   
![207](/assets/images/207.png)   

