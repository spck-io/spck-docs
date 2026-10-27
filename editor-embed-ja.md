# エディターの埋め込み

Spck Editor を iframe に埋め込むと、編集可能なサンプル、チュートリアル、コード用ツールを作成できます。`SpckEditor` ラッパーは `postMessage` と `MessageChannel` で iframe と通信します。

## <a name="screen-reader-support"></a>スクリーンリーダー対応（試験的）

アクセシビリティ機能と現在の制限は[スクリーンリーダー対応（試験的）](./screen-reader-support#screen-reader-limitations)をご覧ください。埋め込みエディターではモバイルのスクリーンリーダー編集モードは自動的に有効になりません。

設定、プロジェクトとファイル、エディター設定、イベント、トラブルシューティングは[完全な API リファレンス（英語）](/en/editor-embed)をご覧ください。ソースコードと TypeScript 宣言は [spckio/spck-embed](https://github.com/spckio/spck-embed) にあります。
