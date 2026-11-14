# @tanuden/biome-config

[English](./README.md) | **日本語**

TanudenのTypeScriptプロジェクト向けBiomeリンタープリセットです。

対象:

- Electronアプリ
- Nodeサービス
- ライブラリ

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
| 末尾のカンマ（JS、JSON） | なし           |
| アロー関数の丸括弧       | 常に           |
| ブラケット内のスペース   | オン           |
| ブラケットを同一行に配置 | オフ           |
| CSSのクォート            | ダブルクォート |

### リンター

| ルール                      | レベル | 備考                                    |
| --------------------------- | ------ | --------------------------------------- |
| `useImportType`             | error  |                                         |
| `useFilenamingConvention`   | error  | kebab-caseまたはPascalCaseのファイル名  |
| `useExhaustiveDependencies` | warn   |                                         |
| `noBarrelFile`              | warn   |                                         |
| `noFloatingPromises`        | warn   |                                         |
| `noArrayIndexKey`           | off    | `recommended`プリセットへの意図的な例外 |

## 使用方法

### インストール

```bash
npm install --save-dev @tanuden/biome-config @biomejs/biome@2.6.3
```

`@biomejs/biome` 2.6.xが必要です（2.6.3で検証済み）。

### `biome.json` への追加

biomeの `recommended` プリセットをベースとして使用してください。
Reactプロジェクトでは、必要に応じて `react` ドメインを使用してください。

```json
{
  "$schema": "https://biomejs.dev/schemas/2.6.3/schema.json",
  "extends": ["@tanuden/biome-config/biome"]
}
```

## オープンソース @ タヌ電

@tanuden/biome-configはMITライセンスのオープンソースソフトウェア（OSS）です。ライセンスに従う限り、このリポジトリで提供されるコードを自由に配布・利用・改変できます。

ライセンスの全文はリポジトリのルート（[こちら](https://github.com/tanuden/biome-config/blob/main/LICENSE)）にあります。
