# <a name="editor-lite"></a>Spck Editor Lite

## <a name="overview"></a>概述

Spck Editor Lite 是 Spck Editor 的一次性购买版本，无需订阅即可解锁高级编辑功能。它在 Android 和 iOS 上作为独立应用提供。

Lite 包含免费版的所有功能，另外还有：

- **Predictive Keyboard** -- 附加键盘上的上下文感知符号建议
- **自定义代码片段** -- 用户定义的带有制表位占位符的代码模板
- **Neon 主题** -- 独家编辑器主题

这些功能也可在 Spck Editor 完整版中通过激活 Gold 或 Supporter 订阅来使用。Lite 应用以一次性购买的方式提供相同的功能。

## <a name="predictive-keyboard"></a>Predictive Keyboard

Predictive Keyboard 将标准附加键盘替换为一行上下文感知的符号键。无需长按按键从菜单中选择，最可能的符号会根据光标在文件中的位置直接显示。

### 工作原理

预测通过按语言构建的统计频率表生成。当光标移动时，键盘会根据每个符号在实际代码中该类型位置出现的频率重新排列符号。支持的语言包括 JavaScript、TypeScript、Python、HTML、CSS、JSON、Java、C++、Go、Markdown 和纯文本。

### 启用或禁用

前往 `Settings > Touch > Predictive Keyboard` 切换该功能。在 Lite 中，Predictive Keyboard 默认启用。关闭后将恢复标准附加键盘。

> Predictive Keyboard 仅在触摸设备上可用。使用物理键盘或在连接外部键盘的平板模式下不会显示。

## <a name="custom-snippets"></a>自定义代码片段

自定义代码片段允许您创建可重复使用的代码模板，在输入时显示在自动补全列表中。每个代码片段与特定语言关联，因此您的 JavaScript 代码片段不会出现在 Python 文件中。

### 创建代码片段

1. 打开 `Settings > Editor > Custom Snippets`
2. 选择语言（例如 JavaScript、Python、HTML）
3. 点击**添加代码片段**
4. 输入**触发器** -- 您键入以调用代码片段的缩写
5. 输入**内容** -- 将要插入的代码

### 制表位和占位符

代码片段支持制表位，以便在插入后光标在可编辑位置之间跳转：

- `$1`、`$2`、`$3` -- 按遍历顺序编号的制表位
- `$0` -- 所有制表位之后的最终光标位置
- `${1:defaultText}` -- 带有预选占位符文本的制表位，便于替换

示例 -- JavaScript `for` 循环代码片段：

**触发器：** `forloop`

**内容：**
```
for (let ${1:i} = 0; ${1:i} < ${2:array}.length; ${1:i}++) {
  $0
}
```

输入 `forloop` 并从自动补全中选择后，将插入完整的循环。按 Tab 键在 `i`、`array` 和循环体之间跳转。

### 导入和导出

您可以将所有代码片段导出到文件，并在另一台设备上导入。这对于在手机之间共享代码片段集合或备份配置非常有用。

## <a name="neon-theme"></a>Neon 主题

Lite 包含 **Neon** 编辑器主题，这是一款具有鲜艳强调色的深色主题。它在 Lite 中被设为默认主题，可随时在 `Settings > Appearance > Theme` 中更改。

## <a name="comparison"></a>功能对比

| 功能 | 免费 | Lite（一次性购买） | 完整版（订阅） |
| --- | :---: | :---: | :---: |
| 代码编辑和语法高亮 | 是 | 是 | 是 |
| Git 集成 | 是 | 是 | 是 |
| 附加键盘 | 是 | 是 | 是 |
| 触摸键盘和光标 | 是 | 是 | 是 |
| 项目预览 | 是 | 是 | 是 |
| Predictive Keyboard | -- | 是 | Gold / Supporter |
| 自定义代码片段 | -- | 是 | Gold / Supporter |
| Neon 主题 | -- | 是 | -- |
| AI 助手 | -- | -- | 是 |
| 用户账户和云同步 | -- | -- | 是 |
| Labs / 社区项目 | -- | -- | 是 |
