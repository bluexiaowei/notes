# git message 规范

> 使用工具规范团队的 git message 提交规范。

## 使用

安装依赖

```shell
yarn add commitizen -D

npx commitizen init cz-conventional-changelog-chinese --yarn --dev --exact
```

修改文件 `package.json`

```json5
{
    // ...
    "scripts" {
        // ...
        "commit": "npx cz"
    },
}
```

运行

```shell
npm run commit
```

## 学习资料

- [commitizen](https://github.com/commitizen/cz-cli)
- [cz-conventional-changelog-chinese](https://github.com/rhinel/cz-conventional-changelog-chinese)
