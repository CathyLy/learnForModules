                            ### 深入理解 CocoaPods
#### 一.核心组件
    CocoaPods是用 Ruby 写的,最重要的ge'm:CocoaPods/CocoaPods, CocoaPods/Core, 和 CocoaPods/Xcodeproj
##### 1.CocoaPods/CocoaPod
    每当执行一个 pod 命令时，这个组件都将被激活
##### 2.CocoaPods/Core
    Core 组件提供支持与 CocoaPods 相关文件的处理，文件主要是 Podfile 和 podspecs
    a.Podfile
      
    b.Podspec 
      该文件描述了一个库是怎样被添加到工程中的.
      它支持的功能有：列出源文件、framework、编译选项和某个库所需要的依赖等
##### 3.CocoaPods/Xcodeproj
    这个 gem 组件负责所有工程文件的整合.它能够对创建并修改 .xcodeproj 和 .xcworkspace 文件
    
#### 二.运行 pod install 命令
    运行 pod install 命令时会引发许多操作 ,--verbose 可以详细了解命令执行的内容
    1.读取 Podfile 文件
       在加载 podspecs 过程中，CocoaPods 就建立了包括版本信息在内的所有的第三方库的列表。
       Podspecs 被存储在本地路径 ~/.cocoapods 中
    2.版本控制和冲突
    
    3.加载源文件
      CocoaPods 执行的下一步是加载源码。每个 .podspec 文件都包含一个源代码的索引，这些索引一般包裹一个 git 地址和 git tag.
      它们以 commit SHAs 的方式存储在 ~/Library/Caches/CocoaPods 中。这个路径中文件的创建是由 Core gem 负责的
    4.生成 Pods.xcodeproj
      每次 pod install 执行,如果检测到改动时，CocoaPods 会利用 Xcodeproj gem 组件对 Pods.xcodeproj 进行更新。
      如果该文件不存在，则用默认配置生成。否则，会将已有的配置项加载至内存中
    5.安装第三方库
      由于每个第三方库有不同的 target,因此对于每一个库,都会有几个文件需要添加:
      a.一个包含编译选项的 .xcconfig 文件
      b.一个同时包含编译设置和 CocoaPods 默认配置的私有 .xcconfig 文件
      c.一个编译所必须的 prefix.pch 文件
      d.另一个编译必须的文件 dummy.m
    6.写入至磁盘
      为了让这些成果能被重复利用，我们需要将所有的结果保存到一个文件中.Pods.xcodeproj,Podfile.lock和Manifest.lock都将写入磁盘.
    7.Podfile.lock
      它记录了需要被安装的 pod 的每个已安装的版本,
      如果你想知道已安装的 pod 是哪个版本，可以查看这个文件
      推荐将 Podfile.lock 文件加入到版本控制中,这有助于整个团队的一致性
    8.Manifest.lock
      这是每次运行 pod install 命令时创建的 Podfile.lock 文件的副本
      如果你遇见过这样的错误 沙盒文件与 Podfile.lock 文件不同步 (The sandbox is not in sync with the Podfile.lock),
      因为Manifest.lock文件和Podfile.lock文件不一致所引起的.
      由于Pods所在的目录并不总在版本控制之下,这样可以保证开发者运行app之前更新他们Pods
    
    9.xcproj
    
    mkdir ~/Desktop/objcio-command-line
    cd !$
    touch helloworld.c
    xcrun clang helloworld.c
    ./a.out
    xcrun size -x -l -m a.out


    