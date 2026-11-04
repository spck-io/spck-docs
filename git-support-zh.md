# <a name="git-support"></a>Git 支持

Spck 支持 Android 和 iOS 本地项目、浏览器项目，以及通过 Spck CLI 连接的远程项目使用 Git。本指南介绍提供商凭据、拉取请求、提交检查、冲突解决和平台限制。

免费版提供基本 Git 集成、提交历史和合并冲突解决。[增强 Git 集成](#enhanced-git-integration)增加拉取请求管理和提交文件差异查看。

## <a name="git-credentials"></a>Git 凭据与拉取请求

打开 **Git menu → Git Credentials**，选择提供商并保存访问令牌。下方令牌设置和帮助链接会在新标签页打开，方便返回 Spck 粘贴令牌。

| 提供商 | 令牌设置 | Git 与拉取请求权限 |
| --- | --- | --- |
| GitHub | <a href="https://github.com/settings/personal-access-tokens/new?contents=write&amp;pull_requests=write&amp;metadata=read&amp;name=Spck-Editor&amp;expires_in=90" target="_blank" rel="noopener noreferrer">创建 GitHub 令牌</a> · <a href="https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens" target="_blank" rel="noopener noreferrer">设置指南</a> | 选择仓库。创建链接会预选 **Contents: Read and write**、**Pull requests: Read and write** 与 **Metadata: Read**。 |
| GitLab | <a href="https://gitlab.com/-/user_settings/personal_access_tokens?name=Spck-Editor&amp;scopes=api" target="_blank" rel="noopener noreferrer">创建 GitLab 令牌</a> · <a href="https://docs.gitlab.com/user/profile/personal_access_tokens/#prefill-personal-access-token-details" target="_blank" rel="noopener noreferrer">设置指南</a> | 创建链接会预选用于合并请求的 `api` 范围。 |
| Bitbucket Cloud | <a href="https://id.atlassian.com/manage-profile/security/api-tokens" target="_blank" rel="noopener noreferrer">创建 API 令牌</a> · <a href="https://support.atlassian.com/bitbucket-cloud/docs/create-an-api-token/" target="_blank" rel="noopener noreferrer">设置指南</a> | 选择 **Create API token with scopes**、**Bitbucket**，然后手动选择 `read:repository:bitbucket`、`write:repository:bitbucket`、`read:pullrequest:bitbucket`、`write:pullrequest:bitbucket`。API 身份验证使用 Atlassian 账户邮箱。 |
| Azure DevOps | <a href="https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate" target="_blank" rel="noopener noreferrer">PAT 创建指南</a> | 打开组织中的 **User settings → Personal access tokens → New Token**，选择组织，并手动选择 **Code (Read & write)**。 |

创建拉取请求前，请先提交并推送源分支，再打开 **Git menu → Create PR**。选择远程仓库和凭据，指定不同的目标分支，并输入标题和描述。**Generate with AI** 可以根据两分支共同祖先之后已提交的更改起草消息；请先获取目标分支。检查草稿后再选择 **Create PR**。GitLab 创建的是合并请求。

创建和管理拉取请求是[增强 Git 集成](#enhanced-git-integration)中的 **Premium 功能**。Lite 的一次性购买已包含此功能。完整版中，请使用具有有效 Supporter、Gold 或 Node 订阅的账户，或拥有 Spck for NodeJS 终端终身解锁的账户登录。

## <a name="pull-request-management"></a>拉取请求管理（Premium）

无需离开编辑器即可管理拉取请求。支持的远程服务包括 **GitHub.com、GitLab.com、Bitbucket Cloud 和 Azure DevOps**；GitLab 称为合并请求。

1. 打开 Git 项目，在 **Git menu → Git Credentials** 中添加具有上述权限的提供商令牌。
2. 打开 **Branches menu → Pull Requests**，选择远程仓库和凭据以列出未关闭的请求。
3. 选择请求，查看标题、描述、作者、源分支、目标分支和状态。
4. 选择已更改文件，在合并前检查只读差异。
5. 使用 **Merge** 合并符合条件的请求，或用 **Close** 不经合并直接关闭。必要审查、检查、令牌权限和分支规则仍适用；草稿和存在冲突的请求无法在此对话框合并。

提供商上的内容发生变化后，使用 **Refresh** 重新加载列表。请求详情也提供访问提供商的链接，以便进行审查、检查和其他操作。

新建请求请按上述步骤使用 **Git menu → Create PR**。如果源分支尚需推送，对话框会在创建前提供 **Push**。可选的 AI 起草使用已配置的 AI 服务及其用量限制，与 Lite 自带的拉取请求访问权限分开。

如果因令牌权限导致创建失败，请通过提供商链接创建或更新令牌，保存至 **Git Credentials**，然后重试。PR 草稿会保留。

## <a name="enhanced-git-integration"></a>增强 Git 集成

增强 Git 集成增加两项用于审阅和分享更改的工具：

- **拉取请求管理：** 创建请求、浏览未关闭请求、检查更改文件与差异，以及合并或关闭请求。设置和步骤请参阅[拉取请求管理](#pull-request-management)。
- **提交检查：** 无需修改工作文件即可浏览提交中的更改文件及其差异。

打开 Git 面板的 **History** 标签页，选择提交以查看新增、修改和删除的文件。选择文件可打开相对于提交第一个父提交的只读差异。首次提交与空树比较。查看器使用已提交的版本，因此未提交的编辑不会影响差异。二进制文件无法显示为文本差异。

也可长按历史记录条目，或用鼠标右键单击，然后选择 **View Commit**。

增强 Git 集成包含于：

- **Spck Editor Lite：** 一次性购买后永久解锁，无需登录。
- **Spck for NodeJS 终端终身购买：** 为购买所属账户永久解锁，需要登录。
- **Supporter、Gold 或 Node 订阅：** 订阅有效期间解锁，需要登录。

基本 Git 集成和提交历史浏览仍可在免费版使用。方案详情请参阅[价格](https://spck.io/pricing)。

## <a name="merge-conflict-resolution"></a>解决合并冲突

差异查看器也可用于解决工作文件中的冲突。这属于基本 Git 集成，无需 Premium。

1. 从 Git 更改列表打开存在冲突的文件。
2. 为每个冲突选择 **Accept Current**、**Accept Incoming** 或 **Accept Both**。也可编辑文件，手动组合更改。
3. 检查结果。移除全部冲突标记后，在差异查看器中选择 **Resolve**，将已解决文件加入暂存区。
4. 解决其余文件后提交合并。

在触控设备上，长按文件或 Git 条目可打开上下文菜单。Git 状态字母补充文件名颜色，便于识别更改。

## <a name="git-limitations"></a>Git 限制

### <a name="git-limitations-overview"></a>概述

Git 的实现取决于项目保存位置和使用的 Spck 版本：

| 环境 | Git 实现 | 主要约束 |
| --- | --- | --- |
| Android 和 iOS 应用，包括 Lite 与 Spck for NodeJS | 为本地项目使用原生编译的 **libgit2** | 项目必须位于设备存储中；仍受设备资源和文件系统限制。 |
| 浏览器与嵌入式编辑器 | 运行于 JavaScript 的 [isomorphic-git](https://isomorphic-git.org/) | 受浏览器内存、存储和网络限制。 |
| 通过 Spck CLI 使用的远程项目 | 主机的 **Git 二进制程序** | 使用主机资源、文件系统、凭据和已安装的 Git。 |

当前移动版本使用原生 Git，而非加载浏览器 Git 引擎。如果本地操作提示 **Native Git requires a device folder**，请将项目移至设备存储。仅保存在编辑器浏览器数据库中的项目无法使用移动原生 Git 客户端。

拉取请求管理使用 **Git Credentials** 中保存的令牌直接调用提供商 API。不使用浏览器登录 Cookie，也不缓存 API 响应，因此刷新可获取最新请求状态和分支信息。令牌权限请参阅 [Git 凭据与拉取请求](#git-credentials)，支持的服务和操作请参阅[拉取请求管理](#pull-request-management)。

### <a name="git-limitations-memory"></a>内存约束

- Android 和 iOS 原生 Git 在 JavaScript Git 引擎之外执行仓库操作。浏览器引擎的内存约束不是移动 Git 的固定上限。
- 原生 Git 仍需要可用内存和磁盘空间。大型仓库或 pack 文件可能超过设备资源，导致操作失败或应用被系统终止。
- 浏览器 Git 仍受 JavaScript 内存和浏览器存储预算限制。处理大型 pack 文件可能需要大量内存，导致克隆或获取失败。

> 💡 **提示：** 对于大型仓库，尽可能使用浅克隆，或考虑只处理仓库中较小的部分。

### <a name="git-limitations-symlinks"></a>符号链接兼容性

- 浏览器存储和编辑器的设备文件系统层对包含符号链接的仓库使用**模拟符号链接**。
- 移动 Git 改用 libgit2 不会移除文件系统限制，也不保证支持操作系统的真实符号链接。
- 需要真实符号链接并在运行时解析目标的构建工具、包管理器或脚本，使用模拟链接时可能有不同表现。
- 如果项目必须使用真实符号链接，请在文件系统和权限均支持的主机上使用远程项目。

### <a name="git-limitations-cli"></a>使用 CLI 作为替代方案

对于大型仓库，或需要主机文件系统和 Git 工具的工作，请使用**通过 Spck CLI 连接的远程项目**。您在 Spck 编辑时，Git 操作由**主机 Git 二进制程序**执行：

- 仓库操作使用主机内存和磁盘，而非移动设备或浏览器资源。
- 符号链接遵循主机操作系统的文件系统支持情况和权限。
- 编辑器 Git 控件未提供的命令，请使用主机 Git 工具执行。

主机连接步骤请参阅 [Spck CLI 入门](./cli-start)。远程项目需要 Spck 账户，并受方案访问限制；Lite 的订阅要求请参阅[远程项目](./editor-lite#remote-projects)。克隆到设备存储仍使用移动应用的原生 Git 客户端。

## <a name="git-related-guides"></a>相关指南

- [屏幕阅读器支持（实验性）](./screen-reader-support)：无障碍导航、源代码管理控件和反馈。
- [Spck Editor Lite](./editor-lite#enhanced-git-integration)：一次性购买包含的 Git 工具。
- [Spck CLI 入门](./cli-start)：连接远程项目以使用主机 Git 工具。
