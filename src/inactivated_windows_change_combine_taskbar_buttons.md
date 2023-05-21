# 未激活的 Windows 修改“合并任务栏按钮”

> Windows 10 未激活的时候，虽然可以使用，但是一些个性化功能无法调整，比如无法修改“合并任务栏按钮”的方式。
> 鉴于使用的是虚拟机，购买激活码也不合适，所以找了一下其他方法来解决。

1. 按下 `win + R`，输入 `regedit`，打开 `注册表编辑器`。

1. 打开目录 `HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced`。

1. 根据个人需求，按照下表新建或调整数据。

   | Key                | Type      | Value | Notice                             |
   | :----------------- | :-------- | :---- | :--------------------------------- |
   | TaskbarGlomLevel   | REG_DWORD | 2     | 主屏任务栏按钮不合并               |
   | MMTaskbarGlomLevel | REG_DWORD | 2     | 多显示器其他任务栏按钮不合并       |
   | MMTaskbarMode      | REG_DWORD | 2     | 多显示器其他任务栏只显示打开的程序 |

1. `注册表编辑器`的内容修改后，打开 `任务管理器`，点击 `进程`，找到 `Windows 资源管理器`，右键选中，点击 `重新启动`。

1. 此后即可生效。
