## 1. jslint jshint eslint

- 1. JSLint:
    - 创作者： Douglas Crockford.
    - 特点： JSLint 是早期的 JavaScript 代码检查工具之一，它设计目标是通过强制实施一种特定的编码风格来帮助开发者捕获潜在的错误和不良实践。
    - 约束： JSLint 的规则相对较为严格，不太容易自定义或配置。它可能会直接阻止代码执行，而不仅仅是发出警告。
- 2. JSHint:
    - 创作者： Anton Kovalyov.
    - 特点： JSHint 是在 JSLint 的基础上创建的一个分支，旨在提供更大的灵活性和可配置性。它允许开发者通过配置文件来定义规则，以适应不同的项目和团队需求。
    - 可配置性： JSHint 相对于 JSLint 更容易定制和配置，允许选择性地启用或禁用规则。
- 3. ESLint:
    - 创作者： Nicholas C. Zakas.
    - 特点： ESLint 是一个更现代、更灵活的 JavaScript 代码检查工具。它提供了广泛的配置选项，允许开发者通过配置文件和插件来定义和扩展规则。
    - 生态系统： ESLint 的生态系统更为庞大，拥有丰富的插件和支持，可以与各种框架和工具集成。
    - 可插拔性： ESLint 具有可插拔的体系结构，使得用户能够通过自定义规则和插件来适应不同的开发环境。
    - JSCS 于2016年停止开发，迁移到eslint(完全兼容JSCS)
    - v8.53.0 弃用警告 https://eslint.org/blog/2023/10/deprecating-formatting-rules/#javascript%E2%80%99s-explosion-and-the-maintenance-burden

## 2. 命令
    - `npx eslint xxx xxx` 命令行检查某个文件(多个文件)
    - `npx eslint src/**`  检查目录下所有文件
    - `npx eslint --fix xxx`  命令行自动修复某个文件(多个文件)

## 3. 关闭检查
```js
alert('foo'); // eslint-disable-line

// eslint-disable-next-line -- I don't want eslint(注释) 
alert('foo');

/* eslint-disable-next-line */
alert('foo');

alert('foo'); /* eslint-disable-line */

// eslint-disable-next-line no-alert, quotes, semi
alert('foo');

foo(); // eslint-disable-line plugin/rule-name

/* 
*  块关闭 
*/
/* eslint-disable */
console.log("bar")
alert('foo');
/* eslint-enable */

/* eslint-disable no-alert, no-console */
alert('foo');
console.log('bar');
/* eslint-enable no-alert, no-console */

/*
*  整个文件关闭，在第一行使用  eslint-disable 
*/
/* eslint-disable */
alert('foo');
//...

/* eslint-disable no-alert */
alert('foo');
//...

```

## 4. 配置的优先级
由于 ESLint 支持多处配置，配置之间可能会冲突，需要规定优先级：
- 配置类型上： 注释 > 命令行参数 > 配置文件
- 文件层级上：（相对目标文件）近 > 远
- 同一目录内：（只会采用一个配置文件）js > cjs > yaml > yml > json > package.json
- 同一配置内：overrides > rule > extends
- 同一选项内：后者 > 前者
