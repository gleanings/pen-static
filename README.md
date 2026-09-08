# @vvi/pen-static

[![version](<https://img.shields.io/npm/v/@vvi/pen-static.svg?logo=npm&logoColor=rgb(0,0,0)&label=版本号&labelColor=rgb(73,73,228)&color=rgb(0,0,0)>)](https://www.npmjs.com/package/@vvi/pen-static) [![issues 提交](<https://img.shields.io/badge/issues-提交-rgb(255,0,63)?logo=github>)](https://github.com/gleanings/pen-static/issues)

## 安装

```bash
npm install --save @vvi/pen-static
```

## ANSI 模块相关

- `esc` ANSI 转义符
- `csi` CSI（Control Sequence Introducer）带 `[` 的 `esc` 字符串 `\u001b[` 或者是 `\x1b`
- `terminalResetStyle` 重置属性样式，即 `\x1b[0m`
- `terminalRegExp` 一个用于创建 ANSI 的正则字符串的函数，可用与判断字符串是否包含 ANSI 转义或是清理

### `esc`

`esc` 表示 ANSI 的控制序列前缀描述，即 `\x1b` 或者是 `\u001b`。

```ts
import { esc } from '@vvi/pen-static';
// 光标向上
const cursorMoveUpStr = esc.concat('[2A');

console.log(cursorMoveUpStr);
```

### `csi`

`csi` 表示 ANSI 的控制序列，即 `\x1b[` 或者是 `\u001b[`。

```ts
import { csi } from '@vvi/pen-static';
// 光标向上
const cursorMoveUpStr = csi.concat('2A');

console.log(cursorMoveUpStr);
```

### `terminalResetStyle`

`terminalRestStyle` 表示 ANSI 的属性重置，即 `\x1b[0m` 或 `\u001b[0m` 或 `\x1b[m` 或 `\u001b[m`。

```ts
import { pen } from '@vvi/pen';
import { terminalResetStyle } from '@vvi/pen-static';

pen.red`我是红色的文本${terminalResetStyle.concat('其实，在使用 terminalResetStyle 的时候会被截断，而最后的返回，这里也是红的')}我也是红色的`;
```

### `terminalRegExp` 正则

生成一段长的 ANSI 正则字符串，用于判断字符串是否包含 ANSI 转义或是清理字符串中的 ANSI 转义码。

```ts
import { terminalRegExp } from '@vvi/pen-static';

const tempRegExp = terminalRegExp();

tempRegExp.latestIndex = 0;

console.log(tempRegExp.test('\x1b[0m')); // true

tempRegExp.latestIndex = 0;

console.log(tempRegExp.test('\x1b[?25l')); // true

tempRegExp.latestIndex = 0;

console.log(tempRegExp.test('\x1b[38;5;236m')); // true
```

## 状态

此软件包是 `MrMudBean` 生态系统的一部分。
它使用严格的 TypeScript 编写，并通过 Rollup 构建进行验证。
虽然单元测试较少，但 API 稳定，并在生产环境中大量使用。
