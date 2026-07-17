# Xiaomi 17 Series — Picters Kernel

A custom kernel for the **Xiaomi 17 Series** (`sm8850`, codename *pudding*), forked from the
Kokuban kernel for Android 16 / GKI 2.0 (Linux 6.12). It adds a set of extra out-of-tree modules
(Wi-Fi injection & monitor-mode adapters, Bluetooth, USB gadget/HID, SDR/DVB, CAN, USB serial,
NTFS/NFS) while staying **KMI-safe** — it boots on the stock vendor image with camera, mobile
data and internal Wi-Fi all working. Root is **ReSukiSU** + **SuSFS**.

## Branches

| Branch | Kernel |
| :-- | :-- |
| **`main`** | Stock — clean baseline, no extra modules |
| **`resukisu`** | The full extra-modules feature set + ReSukiSU root |

Build/flash **`resukisu`**.

## Install

1. **Flash the kernel** — flash `Mi17_Kernel-…-ReSuki-…-susfs-….zip` from the latest release with
   your KernelSU/Magisk manager (*Flash AnyKernel3 zip*), then reboot.
2. **Install the drivers** — install the matching `…-OOT-Modules-….zip` (**Modules pack**) from the
   same release (*Modules → Install from storage*) and reboot. Non-Wi-Fi drivers load at boot.

## Wi-Fi: Stock ↔ Inject

Internal Wi-Fi (Qualcomm `qca_cld3`) and the external injection adapters use different `cfg80211`
builds and can't run together, so you switch between them from the **Picters Modules Manager** app
(shipped in the Modules pack, opened from its Action button):

- **Inject** — instant. Unloads the vendor Wi-Fi stack, loads the kernel `cfg80211` + adapter
  drivers. Internal Wi-Fi turns off; plug a USB adapter and `iw dev` shows `wlanN`.
- **Stock** — requires a reboot (the Qualcomm Wi-Fi firmware only initialises at boot).

## Credits

Base kernel: **Kokuban / YuzakiKokuban** · Root: **ReSukiSU / KernelSU** · SuSFS: **simonpunk** ·
Injection drivers: **aircrack-ng**, **morrownr**.
