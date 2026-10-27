# <a name="git-support"></a>Git 支援

Spck 支援在 Android 與 iOS 本機專案、瀏覽器專案，以及透過 Spck CLI 連線的遠端專案中使用 Git。本指南說明服務供應商憑證、提取要求、提交檢視、衝突解決及平台限制。

免費版提供基本 Git 整合、提交歷史紀錄與合併衝突解決。[增強 Git 整合](#enhanced-git-integration)另提供提取要求管理及提交檔案差異檢視。

## <a name="git-credentials"></a>Git 憑證與提取要求

開啟 **Git menu → Git Credentials**，選擇供應商並儲存存取權杖。下方權杖設定與說明連結會在新分頁開啟，方便返回 Spck 貼上權杖。

| 供應商 | 權杖設定 | Git 與提取要求權限 |
| --- | --- | --- |
| GitHub | <a href="https://github.com/settings/personal-access-tokens/new?contents=write&amp;pull_requests=write&amp;metadata=read&amp;name=Spck-Editor&amp;expires_in=90" target="_blank" rel="noopener noreferrer">建立 GitHub 權杖</a> · <a href="https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens" target="_blank" rel="noopener noreferrer">設定指南</a> | 選擇儲存庫。建立連結會預選 **Contents: Read and write**、**Pull requests: Read and write** 與 **Metadata: Read**。 |
| GitLab | <a href="https://gitlab.com/-/user_settings/personal_access_tokens?name=Spck-Editor&amp;scopes=api" target="_blank" rel="noopener noreferrer">建立 GitLab 權杖</a> · <a href="https://docs.gitlab.com/user/profile/personal_access_tokens/#prefill-personal-access-token-details" target="_blank" rel="noopener noreferrer">設定指南</a> | 建立連結會預選合併要求所需的 `api` 範圍。 |
| Bitbucket Cloud | <a href="https://id.atlassian.com/manage-profile/security/api-tokens" target="_blank" rel="noopener noreferrer">建立 API 權杖</a> · <a href="https://support.atlassian.com/bitbucket-cloud/docs/create-an-api-token/" target="_blank" rel="noopener noreferrer">設定指南</a> | 選擇 **Create API token with scopes**、**Bitbucket**，再手動選取 `read:repository:bitbucket`、`write:repository:bitbucket`、`read:pullrequest:bitbucket`、`write:pullrequest:bitbucket`。API 驗證使用 Atlassian 帳號的電子郵件地址。 |
| Azure DevOps | <a href="https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate" target="_blank" rel="noopener noreferrer">PAT 建立指南</a> | 開啟組織中的 **User settings → Personal access tokens → New Token**，選擇組織，並手動選取 **Code (Read & write)**。 |

建立提取要求前，請先提交並推送來源分支，再開啟 **Git menu → Create PR**。選擇遠端儲存庫與憑證，指定不同的目標分支，並輸入標題及描述。**Generate with AI** 可根據兩分支共同祖先之後已提交的變更撰寫草稿；請先擷取目標分支。檢查草稿後再選擇 **Create PR**。GitLab 建立的是合併要求。

建立與管理提取要求是[增強 Git 整合](#enhanced-git-integration)中的 **Premium 功能**。Lite 的一次性購買已包含此功能。完整版請使用具有有效 Supporter、Gold 或 Node 訂閱的帳號，或擁有 Spck for NodeJS 終端機終身解鎖的帳號登入。

## <a name="pull-request-management"></a>提取要求管理（Premium）

無須離開編輯器即可管理提取要求。支援的遠端服務包括 **GitHub.com、GitLab.com、Bitbucket Cloud 與 Azure DevOps**；GitLab 稱為合併要求。

1. 開啟 Git 專案，在 **Git menu → Git Credentials** 加入具有上述權限的供應商權杖。
2. 開啟 **Git menu → Pull Requests**，選擇遠端儲存庫及憑證，列出尚未關閉的要求。
3. 選擇要求，查看標題、描述、作者、來源與目標分支及狀態。
4. 選擇變更檔案，在合併前檢查唯讀差異。
5. 用 **Merge** 合併符合條件的要求，或用 **Close** 不經合併直接關閉。必要的審查、檢查、權杖權限與分支規則仍適用；草稿及有衝突的要求無法在此對話方塊合併。

供應商上的內容變動後，使用 **Refresh** 重新載入清單。要求詳情也提供前往供應商的連結，以進行審查、檢查及其他操作。

新建要求請依上述步驟使用 **Git menu → Create PR**。若來源分支尚需推送，對話方塊會在建立前提供 **Push**。選用的 AI 草稿使用已設定的 AI 服務及其用量限制，與 Lite 內含的提取要求使用權限分開。

若因權杖權限而建立失敗，請透過供應商連結建立或更新權杖，儲存至 **Git Credentials** 後重試。PR 草稿會保留。

## <a name="enhanced-git-integration"></a>增強 Git 整合

增強 Git 整合增加兩項檢閱與分享變更的工具：

- **提取要求管理：** 建立要求、瀏覽尚未關閉的要求、檢查變更檔案與差異，以及合併或關閉要求。設定與步驟請參閱[提取要求管理](#pull-request-management)。
- **提交檢視：** 無須變更工作檔案，即可瀏覽提交中的變更檔案與差異。

開啟 Git 面板的 **History** 分頁，選擇提交以查看新增、修改與刪除的檔案。選擇檔案會開啟相對於提交第一個父提交的唯讀差異。首次提交與空樹比較。檢視器使用已提交的版本，因此未提交的編輯不影響差異。二進位檔案無法顯示為文字差異。

也可以長按歷史紀錄項目，或按滑鼠右鍵，再選擇 **View Commit**。

增強 Git 整合包含於：

- **Spck Editor Lite：** 一次性購買後永久解鎖，無須登入。
- **Spck for NodeJS 終端機終身購買：** 為購買所屬帳號永久解鎖，須登入。
- **Supporter、Gold 或 Node 訂閱：** 訂閱有效期間解鎖，須登入。

基本 Git 整合與提交歷史紀錄瀏覽仍可在免費版使用。方案詳情請參閱[價格](https://spck.io/pricing)。

## <a name="merge-conflict-resolution"></a>解決合併衝突

差異檢視器也可用來解決工作檔案中的衝突。這屬於基本 Git 整合，無須 Premium。

1. 從 Git 變更清單開啟有衝突的檔案。
2. 為每個衝突選擇 **Accept Current**、**Accept Incoming** 或 **Accept Both**。也可編輯檔案，手動組合變更。
3. 檢查結果。移除全部衝突標記後，在差異檢視器選擇 **Resolve**，將已解決檔案加入暫存區。
4. 解決其餘檔案後提交合併。

在觸控裝置上，長按檔案或 Git 項目可開啟快顯功能表。Git 狀態字母補充檔名顏色，方便識別變更。

## <a name="git-limitations"></a>Git 限制

### <a name="git-limitations-overview"></a>概覽

Git 的實作取決於專案儲存位置和使用的 Spck 版本：

| 環境 | Git 實作 | 主要限制 |
| --- | --- | --- |
| Android 與 iOS 應用程式，包括 Lite 和 Spck for NodeJS | 本機專案使用原生編譯的 **libgit2** | 專案必須位於裝置儲存空間；仍受裝置資源及檔案系統限制。 |
| 瀏覽器與嵌入式編輯器 | 以 JavaScript 執行的 [isomorphic-git](https://isomorphic-git.org/) | 受瀏覽器記憶體、儲存空間及網路限制。 |
| 透過 Spck CLI 使用的遠端專案 | 主機的 **Git 執行檔** | 使用主機資源、檔案系統、憑證及已安裝的 Git。 |

目前行動版本使用原生 Git，而非載入瀏覽器 Git 引擎。若本機操作顯示 **Native Git requires a device folder**，請將專案移至裝置儲存空間。僅存於編輯器瀏覽器資料庫的專案無法使用行動原生 Git 用戶端。

提取要求管理使用 **Git Credentials** 中儲存的權杖直接呼叫供應商 API。不使用瀏覽器登入 Cookie，也不快取 API 回應，因此重新整理可取得最新要求狀態與分支資訊。權杖權限請參閱 [Git 憑證與提取要求](#git-credentials)，支援的服務及操作請參閱[提取要求管理](#pull-request-management)。

### <a name="git-limitations-memory"></a>記憶體限制

- Android 與 iOS 原生 Git 在 JavaScript Git 引擎之外執行儲存庫操作。瀏覽器引擎的記憶體限制不是行動 Git 的固定上限。
- 原生 Git 仍需要可用記憶體與磁碟空間。大型儲存庫或 pack 檔案可能超過裝置資源，造成操作失敗或應用程式被系統終止。
- 瀏覽器 Git 仍受 JavaScript 記憶體與瀏覽器儲存額度限制。處理大型 pack 檔案可能需要大量記憶體，造成複製或擷取失敗。

> 💡 **提示：** 對於大型儲存庫，盡可能使用淺層複製，或考慮只處理儲存庫中較小的部分。

### <a name="git-limitations-symlinks"></a>符號連結相容性

- 瀏覽器儲存空間與編輯器的裝置檔案系統層，對含有符號連結的儲存庫使用**模擬符號連結**。
- 行動 Git 改用 libgit2 不會移除檔案系統限制，也不保證支援作業系統的真實符號連結。
- 需要真實連結並在執行時解析目標的建置工具、套件管理員或指令碼，使用模擬連結時可能有不同表現。
- 若專案需要真實符號連結，請在檔案系統與權限皆支援的主機上使用遠端專案。

### <a name="git-limitations-cli"></a>使用 CLI 作為替代方案

對於大型儲存庫，或需要主機檔案系統與 Git 工具的工作，請使用**透過 Spck CLI 連線的遠端專案**。您在 Spck 編輯時，Git 操作由**主機的 Git 執行檔**執行：

- 儲存庫操作使用主機記憶體與磁碟，而非行動裝置或瀏覽器資源。
- 符號連結遵循主機作業系統的檔案系統支援狀況及權限。
- 編輯器 Git 控制項未提供的指令，請使用主機 Git 工具執行。

主機連線步驟請參閱 [Spck CLI 入門](./cli-start)。遠端專案需要 Spck 帳號，並受方案存取限制；Lite 訂閱需求請參閱[遠端專案](./editor-lite#remote-projects)。複製到裝置儲存空間仍使用行動應用程式的原生 Git 用戶端。

## <a name="git-related-guides"></a>相關指南

- [螢幕閱讀器支援（實驗性）](./screen-reader-support)：無障礙導覽、原始碼管理控制項及意見回饋。
- [Spck Editor Lite](./editor-lite#enhanced-git-integration)：一次性購買內含的 Git 工具。
- [Spck CLI 入門](./cli-start)：連線遠端專案以使用主機 Git 工具。
