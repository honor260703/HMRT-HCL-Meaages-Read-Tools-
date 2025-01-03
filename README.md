# HMRT(HCL-Meaages-Read-Tools).py 脚本介绍

## 概述
`HMRT(HCL-Meaages-Read-Tools).py` 是一个用于处理 `.net` 文件并生成 `MobaXterm Sessions.mxtsessions` 文件的Python脚本。该脚本能够读取指定目录下的所有 `.net` 文件，提取其中的设备信息，并根据这些信息生成 `MobaXterm Sessions.mxtsessions` 文件。
## HCL不是自带可以连到MobaXterm吗？为什么还需要这个工具？
![图片](https://github.com/user-attachments/assets/1b0f941f-a6e2-4a71-8bbf-9684306daaf0)

如上图所示，当HCL与MobaXterm绑定后，再双击网络设备启动MobaXterm会话，新建的MobaXterm会话名只会显示本地IP，不会显示设备名，而自己手动去修改会话名或直接新建Telnet会话又过于繁琐且麻烦
而使用脚本就不会存在这种问题
![图片](https://github.com/user-attachments/assets/c480627e-db2a-43d7-8272-4e8ec0c27644)
## 我该怎么使用？
很简单，你只需要花费你一丢丢流量去下载exe程序，并放在保存好的HCL拓扑文件夹内，确保exe程序身边确实有.net文件
![图片](https://github.com/user-attachments/assets/21e1313a-8c80-41c6-8940-1382dd1b68b0)
然后直接双击运行exe程序
![图片](https://github.com/user-attachments/assets/55fb30a4-e4a9-4895-9b19-afcf13e06399)
便可以直接生成会话文件，最后再导入进你电脑的MobaXterm内就行
## 版权声明
本代码遵循MIT许可证。同时，使用者在使用、修改和分发本代码时，应保留所有原始注释。

## 作者信息
- **作者**: 黄荣彬
- **Email**: 2607037721@qq.com

## 主要功能

1. **读取 `.net` 文件**:
   - 脚本会遍历指定目录及其子目录，查找所有后缀名为 `.net` 的文件。
   - 使用多种编码格式（UTF-8, GBK, GB2312, ISO-8859-1, Latin-1）尝试读取文件内容。

2. **提取设备信息**:
   - 使用正则表达式从 `.net` 文件内容中提取设备名称、设备ID和设备MAC地址。
   - 提取的信息包括：
     - 设备名称 (`device_name`)
     - 设备ID (`device_id`)
     - 设备MAC地址 (`bridge_mac`)

3. **打印设备信息**:
   - 对提取的设备信息按设备ID升序排序。
   - 打印设备总数，并逐个打印每个设备的名称、ID和MAC地址。

4. **生成 `MobaXterm Sessions.mxtsessions` 文件**:
   - 创建或更新 `MobaXterm Sessions.mxtsessions` 文件。
   - 文件开头包含每个 `.net` 文件的固定三行内容：
     - `[Bookmarks]`
     - `SubRep=<.net文件名>`
     - `ImgNum=41`
   - 对于每个设备，生成一个会话条目，格式如下：
     - `<设备名>=#98#1%127.0.0.1%<30000+设备ID>%%%2%%%%%0%0%%1080%%%0%-1%0#MobaFont%11%0%0%-1%40%236,236,236%30,30,30%180,180,192%0%-1%0%%xterm%-1%0%_Std_Colors_0_%80%24%0%1%-1%<none>%%0%1%-1%-1%#0# #-1`
