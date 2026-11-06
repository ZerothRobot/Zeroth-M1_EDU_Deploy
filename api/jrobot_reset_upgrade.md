# JRobot Reset and Upgrade Guide

## Full System Reset

Choose either of the following reset methods. The robot will reboot after the reset is triggered.

### Reset Using the Physical Button

Press and hold the small button next to the USB Type-C port on the top of the robot's backpack for **3 seconds**.

### Reset via Shell

Access the robot's shell and run the following commands to trigger a reset:

```bash
mkdir -p /userdata/factory
touch /userdata/factory/.reset_overlay
sync
reboot
```

## App Upgrade

### 1. Download the Upgrade Package

Download the upgrade package from the [GitHub Releases page](https://github.com/ZerothRobot/Zeroth-M1_EDU_Deploy/releases).

### 2. Transfer and Install the Package

Use ADB or SSH to transfer the archive to the robot's `/userdata` directory. Then access the robot's shell and run:

```bash
# Replace app_package.tar.gz with the actual archive filename.
cd /userdata && tar -xf app_package.tar.gz

# The upgrade file inside the archive has a fixed filename: app_package.bin.
/usr/bin/upgrade_app /userdata/app_package.bin
```

### 3. Check the Upgrade Results

View the saved upgrade result:

```bash
cat /userdata/update/app/result
```

### Recover from an Incorrect Upgrade File

If the upgrade fails because an incorrect upgrade file was used, the system will enter maintenance mode. Transfer and extract the correct package as described above, then run `/usr/bin/upgrade_app /userdata/app_package.bin` again.

The following file exists only when the system is in maintenance mode:

```bash
cat /run/app-upgrade-recovery
```
