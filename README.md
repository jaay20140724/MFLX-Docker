# MFLX-Docker.Baota

MFLX 面板（Minecraft 开服器管理面板）的宝塔面板 Docker 应用商店一键部署模板，参考 [NapCat-Docker.Baota](https://github.com/makotowu/NapCat-Docker.Baota) 的模板结构制作。

## 什么是 MFLX

MFLX 是 Minecraft 开服器管理面板：服务器管理、远程 API、整合包一键安装、AI 助手，支持 Windows / Linux 双平台。

## 通过宝塔面板使用

1. 宝塔面板 → **Docker → 应用商店** → 分类 **外部应用** → 右上角 **导入应用**
2. 填写本仓库地址 `https://github.com/你的账号/MFLX-Docker.Baota.git`，点击导入
3. 选择 **MFLX 面板** 应用，点击安装
4. 填写镜像地址与端口等配置，等待安装即可

## 镜像准备

MFLX 面板目前不提供公开 Docker Hub 镜像，需要自行构建并推送（付费版请使用私有仓库）：

```bash
# 在已有 Dockerfile 的发布目录构建（Dockerfile 已随 Linux 发布包提供）
cd /opt/mcpanel-docker
docker build -t mflx/mcpanel:latest .

# 登录并推送（私有仓库或 Docker Hub）
docker login
docker tag mflx/mcpanel:latest docker.io/你的账号/mflx-mcpanel:latest
docker push docker.io/你的账号/mflx-mcpanel:latest
```

部署时在「镜像地址」一栏填写推送后的完整镜像名；使用私有仓库时，请在宝塔 Docker → 仓库 中先登录对应仓库账号。

## 端口与数据

| 项目 | 默认值 | 说明 |
|------|--------|------|
| 面板 Web 端口 | 8080 | 管理界面 |
| 远程 API 端口 | 8570 | 按需开启 |
| 数据目录 | `${APP_PATH}/data` | 容器内 `/opt/mcpanel`，备份该目录即备份全部数据 |

## 目录结构

```
apphub/
└── mflx/
    ├── app.json               # 应用配置（字段、环境变量、卷）
    ├── icon.png               # 应用图标
    └── latest/
        ├── docker-compose.yml
        └── .env
```

## 资源

- [MFLX 官网](https://MFLX.p8.ink)
*（内容由AI生成，仅供参考）*
