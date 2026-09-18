# 项目名称

> 一句话描述项目，例：C++练习，熟悉VS

## 📖 项目介绍

基于 CLion 开发的控制台程序。

- 开发IDE：CLion
- 编程语言：C / C++ / C#
- 项目类型：控制台应用

## ⚙️ 环境依赖

### C / C++

1. CMake
2. C/C++编译器：MinGW-w64 / GCC / Clang
3. CLion自动读取`CMakeLists.txt`构建项目

### C#

1. .NET SDK
2. CLion自带.NET插件支持C#项目

## 🚀 编译与运行

### C / C++

1. 将仓库克隆到本地，使用CLion打开项目文件夹
2. CLion自动加载CMake配置，等待项目索引完成
3. 右上角选择构建目标（Debug / Release）
4. 点击运行按钮 ▶️ 或者快捷键 `Shift+F10` 运行程序
5. `Shift+F9` 启动调试

> 手动CMake命令（终端）

```bash
mkdir build && cd build
cmake ..
make
./程序名
```

# Visual Studio 2019/2022/2026 开发 C++

## 前置

安装VS安装器，勾选 **使用C++的桌面开发** 工作负载。

> 项目路径、文件夹名称**禁止中文、空格**。

## 新建C++控制台项目

1. 创建新项目 → 选择 **控制台应用**
2. 生成默认项目，`.cpp` 主文件。

### 测试代码

```cpp
#include <iostream>
#include <windows.h>

int main()
{
    SetConsoleOutputCP(65001);
    std::cout << "VS C++中文测试：你好世界！" << std::endl;
    return 0;
}
```

## ✅中文乱码完整配置（MSVC）

1. **文件编码** ：文件 → 高级保存选项
   编码选择：**Unicode (UTF‑8 带签名)‑代码页 65001**（UTF‑8 with BOM）

> 找不到高级保存选项：工具 → 自定义 → 命令，添加到文件菜单。

2. **控制台编码**：**项目添加编译参数 `/utf‑8`（最重要）** 右键项目 → 属性 → 配置属性 → **C/C++ → 命令行** 其他选项填入：

```plaintext
/utf-8
```

确定，点击 **重新生成解决方案**。

> `/utf‑8`：源码和字符串都使用UTF‑8编码。

3. 代码兜底（main第一行）

```cpp
SetConsoleOutputCP(65001);
```

## 常用快捷键

- `Ctrl+Shift+B`：生成解决方案（编译）
- `Ctrl+F5`：不调试运行
- `F5`：调试运行，支持断点
- `F10`：单步跳过
- `F11`：单步进入

## 项目结构

```plaintext
Demo/
├─ Demo.sln          // 解决方案
├─ Demo.vcxproj      // C++项目文件
└─ Demo.cpp          // 源代码
```

## 多文件C++项目

直接往项目里添加 `.h`头文件、`.cpp`源文件。
所有cpp文件会自动参与编译，**不需要手动写编译命令**。

## 常见坑

1. 路径带中文：编译报错、头文件找不到、乱码。
2. 忘记加 `/utf‑8`：中文输出问号、编译报“不能映射字符”。
3. 只点运行没有重新生成：修改代码不生效。
4. 控制台一闪而过：
   调试模式VS新版会自动暂停；旧版本可以末尾加：

```cpp
#include <stdlib.h>
system("pause");
```

## VS2022优化

工具 → 选项 → 调试 → 常规
✅勾选 **使用Windows Terminal进行控制台调试启动**，对UTF‑8中文支持更好。

---

# VS各语言速记复习

| 语言     | VS工作负载     | 乱码核心配置                                    |
| ------ | ---------- | ----------------------------------------- |
| C++    | 使用C++的桌面开发 | 编译参数 `/utf‑8`，UTF‑8带BOM保存                 |
| C#     | .NET桌面开发   | `Console.OutputEncoding = Encoding.UTF8;` |
| Python | Python开发   | 环境变量 `PYTHONIOENCODING=utf‑8`             |
| Java   | 无原生支持      | 只适合编辑，javac手动编译 `-encoding UTF‑8`         |

> 对比：
> 
> - VS：C++/C#/Python很强，适合Windows平台大型程序。
> - VSCode：轻量，跨平台，C/C++需要手动配置`.vscode`。
> - CLion：C/C++跨平台，CMake项目管理。

需要我把 **VS、VSCode、CLion、Dev‑C++ 的C++开发对比总结**吗？

# C++四大IDE对比总结（VS2022 / VSCode / CLion / Dev‑C++）

> 系统：Windows，编译器分别：MSVC、MinGW‑GCC、MinGW‑GCC、MinGW‑GCC

| 项目     | Visual Studio         | VSCode                                     | CLion                | Embarcadero Dev‑C++ |
| ------ | --------------------- | ------------------------------------------ | -------------------- | ------------------- |
| 编译器    | MSVC                  | MinGW‑GCC                                  | MinGW‑GCC            | MinGW‑GCC           |
| 项目管理   | sln+vcxproj，图形化管理     | 无原生项目，文件夹模式                                | CMake                | 简易项目管理              |
| 配置文件   | 图形界面配置，几乎不用手写json     | `.vscode/tasks.json .vscode/launch.json`   | CMakeLists.txt       | 编译选项图形勾选            |
| 中文乱码核心 | 编译参数 `/utf‑8`         | `‑finput‑charset=UTF‑8 ‑fexec‑charset=GBK` | CMakeLists添加gcc字符集参数 | 编译选项添加gcc字符集参数      |
| 调试能力   | ⭐⭐⭐⭐⭐ 功能最全            | ⭐⭐⭐ 需要配置gdb                                | ⭐⭐⭐⭐⭐                | ⭐⭐ 调试弱，容易卡          |
| 多文件项目  | 直接添加cpp/h，自动编译        | tasks.json配置编译全部cpp                        | CMakeLists管理         | 添加到项目中              |
| 适合场景   | Windows大型项目、MFC、课程大作业 | 刷题、小demo、跨平台轻量开发                           | 算法、C++工程、CMake项目     | 入门教学、课堂作业，新手练习      |
| 缺点     | 软件体积巨大，启动慢            | 全部配置需要手动写，容易踩坑                             | 体积大，商业收费             | 老旧，功能简陋，调试不好用       |
| 快捷键    | `F5`调试，`Ctrl+F5`运行    | `F5`调试，`Ctrl+Shift+B`编译                    | `F5`调试               | F8编译运行              |

## 关键配置要点：

### Visual Studio（MSVC）

1.工作负载：**使用C++的桌面开发**

2.文件保存：**UTF‑8带BOM**

3.中文编码：项目属性 → C/C++ → 命令行：`/utf‑8`

main开头可加兜底：`SetConsoleOutputCP(65001);`

### VSCode（MinGW‑GCC）

1. 安装 C/C++ Extension Pack，MinGW‑w64配置PATH
2. 必须打开文件夹，生成`.vscode`三套json
3. tasks.json g++参数带上：`‑finput‑charset=UTF‑8 ‑fexec‑charset=GBK ‑g ‑std=c++17`
4. F5调试依赖gdb.exe路径配置正确

### CLion（MinGW‑GCC）

1. 新建CMake项目，所有编译配置写在`CMakeLists.txt`

```cmake
if(CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
    add_compile_options(-finput-charset=UTF-8 -fexec-charset=GBK)
endif()
```

2. Reload CMake Project；取消勾选 `Emulate terminal in output console`

### Dev‑C++（MinGW‑GCC）

1. 工具 → 编译选项，添加编译命令： `‑finput‑charset=UTF‑8 ‑fexec‑charset=GBK`
2. 文件编码优先 **UTF‑8 with BOM**

## 通用避坑（四个IDE全部适用）

1. 项目路径、文件夹、文件名**不要中文、空格**
2. Windows不要开启Beta全局UTF‑8，会大量老软件异常
3. C/C++调试一定要加调试符号：
   - MSVC：Debug模式
   - GCC：编译参数 `-g`
4. 编辑器乱码=文件编码；运行输出乱码=编译器参数/控制台代码页

## 选型建议

- 学校课程大作业Windows平台：**Visual Studio**
- 刷题、写小demo，追求轻量：**VSCode**
- 学习CMake、C++工程开发：**CLion**
- 刚入门学习语法，课堂教学：**Dev‑C++**

> 到这里，主流IDE(C/C++/C#/Java/Python)的基础使用和乱码问题全部梳理完毕。
> 接下来可以：
> 
> 做一份综合实操练习题；
> 
> 整理一份环境踩坑排错清单（PATH、环境变量、各种报错）。
