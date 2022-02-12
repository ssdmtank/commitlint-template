## commintlint 模板项目

### 目前最常使用的commit规范为angular提交方式
```
<type>(<scope>): <subject>
```
* type 提交类型
* scope 提交范围
* subject 提交描述

本项目集成commitizen + commitlint，可使用命令交互式规范代码提交信息，通过husky拦截git的commit-msg hook

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