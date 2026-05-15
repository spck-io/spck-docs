# <a name="editor-lite"></a>Spck Editor Lite

## <a name="overview"></a>概覽

Spck Editor Lite 是 Spck Editor 的一次性購買版本，無需訂閱即可解鎖進階編輯功能。它在 Android 和 iOS 上以獨立應用程式的形式提供。

Lite 包含免費版的所有功能，另外還有：

- **Predictive Keyboard** -- 附加鍵盤上的情境感知符號建議
- **自訂程式碼片段** -- 使用者定義的含有定位點佔位符的程式碼範本
- **Neon 佈景主題** -- 專屬編輯器佈景主題

這些功能也可在 Spck Editor 完整版中透過啟用 Gold 或 Supporter 訂閱來使用。Lite 應用程式以一次性購買的方式提供相同的功能。

## <a name="predictive-keyboard"></a>Predictive Keyboard

Predictive Keyboard 將標準附加鍵盤替換為一列情境感知的符號鍵。無需長按按鍵從選單中選擇，最可能的符號會根據游標在檔案中的位置直接顯示。

### 運作方式

預測透過按語言建立的統計頻率表產生。當游標移動時，鍵盤會根據每個符號在實際程式碼中該類型位置出現的頻率重新排列符號。支援的語言包括 JavaScript、TypeScript、Python、HTML、CSS、JSON、Java、C++、Go、Markdown 和純文字。

### 啟用或停用

前往 `Settings > Touch > Predictive Keyboard` 切換該功能。在 Lite 中，Predictive Keyboard 預設為啟用。關閉後將恢復標準附加鍵盤。

> Predictive Keyboard 僅在觸控裝置上可用。使用實體鍵盤或在連接外部鍵盤的平板模式下不會顯示。

## <a name="custom-snippets"></a>自訂程式碼片段

自訂程式碼片段允許您建立可重複使用的程式碼範本，在輸入時顯示在自動完成清單中。每個程式碼片段與特定語言關聯，因此您的 JavaScript 程式碼片段不會出現在 Python 檔案中。

### 建立程式碼片段

1. 開啟 `Settings > Editor > Custom Snippets`
2. 選擇語言（例如 JavaScript、Python、HTML）
3. 點擊**新增程式碼片段**
4. 輸入**觸發器** -- 您鍵入以呼叫程式碼片段的縮寫
5. 輸入**內容** -- 將要插入的程式碼

### 定位點和佔位符

程式碼片段支援定位點，以便在插入後游標在可編輯位置之間跳轉：

- `$1`、`$2`、`$3` -- 按遍歷順序編號的定位點
- `$0` -- 所有定位點之後的最終游標位置
- `${1:defaultText}` -- 含有預先選取的佔位符文字的定位點，便於替換

範例 -- JavaScript `for` 迴圈程式碼片段：

**觸發器：** `forloop`

**內容：**
```
for (let ${1:i} = 0; ${1:i} < ${2:array}.length; ${1:i}++) {
  $0
}
```

輸入 `forloop` 並從自動完成中選取後，將插入完整的迴圈。按 Tab 鍵在 `i`、`array` 和迴圈主體之間跳轉。

### 匯入和匯出

您可以將所有程式碼片段匯出到檔案，並在另一台裝置上匯入。這對於在手機之間分享程式碼片段集合或備份設定非常實用。

## <a name="neon-theme"></a>Neon 佈景主題

Lite 包含 **Neon** 編輯器佈景主題，這是一款具有鮮豔強調色的深色佈景主題。它在 Lite 中被設為預設佈景主題，可隨時在 `Settings > Appearance > Theme` 中變更。

## <a name="comparison"></a>功能比較

| 功能 | 免費 | Lite（一次性購買） | 完整版（訂閱） |
| --- | :---: | :---: | :---: |
| 程式碼編輯和語法醒目提示 | 是 | 是 | 是 |
| Git 整合 | 是 | 是 | 是 |
| 附加鍵盤 | 是 | 是 | 是 |
| 觸控鍵盤和游標 | 是 | 是 | 是 |
| 專案預覽 | 是 | 是 | 是 |
| Predictive Keyboard | -- | 是 | Gold / Supporter |
| 自訂程式碼片段 | -- | 是 | Gold / Supporter |
| Neon 佈景主題 | -- | 是 | -- |
| AI 助理 | -- | -- | 是 |
| 使用者帳戶和雲端同步 | -- | -- | 是 |
| Labs / 社群專案 | -- | -- | 是 |
