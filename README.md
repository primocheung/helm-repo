# helm-repo

[English](README.md) | [中文](README.zh.md)

Helm chart repository (packages only) hosted via GitHub Pages.

## How this repo works

- Store packaged charts (`.tgz`) under `packages/` in the default branch.
- Workflow `.github/workflows/release.yml` publishes all `.tgz` to `gh-pages` and generates `index.yaml`.
- Configure Settings → Pages: Branch `gh-pages`, Folder `/ (root)`.

## Add/Update a chart package

1) Build the chart in your source repo: `helm package charts/<name>` → produces `<name>-<version>.tgz`.
2) Copy the `.tgz` into this repo under `packages/` and push to `main/master`.
3) Wait for GitHub Actions to finish. The package and `index.yaml` will be available at [https://xxx.github.io/helm-repo/](https://xxx.github.io/helm-repo/).

## Client usage

- `helm repo add myrepo https://xxx.github.io/helm-repo/`
- `helm repo update && helm search repo myrepo`
- `helm install demo myrepo/<chart-name> --version <x.y.z>`

## Notes

- Keep every released version; do not replace files in-place. Push a new `.tgz` when version changes.
- The repo does not contain chart source; only packaged artifacts.
