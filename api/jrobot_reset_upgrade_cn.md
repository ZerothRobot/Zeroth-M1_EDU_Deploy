# JRobot 重置和升级说明

> **版本要求：** 以下操作仅在升级到 `v1.7.13.1_rl_202611061340` 或更新版本后可用。

## 整机重置

可选择以下任一方式触发重置。触发后，机器人会自动重启。

### 通过物理按键重置

长按机器人背包顶部 USB Type-C 接口旁的小按钮 **3 秒**。

### 通过 Shell 重置

进入机器人的 Shell，执行以下命令触发重置：

```bash
mkdir -p /userdata/factory
touch /userdata/factory/.reset_overlay
sync
reboot
```

这种方式是重置系统分区和APP分区为出厂状态，不删除程序运行数据（/userdata）。若要清理程序数据，请使用背包上方的重置按键。

## App 升级

### 1. 下载升级包

从 [GitHub Releases 页面](https://github.com/ZerothRobot/Zeroth-M1_EDU_Deploy/releases)下载升级包。

### 2. 传输并安装升级包

通过 ADB 或 SSH 将升级包传输到机器人的 `/userdata` 目录，然后进入机器人的 Shell，执行以下命令：

```bash
# Replace app_package.tar.gz with the actual archive filename.
cd /userdata && tar -xf app_package.tar.gz

# The upgrade file inside the archive has a fixed filename: app_package.bin.
/usr/bin/upgrade_app /userdata/app_package.bin
```

### 3. 查看升级结果

执行以下命令查看保存的升级结果：

```bash
cat /userdata/update/app/result
```

### 使用错误升级文件后的恢复

如果使用了错误的升级文件而导致升级失败，系统会进入维护模式。按照上述步骤传输并解压正确的升级包，然后重新执行 `/usr/bin/upgrade_app /userdata/app_package.bin`。

以下文件仅在系统处于维护模式时存在：

```bash
cat /run/app-upgrade-recovery
```
