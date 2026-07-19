<div align="center">

<img src="assets/logo.jpg" alt="Picters kernel" width="640">

# Picters Kernel · Xiaomi SM8850

**A custom Android 16 kernel for the Xiaomi Mi 17 (sm8850 "Pudding")** — built for people who like plugging weird things into their phone. 📡🔌

`6.12.23-android16` &nbsp;•&nbsp; ReSukiSU (KernelSU) &nbsp;•&nbsp; SUSFS &nbsp;•&nbsp; out-of-tree USB Wi-Fi

</div>

---

## ✨ Why this one?

It's not just a stock kernel with a fresh coat of paint. It's built around **external USB Wi-Fi** — the stuff that normally *just doesn't work* on a phone:

- 📶 **External adapters actually work.** Realtek RTL8812AU / 8812BU / 8814AU / 8188EUS dongles run out of the box — for **packet injection & monitor mode**, *and* as a plain managed station right inside stock Xiaomi Settings.
- 🧩 **Piles of drivers baked in** — Realtek Wi-Fi (aircrack-ng + morrownr), CAN bus, DVB-T / RTL-SDR, USB-serial and friends. Nothing to compile by hand.
- 🛡️ **Root that stays out of the way** — ReSukiSU (KernelSU) with SUSFS.
- 📱 **A real companion app ships with it** — *Picters Modules Manager* — one tap to flip Wi-Fi between **Stock** and **Inject**, hand an adapter back to Android, and keep everything updated.

<div align="center">
<img src="assets/manager.jpg" width="43%" alt="Picters Modules Manager with two adapters loaded">
&nbsp;&nbsp;
<img src="assets/iwdev.jpg" width="43%" alt="Two adapters in monitor mode via iw dev">
<br>
<sub><b>Left:</b> the manager app, two dongles loaded &nbsp;·&nbsp; <b>Right:</b> both in monitor mode, running this kernel</sub>
</div>

---

## 🚀 Getting it running

1. Grab the latest build from **[Releases](../../releases)** — you get two zips:
   - `Mi17_Kernel-…zip` — the kernel (AnyKernel3).
   - `…OOT-Modules…zip` — the drivers **+ the manager app**.
2. Flash them in **KernelSU / Magisk** (or let the manager app do it), then reboot.
3. Open **Picters Modules Manager**, switch Wi-Fi to **Inject**, plug in your adapter — done. 🎉

> 💡 The app can update the kernel, the modules and itself in one tap, with an **A/B slot picker** — so you rarely open a recovery again.

---

## 🔧 Under the hood

| | |
|---|---|
| **Base** | Android 16 GKI · Linux **6.12.23** · Xiaomi **sm8850** |
| **Root** | ReSukiSU (KernelSU) + SUSFS |
| **Wi-Fi injection** | `88XXau` (RTL8812AU), `88x2bu` (RTL8812BU), `8814au`, `8188eus` — patched to behave on 6.12 (no UBSAN panics, clean cfg80211 hand-off) |
| **Also aboard** | CAN, DVB-T / RTL-SDR, USB-serial (CP210x / CH341 / FTDI / PL2303) … |
| **Built in** | CI — every release stamped with a version the app can track |

---

## 🙏 Credits

Standing on the shoulders of giants:
**ReSukiSU / KernelSU** · **SUSFS** · [**aircrack-ng**](https://github.com/aircrack-ng/rtl8812au) · [**morrownr**](https://github.com/morrownr) · **AnyKernel3** (osm0sis) · [**YuzakiKokuban**](https://github.com/YuzakiKokuban) for the build tooling.

<div align="center"><sub>Made with too many USB adapters and not nearly enough sleep. 🥲</sub></div>
