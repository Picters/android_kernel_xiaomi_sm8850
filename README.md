# Xiaomi 17 Series — NetHunter Kernel (ReSukiSU)

A custom kernel for the **Xiaomi 17 Series** (`sm8850`, codename *pudding*), forked from
the Kokuban kernel and bringing a **Kali NetHunter–grade** feature set to Android 16 /
GKI 2.0 (Linux 6.12) — while staying **KMI-safe**, so it boots on the stock vendor image
with no bootloop and no broken hardware.

> Maintained by **Picters**. This is a fork. The goal: a daily-drivable kernel that is
> **as close as possible to a real NetHunter kernel** on modern, locked-KMI hardware.

## Branches

| Branch | Kernel | Use |
| :-- | :-- | :-- |
| **`main`** | **Stock** — clean baseline kernel, no NetHunter modifications | Everyday use / reference |
| **`resukisu`** | **NetHunter** — the full pentest feature set below, ReSukiSU root | Kali NetHunter |

`main` is kept as the untouched stock reference. **All NetHunter work lives on the
`resukisu` branch** — that is the branch to build/flash for pentesting.

## What the NetHunter (`resukisu`) kernel adds

**Wi-Fi injection / monitor-mode adapters** (out-of-tree + in-tree drivers):
- **Realtek** — RTL8812AU, RTL8188EUS, RTL8814AU, **RTL8812BU / RTL8822BU** (88x2bu),
  RTL8187, RTL8192CU, RTL8XXXU
- **Atheros** — ath9k_htc (AR9271), carl9170, ath6kl / ath6kl_usb
- **Ralink / MediaTek** — rt2800usb (RT33xx/35xx/3573/53xx/55xx), mt7601u
- **ZyDAS** — zd1211rw

**Bluetooth** adapters — btusb (BCM/RTL/Intel), bfusb, hci_uart, BlueZ (rfcomm / bnep / hidp)
**USB gadget / HID** — BadUSB & HID keyboard injection (USB Arsenal), NCM/ECM/EEM ethernet gadget
**SDR & DVB** — RTL-SDR (RTL2832U) with R820T / E4000 / FC001x tuners (rtl_433, GQRX, …)
**CAN bus** — can-utils + USB CAN adapters (Kvaser, PEAK, GS_USB, ESD, EMS, 8devices)
**USB serial** — CH341, CP210x, FTDI, PL2303 (Proxmark, hardware hacking)
**Storage / loot** — NTFS3, NFS (client + server)
**Root** — **ReSukiSU** (KernelSU fork) + **SuSFS**

Every injection / adapter driver is compiled against this kernel and shipped as a
**systemless KernelSU/Magisk module** — see *Install*.

## Install

1. **Flash the kernel** — flash `Mi17_Kernel-…-ReSuki-…-susfs-….zip` from the latest
   release with your KernelSU / ReSukiSU / SukiSU / Magisk manager
   (*Flash AnyKernel3 zip*), then reboot.
2. **Install the drivers** — install the matching **`…-OOT-Modules-….zip`** from the same
   release via your manager (*Modules → Install from storage*) and reboot. This delivers
   the injection / BT / CAN / SDR / NTFS drivers to `/system/lib/modules`.

## Wi-Fi injection — Picters Manager

On this SoC the internal Wi-Fi (Qualcomm `qca_cld3`) and the external injection adapters
are built against **different `cfg80211`** modules and can't run at the same time — this
is normal for NetHunter on GKI, so you toggle between them.

The **OOT-Modules** package ships **Picters Manager** — a WebUI you open from your root
manager (the module's *Open/Action* button):

- **Switch to Injection Mode** — *instant.* Unloads the vendor Wi-Fi stack and loads the
  kernel `cfg80211` + adapter drivers. Internal Wi-Fi turns **off**; plug your USB adapter
  and `iw dev` shows `wlanN`.
- **Disable injection** — **requires a reboot.** The Qualcomm Wi-Fi firmware runs on the
  WCN co-processor and is only (re)initialised at boot, so a live module reload can't bring
  internal Wi-Fi back cleanly. Reboot to return to normal internal Wi-Fi.

CLI equivalent: `su -c 'sh /sdcard/nh-inject.sh 88XXau'` (or `8188eu` / `8814au` / `88x2bu`).

## Notes

- KMI-safe: `module_layout` matches the stock baseline, so stock vendor modules keep
  loading — the device boots normally with camera, flashlight, internal Wi-Fi and mobile
  data all working.
- Do **not** modify `/vendor`; the injection toggle is entirely runtime and reversible.

## Credits

Base kernel: **Kokuban / YuzakiKokuban** · Root: **ReSukiSU / KernelSU** · SuSFS: **simonpunk** ·
Injection drivers: **aircrack-ng**, **morrownr** · NetHunter: **Kali / OffSec**.
