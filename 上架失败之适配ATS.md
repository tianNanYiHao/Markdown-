#上架失败之适配ATS


###参考连接:[AFNetwork 3.0 源码解读（五）AFSecurityPolicy](http://blog.csdn.net/yuwuchaio/article/details/50469183)
###参考连接:[iOS开发HTTPS实现之信任SSL证书和自签名证书](https://www.jianshu.com/p/6b9c8bd5005a)
###参考连接:[IOS-关于App Transport Security相关说明及适配](http://blog.csdn.net/maxdong24/article/details/53610127)
###参考连接:[https信任证书的三种方](http://blog.csdn.net/github_34613936/article/details/51490032)
###参考连接:[iOS开发：对于AFNetworking HTTP转HTTPS请求证书问题](https://www.jianshu.com/p/551fa7482def)
###参考连接:[用chrome获取https的证书	](http://blog.csdn.net/lllkey/article/details/17526323)
###参考链接:[chrome浏览器对http和https网站安全提示和证书导入导出](http://blog.csdn.net/wonderful_life_mrchi/article/details/78045512)
###参考连接:[iOS中https的证书验证](http://blog.csdn.net/u012198553/article/details/50946685)
###参考连接:[iOS开发探索-HTTPS传输签名证书的获取](https://www.jianshu.com/p/35bf6eb9c3a1)
###参考连接:[iOS开发实现HTTPS之 cer 文件的使用](http://blog.csdn.net/Kaiccy/article/details/78465507)
###参考链接:[NSURLSession 同步请求(使用信号量)](http://blog.csdn.net/chwow/article/details/51537685)  



>##检测网址是否支持ATS的命令
```
/usr/bin/nscurl --ats-diagnostics --verbose 你的URL
```


###适配之前
####项目之前一直没有涉及去上架的问题,也就没有上架到AppStore.  
####开发时为了方便,也就临时允许了ATS对于HTTP的网络请求.提交AppStore以后被拒,于是使用vpn去做连接测试,果然连接不上.
####于是,开启ATS吧.


```
	<key>NSAppTransportSecurity</key>
	<dict>
		<key>NSAllowsArbitraryLoads</key>
		<false/>
	</dict>
```
####问题来了
```
[] nw_coretls_read_one_record tls_handshake_process: [-9801]
NSURLSession/NSURLConnection HTTP load failed (kCFStreamErrorDomainSSL,
```


####诊断项目使用的URL地址发现:

```
Configuring ATS Info.plist keys and displaying the result of HTTPS loads to https://sdb.sandpay.com.cn/app/api/token/getStoken/v1.
A test will "PASS" if URLSession:task:didCompleteWithError: returns a nil error.
================================================================================

Default ATS Secure Connection
---
ATS Default Connection
ATS Dictionary:
{
}
2018-02-13 17:45:44.952 nscurl[32423:2935325] NSURLSession/NSURLConnection HTTP load failed (kCFStreamErrorDomainSSL, -9801)
Result : FAIL
Error : Error Domain=NSURLErrorDomain Code=-1200 "An SSL error has occurred and a secure connection to the server cannot be made." UserInfo={_kCFStreamErrorCodeKey=-9801, NSLocalizedRecoverySuggestion=Would you like to connect to the server anyway?, NSUnderlyingError=0x7fe244d37b10 {Error Domain=kCFErrorDomainCFNetwork Code=-1200 "(null)" UserInfo={_kCFStreamPropertySSLClientCertificateState=0, _kCFNetworkCFStreamSSLErrorOriginalValue=-9801, _kCFStreamErrorDomainKey=3, _kCFStreamErrorCodeKey=-9801}}, NSLocalizedDescription=An SSL error has occurred and a secure connection to the server cannot be made., NSErrorFailingURLKey=https://sdb.sandpay.com.cn/app/api/token/getStoken/v1, NSErrorFailingURLStringKey=https://sdb.sandpay.com.cn/app/api/token/getStoken/v1, _kCFStreamErrorDomainKey=3}
---

================================================================================

Allowing Arbitrary Loads

---
Allow All Loads
ATS Dictionary:
{
    NSAllowsArbitraryLoads = true;
}
Result : PASS
---

================================================================================

Configuring TLS exceptions for sdb.sandpay.com.cn

---
TLSv1.2
ATS Dictionary:
{
    NSExceptionDomains =     {
        "sdb.sandpay.com.cn" =         {
            NSExceptionMinimumTLSVersion = "TLSv1.2";
        };
    };
}
2018-02-13 17:45:45.059 nscurl[32423:2935325] NSURLSession/NSURLConnection HTTP load failed (kCFStreamErrorDomainSSL, -9801)
Result : FAIL
Error : Error Domain=NSURLErrorDomain Code=-1200 "An SSL error has occurred and a secure connection to the server cannot be made." UserInfo={_kCFStreamErrorCodeKey=-9801, NSLocalizedRecoverySuggestion=Would you like to connect to the server anyway?, NSUnderlyingError=0x7fe244d34660 {Error Domain=kCFErrorDomainCFNetwork Code=-1200 "(null)" UserInfo={_kCFStreamPropertySSLClientCertificateState=0, _kCFNetworkCFStreamSSLErrorOriginalValue=-9801, _kCFStreamErrorDomainKey=3, _kCFStreamErrorCodeKey=-9801}}, NSLocalizedDescription=An SSL error has occurred and a secure connection to the server cannot be made., NSErrorFailingURLKey=https://sdb.sandpay.com.cn/app/api/token/getStoken/v1, NSErrorFailingURLStringKey=https://sdb.sandpay.com.cn/app/api/token/getStoken/v1, _kCFStreamErrorDomainKey=3}
---

---
TLSv1.1
ATS Dictionary:
{
    NSExceptionDomains =     {
        "sdb.sandpay.com.cn" =         {
            NSExceptionMinimumTLSVersion = "TLSv1.1";
        };
    };
}
2018-02-13 17:45:45.088 nscurl[32423:2935325] NSURLSession/NSURLConnection HTTP load failed (kCFStreamErrorDomainSSL, -9801)
Result : FAIL
Error : Error Domain=NSURLErrorDomain Code=-1200 "An SSL error has occurred and a secure connection to the server cannot be made." UserInfo={_kCFStreamErrorCodeKey=-9801, NSLocalizedRecoverySuggestion=Would you like to connect to the server anyway?, NSUnderlyingError=0x7fe244f384b0 {Error Domain=kCFErrorDomainCFNetwork Code=-1200 "(null)" UserInfo={_kCFStreamPropertySSLClientCertificateState=0, _kCFNetworkCFStreamSSLErrorOriginalValue=-9801, _kCFStreamErrorDomainKey=3, _kCFStreamErrorCodeKey=-9801}}, NSLocalizedDescription=An SSL error has occurred and a secure connection to the server cannot be made., NSErrorFailingURLKey=https://sdb.sandpay.com.cn/app/api/token/getStoken/v1, NSErrorFailingURLStringKey=https://sdb.sandpay.com.cn/app/api/token/getStoken/v1, _kCFStreamErrorDomainKey=3}
---

---
TLSv1.0
ATS Dictionary:
{
    NSExceptionDomains =     {
        "sdb.sandpay.com.cn" =         {
            NSExceptionMinimumTLSVersion = "TLSv1.0";
        };
    };
}
Result : PASS
---

================================================================================


```
>##上面的诊断发现   
>Default ATS Secure Connection 结果 : FAIL   
>Allowing Arbitrary Loads 结果: PASS  
>TLSv1.2 结果 : FAIL  
>TLSv1.1 结果 : FAIL  
>TLSv1.0 结果 : PASS
  



##第一个坑出现:
由于苹果ATS不仅对HTTP有限制,对HTTPS也有一些门槛限制.连接的ATS证书都必须满足一下条件,否则也是不能通信的  
>1.服务器所有的连接使用TLS1.2以上版本   
>2.HTTPS证书必须使用SHA256以上哈希算法签名  
>3.HTTPS证书必须使用RSA 2048位或ECC 256位以上公钥算法  
>4.使用前向加密技术



###看完以上帖子可以发现,显然想要支持ATS,后端服务器必然需要支持 TLSv1.2,这个需要联系后端的同学去做配置.  
###这个问题先抛在这里,继续填坑 [^过年以后联系后端同事做配置]

[^过年以后联系后端同事做配置]:注解一

##关于.cer证书的获取
###1.你必然可以联系后端同学去获取,且很多帖子也会告诉你改如何处理这张证书的使用.
###2.可以使用Safari浏览器/谷歌浏览器 - 点击小锁 - 去查看证书和获取
##接入cer证书
>接入cer证书的方案有很多  
>1.NSURLConnection  
>2. NSURLSession  
>3.AFNetworking第三方库

##第二个坑出现
**由于项目中依旧使用的是NSURLConnection的API,且``` 全部请求均为同步post ``` , 不要问我为什么是这样.因此,对于接入cer证书,首先就无法使用NSURLConnection发送异步post来解决(也许有,但是我决定放弃NSURLConnection.),并且NSURLConnection早在iOS9就被废弃,于是替换为NSURLSession**
###该坑的重点是,NSURLSession只有异步请求,没有同步请求了.
```
解决办法: 使用信号量来实现同步POST

   dispatch_semaphore_t semaphore = dispatch_semaphore_create(0); //创建信号量
    __block NSString *json = @"";
    NSURL * Url = [NSURL URLWithString:requestUrl];
    NSMutableURLRequest * UrlRequest = [NSMutableURLRequest requestWithURL:Url];
    
    [UrlRequest setHTTPMethod:@"POST"];
    [UrlRequest setValue:@"application/x-www-form-urlencoded" forHTTPHeaderField:@"Content-Type"];
    [UrlRequest setHTTPBody:[[NSString stringWithFormat:@"%@", messageInfo] dataUsingEncoding:NSUTF8StringEncoding]];
    if (timeoutInterval == 0) {
        UrlRequest.timeoutInterval = 10;
    } else {
        UrlRequest.timeoutInterval = timeoutInterval;
    }
    
    NSURLSession *session = [NSURLSession sharedSession];
    NSURLSessionTask *task = [session dataTaskWithRequest:UrlRequest completionHandler:^(NSData * _Nullable data, NSURLResponse * _Nullable response, NSError * _Nullable error) {

        json = [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding];
        NSLog(@"======= %@",jsonjson);
        if (error) {
            NSLog(@"%@",error);
        }
        dispatch_semaphore_signal(semaphore);   //发送信号
    }];
    
    [task resume];
    dispatch_semaphore_wait(semaphore,DISPATCH_TIME_FOREVER);  //等待


//以上 获取json字符串以后,就等于实现了NSURLSession的同步post

```

##开始接入cer证书,并测试
###待完善.....





