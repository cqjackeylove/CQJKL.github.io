---
layout:post
title:ctfshow_web入门sql
---
今天只有熬夜写wp了  
先从sqlmap这几道题写着走吧   
201  
先上payload      
![201](asset/image/201.png)
这道题是想教我们学会sqlmap使用ua和referer注入  
我最开始倒腾了半天不知道为什么一直注不出来,后来去问了别的大佬一语指出来我的错误,因为我在api/后加了sqlmap.php没有删掉,导致我一直注不出来，我还以为是后面写错了    
![2011](asset/image/2011.png)    

202    
这道题是想让我们通过post方式传参数
![202](asset/image/202.png)    
反正把格式注意到就好了    
![2022](asset/image/2022.png)    
