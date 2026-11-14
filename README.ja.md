# @tanuden/biome-config

[English](https://github.com/tanuden/biome-config/blob/main/README.md) | **日本語**

TanudenのTypeScriptプロジェクト向けBiomeリンタープリセットです。

## プロファイル

| プロファイル | 継承元   | 用途                                                       |
| ------------ | -------- | ---------------------------------------------------------- |
| `base`       | なし     | 最も厳格な共通規約。すべてのプロジェクトの基盤             |
| `node`       | `base`   | Nodeサービス。`.js`インポート拡張子（NodeNext）を追加      |
| `lib`        | `base`   | ライブラリ。`.js`インポート拡張子（NodeNext）を追加       |
| `react`      | `base`   | Reactレンダラー。reactドメイン、kebab + PascalCase命名     |
| `electron`   | `node`   | Electronアプリ。メインプロセスでの `process.env` を許可   |

## スタイル規約

### フォーマッター

| 設定                     | 値             |
| ------------------------ | -------------- |
| インデント               | 2スペース      |
| 行の最大幅               | 100            |
| 改行コード               | LF             |
| セミコロン               | 常に           |
| クォート（JSとJSX）      | ダブルクォート |
| プロパティ名のクォート   | 必要な場合のみ |
| 末尾のカンマ（JS）       | すべて         |
| 末尾のカンマ（JSON）     | なし           |
| アロー関数の丸括弧       | 常に           |
| ブラケット内のスペース   | オン           |
| ブラケットを同一行に配置 | オフ           |
| CSSのクォート            | ダブルクォート |

### リンター

`base` はBiomeの `recommended` プリセットに以下を重ねます:

| ルール                      | レベル | 備考                                          |
| --------------------------- | ------ | --------------------------------------------- |
| `useImportType`             | error  |                                               |
| `useExportType`             | error  |                                               |
| `useFilenamingConvention`   | error  | `base`はkebab-case、`react`はPascalCaseも許可 |
| `noProcessEnv`              | error  | `electron`ではオフ                            |
| `noNonNullAssertion`        | error  |                                               |
| `useShorthandFunctionType`  | error  |                                               |
| `noShadow`                  | error  |                                               |
| `noArrayIndexKey`           | error  |                                               |
| `noFloatingPromises`        | error  | nursery                                       |
| `noMisusedPromises`         | error  | nursery                                       |
| `useAwaitThenable`          | error  | nursery                                       |
| `noPromiseExecutorReturn`   | error  | nursery                                       |
| `usePromiseRejectErrors`    | error  | nursery                                       |
| `noReturnInFinally`         | error  | nursery                                       |
| `useExplicitReturnType`     | error  | nursery、自動修正なし                         |
| `useExplicitType`           | error  | nursery、自動修正なし                         |
| `useExhaustiveDependencies` | warn   |                                               |
| `noBarrelFile`              | warn   |                                               |
| `noConsole`                 | warn   | 警告で `biome check` が失敗することはない     |
| `useImportExtensions`       | error  | `node`と`lib`のみ（`.js`拡張子）              |

`react` はさらにreactルールドメイン（`recommended`）に加え、`noLeakedRender`、`noNestedComponentDefinitions`、`useReactNamingConvention`、`noReactObjectTypeAsDefaultProp`、`useSelfClosingElements`、`useUniqueElementIds` をerrorで、`noReactForwardRef`、`useComponentExportOnlyModules`、`useImageSize`、`useControlLabel` をwarnで有効化し、`noImgElement`、`noJsxLiterals`、`noInlineStyles`、`useReactFunctionComponentDefinition` を明示的にオフにします。

一部のルールはnurseryルールです。`@biomejs/biome` は正確にピン留めしてください（2.6.3で検証済み）。Biomeのアップグレードは意図的なレビュー済みの変更であって、日常のメンテナンスではありません。`--error-on-warnings` を渡さないでください。`noConsole` は意図的にwarnです。

## 使用方法

### インストール

```bash
npm install --save-dev @tanuden/biome-config @biomejs/biome@2.6.3
```

### ルートの `biome.json`

プロジェクトの種類に合わせたプロファイルを継承してください:

```json
{
  "$schema": "https://biomejs.dev/schemas/2.6.3/schema.json",
  "extends": ["@tanuden/biome-config/electron"]
}
```

### サブツリー用のネスト設定（モノレポ）

`"root": false` を持つネストされた `biome.json` は、そのサブツリーにおいてルート設定を置き換えます（`"//"` を継承しない限り）。したがって、サブツリー固有の除外や緩和はネストされたファイルに記述します。ネストされた設定はルートからの実行（`biome check .`）で自動的に検出されます。

```json
{
  "$schema": "https://biomejs.dev/schemas/2.6.3/schema.json",
  "root": false,
  "extends": ["@tanuden/biome-config/react"],
  "files": {
    "includes": ["**", "!locales", "!src/assets"]
  },
  "linter": {
    "rules": {
      "security": {
        "noDangerouslySetInnerHtml": "off"
      }
    }
  }
}
```

## オープンソース @ タヌ電

@tanuden/biome-configはMITライセンスのオープンソースソフトウェア（OSS）です。ライセンスに従う限り、このリポジトリで提供されるコードを自由に配布・利用・改変できます。

ライセンスの全文はリポジトリのルート（[こちら](https://github.com/tanuden/biome-config/blob/main/LICENSE)）にあります。
