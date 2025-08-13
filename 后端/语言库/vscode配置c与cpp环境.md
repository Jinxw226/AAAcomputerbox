#vscode配置c与cpp环境 
# 步骤

1. 下载 [MinGW-W64](https://so.csdn.net/so/search?q=MinGW-W64&spm=1001.2101.3001.7020)
	- 官网：[Pre-built Toolchains - mingw-w64](https://www.mingw-w64.org/downloads/)
	- **MinGW-W64下载链接：**[Releases · msys2/msys2-installer (github.com)](https://github.com/msys2/msys2-installer/releases/)
	![[Pasted image 20250812141145.png]]
	![[下载mingw包.png]]
2. 安装
	![[Pasted image 20250812141308.png]]
	![[Pasted image 20250812141345.png]]
	默认勾选`立即运行MSYS2`，单击`完成`。
	当按下`完成`之后，会弹出打开一个 MSYS2 终端窗口。
	![[MSYS2 终端窗口.png]]
	在此终端中，通过输入以下命令并按回车键，安装 MinGW-w64 工具链：
	```shell
	pacman -S --needed base-devel mingw-w64-ucrt-x86_64-toolchain
	```
	出现这个界面，直接按回车键，默认接受所有的安装包。
	![[Pasted image 20250812141508.png]]
	当系统提示是否继续安装时，请输入`y`并回车。
	![[Pasted image 20250812141530.png]]
	之后就进入安装过程，稍等片刻。
	当所有的包都安装好后，直接关闭终端。
	![[Pasted image 20250812141550.png]]
3. 配置环境变量
	打开安装 MSYS2 的目录，先找到`ucrt64`文件夹并进入，再找到`bin`文件夹并进入，然后在地址栏中，复制路径。
	如果一开始用默认路径，那路径就是`C:\msys64\ucrt64\bin`。
	调出环境变量配置面板，双击系统变量path，新建刚才复制的路径
	![[Pasted image 20250812141831.png]]
	验证是否配置成功win+r
	回车之后，就可以调出 CMD 的终端窗口了，然后分别输入下面的命令，每输入一次命令后回车一次。
	```cmd
	gcc --version
	g++ --version
	gdb --version
	```
	出现如下图一样的信息，就说明 C/C++ 的编译环境已经安装好。
	![[Pasted image 20250812141944.png]]
4. vscode配置
	把tasks.json文件配置如下：
```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "C: gcc.exe 编译活动文件",
      "type": "shell",
      "command": "D:/msys64/ucrt64/bin/gcc.exe",
      "args": [
        "-fdiagnostics-color=always",
        "-g",
        "${file}",
        "-o",
        "${fileDirname}/${fileBasenameNoExtension}.exe",
        "-Wall",
        "-std=c11",
        "-mconsole"
      ],
      "group": "build",
      "problemMatcher": [
        "$gcc"
      ]
    },
    {
      "label": "C++: g++.exe 编译活动文件",
      "type": "shell",
      "command": "D:/msys64/ucrt64/bin/g++.exe",
      "args": [
        "-fdiagnostics-color=always",
        "-g",
        "${file}",
        "-o",
        "${fileDirname}/${fileBasenameNoExtension}.exe",
        "-Wall",
        "-std=c++17",
        "-mconsole"
      ],
      "group": "build",
      "problemMatcher": [
        "$gcc"
      ]
    },
    {
      "type": "cppbuild",
      "label": "C/C++: g++.exe 生成活动文件",
      "command": "D:\\msys64\\ucrt64\\bin\\g++.exe",
      "args": [
        "-fdiagnostics-color=always",
        "-g",
        "${file}",
        "-o",
        "${fileDirname}\\${fileBasenameNoExtension}.exe"
      ],
      "options": {
        "cwd": "${fileDirname}"
      },
      "problemMatcher": [
        "$gcc"
      ],
      "group": {
        "kind": "build",
        "isDefault": true
      },
      "detail": "调试器生成的任务。"
    }
  ]
}
```

将launch.json文件配置如下：
```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "C++: GDB 调试",
      "type": "cppdbg",
      "request": "launch",
      "program": "${fileDirname}/${fileBasenameNoExtension}.exe",
      "args": [],
      "stopAtEntry": false,
      "cwd": "${workspaceFolder}",
      "environment": [],
      "externalConsole": true,  // 改为true以显示独立控制台
      "MIMode": "gdb",
      "miDebuggerPath": "D:/msys64/ucrt64/bin/gdb.exe",
      "setupCommands": [
        {
          "description": "为 gdb 启用整齐打印",
          "text": "-enable-pretty-printing",
          "ignoreFailures": true
        }
      ],
      "preLaunchTask": "C++: g++.exe 编译活动文件"  // 确保与tasks.json一致
    }
  ]
}
```


> [!NOTE] 注意
> 配置文件中的环境变量需要改成自己系统中的！！！

调试选择
![[Pasted image 20250813175308.png]]