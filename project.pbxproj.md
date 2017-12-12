###  .xcodeproj文件内容
    xcode将我们的配置信息都统一写到了project.pbxproj文件里，.xcodeproj文件可以通过显示包内容查看：
    一).project.pbxproj  是工程描述文件，描述了工程里的源码文件，schema设置等
    二).project.xcworkspace
    三).xcuserdata  一般是跟用户相关的一些设置，如断点记录等，一般不会放到版本管理中
    
### 一.project.pbxproj 的解析
#### 1.内容规则
      1).project.pbxproj使用UUID作为交叉引用的索引，保证每一个配置信息对象的唯一性，UUID是根据机器硬件和时间戳生成，避免了多人在同一时间段
        操作修改工程文件带来的问题，工程中每一个配置对象都有一个唯一的UUID，其他配置对象想要引用某一个配置对象直接是有UUID
    
      2).可以把整个文件的内容想象成一个字典，字典的第一层总共有5个键值对，key分别是archiveVersion、objectVersion，classes、objects、rootObject
    
      3).所有的配置对象都放在了objects对应的value中，objects中的键值被分成了若干个section，每一个对象内部的属性会把isa排在最前面
         /* Begin PBXNativeTarget section */
		4CB9151A1FCD5E8F00873A58 /* Build_demo */ = {
			isa = PBXNativeTarget;
			buildConfigurationList = 4CB915341FCD5E8F00873A58 /* Build configuration list for PBXNativeTarget "Build_demo" */;
			buildPhases = (
				4CB915171FCD5E8F00873A58 /* Sources */,
				4CB915181FCD5E8F00873A58 /* Frameworks */,
				4CB915191FCD5E8F00873A58 /* Resources */,
			);
			buildRules = (
			);
			dependencies = (
			);
			name = Build_demo;
			productName = Build_demo;
			productReference = 4CB9151B1FCD5E8F00873A58 /* Build_demo.app */;
			productType = "com.apple.product-type.application";
		};
        /* End PBXNativeTarget section */
    
    
    
#### 2.内容类型
    1.工程文件关联信息,如PBXBuildFile、PBXFileReference
    2.组织结构分类信息，如PBXGroup
    3.项目工程配置信息，如XCBuildConfiguration、XCConfigurationList

#### 3.元素
    以下是文件格式中包含的元素列表： 
  
![image](https://raw.githubusercontent.com/CathyLy/imageForSource/master/pbxproj/element.png)
    
#### 4.root element
    根部分包含的一般信息
    

属性 | 类型 | 值 |注释
---|---|-----|----------------|
archiveVersion | number | 1 |      默认值 |
classes | List | 空   |
objectVersion | number |    | xcode版本的兼容性枚举  |
objects | Map | 元素结构   | 元素标识符索引的组织结构
rootObject | Reference | 元素索引   | 对象是PBXProject元素的引用

#### 5.PBXAggregateTarget

![image](https://raw.githubusercontent.com/CathyLy/imageForSource/master/pbxproj/PBXAggregateTarget.png)


#### 6.PBXBuildFile

![image](https://raw.githubusercontent.com/CathyLy/imageForSource/master/pbxproj/PBXBuildFile.png)


    /* Begin PBXBuildFile section */
		4CB915201FCD5E8F00873A58 /* AppDelegate.m in Sources */ = {isa = PBXBuildFile; fileRef = 4CB9151F1FCD5E8F00873A58 /* AppDelegate.m */; };
		4CB915231FCD5E8F00873A58 /* ViewController.m in Sources */ = {isa = PBXBuildFile; fileRef = 4CB915221FCD5E8F00873A58 /* ViewController.m */; };
		4CB915261FCD5E8F00873A58 /* Main.storyboard in Resources */ = {isa = PBXBuildFile; fileRef = 4CB915241FCD5E8F00873A58 /* Main.storyboard */; };
		4CB9152B1FCD5E8F00873A58 /* Assets.xcassets in Resources */ = {isa = PBXBuildFile; fileRef = 4CB9152A1FCD5E8F00873A58 /* Assets.xcassets */; };
		4CB9152E1FCD5E8F00873A58 /* LaunchScreen.storyboard in Resources */ = {isa = PBXBuildFile; fileRef = 4CB9152C1FCD5E8F00873A58 /* LaunchScreen.storyboard */; };
		4CB915311FCD5E8F00873A58 /* main.m in Sources */ = {isa = PBXBuildFile; fileRef = 4CB915301FCD5E8F00873A58 /* main.m */; };
		4CB915391FCD7ADA00873A58 /* Person.m in Sources */ = {isa = PBXBuildFile; fileRef = 4CB915381FCD7ADA00873A58 /* Person.m */; };
		4CB9153C1FCD7C3E00873A58 /* hello.c in Sources */ = {isa = PBXBuildFile; fileRef = 4CB9153A1FCD7C3E00873A58 /* hello.c */; };
    /* End PBXBuildFile section */
    
#### 7.PBXBuildPhase
    build phases的一个抽象父类元素
#### 8.PBXContainerItemProxy
![image](https://raw.githubusercontent.com/CathyLy/imageForSource/master/pbxproj/PBXContainerItemProxy.png)

#### 9.PBXCopyFilesBuildPhase
![image](https://raw.githubusercontent.com/CathyLy/imageForSource/master/pbxproj/PBXCopyFilesBuildPhase.png)
 
    /* Begin PBXCopyFilesBuildPhase section */
		4CB59AA11FDFA79700A38F5C /* CopyFiles */ = {
			isa = PBXCopyFilesBuildPhase;
			buildActionMask = 2147483647;
			dstPath = "";
			dstSubfolderSpec = 7;
			files = (
			);
			runOnlyForDeploymentPostprocessing = 0;
		};
    /* End PBXCopyFilesBuildPhase section */
		
		
#### 10.PBXFileElement
    file and group 的抽象父类
#### 11.PBXFileReference
    PBXFileReference使用来跟踪每一个外部文件引用的项目：源文件、资源文件、库、生成的应用程序文件等等
   
![image](https://raw.githubusercontent.com/CathyLy/imageForSource/master/pbxproj/PBXFileReference.png)

#### 12.PBXFrameworksBuildPhase
    build phase的连接类库

![image](https://raw.githubusercontent.com/CathyLy/imageForSource/master/pbxproj/PBXFrameworksBuildPhase.png)

#### 13.PBXGroup
     group files or group 的元素 

![image](https://raw.githubusercontent.com/CathyLy/imageForSource/master/pbxproj/PBXGroup.png)
 
    /* Begin PBXGroup section */
		4CB915121FCD5E8F00873A58 = {
			isa = PBXGroup;
			children = (
				4CB9151D1FCD5E8F00873A58 /* Build_demo */,
				4CB9151C1FCD5E8F00873A58 /* Products */,
			);
			sourceTree = "<group>";
		};
		4CB9151C1FCD5E8F00873A58 /* Products */ = {
			isa = PBXGroup;
			children = (
				4CB9151B1FCD5E8F00873A58 /* Build_demo.app */,
			);
			name = Products;
			sourceTree = "<group>";
		};
		4CB9151D1FCD5E8F00873A58 /* Build_demo */ = {
			isa = PBXGroup;
			children = (
				4CB9151E1FCD5E8F00873A58 /* AppDelegate.h */,
				4CB9151F1FCD5E8F00873A58 /* AppDelegate.m */,
				4CB915211FCD5E8F00873A58 /* ViewController.h */,
				4CB915221FCD5E8F00873A58 /* ViewController.m */,
				4CB915371FCD7ADA00873A58 /* Person.h */,
				4CB915381FCD7ADA00873A58 /* Person.m */,
				4CB9153A1FCD7C3E00873A58 /* hello.c */,
				4CB9153B1FCD7C3E00873A58 /* hello.h */,
				4CB915241FCD5E8F00873A58 /* Main.storyboard */,
				4CB9152A1FCD5E8F00873A58 /* Assets.xcassets */,
				4CB9152C1FCD5E8F00873A58 /* LaunchScreen.storyboard */,
				4CB9152F1FCD5E8F00873A58 /* Info.plist */,
				4CB915301FCD5E8F00873A58 /* main.m */,
			);
			path = Build_demo;
			sourceTree = "<group>";
		};
    /* End PBXGroup section */
    
#### 14.PBXHeadersBuildPhase

    build phase的连接类库

![image](https://raw.githubusercontent.com/CathyLy/imageForSource/master/pbxproj/PBXHeadersBuildPhase.png)

#### 15.PBXLegacyTarget
#### 16.PBXNativeTarget
    build target元素的一个二进制内容(应用程序或库) 

![image](https://raw.githubusercontent.com/CathyLy/imageForSource/master/pbxproj/PBXNativeTarget.png)

     /* Begin PBXNativeTarget section */
		4CB9151A1FCD5E8F00873A58 /* Build_demo */ = {
			isa = PBXNativeTarget;
			buildConfigurationList = 4CB915341FCD5E8F00873A58 /* Build configuration list for PBXNativeTarget "Build_demo" */;
			buildPhases = (
				4CB915171FCD5E8F00873A58 /* Sources */,
				4CB915181FCD5E8F00873A58 /* Frameworks */,
				4CB915191FCD5E8F00873A58 /* Resources */,
				4CB59AA11FDFA79700A38F5C /* CopyFiles */,
			);
			buildRules = (
			);
			dependencies = (
			);
			name = Build_demo;
			productName = Build_demo;
			productReference = 4CB9151B1FCD5E8F00873A58 /* Build_demo.app */;
			productType = "com.apple.product-type.application";
		};
    /* End PBXNativeTarget section */


#### 17.PBXProject
     build target元素的一个二进制内容(应用程序或库)
     
![image](https://raw.githubusercontent.com/CathyLy/imageForSource/master/pbxproj/PBXProject.png)
     
     /* Begin PBXProject section */
		4CB915131FCD5E8F00873A58 /* Project object */ = {
			isa = PBXProject;
			attributes = {
				LastUpgradeCheck = 0900;
				ORGANIZATIONNAME = nothing;
				TargetAttributes = {
					4CB9151A1FCD5E8F00873A58 = {
						CreatedOnToolsVersion = 9.0;
						ProvisioningStyle = Manual;
					};
				};
			};
			buildConfigurationList = 4CB915161FCD5E8F00873A58 /* Build configuration list for PBXProject "Build_demo" */;
			compatibilityVersion = "Xcode 8.0";
			developmentRegion = en;
			hasScannedForEncodings = 0;
			knownRegions = (
				en,
				Base,
			);
			mainGroup = 4CB915121FCD5E8F00873A58;
			productRefGroup = 4CB9151C1FCD5E8F00873A58 /* Products */;
			projectDirPath = "";
			projectRoot = "";
			targets = (
				4CB9151A1FCD5E8F00873A58 /* Build_demo */,
			);
		};
    /* End PBXProject section */
    
#### 18.PBXResourcesBuildPhase
    build phase的复制资源
![image](https://raw.githubusercontent.com/CathyLy/imageForSource/master/pbxproj/PBXResourcesBuildPhase.png)

     /* Begin PBXResourcesBuildPhase section */
		4CB915191FCD5E8F00873A58 /* Resources */ = {
			isa = PBXResourcesBuildPhase;
			buildActionMask = 2147483647;
			files = (
				4CB9152E1FCD5E8F00873A58 /* LaunchScreen.storyboard in Resources */,
				4CB9152B1FCD5E8F00873A58 /* Assets.xcassets in Resources */,
				4CB915261FCD5E8F00873A58 /* Main.storyboard in Resources */,
			);
			runOnlyForDeploymentPostprocessing = 0;
		};
    /* End PBXResourcesBuildPhase section */


#### 19.PBXShellScriptBuildPhase
    build phase的复制资源 
   
![image](https://raw.githubusercontent.com/CathyLy/imageForSource/master/pbxproj/PBXShellScriptBuildPhase.png)

#### 20.PBXSourcesBuildPhase
    This is the element for the sources compilation build phase. 
![image](https://raw.githubusercontent.com/CathyLy/imageForSource/master/pbxproj/PBXSourcesBuildPhase.png)

    
    /* Begin PBXSourcesBuildPhase section */
		4CB915171FCD5E8F00873A58 /* Sources */ = {
			isa = PBXSourcesBuildPhase;
			buildActionMask = 2147483647;
			files = (
				4CB9153C1FCD7C3E00873A58 /* hello.c in Sources */,
				4CB915231FCD5E8F00873A58 /* ViewController.m in Sources */,
				4CB915391FCD7ADA00873A58 /* Person.m in Sources */,
				4CB915311FCD5E8F00873A58 /* main.m in Sources */,
				4CB915201FCD5E8F00873A58 /* AppDelegate.m in Sources */,
			);
			runOnlyForDeploymentPostprocessing = 0;
		};
    /* End PBXSourcesBuildPhase section */
    
#### 21.PBXTarget
    This element is an abstract parent for specialized targets.
#### 22.PBXTargetDependency
    This is the element for referencing other target through content proxies. 
  
![image](https://raw.githubusercontent.com/CathyLy/imageForSource/master/pbxproj/PBXTargetDependency.png)

#### 23.PBXVariantGroup
     This is the element for referencing localized resources. 
![image](https://raw.githubusercontent.com/CathyLy/imageForSource/master/pbxproj/PBXVariantGroup.png)
    
    /* Begin PBXVariantGroup section */
		4CB915241FCD5E8F00873A58 /* Main.storyboard */ = {
			isa = PBXVariantGroup;
			children = (
				4CB915251FCD5E8F00873A58 /* Base */,
			);
			name = Main.storyboard;
			sourceTree = "<group>";
		};
		4CB9152C1FCD5E8F00873A58 /* LaunchScreen.storyboard */ = {
			isa = PBXVariantGroup;
			children = (
				4CB9152D1FCD5E8F00873A58 /* Base */,
			);
			name = LaunchScreen.storyboard;
			sourceTree = "<group>";
		};
    /* End PBXVariantGroup section */
 
 #### 24.XCBuildConfiguration

    This is the element for defining build configuration. 
![image](https://raw.githubusercontent.com/CathyLy/imageForSource/master/pbxproj/XCBuildConfiguration.png)


#### 25.XCConfigurationList
     This is the element for listing build configurations. 
     
![image](https://raw.githubusercontent.com/CathyLy/imageForSource/master/pbxproj/XCConfigurationList.png)
     
     /* Begin XCConfigurationList section */
		4CB915161FCD5E8F00873A58 /* Build configuration list for PBXProject "Build_demo" */ = {
			isa = XCConfigurationList;
			buildConfigurations = (
				4CB915321FCD5E8F00873A58 /* Debug */,
				4CB915331FCD5E8F00873A58 /* Release */,
			);
			defaultConfigurationIsVisible = 0;
			defaultConfigurationName = Release;
		};
		4CB915341FCD5E8F00873A58 /* Build configuration list for PBXNativeTarget "Build_demo" */ = {
			isa = XCConfigurationList;
			buildConfigurations = (
				4CB915351FCD5E8F00873A58 /* Debug */,
				4CB915361FCD5E8F00873A58 /* Release */,
			);
			defaultConfigurationIsVisible = 0;
			defaultConfigurationName = Release;
		};
    /* End XCConfigurationList section */

	在ci编译前用服务器上相应的mobileprovision替换PROVISIONING_PROFILE后面的mobileprovision(ps:mobileprovision文件名通常以字符串命令)
	
	