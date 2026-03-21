# 🚀 AndroidOne Experience Build Instructions

This guide walks you through setting up, syncing, building, and customizing your own AndroidOne Experience ROM for your device.

---

## 📦 Initialize the Local Repository

First, initialize your repo with the AndroidOne manifest:

```bash
repo init -u https://github.com/LineageOS-Fork-edition/manifest.git -b 16-QPR2 --depth=1 --git-lfs
```

---

## 🔄 Sync the Source

Now sync the source code. This step may take some time depending on your internet connection and CPU:

```bash
repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags
```

---

## ⚙️ Set Up the Environment

After syncing, initialize the build environment:

```bash
source build/envsetup.sh
```

---

## 📱 Choose a Target Device

```bash
lunch aosp_<device>-bp1a-user
```
> Replace `<device>` with your actual device codename.

---

## 🛠️ Build the Code

Now you’re ready to build! Use the following command to compile the ROM:

```bash
mka bacon -j$(nproc --all) | tee log.txt
```

The build output will be saved to `log.txt` for review.

---

## 🧩 Optional Build Flags

You can customize your ROM build by including the following flags in your **device tree** (usually in `aosp_<device>.mk` or `device.mk`):

### ✅ Flag Values

| Flag | Value |
|------|-------|
| `TARGET_SUPPORT_MINIMAL_GAPPS`    | `true`  |
| `TARGET_SUPPORT_PIXEL_LAUNCHER` | `true` |
| `TARGET_HAS_GEMINI_BOOTANIMATION` | `true` |
| `TARGET_BOOT_ANIMATION_RES`       | `720` |
| `TARGET_SUPPORT_LIVE_WALLPAPER`   | `false` |
| `GMS_VOICE_MODEL_INCLUDED`        | `false` |

### 📝 Description of Flags

| Flag | Description |
|------|-------------|
| `TARGET_SUPPORT_MINIMAL_GAPPS`    | Set to `true` to include **Minimal GMS package** in the ROM build. Ideal for users who want basic Google services without the full bloat of standard GApps. |
| `TARGET_SUPPORT_PIXEL_LAUNCHER` | Set to `true` to include the **Pixel Launcher** in the ROM build. This provides the Google Pixel home screen experience with features such as **At-a-Glance, Google Discover integration, and the Pixel-style app drawer**. **Default is `false`**, which means the ROM will use the **Launcher3QuickStep** instead. |
| `TARGET_HAS_GEMINI_BOOTANIMATION` | Enables the new Gemini Google bootanimation. Add this in the device tree to use it. **Default is White Google bootanimation**. |
| `TARGET_BOOT_ANIMATION_RES` | Use this if your device has a 720p screen. Helps set appropriate boot animation resolution. **Default is White Google bootanimation**. |
| `TARGET_SUPPORT_LIVE_WALLPAPER` | Set to `false` to **exclude** Pixel 3XL live wallpapers from the build. reducing OTA zip size by ~167MB. |
| `GMS_VOICE_MODEL_INCLUDED` | Set to `false` to **exclude** prebuilt voice models, reducing OTA zip size by ~100MB. |

---

## 💬 Need Help?

If you run into issues or have questions, feel free to open an issue on the [GitHub repo](https://github.com/AndroidOne-Experience/manifest/issues) or join the community chat (if available).

Happy Building! 🔧📱
