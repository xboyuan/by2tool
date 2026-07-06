# BoYuan Tools

BoYuan 日常工具集合仓库。

这个仓库后续会持续沉淀各种脚本、运维工具和交付辅助工具。当前已经包含的 `by2tool` 是其中一个面向 Docker Compose、Harbor、多架构镜像迁移场景的运维工具。

## 工具列表

| 工具 | 说明 | 状态 |
| --- | --- | --- |
| `by2tool` | BoYuan 运维工具箱，支持镜像导出、镜像导入、服务管理、环境检查和脚本自更新 | 可用 |

## by2tool

`by2tool` 是一个单文件 Shell 工具，适合放在 Linux 服务器上直接执行。当前主要用于处理 Docker Compose 项目中的镜像迁移，尤其是测试环境与异构架构环境之间的镜像导出和导入。

主要能力：

- 交互式菜单操作，支持键盘光标选择。
- 从 `docker compose config` 中自动识别镜像。
- 支持按平台导出镜像，默认 `linux/amd64`，也可以手动选择 ARM 架构。
- 支持导出全部镜像、按 Harbor/项目路径筛选导出、单独导出某一个镜像。
- 支持导入镜像包，并保留镜像原始 tag。
- 支持环境检查、服务状态查看、服务启动、停止和重启。
- 支持从 GitHub 或 Gitee 自动更新脚本。

## 快速安装

GitHub：

```bash
cd /home/data/jar && curl -fsSL https://raw.githubusercontent.com/xboyuan/by2tool/main/by2tool -o by2tool && chmod +x by2tool && ./by2tool
```

国内网络推荐使用 Gitee：

```bash
cd /home/data/jar && curl -fsSL https://gitee.com/bydzlby/by2tool/raw/main/by2tool -o by2tool && chmod +x by2tool && ./by2tool
```

## 常用命令

交互式启动：

```bash
./by2tool
```

自动更新脚本：

```bash
./by2tool --mode update
```

指定从 Gitee 更新：

```bash
./by2tool --mode update --update-source gitee
```

指定从 GitHub 更新：

```bash
./by2tool --mode update --update-source github
```

## 镜像导出示例

按默认平台导出 Docker Compose 中的镜像：

```bash
./by2tool --mode export
```

只导出指定 Harbor 下的镜像：

```bash
./by2tool --mode export --registry-prefix 'harbor.kocel.com:8082/*'
```

只导出指定项目路径下的镜像：

```bash
./by2tool --mode export --registry-prefix 'harbor.kocel.com:8082/ktmp/*'
```

指定 ARM64 平台导出：

```bash
./by2tool --mode export --platform linux/arm64
```

## 镜像导入示例

```bash
./by2tool --mode import --input ./support_all_images.tar
```

也可以直接运行 `./by2tool`，在交互菜单中选择导入功能。

## 更新源策略

`by2tool` 默认使用自动更新源：

- 能快速访问 GitHub 时，优先使用 GitHub。
- GitHub 不可用或访问较慢时，自动切换到 Gitee。
- 也可以通过 `--update-source github` 或 `--update-source gitee` 手动指定。

## 适用场景

- Docker Compose 项目离线交付。
- x86 测试环境向 ARM 环境迁移镜像。
- Harbor 多架构镜像按指定平台导出。
- 内网服务器无外网访问时，提前打包镜像再导入。
- 运维现场需要快速检查 Docker、Compose、镜像和服务状态。

## 仓库规划

这个仓库不是单一脚本仓库，而是 BoYuan 工具集合。后续可以继续加入：

- 运维巡检脚本。
- 部署辅助脚本。
- 日志采集和问题定位工具。
- 数据备份、恢复和迁移工具。
- 项目交付和环境初始化工具。

新增工具时，建议保持单工具自包含、低依赖、可直接执行，并在 README 的工具列表中补充说明。

