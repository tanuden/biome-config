# @tanuden/biome-config

**English** | [日本語](https://github.com/tanuden/biome-config/blob/main/README.ja.md)

Biome linter preset for Tanuden typescript projects.

For use on:

- Electron Apps
- Node services
- Libraries

## Style contract

### Formatter

| Setting                    | Value     |
| -------------------------- | --------- |
| Indent                     | 2 spaces  |
| Line width                 | 100       |
| Line endings               | LF        |
| Semicolons                 | Always    |
| Quotes (JS and JSX)        | Double    |
| Quote properties           | As needed |
| Trailing commas (JS, JSON) | None      |
| Arrow parentheses          | Always    |
| Bracket spacing            | On        |
| Bracket same line          | Off       |
| CSS quotes                 | Double    |

### Linter

| Rule                        | Level | Notes                                 |
| --------------------------- | ----- | ------------------------------------- |
| `useImportType`             | error |                                       |
| `useFilenamingConvention`   | error | kebab-case or PascalCase filenames    |
| `useExhaustiveDependencies` | warn  |                                       |
| `noBarrelFile`              | warn  |                                       |
| `noFloatingPromises`        | warn  |                                       |
| `noArrayIndexKey`           | off   | deliberate exception to `recommended` |

## Usage

### Install

```bash
npm install --save-dev @tanuden/biome-config @biomejs/biome@2.6.3
```

Requires `@biomejs/biome` 2.6.x (verified on 2.6.3).

### Adding to `biome.json`

The biome `recommended` preset should be used as the base.
Use the `react` domain for React projects where necessary.

```json
{
  "$schema": "https://biomejs.dev/schemas/2.6.3/schema.json",
  "extends": ["@tanuden/biome-config/biome"]
}
```

## Open Source @ Tanuden

@tanuden/biome-config is Open Source Software (OSS), licensed under MIT. You may freely distribute, use and modify code provided to you in repository in accordance with it.

A copy of the license can be found at the root of the repository [here](https://github.com/tanuden/biome-config/blob/main/LICENSE).
