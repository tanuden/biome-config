# @tanuden/biome-config

**English** | [日本語](https://github.com/tanuden/biome-config/blob/main/README.ja.md)

Biome linter preset for Tanuden typescript projects.

## Profiles

| Profile    | Extends | For                                                        |
| ---------- | ------- | ---------------------------------------------------------- |
| `base`     | —       | Tightest shared contract, embed in every project           |
| `node`     | `base`  | Node services; adds `.js` import extensions (NodeNext)     |
| `lib`      | `base`  | Libraries; adds `.js` import extensions (NodeNext)         |
| `react`    | `base`  | React renderers; react domain, kebab + PascalCase naming  |
| `electron` | `node`  | Electron apps; allows `process.env` in the main process    |

## Style contract

### Formatter

| Setting                 | Value     |
| ----------------------- | --------- |
| Indent                  | 2 spaces  |
| Line width              | 100       |
| Line endings            | LF        |
| Semicolons              | Always    |
| Quotes (JS and JSX)     | Double    |
| Quote properties        | As needed |
| Trailing commas (JS)    | All       |
| Trailing commas (JSON)  | None      |
| Arrow parentheses       | Always    |
| Bracket spacing         | On        |
| Bracket same line       | Off       |
| CSS quotes              | Double    |

### Linter

`base` layers these on top of the Biome `recommended` preset:

| Rule                       | Level | Notes                                          |
| -------------------------- | ----- | ---------------------------------------------- |
| `useImportType`            | error |                                                |
| `useExportType`            | error |                                                |
| `useFilenamingConvention`  | error | `base`: kebab-case; `react`: + PascalCase      |
| `noProcessEnv`             | error | off in `electron`                              |
| `noNonNullAssertion`       | error |                                                |
| `useShorthandFunctionType` | error |                                                |
| `noShadow`                 | error |                                                |
| `noArrayIndexKey`          | error |                                                |
| `noFloatingPromises`       | error | nursery                                        |
| `noMisusedPromises`        | error | nursery                                        |
| `useAwaitThenable`         | error | nursery                                        |
| `noPromiseExecutorReturn`  | error | nursery                                        |
| `usePromiseRejectErrors`   | error | nursery                                        |
| `noReturnInFinally`        | error | nursery                                        |
| `useExplicitReturnType`    | error | nursery, no auto-fix                           |
| `useExplicitType`          | error | nursery, no auto-fix                           |
| `useExhaustiveDependencies`| warn  |                                                |
| `noBarrelFile`             | warn  |                                                |
| `noConsole`                | warn  | warnings never fail `biome check`              |
| `useImportExtensions`      | error | `node` and `lib` only (`.js` extensions)       |

`react` additionally enables the react rule domain (`recommended`) plus
`noLeakedRender`, `noNestedComponentDefinitions`, `useReactNamingConvention`,
`noReactObjectTypeAsDefaultProp`, `useSelfClosingElements`,
`useUniqueElementIds` at error, `noReactForwardRef`,
`useComponentExportOnlyModules`, `useImageSize`, `useControlLabel` at warn, and
explicitly turns off `noImgElement`, `noJsxLiterals`, `noInlineStyles`,
`useReactFunctionComponentDefinition`.

Several rules are nursery rules. Pin `@biomejs/biome` exactly (verified on
2.6.3); a Biome upgrade is a deliberate, reviewed change, not routine
maintenance. Do not pass `--error-on-warnings`: `noConsole` is warn on
purpose.

## Usage

### Install

```bash
npm install --save-dev @tanuden/biome-config @biomejs/biome@2.6.3
```

### Root `biome.json`

Extend the profile for the project type:

```json
{
  "$schema": "https://biomejs.dev/schemas/2.6.3/schema.json",
  "extends": ["@tanuden/biome-config/electron"]
}
```

### Nested config for a subtree (monorepo)

A nested `biome.json` with `"root": false` replaces the root config for its
subtree (unless it extends `"//"`), so subtree-specific excludes and
relaxations live in the nested file. Nested configs are auto-discovered from
root runs (`biome check .`).

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

## Open Source @ Tanuden

@tanuden/biome-config is Open Source Software (OSS), licensed under MIT. You may freely distribute, use and modify code provided to you in repository in accordance with it.

A copy of the license can be found at the root of the repository [here](https://github.com/tanuden/biome-config/blob/main/LICENSE).
