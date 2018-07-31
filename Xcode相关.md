#[.a和.framework的区别](https://blog.csdn.net/li198847/article/details/63685640)

```
一、库： 
库是共享程序代码的方式，一般分为静态库和动态库

二、静态库与动态库的区别： 
静态库：连接时完整地拷贝至可执行文件中，被多次使用就有多份冗余拷贝。 
动态库：连接时不复制，程序运行时由系统动态加载到内存，供程序调用，系统只加载一次，多个程序共用，节省内存。

三、iOS静态库形式和动态库形式： 
静态库：.a和.framework 
动态库：.dylib和.framework

四、framework静态库和动态库的区分： 
系统的.framework是动态库，我们自己建立的.framework是静态库

五、.a和.framwork的区别： 
.a是一个纯二进制文件，.framework中除了有二进制文件外还有资源文件。 
.a文件不能直接使用，至少要有.h文件配合，.framework文件可以直接使用。 
.a + .h + sourceFile = .framework

六、使用静态库的原因： 
实现iOS程序的模块化，可以把固定的业务模块化成静态库。 
分享你的代码库给别人，但并不公开你的源码
```


#[Alcatraz的安装和使用](https://www.cnblogs.com/wendingding/p/4964661.html)

#[Xcode 8+安装Alcatraz插件管理器](https://blog.csdn.net/zhongtiankai/article/details/72598467)
#[解决Xcode 8以后的Alcatraz等插件不可用](https://blog.csdn.net/jingfa1993/article/details/65633047)
```
//要使用插件 - 使用 xcode_plgins 插件进行 xcod解签(解除Xcod8的封印 XD )
//1.查看并更新所有已经安装的插件的签名 !
update_xcode_plugins
//2.解签! 对Xcode执行去除签名验证的操作，对于后期打包上传AppStore可能有影响
 update_xcode_plugins --unsign
 
//3.需要打包上传AppStore时, 需重新对Xcode进行恢复(封印!)
update_xcode_plugins --restore


//插件的文件目录地址
~/Library/Application Support/Developer/Shared/Xcode/Plug-ins
```



