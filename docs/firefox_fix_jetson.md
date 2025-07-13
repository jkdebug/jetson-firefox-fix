# 🧠 Firefox Fix on Jetson AGX Orin (Ubuntu 22.04, aarch64)

The default Firefox install via `apt` on Ubuntu pulls a Snap version, which fails on Jetson Orin due to sandboxing/SELinux issues.

## 🔧 Context: Why This Fix Exists

While setting up a NVIDIA Jetson AGX Orin running Ubuntu 22.04 (JetPack 6.0), I tried launching Firefox but encountered a sandbox error:

cannot set capabilities: Operation not permitted
exec: "matchpathcon": executable file not found in $PATH

This happens because Ubuntu installs Firefox as a **Snap package**, which doesn't play well with Jetson environments lacking full Snap/SELinux support.

The goal was to get a **fully working, non-Snap Firefox installation** for debugging tools, documentation, and secure browsing on Jetson — with GUI support and no sandboxing errors.

---



## ✅ Working Fix: Use Mozilla `.deb` Version

### 1. Remove Snap version:
```bash
sudo snap remove firefox
```

### 2. Pin the Mozilla PPA:
```bash
echo '
Package: *
Pin: release o=LP-PPA-mozillateam
Pin-Priority: 1001
' | sudo tee /etc/apt/preferences.d/mozilla-firefox
```

### 3. Add the Mozilla PPA:
```bash
sudo add-apt-repository ppa:mozillateam/ppa -y
sudo apt update
```

### 4. Install `.deb` Firefox manually:
```bash
sudo apt install firefox=140.0.4+build1-0ubuntu0.22.04.1~mt1
```

---

### ✅ Confirmed Working:
```bash
Linux ubuntu 5.15.148-tegra aarch64 (Jetson AGX Orin, JetPack 6.0)
```
