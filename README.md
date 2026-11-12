# ene-rgb

铭瑄（Maxsun）等主板上的 **ENE 6K7750** 板载 ARGB 控制器 Linux 控制方案。
这个芯片就是 `lsusb` 里的 `0cf2:7750 ENE Technology, Inc. MS-ARGB`，OpenRGB
完全认不到它，本仓库用逆向出来的 USB 协议直接驱动。

实测主板：**MAXSUN MS-B550M GAMING WIFI**（分组 `[128, 128, 1, 1, 6]`，
第 0 组是机箱底部三个风扇，第 1 组是其余风扇和板载灯条）。

## 特性

- 常亮：芯片单次刷色后约 1~2 分钟进入睡眠，守护进程每秒重刷一次维持
- 休眠恢复、USB 重新枚举后自动重新打开设备
- GTK4 + libadwaita 面板，调颜色、亮度、一键关灯，跟随系统深浅色
- 只动 LED 寄存器，不碰风扇转速

## 安装

```sh
sudo pacman -U ene-rgb-1.0.0-1-any.pkg.tar.zst
sudo udevadm control --reload && sudo udevadm trigger
systemctl --user enable --now ene-rgb.service
```

重新登录一次让 `uaccess` 规则对当前会话生效。

## 使用

面板：应用菜单里的「机箱灯效」，或者直接 `ene-rgb-gui`。
命令行：`ene-rgb info | fill <组|all> RRGGBB | backup <文件> | restore <文件> | off`

配置存在 `~/.config/ene-rgb/state.json`，面板改完守护进程一秒内跟上。

## 自己校准分组

```sh
ene-rgb fill 0 FF0000   # 看哪组亮
ene-rgb off all
```

## 许可

本项目 MIT。底层协议实现来自
[teamlocabit/ene-6k7750-rgb](https://github.com/teamlocabit/ene-6k7750-rgb)
（MIT），见 NOTICE。
