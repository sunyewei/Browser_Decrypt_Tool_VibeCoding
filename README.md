# 📂 AES-256 离线批量加解密工具 (Vibe-Coding版)

![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)
![Tech Stack](https://img.shields.io/badge/Tech-Vanilla_JS_|_Web_Crypto_API-success)

一个极其轻量、安全且优雅的纯前端文件批量加解密工具。完全基于浏览器的原生 `Web Crypto API` 构建，**所有数据处理均在本地完成，无任何服务器上传行为**，最大程度保障您的数据隐私与安全。

## ✨ 核心特性

- **🔒 安全保障**：采用 `AES-GCM` 256位加密算法，搭配 PBKDF2 密钥派生和随机 Salt/IV，每次加密的密文均不相同，防破解能力极强。
- **🌐 100% 纯本地运行**：无需后端服务器，断网环境依然可用，绝对防止隐私泄露。
- **📦 丝滑的批量处理**：
  - 支持拖拽添加、框选添加、多次累加文件。
  - 批量加密完成后，自动将所有文件打包为 `.zip` 下载。
- **📶 网络自适应（优雅降级）**：内置智能网络探测，如果由于网络不稳定或内网环境导致 `JSZip` 打包库加载失败，程序会自动降级为“逐一排队下载”模式，拒绝报错罢工。
- **🏷️ 文件指纹校验**：自动计算并展示文件的原始 `SHA-256` 指纹以及加解密后的指纹，确保文件完整性，防篡改。
- **💪 密码强度检测**：实时检测并提示密码强度，引导使用更安全的密码组合。

## 📖 分步使用指南

本工具无需外部依赖，在本地进行运算，只需一个现代化浏览器即可完成所有操作。

### 🔒 场景一：如何批量加密文件

**第 1 步：设置加密密码**
在顶部的“加解密密码”输入框中，输入您想设置的密码。
> 💡 **提示**：下方会自动显示密码强度条，建议使用“大小写字母+数字+符号”的高强度组合。**请务必牢记此密码，丢失将无法恢复文件！**

**第 2 步：导入需要加密的文件**
您可以点击中间的虚线框选择文件，或者**直接将多个文件/文件夹内的文件拖拽到虚线框内**。
* 支持多次拖拽累加文件。
* 列表会实时显示文件的原始 SHA-256 指纹。

**第 3 步：一键批量加密**
点击蓝色的 **“批量加密”** 按钮。
* 工具会在本地运算，列表右侧会实时显示处理状态和“加密后指纹”。
* 处理完成后，浏览器会自动弹出一个名为 `Encrypted_Files.zip` 的压缩包下载提示（如果文件较少或处于断网降级模式，则会逐个下载以 `.enc` 结尾的加密文件）。

---

### 🔓 场景二：如何批量解密文件

**第 1 步：输入原本的密码**
在“加解密密码”框中，准确输入您当时加密这些文件时使用的密码。

**第 2 步：导入加密文件 (.enc)**
将之前加密生成的 `.enc` 文件（需要先从 ZIP 压缩包中解压出来）拖拽到网页的虚线框中。

**第 3 步：一键批量解密**
点击绿色的 **“批量解密”** 按钮。
* 工具会自动验证密码并解密文件。
* 成功后，浏览器会自动将恢复成原格式的文件下载到您的电脑中。
* 如果密码错误或文件被篡改，列表状态会标红提示“失败”。

## 🛠️ 技术栈与原理

- **界面与交互**：Vanilla HTML5 / CSS3 / ES6 JavaScript
- **核心加密逻辑**：[Web Crypto API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Crypto_API)
  - **Key Derivation**: `PBKDF2` (100,000次迭代, SHA-256)
  - **Encryption**: `AES-GCM` (256-bit, 随机 16-byte Salt, 随机 12-byte IV)
- **文件打包**：[JSZip](https://stuk.github.io/jszip/) (通过 CDN 引入，带有断网降级机制)

## ⚠️ 安全与免责声明

- **密码丢失无法找回**：由于本工具是完全纯前端且无数据库的，**一旦您遗忘密码，您的文件将面临永久无法解密的风险**，请务必妥善保管您的密码！
- 文件体积受限于浏览器内存（RAM）。对于 GB 级别的超大文件，可能会导致浏览器内存溢出（OOM），建议用于处理日常文档、图片及中小型文件。

## 💡 关于 "Vibe-Coding" 

本项目的诞生经历了多轮灵感碰撞与迭代（Vibe-Coding）。从最基础的单文件加解密，到加入拖拽与批量处理，再到引入哈希指纹校验，最后加入了对弱网环境极度友好的“优雅降级”设计。代码本身不仅追求功能实现，更追求极致的用户体验与鲁棒性。

## 📄 开源协议 (License)

本项目基于 [MIT License](LICENSE) 开源。

Copyright (c) 2026 

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.