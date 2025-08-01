# semantic-release-bolierplate 

一个用于使用 semantic-release 的启动模板，具有使用 semantic-release 进行自动版本控制和发布的功能。

## 特性

- 🚀 使用 semantic-release 自动发布
- 🎯 TypeScript 支持
- 📝 自动生成更新日志
- 🔄 GitHub Actions 工作流程用于 CI/CD
- 📊 GitHub Pages 文档托管

## 开始使用

### 设置令牌

此模板使用 GitHub Actions 进行自动发布。您需要设置以下令牌：

#### 1. GitHub 令牌 (GH_TOKEN)

1. [创建 Github 个人访问令牌](https://github.com/settings/tokens)
2. 点击 `Generate new token`
3. 根据你的需求选择 `Repository access`
3. 生成具有以下权限的新令牌：
   - Actions - read and write
   - Commit statuses - read and write
   - Contents - read and write
   - Deployments - read and write
4. 

#### 2. NPM 令牌 (NPM_TOKEN)
1. 访问 [npmjs.com](https://www.npmjs.com/)
2. 导航到您的个人设置
3. 选择 "Access Tokens"
4. 创建新的访问令牌（注意把权限勾上）

#### 3.  Github设置环境变量

1. 仓库中 访问 settings / secrets and variables / actions / Repository secrets
2. 将刚刚的 GH_TOKEN 和 NPM_TOKEN 设置进去

#### 4. 开启 GitHub Actions

1. 参考本仓库的 `release.yml`


#### 5. releaserc.json
```json
{
  // 你自己的仓库地址
  repositoryUrl: '',
  branches: ["master"], // 指定在哪个分支下要执行发布操作
  plugins: [
    // 1. 解析 commit 信息，默认就是 Angular 规范
    "@semantic-release/commit-analyzer",
    // 2. 生成发布信息
    "@semantic-release/release-notes-generator",
    // 3. 把发布日志写入该文件
    [
      "@semantic-release/changelog",
      {
        changelogFile: "CHANGELOG.md", 
      },
    ],
    // 4. 发布 NPM
    "@semantic-release/npm", 
    // 5. changelog 和 vesion，需要重新写入 package.json
    [
      "@semantic-release/git",
      {
        assets: ["CHANGELOG.md", "package.json"],
      },
    ],
  ],
};


```

## 发布流程

此模板使用 semantic-release 进行自动版本控制和发布。当更改推送到主分支时，会自动触发发布流程。

提交消息应遵循 [Conventional Commits](https://www.conventionalcommits.org/) 规范：

- `feat: ...` - 新功能（次要版本发布）
- `fix: ...` - 错误修复（补丁版本发布）
- `BREAKING CHANGE: ...` - 破坏性更改（主要版本发布）