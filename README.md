# 我的 Rime 配置（已更新为 Fcitx5 Flatpak）

## 安装流程

### 安装 Fcitx5 及 Rime 插件（Flatpak）
```bash
# 添加 flathub 仓库（若已添加可跳过）
flatpak remote-add --user --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo

# 安装 Fcitx5 框架
flatpak install org.fcitx.Fcitx5

# 安装 Rime 输入法引擎
flatpak install org.fcitx.Fcitx5.Addon.Rime
```

### 克隆 rime-ice 方案
```bash
git clone https://github.com/wdnb/rime-ice.git
```
### 复制内容到 Fcitx5 的 Rime 配置目录
- 注意路径已变为 Flatpak 的 Rime 用户目录
```bash
cp -r rime-ice/* ~/.var/app/org.fcitx.Fcitx5/data/fcitx5/rime/
```
### 自启动并自替换系统自带ibus输入法
```bash
# 增加环境变量
vim ~/.profile
export XMODIFIERS=@im=fcitx
export QT_IM_MODULE=fcitx

# 开机自启动

mkdir -p ~/.config/autostart

cat > ~/.config/autostart/fcitx5.desktop << 'EOF'
[Desktop Entry]
Type=Application
Name=Fcitx 5
Exec=flatpak run org.fcitx.Fcitx5
Icon=org.fcitx.Fcitx5
X-GNOME-Autostart-enabled=true
EOF
```
### 重启
