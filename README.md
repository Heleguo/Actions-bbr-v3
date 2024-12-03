### 自动内核编译与BBR v3安装

嘿，朋友们！🌟  
作为一个热爱技术的我们，效率一定是第一追求。今天分享一个超有趣的 GitHub Actions 工作流，自动帮你编译最新稳定版 Linux 内核，并集成 Google 的 **BBR v3**。搞定网络性能和内核升级，一条龙服务，不用自己瞎折腾！ 🚀

---

### 📚 项目简介
#### 这套流程能干啥？
1. **定时检查** [Kernel.org](https://www.kernel.org) 上的最新内核稳定版本，保持与世界同步。
2. 自动下载源码，编译并生成适配的 `.deb` 包。
3. **支持 x86_64 和 arm64** 两种架构，还带交叉编译支持。
4. **自带 Google BBR v3**，升级你的网络体验，低延迟更顺滑！
5. 编译完成的内核包会自动发布到 **GitHub Releases**，直接下载使用。

---

### 🎯 如何使用？

#### 🛠 1. 准备工作
1. 确保你的 **GitHub 仓库** 已经配置：
   - 添加 Secrets：  
     - `GITHUB_TOKEN`：用来发布 Release。

2. 准备内核配置文件：
   - `x86-64.config`（64 位 x86 架构）
   - `arm64.config`（ARM 架构）  
   把这两个文件放在仓库的根目录，工作流会根据架构自动选择对应配置。

---

#### ⏱ 2. 定时运行
- **每日凌晨 0 点（UTC）**，会自动检查内核版本是否更新。
- 如果版本一致，就跳过编译；有新版本则直接开始工作！

**时间可以根据需要调整**，修改 `schedule` 部分的 `cron` 参数即可。

---

### 💻 核心流程一览

```yaml
on:
  push:
    branches: [main]
  workflow_dispatch:
  schedule:
    - cron: '0 0 * * *'  # 每天凌晨 0 点运行（UTC 时间）
```

核心编译命令：
- `make LOCALVERSION=-joeyblog-joeyblog.net bindeb-pkg -j$(nproc)`  
超快！还带个性化后缀，让生成的内核包独具一格。

---

### ✨ 功能亮点
1. **实时检测内核版本**  
   - 动态获取 [Kernel.org](https://www.kernel.org) 上的最新稳定版。
   - 自动比对版本，如果已存在对应 Release，直接跳过！

2. **完整的 BBR v3 集成**  
   - 自动拉取 Google BBR 的代码分支，生成优化内核。

3. **架构支持齐全**  
   - 适配 `x86_64` 和 `arm64` 两种架构，还支持交叉编译。

4. **结果直观可用**  
   - 自动生成 `.deb` 安装包。
   - 内核包打包为 `tar.gz`，方便分发和下载。

---



### 📜 附录
#### 📘 博客
更详细的技术分析和教程，欢迎访问我的博客：  
🌐 **[Joey's Blog](https://joeyblog.net)**  

#### 💬 Telegram 群组
技术交流、吐槽或者提建议，欢迎加入我们的小圈子！  
👉 [加入 Telegram 群聊](https://t.me/+ft-zI76oovgwNmRh)

---

让代码跑起来，享受自动化的乐趣！🛠  
如果觉得这个项目有帮助，记得点个 Star ⭐ 支持一下！  

Happy Coding！🎉
