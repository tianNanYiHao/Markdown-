#[Wolfgang89/SpecFile](https://github.com/Wolfgang89/SpecFile)

#[使用CocoaPods开发并打包静态库](http://www.cnblogs.com/brycezhang/p/4117180.html)

#[CocoaPods开发静态库并建立Podspec - 看完其他贴,最后看我](https://www.jianshu.com/p/9cfd5425ad90)
>!!!!!!!!!!!!!!!!!!!!然后执行pod package SDKLib.podspec --force --verbose.通过这个命令打包时候会自动将podspec中dependency的第三方库进行重命名.这样打出来的是SDKLib.framework.!!!!!!!!!!!!!!!!!!!!!!!!!!!!

```
需要特别强调的是，该插件通过对引用的三方库进行重命名很好的解决了类库命名冲突的问题。
```
####.podspec配置文件如下
```
#
# Be sure to run `pod lib lint SOCRLib.podspec' to ensure this is a
# valid spec before submitting.
#
# Any lines starting with a # are optional, but their use is encouraged
# To learn more about a Podspec see https://guides.cocoapods.org/syntax/podspec.html
#

Pod::Spec.new do |s|
# 名字要一致
  s.name             = 'SOCRLib'
# 版本要和git的tag版本一致
  s.version          = '0.2.0'
# 描述
  s.summary          = '通付盾活体识别SDK二次封装'

# This description is used to generate tags and improve search results.
#   * Think: What does it do? Why did you write it? What is the focus?
#   * Try to keep it short, snappy and to the point.
#   * Write the description between the DESC delimiters below.
#   * Finally, don't worry about the indent, CocoaPods strips it!

    s.description      = <<-DESC
        描述信息:这是一个二次封装SDK的lib,将会用到很多著名第三方SDK,该功能用于打包包含这些著名第三方(该插件通过对引用的三方库进行重命名很好的解决了类库命名冲突的问题。http://www.cnblogs.com/brycezhang/p/4117180.html)
                       DESC
    # 主页信息网址
    s.homepage         = 'https://github.com/tianNanYiHao/SOCRLib'
    # 截图地址
    # s.screenshots     = 'www.example.com/screenshots_1', 'www.example.com/screenshots_2'
    # 证书 一般用下面的格式 如果用了其他的格式 需要相应的修改
    s.license          = { :type => 'MIT', :file => 'LICENSE' }
    # 作者信息及邮箱
    s.author           = { 'tianNanYiHao' => '851085835@qq.com' }
    # spec配置文件的位置
    s.source           = { :git => '/Users/tiannanyihao/Desktop/SOCRLib', :tag => s.version.to_s }
    # 媒体文件
    # s.social_media_url = 'https://twitter.com/<TWITTER_USERNAME>'
    # 工程依赖系统版本
    s.ios.deployment_target = '8.0'
    # 源文件 包含 h,m
    s.source_files = 'SOCRLib/Classes/**/*.{h,m}'
    # 资源文件 .png/.bundle等(多个)
    # 'SOCRLib/Assets/*.png',
    s.resource_bundles = {
       'SOCRLib' =>[
                    'SOCRLib/Assets/com.baidu.idl.face.faceSDK.bundle',
                    'SOCRLib/Assets/com.baidu.idl.face.model.bundle',
                    'SOCRLib/Assets/CWResource.bundle'
                    ]
    }
    # 公开头文件 打包只公开特定的头文件
    s.public_header_files = 'SOCRLib/Classes/head/SOCR.h'
    # 调试公开所有的头文件 这个地方下面的头文件 如果是在Example中调试 就公开全部，需要打包就只公开特定的h文件
    # s.public_header_files = 'Pod/Classes/**/*.h'
    # 私有头文件
    # subcfiles.private_header_files = "MyLibrary/cfiles/**/*.h"
    # 是否是静态库 这个地方很重要 假如不写这句打出来的包 就是动态库 不能使用 一运行会报错 image not found
    s.static_framework  =  true
    # 载入第三方.a (如paynuc.a这种)
    #s.vendored_libraries = 'SOCRLib/Classes/openssl/include/*.{a}'
    # 载入第三方.a头文件
    #s.xcconfig = { 'USER_HEADER_SEARCH_PATHS' => 'SOCRLib/Classes/openssl/include/openssl/*.{h}' }
    # 链接设置 重要
    s.xcconfig = {'OTHER_LDFLAGS' => '-ObjC'}

    # 第三方开源框架(多个)
    s.dependency 'Masonry'

    # 第三方非开源framework(多个)
    s.vendored_frameworks = [
                            'SOCRLib/Classes/framework/IDLFaceSDK.framework',
                            'SOCRLib/Classes/framework/PayEgisFace.framework'
                            ]
    # 系统动态库(多个)
    s.frameworks = 'UIKit','CoreMedia','AVFoundation','Foundation'
    # 系统类库(多个) 注意:系统类库不需要写全名 去掉开头的lib
    s.libraries = 'stdc++'
end

```


#[关于使用CocoaPods的package打包Framework以及使用注意](https://www.jianshu.com/p/611049483be4)

#[CocoaPodsFramework静态库制作](https://blog.csdn.net/bsn1928/article/details/51362802)

#[3分钟让你的框架支持cocoapods,podspec文件讲解](https://www.jianshu.com/p/8a7b9232cbab)




#一些遇到的坑及解决办法
###[[Cocoapods]项目添加Cocoapods支持遇到的坑](https://www.jianshu.com/p/283584683b0b)

###[如何解决上传依赖Masonry的开源项目到Cocoapods时报错的问题](https://www.jianshu.com/p/282e5c7fe00e)

>file not found with <angled> include; use "quotes" instead 
>
>这个错误提示不能使用<>大括号来引用静态库而要使用“”来引用静态库
>
>import <Masonry> 会导致以上执行 pod lib lint SOCR.podspec 检查文件时,报错

###[通过CocoaPods打包framework](https://www.jianshu.com/p/e744b56d57ea)

###[[iOS dev] 使用cocoapods打包静态库(依赖私有库，开源库，私有库又包含静态库)](https://www.aliyun.com/jiaocheng/352443.html)




