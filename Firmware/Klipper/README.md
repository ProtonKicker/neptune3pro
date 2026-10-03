# Neptune 3 Pro Klipper firmware (ZNP Robin Nano DW v2.2)

Prebuilt MCU firmware in this folder. For Pro/Plus/Max with the **v2.2** board
(STM32F401) only — not the base Neptune 3 (v2.1). Built from upstream Klipper
master `461c4e3`: 32KiB bootloader, 8 MHz crystal, `USART1 PA10/PA9`, 250000 baud.
See `BUILD_INFO.txt` for details.

## First flash (stock Marlin → Klipper)

1. Format an SD card as **MBR + FAT32** (printer ignores ExFAT).
2. Copy `ZNP_ROBIN_NANO.bin` to the SD root.
3. Printer OFF → insert SD → power ON. The screen shows `UPGRADE FIRMWARE`
   with a **stuck progress bar — that's normal**. Wait ~2 min.
4. Power OFF → remove SD. Success = file renamed to `ZNP_ROBIN_NANO.CUR`
   when you check the SD on a computer.
5. **Unplug the stock touchscreen** (Klipper can't use it; it fights the host
   serial port). Power ON.
6. Connect USB to your Klipper host (`klipperformac serial --auto`, then `up`)
   and use Fluidd/Mainsail with a Neptune 3 Pro `printer.cfg`.

## Later updates

Don't pull the SD — leave a FAT32 card in the printer and run:

```sh
./scripts/flash-sdcard.sh /dev/cu.usbserial-XXXX znp-robin-nano-dw-v2.2
```

## Files

- `ZNP_ROBIN_NANO.bin` — flash this (renamed `klipper.bin`)
- `klipper.bin` — identical raw build output
- `firmware.config.txt` / `firmware.defconfig.txt` — exact build config
- `BUILD_INFO.txt` — version, toolchain, rebuild notes
