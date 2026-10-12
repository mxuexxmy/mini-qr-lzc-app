# Mini QR 懒猫微服应用

把 [Mini QR](https://github.com/lyqht/mini-qr) 打包成懒猫微服 LPK V2 应用。本仓库只放懒猫侧的元数据、运行清单和镜像引用，不包含 Mini QR 源码。

| 项 | 值 |
| --- | --- |
| 包名 | `xyz.mxue.miniqr` |
| 版本 | `0.33.0` |
| 子域名 | `miniqr` |
| 协议 | GPL-3.0 |
| 最低系统版本 | lzcos 1.5.0 |
| 权限 | 无 |

应用是静态页面，容器内由 `serve` 监听 8080。不持久化数据，也不申请文档或外设权限。

## 镜像

上游没有发布 `ghcr.io/lyqht/mini-qr:v0.33.0`。v0.33.0 对应的提交是 `fe46504853c597e44b2e39d3decb5df2184c6605`，和 `ghcr.io/lyqht/mini-qr:main` 是同一份镜像：

```text
ghcr.io/lyqht/mini-qr@sha256:1d7cbdcd8667dfc5d3d3719c0c097a28c653576a7518bac5f72c112aaf9ec501
```

界面里的更新日志仍显示到 v0.30.0。上游改成手动发版后，镜像内的 `CHANGELOG.md` 没有跟上 git 标签，代码本身已经是 v0.33.0。不要改用 `latest`，那个标签目前指向未合并的依赖更新构建。

这份镜像已复制到懒猫官方仓库：

| 架构 | 地址 |
| --- | --- |
| amd64 | `registry.lazycat.cloud/mxuexxmy/lyqht/mini-qr:56b7440145c6cb8e` |
| arm64 | `registry.lazycat.cloud/mxuexxmy/lyqht/mini-qr:fb143bda08a1c9d6` |

`lzc-manifest.yml` 使用 amd64 地址。安装时微服从官方仓库拉取镜像，LPK 本身不内嵌镜像层。

## 打包安装

需要 lzc-cli 2.0 或更高版本，并且当前默认微服已授权开发公钥。

```bash
mkdir -p dist
lzc-cli project build
lzc-cli app install ./dist/xyz.mxue.miniqr-v0.33.0.lpk
```

安装后通过 `https://miniqr.<微服域名>` 访问，使用微服账号登录。`dist/` 和 `.lzc-cli-cache/` 不入库。

## 本地运行

`Dockerfile` 固定上游镜像摘要，供本机查看页面，不参与 LPK 构建。

```bash
docker compose up --build
```

浏览器打开 http://127.0.0.1:8080 。
