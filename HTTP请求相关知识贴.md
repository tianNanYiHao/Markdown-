

#[HTTP请求行、请求头、请求体详解](https://blog.csdn.net/u010256388/article/details/68491509)
###常见请求报文头属性
1.Accept :请求报文可通过一个“Accept”报文头属性告诉服务端 客户端接受什么类型的响应。

>Accept属性的值可以为一个或多个MIME类型的值，关于MIME类型，大家请参考：http://en.wikipedia.org/wiki/MIME_type 
>
>```常见的MIME类型
超文本标记语言文本 .html,.html text/html 
普通文本 .txt text/plain 
RTF文本 .rtf application/rtf 
GIF图形 .gif image/gif 
JPEG图形 .ipeg,.jpg image/jpeg 
au声音文件 .au audio/basic 
MIDI音乐文件 mid,.midi audio/midi,audio/x-midi 
RealAudio音乐文件 .ra, .ram audio/x-pn-realaudio 
MPEG文件 .mpg,.mpeg video/mpeg 
AVI文件 .avi video/x-msvideo 
GZIP文件 .gz application/x-gzip 
TAR文件 .tar application/x-tar 
>```
>
>

2.Cookie 
>客户端的Cookie就是通过这个报文头属性传给服务端的哦！
>
>Cookie: $Version=1; Skin=new;jsessionid=5F4771183629C9834F8382E23BE13C4C  
>
>服务端是怎么知道客户端的多个请求是隶属于一个Session呢？注意到后台的那个jsessionid=5F4771183629C9834F8382E23BE13C4C木有？原来就是通过HTTP请求报文头的Cookie属性的jsessionid的值关联起来的！（当然也可以通过重写URL的方式将会话ID附带在每个URL的后面哦）。


3.Referer 
>表示这个请求是从哪个URL过来的，假如你通过google搜索出一个商家的广告页面，你对这个广告页面感兴趣，鼠标一点发送一个请求报文到商家的网站，这个请求报文的Referer报文头属性值就是http://www.google.com。
>
>

4.Cache-Control
>对缓存进行控制，如一个请求希望响应返回的内容在客户端要被缓存一年，或不希望被缓存就可以通过这个报文头达到目的
>
>如以下设置，相当于让服务端将对应请求返回的响应内容不要在客户端缓存：
>```
>Cache-Control: no-cache  
>```
>
------

###常见响应报文头属性
####1.响应状态码 
>
>```
>1xx 消息，一般是告诉客户端，请求已经收到了，正在处理，别急...
2xx 处理成功，一般表示：请求收悉、我明白你要的、请求已受理、已经处理完成等信息.
3xx 重定向到其它地方。它让客户端再发起一个请求以完成整个处理。
4xx 处理发生错误，责任在客户端，如客户端的请求一个不存在的资源，客户端未被授权，禁止访问等。
5xx 处理发生错误，责任在服务端，如服务端抛出异常，路由出错，HTTP版本不支持等。
>```
>


####2.常见的HTTP响应报文头属性 
1.Cache-Control 
>响应输出到客户端后，服务端通过该报文头属告诉客户端如何控制响应内容的缓存。 

>下面，的设置让客户端对响应内容缓存3600秒，也即在3600秒内，如果客户再次访问该资源，直接从客户端的缓存中返回内容给客户，不要再从服务端获取（当然，这个功能是靠客户端实现的，服务端只是通过这个属性提示客户端“应该这么做”，做不做，还是决定于客户端，如果是自己宣称支持HTTP的客户端，则就应该这样实现）。
>
>```
>Cache-Control: max-age=3600 
>```





