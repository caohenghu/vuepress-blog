---
category: 技术
tags:
  - git
date: 2020-03-03
title: 如何生成changelog
vssue-title: 如何生成changelog
---

> 在使用 `git` 提交 `commit` 时，最好有一个规范，这样可以很方便地生成 `changelog`。

<!-- more -->

## commit msg 规范

1. 安装依赖包

```sh
# 强制commit msg需符合规范才能提交
$ yarn add -D @commitlint/config-conventional @commitlint/cli husky

# 用来生成CHANGELOG.md
$ yarn add -D conventional-changelog-cli
```

2. 在`package.json`里添加配置

```json
{
  "scripts": {
    "changelog": "conventional-changelog -p angular -i CHANGELOG.md -s -r 0"
  },
  "husky": {
    "hooks": {
      "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
    }
  },
  "commitlint": {
    "extends": ["@commitlint/config-conventional"]
  }
}
```

3. 生成`CHANGELOG.md`

```sh
# 执行script里的代码
$ yarn changelog
```

## 便捷输入 commit msg

> 如果对规范比较了解，可以不使用这个工具

1. 安装依赖包

```sh
# 在全局安装后可以使用 git cz 来代替 git commit，如果装在本地则需要使用 yarn git-cz
$ yarn global add commitizen

# 安装后就有友好提示了
$ yarn add -D cz-conventional-changelog
```

2. 在`package.json`里添加配置

```json
{
  "config": {
    "commitizen": {
      "path": "cz-conventional-changelog"
    }
  }
}
```

3. 所有的`commit msg`类型，使用的是`angular`规范

- **feat:** A new feature
- **fix:** A bug fix
- **docs:** Documentation only changes
- **style:** Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
- **refactor:** A code change that neither fixes a bug nor adds a feature
- **perf:** A code change that improves performance
- **test:** Adding missing tests or correcting existing tests
- **build:** Changes that affect the build system or external dependencies (example scopes: gulp, broccoli, npm)
- **ci:** Changes to our CI configuration files and scripts (example scopes: Travis, Circle, BrowserStack, SauceLabs)
- **chore:** Other changes that don't modify src or test files
- **revert:** Reverts a previous commit
