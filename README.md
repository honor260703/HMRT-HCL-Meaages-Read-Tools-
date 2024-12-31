# HMRT(HCL-Meaages-Read-Tools).py 脚本介绍

## 概述
`HMRT(HCL-Meaages-Read-Tools).py` 是一个用于处理 `.net` 文件并生成 `MobaXterm Sessions.mxtsessions` 文件的Python脚本。该脚本能够读取指定目录下的所有 `.net` 文件，提取其中的设备信息，并根据这些信息生成 `MobaXterm Sessions.mxtsessions` 文件。

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
