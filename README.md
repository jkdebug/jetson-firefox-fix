# 🦊 Jetson Firefox Fix (Ubuntu 22.04, JetPack 6.x)

This repo documents a tested workaround to get a fully functional **non-Snap version of Firefox** running on **NVIDIA Jetson AGX Orin** systems using Ubuntu 22.04.

## ⚙️ Why This Exists

Snap packages often fail on Jetson platforms due to missing SELinux components and sandboxing issues. This project provides a clean `.deb`-based installation path that avoids those problems — enabling:

- Secure browsing
- GUI-based documentation access
- Stable dev tools (for debugging, docs, etc.)

## ✅ Confirmed Setup

- Jetson AGX Orin (64GB)
- Ubuntu 22.04
- JetPack 6.0
- Kernel: `5.15.148-tegra`

## 📄 Documentation

All steps are in:  
[`docs/firefox_fix_jetson.md`](docs/firefox_fix_jetson.md)

## 👷 Maintainer

**@jkdebug**  
Detroit-area embedded hardware engineer building rugged Jetson-based compute systems.

