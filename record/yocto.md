# BitBake 构建命令

| 命令 | 说明 |
|------|------|
| `bitbake <recipe>` | 构建指定的配方（如 `core-image-minimal`） |
| `bitbake -c clean <recipe>` | 清理配方的构建输出（`tmp/work` 下对应目录） |
| `bitbake -c cleanall <recipe>` | 彻底清理：包括下载的源码包和构建输出 |
| `bitbake -c cleansstate <recipe>` | 清理共享状态缓存（`sstate-cache`） |
| `bitbake -c fetch <recipe>` | 仅下载配方的源代码，不构建 |
| `bitbake -c unpack <recipe>` | 解压源码到工作目录，不编译 |
| `bitbake -c compile <recipe>` | 仅编译（前提是已执行过 `unpack` 和 `configure`） |
| `bitbake -c install <recipe>` | 仅安装到临时根文件系统（`do_install`） |
| `bitbake -c package <recipe>` | 仅打包（生成 `rpm`/`ipk`/`deb` 等） |
| `bitbake -c rootfs <image>` | 仅构建根文件系统 |
| `bitbake -c menuconfig <kernel-recipe>` | 配置内核（如 `virtual/kernel`） |
|                     `bitbake -c savedefconfig <kernel-recipe>`                    |             保存（如 `virtual/kernel`）             |
| `bitbake -c listtasks <recipe>` | 列出配方支持的所有任务 |
| `bitbake -g <recipe>` | 生成依赖图（`PN-buildall` 和 `PN-depends.dot`） |
| `bitbake -e <recipe>` | 输出配方的所有环境变量（含展开值） |
| `bitbake -s` | 显示所有配方及其版本（`show-versions`） |
| `bitbake -S none <recipe>` | 生成锁定签名数据，用于调试依赖变化 |
|              `bitbake -c devshell virtual/kernel`              |          直接进入一个已配置好内核源码的 shell 环境         |

---

## BitBake 常用选项

| 选项 | 说明 |
|------|------|
| `-k` | 继续构建，即使某个任务失败 |
| `-f` | 强制重新执行任务（不依赖 stamps） |
| `-v` | 详细输出（verbose） |
| `-D` | 调试输出，可叠加 `-DD` 或 `-DDD` 增加详细度 |
| `-c <task>` | 执行指定任务（如 `compile`、`install`） |
| `-C <task>` | 重新执行指定任务及其依赖的任务 |
| `--dry-run` | 仅显示将要执行的任务，不实际运行 |
| `--runall <task>` | 为所有依赖的配方运行指定任务 |

---

## devtool 开发工具

devtool 用于简化源码修改、补丁管理和层集成。

### 常用命令

| 命令 | 说明 |
|------|------|
| `devtool add <recipe> <source>` | 创建新配方（源码可为本地路径或 git URL） |
| `devtool modify <recipe>` | 将配方源码提取到工作区进行修改 |
| `devtool build <recipe>` | 构建工作区中的配方 |
| `devtool deploy-target <recipe> <user@host>` | 将构建结果部署到目标设备（通过 ssh） |
| `devtool undeploy-target <recipe> <user@host>` | 从目标设备卸载部署的文件 |
| `devtool finish <recipe> <layer>` | 将工作区的修改保存到指定层（生成补丁和 bbappend） |
| `devtool reset <recipe>` | 清除工作区的修改（可加 `-r` 删除源码目录） |
| `devtool status` | 显示当前工作区中所有配方的状态 |
| `devtool search <keyword>` | 搜索配方（基于描述） |
| `devtool edit-recipe <recipe>` | 编辑配方文件 |
| `devtool upgrade <recipe> <new-version>` | 升级配方到新版本 |
| `devtool check-upgrade-status` | 检查配方是否有可升级的新版本 |

### 常用选项

| 选项 | 说明 |
|------|------|
| `-r` / `--remove-work` | `finish` 或 `reset` 时同时删除源码目录 |
| `-n` / `--no-clean` | `build` 时不先执行 `clean` |
| `-s` / `--same-dir` | `modify` 时在源码目录内构建（而不是使用独立的 build 目录） |

---

## recipetool 配方生成工具

| 命令 | 说明 |
|------|------|
| `recipetool create <source>` | 根据源码自动生成基础配方（如从 git 仓库） |
| `recipetool appendfile <layer> <file>` | 为现有配方追加文件（生成 bbappend） |
| `recipetool newappend <layer>` | 创建空的 bbappend 文件框架 |
| `recipetool setvar <recipe> <var>=<value>` | 修改配方中的变量并生成 bbappend |
| `recipetool show-recipe <recipe>` | 显示配方的详细信息（变量、依赖等） |

---

## 层管理与环境查询

| 命令 | 说明 |
|------|------|
| `bitbake-layers show-layers` | 列出当前所有层及其优先级和路径 |
| `bitbake-layers show-recipes` | 显示所有配方（可加 `-i <layer>` 限制层） |
| `bitbake-layers show-appends` | 列出所有 bbappend 文件及其应用的配方 |
| `bitbake-layers add-layer <layer>` | 将新层添加到 `bblayers.conf` |
| `bitbake-layers remove-layer <layer>` | 从 `bblayers.conf` 中移除层 |
| `bitbake-layers flatten` | 合并所有 bbappend 到临时目录（调试用） |
| `oe-pkgdata-util lookup-recipe <file>` | 根据文件路径查找归属配方（需 source 环境） |
| `oe-pkgdata-util list-pkgs` | 列出所有已打包的软件包 |
| `oe-pkgdata-util find-path <path>` | 查找文件属于哪个软件包 |

---

## 环境初始化与配置

| 命令 | 说明 |
|------|------|
| `source oe-init-build-env <build-dir>` | 初始化 Yocto 构建环境（创建/进入构建目录） |
| `bitbake -e \| grep ^BBLAYERS` | 查看当前加载的层路径 |
| `bitbake -e <recipe> \| grep ^FILESEXTRAPATHS` | 查看配方的额外搜索路径 |
| `bitbake-getvar <var> -r <recipe>` | 获取配方的变量值（如 `bitbake-getvar PN`） |

---

## 常用工作流程示例

```bash
# 1. 初始化环境
source poky/oe-init-build-env build

# 2. 添加自定义层
bitbake-layers add-layer ../meta-myir

# 3. 修改内核源码
devtool modify virtual/kernel
cd workspace/sources/linux-*
# 修改文件...
git add .
git commit -m "fix driver"
devtool finish -r virtual/kernel ../meta-myir

# 4. 构建完整镜像
bitbake core-image-weston

# 5. 运行 QEMU 测试
runqemu qemux86-64 core-image-minimal
```
