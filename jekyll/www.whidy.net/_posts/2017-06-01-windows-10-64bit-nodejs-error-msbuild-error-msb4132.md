---
author: whidy
comments: true
date: 2017-06-01 01:01:56+00:00
excerpt: '在win10 64位系统下,关于nodejs下通过npm install环境部署项目时出现报错''MSBUILD : error MSB4132:
  无法识别工具版本“2.0”。可用的工具版本为 "4.0"。''的解决办法'
layout: post
link: http://www.whidy.net/windows-10-64bit-nodejs-error-msbuild-error-msb4132.html
slug: windows-10-64bit-nodejs-error-msbuild-error-msb4132
title: 'Windows 10 64bit 下nodejs报错"MSBUILD : error MSB4132:..."解决'
wordpress_id: 2916
categories:
- IT技术
- 技术分享
tags:
- nodejs
- 技术
---

最近用自己笔记本办公配置windows 10下的开发环境(当然不排除WIN7下也有可能存在此问题),其中在进行一个项目的NPM INSTALL的时候一直出错...错误如下

![关于NPM INSTALL相关错误信息](http://www.whidy.net/wp-content/uploads/2017/06/errorMsg-400x261.png)

找了很多解决办法...都无效.十分沮丧...前几天在win7 64bit下也是折腾了好几天.依赖关系实在是复杂- -

我先来说说这个问题怎么处理吧.经过大量查找研究得出的结论...用了一行这个命令:

    
    ```
    npm config set msvs_version 2012 --global
    ```


参考资料:

[MSBUILD : error MSB4132: The tools version "2.0" is unrecognized. Available tools versions are "4.0".](https://github.com/chjj/pty.js/issues/60)(用户shawmanz32na的回答,也包含其他可能存在的问题的解决集合链接)

[Cannot install node modules that require compilation on Windows 7 x64/VS2012](http://stackoverflow.com/a/22411007/1342760)

当然也有人说修改注册表的方法,虽然我也用了不过没什么效果.我现在想还原注册表都不行了- -没备份.这里如果大家在试了以上方法仍然无效的情况下可以试试修改注册表的这块的版本号,但是个人不建议,或者提前做好注册表备份.这里不详细说明注册表方法,给个链接大家参考[MSBUILD : error MSB4132: 无法识别工具版本“2.0”。可用的工具版本为 "4.0"。](https://zhidao.baidu.com/question/232438617.html)

当然可能还存在其他的问题比如缺少VC++ 20XX运行库什么的

<del>可以试试这个软件下载站的工具[常用运行库合集(VB+VC运行库)](http://www.7edown.com/soft/down/soft_11510.html)</del>

以上链接怀疑包含广告，暂时删去，还是用一下3DM的运行库吧http://dl.3dmgame.com/201707/110601.html





* * *





## 更新2018.4.12


如果以上方案还是有问题， 比如我今天就出现这个情况了。。。然后又苦恼这个坑爹博主刚才那条命令搞了啥，想要还原，其实我就是改了一下全局的npm中微软编译时依赖库版本，文件路径在这


<blockquote>C:\Users\whidy\AppData\Roaming\npm\etc</blockquote>


你要是不爽就把这个里面的文件**npmrc**删掉就好了，然后再采取最后一个终极方案。前提你的确装了一些库，不过以下会再重新安装一下。方式如下：



 	
  1. **管理员权限**的Windows PowerShell或CMD，执行`npm install --global --production windows-build-tools`

 	
  2. 如果没有手动安装过Python则在上面一步自动安装Python后可能需要手动配置一下环境变量，Windows PowerShell或CMD中执行`npm config set python python2.7`

 	
  3. 重新设置该项目的msvs版本，同样Windows PowerShell或CMD中执行`npm config set msvs_version 2015`，或者全局的话加个`-g`。


再在项目中运行`npm install`，可能会出现很多警告，但是这些可以忽略的。

我不信还会出问题- -！

如果提示这些错误信息


    
    ```
    MSBUILD : error MSB3428: 未能加载 Visual C++ 组件“VCBuild.exe”。要解决此问题，1) 安装 .NET Framework 2.0 SDK；2) 安装 Microso
    ft Visual Studio 200
    5；或 3) 如果将该组件安装到了其他位置，请将其位置添加到系统路径中。 [D:\Webs\infinite-scroll-vuejs\node_modules\node-sass\build\binding.sln]
    ```



也可以按上面的方法尝试解决:

参考：[node-gyp](https://www.npmjs.com/package/node-gyp)

附上**MSVSVersion**版本说明：

    
    ```javascript
    versions = {
      '2017': VisualStudioVersion(
        '2017',
        'Visual Studio 2017',
        (solution_version = '12.00'),
        (project_version = '15.0'),
        (flat_sln = False),
        (uses_vcxproj = True),
        (path = path),
        (sdk_based = sdk_based),
        (default_toolset = 'v141'),
        (compatible_sdks = ['v8.1', 'v10.0'])
      ),
      '2015': VisualStudioVersion(
        '2015',
        'Visual Studio 2015',
        (solution_version = '12.00'),
        (project_version = '14.0'),
        (flat_sln = False),
        (uses_vcxproj = True),
        (path = path),
        (sdk_based = sdk_based),
        (default_toolset = 'v140')
      ),
      '2013': VisualStudioVersion(
        '2013',
        'Visual Studio 2013',
        (solution_version = '13.00'),
        (project_version = '12.0'),
        (flat_sln = False),
        (uses_vcxproj = True),
        (path = path),
        (sdk_based = sdk_based),
        (default_toolset = 'v120')
      ),
      '2013e': VisualStudioVersion(
        '2013e',
        'Visual Studio 2013',
        (solution_version = '13.00'),
        (project_version = '12.0'),
        (flat_sln = True),
        (uses_vcxproj = True),
        (path = path),
        (sdk_based = sdk_based),
        (default_toolset = 'v120')
      ),
      '2012': VisualStudioVersion(
        '2012',
        'Visual Studio 2012',
        (solution_version = '12.00'),
        (project_version = '4.0'),
        (flat_sln = False),
        (uses_vcxproj = True),
        (path = path),
        (sdk_based = sdk_based),
        (default_toolset = 'v110')
      ),
      '2012e': VisualStudioVersion(
        '2012e',
        'Visual Studio 2012',
        (solution_version = '12.00'),
        (project_version = '4.0'),
        (flat_sln = True),
        (uses_vcxproj = True),
        (path = path),
        (sdk_based = sdk_based),
        (default_toolset = 'v110')
      ),
      '2010': VisualStudioVersion(
        '2010',
        'Visual Studio 2010',
        (solution_version = '11.00'),
        (project_version = '4.0'),
        (flat_sln = False),
        (uses_vcxproj = True),
        (path = path),
        (sdk_based = sdk_based)
      ),
      '2010e': VisualStudioVersion(
        '2010e',
        'Visual C++ Express 2010',
        (solution_version = '11.00'),
        (project_version = '4.0'),
        (flat_sln = True),
        (uses_vcxproj = True),
        (path = path),
        (sdk_based = sdk_based)
      ),
      '2008': VisualStudioVersion(
        '2008',
        'Visual Studio 2008',
        (solution_version = '10.00'),
        (project_version = '9.00'),
        (flat_sln = False),
        (uses_vcxproj = False),
        (path = path),
        (sdk_based = sdk_based)
      ),
      '2008e': VisualStudioVersion(
        '2008e',
        'Visual Studio 2008',
        (solution_version = '10.00'),
        (project_version = '9.00'),
        (flat_sln = True),
        (uses_vcxproj = False),
        (path = path),
        (sdk_based = sdk_based)
      ),
      '2005': VisualStudioVersion(
        '2005',
        'Visual Studio 2005',
        (solution_version = '9.00'),
        (project_version = '8.00'),
        (flat_sln = False),
        (uses_vcxproj = False),
        (path = path),
        (sdk_based = sdk_based)
      ),
      '2005e': VisualStudioVersion(
        '2005e',
        'Visual Studio 2005',
        (solution_version = '9.00'),
        (project_version = '8.00'),
        (flat_sln = True),
        (uses_vcxproj = False),
        (path = path),
        (sdk_based = sdk_based)
      )
    };
    ```


参考：https://chromium.googlesource.com/external/gyp/+/master/pylib/gyp/MSVSVersion.py#259
