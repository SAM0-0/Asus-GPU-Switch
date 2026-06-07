# ASUS GPU Mode Switcher

One-click GPU mode switching for ASUS laptops. No bloatware, no background processes.

## The Problem

Switching GPU modes with Armoury Crate is a chore:

1. Open Armoury Crate (slow, heavy app)
2. Wait for it to load
3. Click on Device
4. Click on GPU Performance
5. Click Standard or Eco

That's 5 clicks and ~10 seconds every time.

## The Solution

Two `.exe` files on your taskbar. Click once, done.

- **GPU-Standard.exe** — enables dGPU (hybrid/Optimus mode)
- **GPU-Eco.exe** — disables dGPU (iGPU only, saves battery)

## How to Verify It Works

1. Open **Task Manager** → **Performance** tab
2. You'll see your NVIDIA GPU listed
3. Click **GPU-Eco.exe** → the NVIDIA GPU disappears from Task Manager
4. Click **GPU-Standard.exe** → it reappears

That's it. The GPU is physically powered on/off.

## How It Works

Uses the same ATKACPI driver interface that Armoury Crate uses internally — `DeviceIoControl` calls to `\\.\ATKACPI`. Nothing custom, nothing hacky. Just the direct hardware API without the bloat.

## Note About Armoury Crate

Armoury Crate tracks GPU mode in its own registry and won't sync with this tool. That's fine — Armoury Crate will show whatever state it was in before. The actual hardware state is what matters, and this tool controls that directly.

If you want Armoury Crate to reflect the change, restart the Armoury Crate service after switching. But there's no real need — the GPU state is correct regardless of what the app shows.

## Requirements

- ASUS laptop (ROG, TUF, Zephyrus, etc.)
- Windows 10/11
- ATKACPI driver installed (comes with Armoury Crate or ASUS System Control Interface)

## Compatibility

Uses ACPI device ID `0x00090020`. Tested on:

- ROG Strix / Zephyrus / Flow
- TUF Gaming series
- Most ASUS gaming laptops (2020+)

Some VivoBook/ZenBook models may use a different device ID and won't work.

## Usage

1. Download `GPU-Standard.exe` and `GPU-Eco.exe`
2. Pin both to your taskbar
3. Click to switch — no admin prompt, no background process, instant

## Credits

ACPI protocol reverse-engineered from [G-Helper](https://github.com/seerge/g-helper) and the [Linux asus-wmi kernel driver](https://github.com/torvalds/linux/blob/master/drivers/platform/x86/asus-wmi.c).

## License

MIT
