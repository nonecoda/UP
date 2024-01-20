# 基础命令

> 以下使用 `<>` 包裹的内容，未需要自行替换的数据。  
> 示例中，则会用 `coda` 作为用户名，`your_password` 作为密码来进行展示。

## 定位命令所在位置

- 简介

    `whereis <command_name>` 和 `which <command_name>` 这两个命令都可以用来定位命令所在的位置。

    不同点在于，`which` 只能找到当前用户可以使用的，`whereis` 则没有这项约束。

- 示例

    ```shell
    whereis adduser
    which useradd
    ```

## 新增用户

- 简介：

    大多数 Linux 发行版都自带了 `adduser` 命令，该命令可以说是 `useradd -m` 和 `passwd` 的集合，创建用户很方便。

    在使用 `adduser <username>` 命令后，按需填写 **密码** 等信息，会创建出一个新的用户，并且在 `/home` 目录下创出一个与 `<username>` 同名的文件夹。

- 示例：

    ```shell
    adduser coda

    # 会输出以下文字，按需填写。
    # Adding user `coda' ...
    # Adding new group `coda' (1001) ...
    # Adding new user `coda' (1001) with group `coda' ...
    # Creating home directory `/home/coda' ...
    # Copying files from `/etc/skel' ...
    # New password:
    # Retype new password:
    # passwd: password updated successfully

    # 等同于：
    # useradd -m coda
    # passwd your_password
    ```

## 将用户添加到权限组中

- 简介：

    `usermod -aG <group_name> <username>` 将 `<username>` 添加到 `<group_name>` 组中，如果只是将当前用户追加到组内，可用 `$USER` 替换 `<username>`。

- 示例：

    ```shell
    # 将当前用户追加到 sudo 组中
    usermod -aG sudo $USER
    ```

- Tips:

    如果将用户追加到 **sudo** 组中，但是无法使用 `sudo` 命令来调用其他命令，则需要去 `/etc/sudoers` 文件中 (或 `/etc/sudoers.d/` 目录下) 按需追加相关信息。

    比如：

    ```md
    <!-- root 用户，可以 **不使用密码** 操作所有文件和文件夹 -->
    root ALL=(ALL) NOPASSWD:ALL
    <!-- coda 用户，可以操作所有文件和文件夹，但是需要使用 `sudo` 命令，并 **输入密码** -->
    coda ALL=(ALL) ALL
    <!-- lust 用户，权限与 coda 用户相同，但是 **不可以使用** `passwd` 命令 -->
    lust ALL=(ALL) !/user/bin/passwd
    ```

## 修改主机名称

- 简介

    `hostnamectl set-hostname <new_hostname>`

- 示例

    ```shell
    hostnamectl set-hostname coda-machine
    
    # 查看 hostname。
    # hostname
    ```

- Tips:

    必要时，还需要修改 `/etc/hosts` 文件。
