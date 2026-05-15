# <a name="cli-reference"></a>CLI 参考

## <a name="key-features"></a>核心功能

- **远程文件系统**：通过 Spck Editor 移动应用访问和编辑本地文件
- **Git 集成**：完整的 Git 操作支持（提交、推送、拉取、分支管理）— 需要 Git 2.20.0 及以上版本
- **终端访问**：基于 xterm.js 的交互式终端会话
- **浏览器代理**：在 Spck Editor 内以全屏浏览器视图预览本地服务器
- **快速搜索**：自动检测 ripgrep 的优化文件搜索（安装后速度提升 100 倍）
- **安全可靠**：加密签名请求，支持可选的 Firebase 身份验证

## <a name="relay-server"></a>中继服务器

CLI 通过中继服务器与 Spck Editor 连接，该服务器负责在两者之间转发消息。首次运行时，CLI 会自动选择延迟最低的中继服务器，并将偏好保存到 `~/.spck-editor/.credentials.json`。

**重要提示**：CLI 和 Spck Editor 客户端必须使用同一个中继服务器才能连接。如果客户端无法找到 CLI，请确认两端选择了相同的中继服务器。

### 可用中继服务器

| 地区        | URL                 |
| ------------- | ------------------- |
| 欧洲        | `cli-eu-1.spck.io`  |
| 北美 | `cli-na-1.spck.io`  |
| 南亚    | `cli-sas-1.spck.io` |
| 东亚     | `cli-ea-1.spck.io`  |

### 覆盖中继服务器

```bash
# 使用指定的中继服务器
spck --server cli-eu-1.spck.io

# 简写形式
spck -s cli-na-1.spck.io
```

覆盖设置将被保存并在后续运行中复用。如需重新自动选择，请清除凭证后重启：

```bash
spck --logout
spck
```

### 在 Spck Editor 中选择中继服务器

通过移动应用的 **Link Remote Server** 功能连接时，请在 **Relay Server** 下拉菜单中选择与 CLI 相同的中继服务器。CLI 连接后，输出中会显示中继服务器名称。

## <a name="daily-workflow"></a>日常工作流程

### 开始会话

```bash
cd /path/to/project
spck
# 从移动应用连接（自动连接到已保存的服务器）
# 开始编写代码
```

### 编辑文件

1. 在移动应用中浏览文件
2. 点击打开并编辑
3. 文件自动保存到您的计算机

### 运行 Git 命令

**方式一 - 移动应用图形界面：**

- 打开 Git 面板
- 查看变更，暂存文件
- 提交并推送

**方式二 - 终端：**

```bash
git status
git add .
git commit -m "Update feature"
git push
```

### 终端会话

在移动应用中点击终端图标，即可获得具有用户权限的完整 Shell 访问。

### 结束会话

```bash
# 保持 CLI 运行以便快速重连（推荐）
# 或按 Ctrl+C 停止
```

## <a name="troubleshooting"></a>故障排除

### 根目录未找到

```bash
# 使用正确路径重新配置
spck --setup

# 或直接指定
spck --root /correct/path/to/project
```

### 配置已损坏

```bash
# 清除设置并重新开始
spck --logout
spck --setup
```

### 连接问题

1. 检查网络连接
2. 确认 CLI 和 Spck Editor 使用的是**相同的中继服务器**（CLI 连接后输出中会显示）
3. 尝试退出后重新连接：
   ```bash
   spck --logout
   spck
   ```
4. 检查防火墙设置 — 确保允许 WebSocket 连接（端口 443）

### 二维码无法扫描

- 确认扫描前已安装 Spck Editor 应用
- 使用手动输入：Projects → New Project → Link Remote Server
- 使用设备原生相机应用，而非第三方扫描器

### Git 操作不可用

1. 确认已安装 Git：

   ```bash
   git --version  # 需要 2.20.0 及以上版本
   ```

2. 如需安装：

   ```bash
   # macOS
   brew install git

   # Ubuntu/Debian
   sudo apt-get install git

   # Windows：从 git-scm.com 下载
   ```

### 搜索性能慢

安装 ripgrep 可获得 100 倍速度提升：

```bash
# macOS
brew install ripgrep

# Ubuntu/Debian
sudo apt-get install ripgrep

# Windows (Chocolatey)
choco install ripgrep

# CLI 自动检测并使用 ripgrep
```

### 权限被拒绝

```bash
# 查看权限
ls -la /path/to/file

# 如需修复
chmod 644 /path/to/file

# 不要使用 sudo — CLI 应以文件所有者的身份运行
```

## <a name="connection-limits"></a>连接限制

同时 CLI 连接数上限及每日使用限制取决于您的账号类型：

| 套餐      | CLI 连接数 | 每日限制 |
| --------- | --------------- | ----------- |
| 免费版      | 1               | 30 分钟  |
| 支持者 | 2               | 无限制   |
| 黄金版      | 5               | 无限制   |

免费套餐用量每天在 UTC 时间 12:00 AM 重置。

达到连接数上限时：

```
⚠️  Maximum of X CLI connections reached.
Close other CLI instances and try again.
```

达到免费套餐每日限制时：

```
⚠️  Daily free tier limit of 30 minutes has been reached.
Upgrade to continue using CLI.
```

查看活跃连接：

```bash
spck --account
```

> 💡 **提示**：同一时间只能有一台移动设备连接到一个 CLI 实例。每个 CLI 实例占用一个连接名额。

## <a name="support"></a>支持

- **官网**：[https://spck.io](https://spck.io)
- **客服支持**：通过 Spck Editor 移动应用联系
