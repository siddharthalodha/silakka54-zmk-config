# Silakka54 Wireless ZMK Config

ZMK firmware configuration for the Silakka54 wireless split keyboard (Lily58 compatible) with SuperMini nRF52840.

## Building Firmware

### Via GitHub Actions (recommended)

1. Fork this repository to your own GitHub account
2. Optionally modify `config/lily58.keymap` to your preferences
3. Push your changes to GitHub
4. Go to the **Actions** tab in your repository
5. Download the `firmware.zip` artifact from the latest build

### Building Locally

See the [ZMK documentation](https://zmk.dev/docs/development/setup) for local setup instructions.

## Flashing Firmware

### Requirements

- USB-C cable
- The firmware `.uf2` files (left and right)
- Optional: `zmk_clear.uf2` for resetting pairing

### Steps per half

1. **Connect** the keyboard half (left or right) via USB-C to your computer

2. **Enter bootloader mode** by double-tapping the small reset button on the underside of the board (near the nice!nano/SuperMini)

3. The board will appear as a USB storage device named `NICENANO`

4. **Copy the correct `.uf2` file** to the `NICENANO` drive:
   - `lily58_left-nice_nano_v2-zmk.uf2` for the **left** half
   - `lily58_right-nice_nano_v2-zmk.uf2` for the **right** half

5. The board will automatically restart after copying

6. **Repeat** for the other half

## Resetting Pairing

If you have connection issues between the left and right halves:

1. **Turn off both halves**

2. **For each half** (start with right):
   - Connect via USB-C
   - Double-tap reset button (bootloader mode)
   - Copy `zmk_clear.uf2` to `NICENANO`
   - Wait for restart
   - Double-tap reset button again
   - Copy the correct firmware `.uf2`
   - Repeat for the other half

3. **Turn on both halves** and simultaneously press the reset button on both halves to pair them

4. Connect via Bluetooth to the **left** half (master)

## ZMK Studio

This firmware has ZMK Studio enabled. This allows you to modify your keymap without reflashing:

1. Open [ZMK Studio](https://zmk.studio) in Chrome/Edge
2. Connect your keyboard via USB
3. Modify your keymap - changes are saved immediately

## Modifying the Keymap

The keymap is located in `config/lily58.keymap`. After making changes:

1. Commit and push to GitHub
2. Wait for the GitHub Action to complete
3. Download and flash the new firmware

## Bluetooth Profiles

The firmware supports 5 Bluetooth profiles (BT1-BT5). Switch profiles via the Lower layer:

- `BT_CLR` - Clear current profile
- `BT_SEL 0-4` - Select profile 1-5

## Files

```
silakka54-zmk-config/
├── config/
│   ├── lily58.keymap    # Keymap configuration
│   ├── lily58.conf      # Firmware settings
│   └── west.yml         # ZMK dependencies
├── build.yaml           # Build matrix
└── .github/
    └── workflows/
        └── build.yml    # GitHub Actions workflow
```

## Links

- [ZMK Firmware](https://zmk.dev/)
- [ZMK Studio](https://zmk.studio)
- [Lily58 Keyboard](https://github.com/kata0510/Lily58)
