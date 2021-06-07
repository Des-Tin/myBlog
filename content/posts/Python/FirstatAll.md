---
title: "使用VSCODE学习Python"
date: 2020-06-10T22:26:02+08:00
draft: false
categories: [ "Python" ]
Toc : true
tags: [ "Python", "Develop"]
share : true 
keywords: [ "Python" ]
---

# 如何使用VSCODE作为主要开发环境  
  这是一篇介绍如何安装并使用vscode作为Python的开发环境的教程，读者需要有一系列的计算机操作能力。
## 安装相关软件  
### Python  
  既然是进行Python学习，首先最重要的工作当然是安装Python。
  1. **打开Python.org的官网**
  2. **找到你的操作系统的版本**
  3. **下载**（如果以上官网打不开可以在本博客下载。）

  [windows 32位](https://dev46.baidupan.com/062422bb/2020/06/24/3a6d54d6dd17ea89486eb6463de9e538.exe?st=bJw2wXsd7HIxpYcmdpQ80A&e=1593012609&b=BCYLclQgWTQAOgQ8BHkFMlMoXTkMIwo_aCXcJNwE0Un5VYghwBWA_c&fi=25255024&pid=60-167-78-151&up=1.)  
  [windows 64位](https://vip.d0.baidupan.com/file/?CW9bZQ4/VWRUXQU9AjdcMFdoBDxTfAN4VyQBbwU2VToGK1czCHsDb1MrVzJRKF1qVDoOJQI4UStRMwYmUGpXPwllW2kODFVoVGYFbgJkXGhXPwQ0UzkDMVdjATEFf1UyBnVXPQhnA2BTPVcxUTBdZFQ+DjsCe1EjUSYGPVA+V2YJO1s8DnxVMVQ0BXwCZFxpVyIEN1M6A2RXZwE0BTxVMAY3VzcIbQNmUzJXMlFhXW9UNg4+AmVRMFFgBmZQOFczCTtbPw5rVTRUOgU1AmVcO1c8BC9TaQN5VzUBIQUsVScGY1dyCDwDM1M4VzBRNV1vVDkOMwJtUWRRcAZ0UGVXOwlsW2oOblUwVDcFagJlXG1XPAQwUzsDM1dgASkFd1VyBmBXbAgiA2pTNVcnUXBdLFR5DjYCbFFmUW8GM1A8V2cJOVs5DmtVOFQkBSYCP1wtVzAEMFM+AzBXfgE0BW9VegY3VzQIewNlUzVXMA==)  
  [MacOS-10.9+](/download/python-3.8.3.pkg)  

  4. **接下来就是安装 (注意windows安装的时候要勾上<font style ="color:#FF7F50">Add Python 3.8 to PATH</font>**)  
*无视图上的python3.5字样*  
![setup](/image/python/python-setup.png)  

  5. **运行Python**

     打开命令提示符窗口（在开始菜单中搜索**<font style ="color:#FF7F50">cmd</font>**回车即可）后，输入python并回车，会有两种情况：  
     
      1. 情况一：  
      ```ascii
      ─────────────────────────────────────
      Command Prompt                                          - □ x 
      ─────────────────────────────────────
      Microsoft Windows [Version 10.0.0]            
      (c) 2015 Microsoft Corporation. All rights reserved.
                                                             
      C:\> python                                  
      Python 3.8.x ...                              
      [MSC v... 64 bit (AMD64)] on win32                      
      Type "help", "copyright", "credits" or "license" for mor
      information.                                            
      >>> _                                

      ```
      > 看到上面的画面，就说明Python安装成功！  
      >    你看到提示符`>>>`就表示我们已经在Python交互式环境中了，可以输入任何Python代码，回车后会立刻得到执行结果。    现在，输入**<font style ="color:#FF7F50">exit()</font>**并回车，就可以退出Python交互式环境（直接关掉命令行窗口也可以）。   
    
      2. 情况二：得到一个错误：
       ```ascii
      ─────────────────────────────────────
      Command Prompt                                          - □ x 
      ─────────────────────────────────────
      Microsoft Windows [Version 10.0.0]            
      (c) 2015 Microsoft Corporation. All rights reserved.
                                                             
     C:\> python                                             
     'python' is not recognized as an internal or external 
     command, operable program or batch file.                  
                                                             
     C:\> _                              
      
       ```
       > 这是因为Windows会根据一个**<font style ="color:#FF7F50">Path</font>**的环境变量设定的路径去查找**<font style ="color:#FF7F50">python.exe</font>**，如果没找到，就会报错。  
       > 如果在安装时漏掉了勾选**<font style ="color:#FF7F50">Add Python 3.8 to PATH</font>**，那就要手动把**<font style ="color:#FF7F50">python.exe</font>**所在的路径添加到**<font style ="color:#FF7F50">Path</font>**中。  
       > 如果你不知道怎么修改环境变量，建议把**<font style ="color:#FF7F50">Python安装程序</font>**安装程序重新运行一遍，务必记得勾上**<font style ="color:#FF7F50">Add Python 3.8 to PATH</font>**。  

<br>
<br>

### Visual Studio Code(VSCode)

![vscode](/image/python/vscode.jpg)

Visual Studio Code 的官方下载地址：<https://code.visualstudio.com/Download>

安装过程没有什么需要强调的内容，按照默认设置安装即可。

<br>

<br>

## 配置Python环境  

VSCode虽然安装好了，但是这个原始的VSCode还并不能愉快地开发Python。

我们需要安装一些拓展包（插件）才能继续使用它。


### 中文语言包

![python1](/image/python/python1.jpg)
仅在第一次演示如何搜索拓展包（插件）
![install](/image/python/install.png)
安装后，按下**Ctrl+Shift+P**打开命令面板，之后输入 **"config"** 筛选可用命令列表，最后选择**配置语言**命令，并选择**中文语言**即可生效。
![install](/image/python/install.gif)  

<br>

<br>

### Python相关支持
![need](/image/python/need.jpg)
提供与 Python 相关的绝大多数重要功能，比如调试，语法高亮，常用短语等。

<br>

安装后，写完代码可以直接使用VSCode直接运行了。
![needa](/image/python/needa.png)

<br>

<br>

## 辅助插件（可选）
### Bracket Pair Colorizer  
![need2](/image/python/need2.jpg)
一个可以让不同组的括号以不同颜色区分。
![need2a](/image/python/need2a.jpg)
<center>效果</center>

<br>

<br> 

### One Dark Pro 颜色主题
![need3](/image/python/need3.png)
这个主题比自带的深色主题更加生动鲜活（比如函数名加粗， 单行注释斜体等）。下图是一个简单的对比：
![need3a](/image/python/need3a.jpg)
<center>
自带的 Dark+（左）与 One Dark Pro（右）的效果对比</center>

<br>

<br>  

### Material Icon Theme  

Material质感的图标
![need4](/image/python/need4.jpg)  
![need4a](/image/python/need4a.jpg)

<center>默认图标（左）与 Material 图标（右）的对比</center>

<div align="right"><font style = "color:gray">部分参考</font></div><a herf = "https://zhuanlan.zhihu.com/p/93363496">知乎</a>