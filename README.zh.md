# helm-repo

[English](README.md) | [中文](README.zh.md)

通过 GitHub Pages 托管的 Helm chart 仓库（仅包含打包文件）。

## 仓库工作原理

- 在默认分支的 `packages/` 目录下存储打包的 chart（`.tgz` 文件）。
- 工作流 `.github/workflows/release.yml` 会将所有 `.tgz` 文件发布到 `gh-pages` 分支并生成 `index.yaml`。
- 配置 Settings → Pages：分支选择 `gh-pages`，文件夹选择 `/ (root)`。

## 添加/更新 chart 包

1) 在源仓库中构建 chart：`helm package charts/<name>` → 生成 `<name>-<version>.tgz`。
2) 将 `.tgz` 文件复制到此仓库的 `packages/` 目录下，然后推送到 `main/master` 分支。
3) 等待 GitHub Actions 完成。包和 `index.yaml` 将在 [https://xxx.github.io/helm-repo/](https://xxx.github.io/helm-repo/) 可用。

## 客户端使用

- `helm repo add myrepo https://xxx.github.io/helm-repo/`
- `helm repo update && helm search repo myrepo`
- `helm install demo myrepo/<chart-name> --version <x.y.z>`

## 注意事项

- 保留每个已发布的版本；不要原地替换文件。版本变更时推送新的 `.tgz` 文件。
- 此仓库不包含 chart 源码；仅包含打包后的产物。

