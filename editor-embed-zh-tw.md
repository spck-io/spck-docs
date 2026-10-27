# 嵌入編輯器

將 Spck Editor 嵌入 iframe，即可建立可編輯範例、教學或程式碼工具。`SpckEditor` 包裝器透過 `postMessage` 和 `MessageChannel` 與 iframe 通訊。

## <a name="screen-reader-support"></a>螢幕閱讀器支援（實驗性）

無障礙功能與目前限制請參閱[螢幕閱讀器支援（實驗性）](./screen-reader-support#screen-reader-limitations)。嵌入式編輯器不會自動啟用行動版螢幕閱讀器編輯模式。

設定、專案與檔案、編輯器選項、事件及疑難排解請參閱[完整英文 API 參考](/en/editor-embed)。原始碼與 TypeScript 宣告位於 [spckio/spck-embed](https://github.com/spckio/spck-embed)。
