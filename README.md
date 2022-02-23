## commintlint 模板项目

### 目前最常使用的 commit 规范为 angular 提交方式

```
<type>(<scope>): <subject>
```

- type 提交类型
- scope 提交范围
- subject 提交描述

本项目集成 commitizen + commitlint，可使用命令交互式规范代码提交信息，通过 husky 拦截 git 的 commit-msg hook

```shell
yarn add @commitlint/cli husky --dev
# 激活husky
npm set-script prepare "husky install"
yarn
npx husky add .husky/commit-msg 'npx --no-install commitlint --edit "$1"'
npx husky add .husky/pre-commit  'yarn lint &&  git add . '
# 命令式交互
yarn add @commitlint/cz-commitlint commitizen --dev
# 增加changelog
yarn add conventional-changelog-cli --dev

```

增加 lint 校验

```shell
yarn add eslint prettier lint-staged --dev
# 增加pre-commit hook
npx husky add .husky/pre-commit "npx lint-staged"

# 格式化配置文件
touch .prettierrc.js
touch .eslintrc.js

```

.prettierrc.js

```js
module.exports = {
  semi: false,
  tabWidth: 2,
  singleQuote: true,
  jsxSingleQuote: true,
  printWidth: 100,
}
```

.eslintrc.js

```js
module.exports = {
  env: {
    browser: true,
    commonjs: true,
    es2021: true,
  },
  extends: ['eslint:recommended'],
  parserOptions: {
    ecmaVersion: 8,
  },
  rules: {
    'no-unused-vars': 'off',
    'no-console': 'warn',
    'space-before-function-paren': 'warn',
    semi: ['error', 'never'],
    quotes: ['warn', 'single'],
  },
}
```

````
package.json 增加lint-staged
```js
{
    // ...其他配置
    "lint-staged": {
    "**/*.{js,jsx}": [".prettierrc --write", "eslint --fix"],
    "*.md": ["prettier --write"]
    }
}
````
