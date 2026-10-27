# <a name="getting-started"></a>入門

## <a name="getting-started-overview"></a>概覽

Spck Editor 是一款行動程式碼編輯解決方案，具有為開發者設計的多種變體。

### 版本

#### Spck Editor (免費版)

- 基本的行動程式碼編輯功能
- Android 與 iOS 使用原生 Git；瀏覽器透過 isomorphic-git 整合 Git

#### Spck Editor Lite

**價格**：一次性付款
**功能**：

- 自訂程式碼片段
- 預測鍵盤
- 獨家霓虹主題
- 增強 Git 整合

#### Spck for NodeJS

**平台**：Android 獨家
**主要功能**：支援 NodeJS 的整合終端機

增強 Git 整合包含於有效的 Node 訂閱中，也可透過終端機終身購買永久解鎖。這兩種方式均需要登入。

#### 瀏覽器版本

- 可嵌入任何網站
- 輕量級程式碼編輯介面

[嵌入編輯器](./editor-embed)

### 主要特性

- 行動優先設計
- [Git 支援與限制](./git-support)
- 跨平台相容性
- [螢幕閱讀器支援（實驗性）](./screen-reader-support)

### <a name="git-credentials"></a>Git 憑證與提取要求

<a name="pull-request-management"></a>

請參閱 [Git 支援](./git-support)，了解[權杖設定](./git-support#git-credentials)、[提取要求管理](./git-support#pull-request-management)與[增強 Git 整合](./git-support#enhanced-git-integration)。

### 推薦使用情境

- 隨時隨地的程式碼編輯
- 快速專案修改
- 學習與原型設計

## <a name="getting-started-terminology"></a>術語

| 術語           | 描述                                                                                                       |
| -------------- | ---------------------------------------------------------------------------------------------------------- |
| 導航選單       | 指行動裝置側邊選單上的第一個標籤，此選單在瀏覽器版本或平板模式下不可用                                     |
| 檔案選單       | 指側邊選單或側邊欄上的 _File_ 標籤                                                                         |
| 擴充鍵盤       | 行動裝置上有一個帶有常用編碼符號的擴充鍵盤，可快速插入                                                     |
| 觸控鍵盤       | 通常指包含方向鍵、Tab 鍵等的一行按鍵                                                                       |
| 觸控操作列     | 這是在行動／觸控裝置上選擇文字時彈出在游標上方的浮動選單                                                   |
| 觸控游標       | 在行動／觸控裝置上選擇文字或游標處於活動狀態時出現在螢幕上的游標                                           |
| 平板模式       | 指可在較大觸控裝置（如平板）上啟用的設定                                                                   |
| ⌘ 鍵           | 觸控鍵盤上的此符號與 Windows 上的 Ctrl 鍵或 Mac 上的 Command 鍵相同                                        |
| ⌥ 鍵           | 觸控鍵盤上的此符號與 Windows 上的 Alt 鍵或 Mac 上的 Option 鍵相同                                          |

&nbsp;

&nbsp;

# <a name="screen-reader-support"></a>螢幕閱讀器支援（實驗性）

螢幕閱讀器支援屬於**實驗性**功能。[螢幕閱讀器指南](./screen-reader-support)說明啟用方式、文件編輯、鍵盤導覽、限制及[意見回饋](./screen-reader-support#screen-reader-feedback)。

&nbsp;

&nbsp;

# <a name="keyboard-shortcuts"></a>鍵盤快捷鍵

## <a name="keyboard-shortcuts-overview"></a>概覽

透過這些方便的鍵盤快捷鍵解鎖閃電般的效率！雖然不是完整目錄，但這些精華將大幅提升您的生產力，讓導航變得輕而易舉。

### 主要亮點

- **非詳盡列表**：精選最實用的快捷鍵
- **目的**：透過快速、直觀的命令提升您的工作流程
- **優勢**：節省時間，減少對滑鼠的依賴

> 💡 **專業提示**：記住這些快捷鍵，看著您的生產力飆升！🌟

您可以透過前往 `Settings > Editor > Keyboard Shortcuts` 查看完整的快捷鍵清單。

> 進階使用者也可以直接從擴充鍵盤存取鍵盤快捷鍵，或使用快捷鍵 `⌘ K`

> 透過啟用 `Settings > Touch > Show ⌘ Key` 和 `Settings > Touch > Show ⌥ Key` 啟用 Ctrl/Command 鍵（⌘）和 Alt/Options 鍵

鍵盤焦點、選單啟用與無障礙文件編輯請參閱[螢幕閱讀器支援（實驗性）](./screen-reader-support)。

## <a name="keyboard-shortcuts-editor"></a>編輯器

| 快捷鍵 | 操作                                |
| ------ | ----------------------------------- |
| ⌘ A    | 全選                                |
| ⌘ C    | 複製                                |
| ⌘ V    | 貼上                                |
| ⌘ X    | 剪下                                |
| ⌘ Z    | 還原                                |
| ⌘ ⇧ Z  | 重做                                |
| ⌘ D    | 複製行                              |
| ⌘ /    | 註解/取消註解行                     |
| ⌥ F    | 格式化程式碼                        |
| ⌘ F    | 尋找                                |
| ⌘ G    | 尋找下一個（適用於選取的文字）      |
| ⌘ ⇧ G  | 尋找上一個                          |
| ⌘ L    | 跳至行                              |

## <a name="keyboard-shortcuts-quick-actions"></a>快速操作

| 快捷鍵 | 操作                                |
| ------ | ----------------------------------- |
| ⌘ ⇧ C  | Git 提交                            |
| ⌘ O    | 開啟最近檔案                        |
| ⌘ ⇧ P  | 啟動專案預覽                        |
| ⌘ P    | 切換檔案預覽（SVG、Markdown）       |
| ⌘ K    | **Supporter+**：開啟快捷鍵          |

&nbsp;

&nbsp;

# <a name="touch-settings"></a>觸控設定

## <a name="touch-settings-extra"></a>擴充鍵盤

- 擴充鍵盤是為觸控裝置設計的符號鍵盤。
- 透過長按按鍵可以存取其他按鍵/符號，從而開啟選項選單。
- 您可以在 `Settings > Touch > Extra Keyboard` 選單中啟用或停用它。

> 💡 **專業提示**：請參閱 _**進階編輯**_ 了解與擴充鍵盤相容的環繞文字提示。

## <a name="touch-settings-touch"></a>觸控鍵盤

- 觸控鍵由一行按鍵組成，包括方向鍵、Command 鍵和其他常用按鍵。
- 此功能在觸控裝置上可用。
- 您可以在 `Settings > Touch > Touch Keyboard` 部分切換開啟或關閉。

> 💡 **專業提示**：您可以透過調整設定自訂此鍵盤上的個別按鍵。

## <a name="touch-settings-action-bar"></a>觸控操作列

- 選取文字時，會出現帶有複製、剪下和貼上選項的操作列。
- 此功能可以在 `Settings > Touch > Touch Action Bar` 中啟用或停用。

## <a name="touch-settings-cursors"></a>觸控游標

- 選取文字或游標處於活動狀態時出現的螢幕游標。
- 此功能可以在 `Settings > Touch > Touch Cursors` 中啟用或停用。

> 💡 **專業提示**：除非您將滑鼠/指標裝置與行動裝置配對，否則不建議停用此功能。停用觸控游標可以改善編輯時的螢幕能見度，並在使用外部指標裝置時改善編輯體驗。

## <a name="touch-settings-predictive"></a>預測鍵

- 預測鍵是一個進階功能，取代了標準的擴充鍵盤。
- 提供單次觸碰的符號輸入，而不必在一般擴充鍵盤中長按並選擇
- 按鍵按檔案中特定位置出現符號的統計頻率排序。
- 可以在 `Settings > Touch > Predictive Keyboard` 中開啟或關閉。

> 💡 **專業提示**：預測鍵取代了一般擴充鍵盤，某些使用者可能更喜歡一般鍵盤。預測鍵是編輯器 **Lite** 版本中的預設選項，可以將其關閉以恢復一般擴充鍵盤。

&nbsp;

&nbsp;

# <a name="file-navigation"></a>檔案導航

## <a name="file-navigation-overview"></a>概覽

- 在檔案之間導航有多種方法
- 您可以使用側邊選單中的檔案瀏覽檔案
- 您可以使用麵包屑從當前檔案目錄開始瀏覽檔案
- 您可以開啟最近檔案 `Ctrl-O` 來快速搜尋檔案
- 您可以使用檔案側邊選單中的「Locate」圖示快速定位當前檔案
- 原始碼控制和搜尋側邊選單也提供了在檔案之間導航的獨特方式

## <a name="file-navigation-tabs"></a>檔案標籤管理

### 標籤行為

- 檔案最初開啟時會自動取消固定
- 進行編輯時標籤會被固定

### 標籤排序選項

檔案可以按以下方式排序：

- 字母順序
- 檔案副檔名
- 檔案路徑

### 替代導航管道

- **原始碼控制選單**：透過版本控制上下文導航檔案
- **搜尋選單**：根據搜尋條件尋找和存取檔案

> 💡 **專業提示**：可以在 `Settings > Appearance > Show File Tabs` 中關閉檔案標籤檢視。請參閱 _禪模式_ 了解如何在較小裝置上最大化螢幕空間。

&nbsp;

&nbsp;

# <a name="advanced-editing"></a>進階編輯

## 高效使用預測鍵盤

### 基本選取

- 雙擊以選取單字或文字區塊

### 環繞文字

使用括號或引號對快速環繞選定的文字：

- 圓括號：`( )`
- 方括號：`[ ]`
- 大括號：`{ }`
- 單引號：`' '`
- 雙引號：`" "`

### 導航與編輯

#### 文字搜尋

- `⌘ G`：尋找下一個實例
- `⌘ ⇧ G`：尋找上一個實例

#### 縮排

- 選取文字區塊
- 按 Tab 縮排

&nbsp;

## <a name="multiple-cursors"></a>多游標

### 快速設定

- 使用 Alt/Option 鍵啟用多游標！✨
- 導航到 `Settings > Touch > Show ⌥ Key` 來啟動

### 使用方法

1. 選取 ⌥ 和 ⌘ 鍵
2. 點擊以將游標放置在您想要的確切位置
3. 輕鬆同時編輯多行！💻

> 💡 **專業提示**：多游標編輯 = 閃電般快速的程式碼轉換！⚡️
> 也可以使用命令面板命令 `Add Cursor Above` 和 `Add Cursor Below` 新增多游標，這將在當前游標位置的正上方或正下方新增一個游標。

&nbsp;

&nbsp;

# <a name="enhanced-git-integration"></a>Git 支援

供應商憑證、提取要求管理、提交檢視和增強 Git 整合使用條件請參閱 [Git 指南](./git-support)。

<a name="merge-conflict-resolution"></a>

基本 Git 包含透過差異檢視器的 **Accept Current**、**Accept Incoming**、**Accept Both** 及 **Resolve** 進行的[衝突解決](./git-support#merge-conflict-resolution)。

## <a name="git-limitations"></a>Git 限制

<a name="git-limitations-overview"></a>
<a name="git-limitations-memory"></a>
<a name="git-limitations-symlinks"></a>
<a name="git-limitations-cli"></a>

Android 與 iOS 本機專案使用原生 libgit2，瀏覽器使用 isomorphic-git，遠端專案使用主機 Git 執行檔。儲存需求、記憶體、符號連結及遠端替代方案請參閱 [Git 限制](./git-support#git-limitations)。

&nbsp;

&nbsp;

# <a name="zen-mode"></a>🌟 禪模式

## 概覽

禪模式是一種令人愉悅的、最大化空間的編輯器配置，旨在改變您在緊湊顯示螢幕上的編碼體驗。

禪模式包括：

- 在設定中關閉 `Show Line Numbers`
- 關閉 `Show File Tab`
- 關閉 `Touch Action Bar`

### 主要功能

#### 🧘‍♀️ 最大化螢幕空間

- **告別行號！**
  - 釋放寶貴的水平空間
  - 防止文字感覺擁擠
  - 擁抱簡潔、極簡的外觀

#### 🎨 精簡介面

- **操作列最小化**
  - 告別雜亂的工具列
  - 利用替代輸入方式：
    - 擴充鍵盤的貼上/剪下按鈕
    - 鍵盤快捷鍵（`Ctrl-C/Ctrl-V`）

#### 📂 簡化導航

- **消除檔案標籤**
  - `Ctrl-O` 成為您的新導航好夥伴
  - 更清潔的工作區
  - 更快的上下文切換

> 💡 **專業提示**：並非每個人的編碼風格都相同！我們建議嘗試禪模式，看看它是否與您的工作流程產生共鳴。您完美的編碼環境只需幾個切換即可達成！🌈✨
