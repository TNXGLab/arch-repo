# TNXG Arch Repository

为 [TNXGLab/noctalia](https://github.com/TNXGLab/noctalia) `main` 分支提供自动构建的 Arch Linux `x86_64` 软件包。

源码仓库每次推送到 `main` 后，GitHub Actions 会：

1. 在最新 Arch Linux 容器中构建当前提交。
2. 仅保留最新的 `noctalia` 软件包。
3. 重建 Pacman 数据库并推送到本仓库的 `gh-pages` 分支。

## 使用方式

在 `/etc/pacman.conf` 末尾添加：

```ini
[noctalia]
SigLevel = Optional TrustAll
Server = https://tnxglab.github.io/arch-repo/$arch
```

随后安装或更新：

```bash
sudo pacman -Syu noctalia
```

## 版本与安全

- 软件包版本格式为 `<上游版本>.r<提交数>.<提交短哈希>+tnxg-<pkgrel>`，可直接定位到源码提交。
- 仓库只发布 `TNXGLab/noctalia` 的持续集成构建，不等同于上游稳定版或 AUR 发布版。
- 当前软件包未签名，因此配置使用 `SigLevel = Optional TrustAll`。仅应在信任本仓库和构建流程时启用。

## 仓库结构

```text
x86_64/
├── noctalia-<version>-x86_64.pkg.tar.zst
├── noctalia.db -> noctalia.db.tar.gz
├── noctalia.db.tar.gz
├── noctalia.files -> noctalia.files.tar.gz
└── noctalia.files.tar.gz
```
