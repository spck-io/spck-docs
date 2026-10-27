# 嵌入编辑器

将 Spck Editor 嵌入 iframe，即可创建可编辑示例、教程或代码工具。`SpckEditor` 包装器通过 `postMessage` 和 `MessageChannel` 与 iframe 通信。

## <a name="screen-reader-support"></a>屏幕阅读器支持（实验性）

无障碍功能和当前限制请参阅[屏幕阅读器支持（实验性）](./screen-reader-support#screen-reader-limitations)。嵌入式编辑器不会自动启用移动版屏幕阅读器编辑模式。

配置、项目与文件、编辑器设置、事件和故障排查请参阅[完整英文 API 参考](/en/editor-embed)。源代码与 TypeScript 声明位于 [spckio/spck-embed](https://github.com/spckio/spck-embed)。
