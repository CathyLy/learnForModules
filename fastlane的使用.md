### fastlane的使用
#### 一.自动化流程的工具
    1.scan 自动化测试工具 ,封装了Unit Test
    2.sigh 针对iOS项目开发证书和Provision 的下载工具
    3.match 同步团队每个人的证书和 Provision file 的超赞工具，规范 代码签名
    （虽然里面有些设定比较损）
    4.gym 针对于 iOS 打包和签名的自动化工具，完爆 xctool ，而 shenzhen 也放弃维护
    5.qyer 团队定制的工具，用于检测包和上传到自己的内部分发平台
    6.fastlane 简单理解就是控制整体流程和实现的框架容器
    
#### 二.fastlane的基本构成
    action:fastlane的插件
    lane:fastlane的任务,一个可以包含多个lanes,通过fastlane cli传入制定的lane来执行
    
    lane :adhoc do
    # build version 自动加一
    increment_build_number
    # 执行 pod install
    cocoapods
    # 调用 facebook 的 xctool 进行单元测试
    xctool
    # 对模拟器运行的 App 进行截图
    snapshot
    # 安装团队证书和 profiles
    match
    # 上传 App 元数据和签名的 ipa 到 iTunes Conneects
    deliver
    # 把截图套进一个设备外壳
    frameit
    # 允许自定义的脚本文件
    sh "./customScript.sh"
    # 发消息到 slack
    slack
    end
    
#### 二.安装
    gem install fastlane
#### 三.初始化
    有两种初始化方式:
    
    一是通过命令 fastlane init 会进行联网,根据输入的Apple ID来验证你的应用是否存在,
    通过获取的信息创建一个fastlane的目录,写入相应的文件
    Fastfile:核心文件,主要用于cli调用和处理具体流程
    Appfile : 从 Apple Developer Portal 获取和项目相关的信息
    Deliverfile : 从 iTunes Connect 获取和项目相关的信息
    
声明周期:
方法名 | 说明  
---|---
before_all | 在执行 lane 之前只执行一次
before_each | 每次执行 lane 之前都会执行一次
lane | 自定义的任务
after_each | 每次执行lane之后都会执行一次
after_all| 在执行lane成功结束之后执行一次
error | 在执行上述情况环境报错都会中止并执行一次

#### 四.任务(lane)

任务定义:
 定义 | 是否必须 | 说明 |        备注
-----|---|--------|---------
desc | false |方法描述 | 可多次 使用达到换行的目的
name | true | 方法名   | 符号化的方法名
options | false | 方法参数 | 返回Hash类型
task | true | 方法主体 | 参考 ruby 的方法代码且支持 ruby 代码

任务执行:
    
    默认执行 fastlane build
    传递参数 fastlane build adhoc:true
任务互调:

    lane 其实可以理解为 def 的别名，因此多个 lane 的话实际上是可以相互调用的，
    这样其实我就可以把 cocoapods 的执行放到单独的 lane 里面而不是 before_all ，
    这样执行非构建的任务就不会执行不相关的任务或动作，
    因此 fastlane 而产生了一个私有任务用内部使用 private_lane
    
任务返回值:

    每一个lane最后一行默认作为返回值
    lane :sum do |options|
    options[:a] + optiona[:b]
    end

    lane :calculate do
    value = sum(a: 3, b: 5)
    puts value #=> 8
    end
    
引入外部任务文件:
    
    1.import  导入本地文件
    # 导入 lanes 目录的 AndroidFastfile
    import "lanes/AndroidFastfile"
    
    2.import_from_git - 导入 git 仓库文件
    原理是先把 git 仓库克隆下来后在引入相对于的文件，因此建议国内在没有网络加速（翻墙）的情况下尽量不用引入比较大的 git 仓库，否则使用会需要漫长的等待…
    # 导入 mozilla/firefox-ios 项目下 fastlane 下面 Fastfile 文件
    import_from_git(url: 'https://github.com/mozilla/firefox-ios')
    # 或者
    import_from_git(url: 'git@github.com:mozilla/firefox-ios.git',
                   path: 'fastlane/Fastfile')
                   
    假若外部引入的 Fastfile 有个方法是 build ，在命令行工具直接执行即可，如果外部和内部都有相同的任务名，执行会直接报错：
    $ fastlane ios build
    [!] Lane 'gradle' was defined multiple times!
    
任务查看:
    
    fastlane lanes
#### 五.扩展(action)

    
    
    

    




