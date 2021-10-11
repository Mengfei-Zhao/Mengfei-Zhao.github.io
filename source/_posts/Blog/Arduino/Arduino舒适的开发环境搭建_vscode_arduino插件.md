---
title: Arduino舒适的开发环境搭建：vscode+arduino插件
date: 2021-10-10 12:26:01
tags:
- Arduino
- vscode
categories:
- vscode
- Arduino
comments: true
---


------

* 板卡：Arduino uno
* OS: win10
* 开发环境：vscode + arduino插件
* 工程作用：可以实现arduino的LED闪烁。

------

安装Arduino插件：

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211007192010599.png" alt="image-20211007192010599" style="zoom:70%;" />

目录结构：

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211007192231896.png" alt="image-20211007192231896" style="zoom:67%;" />

### 1、在vscode的用户配置文件settings.json中加入下面这些内容，用来对arduino插件做全局的默认配置：

```json
  "arduino.path": "G:\\Arduino", // arduino IDE安装的位置
  "arduino.commandPath": "arduino_debug.exe", //这是一个上述位置中的exe文件
  "C_Cpp.default.browse.path": [ 
    "G:\\Arduino\\**",
    "G:\\Arduino\\hardware\\tools\\avr\\avr\\include\\**",
    "G:\\Arduino\\hardware\\tools\\avr\\lib\\gcc\\avr\\7.3.0\\include\\**",
    "G:\\Arduino\\hardware\\arduino\\avr\\cores\\arduino\\**",
    "G:\\Arduino\\hardware\\arduino\\avr\\variants\\standard\\**",
    "G:\\ArduinoPrj\\libraries\\**"
  ],
  "C_Cpp.default.includePath": [ //头文件引用路径
    "G:\\Arduino\\**",
    "G:\\Arduino\\hardware\\tools\\avr\\avr\\include\\**",
    "G:\\Arduino\\hardware\\tools\\avr\\lib\\gcc\\avr\\7.3.0\\include\\**",
    "G:\\Arduino\\hardware\\arduino\\avr\\cores\\arduino\\**",
    "G:\\Arduino\\hardware\\arduino\\avr\\variants\\standard\\**",
    "G:\\ArduinoPrj\\libraries\\**"
  ],
  "arduino.logLevel": "info",
  "arduino.allowPDEFiletype": false,
  "arduino.enableUSBDetection": true,
  "arduino.disableTestingOpen": false,
  "arduino.skipHeaderProvider": false,
  "arduino.disableIntelliSenseAutoGen": true,
  "arduino.additionalUrls": [
      "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json",
      "http://arduino.esp8266.com/stable/package_esp8266com_index.json"
  ],
  "arduino.defaultBaudRate": 115200,
```

### 2、在.vscode文件夹下新建一个c_cpp_settings.json，并添加下面内容：

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211008094940783.png" alt="image-20211008094940783" style="zoom:80%;" />

上述中的includePath是需要认真设置的，这个不设置也行，在编写源文件时，会在#include的头文件下面出现红色波浪线，提示找不到文件之类的，例如下方这个。此时点击Quick Fix，把路径添加上就可以了，新添加的路径会自动出现在上方c_cpp_settings.json中的includePath中。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211008095347411.png" alt="image-20211008095347411" style="zoom:80%;" />

### 3、在.vscode文件夹下新建一个arduino.json，并添加下面内容：

```json
{
    "sketch": "appMain.ino", 
    "port": "COM10", 
    "board": "arduino:avr:uno", 
    "output": "./build", 
    "debugger": "jlink",
    "intelliSenseGen": "global"
}
```

### 4、编写源文件

请在[github](https://github.com/Mengfei-Zhao/utility)中下载。

### 5、编译烧录

写好源文件后，点击图中的A是编译，B是烧录，C是修改串口号，D是c_cpp_settings.json中的"name"

![image-20211008100422545](https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211008100422545.png)

### 6、搞定



**工程文件有需要的话，请到[Github](https://github.com/Mengfei-Zhao/utility)中下载**

**另外，vscode-arduino官方的文档看这个[链接](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino)。**

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/点赞.gif" alt="点赞" style="zoom:50%;" />
