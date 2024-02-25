# Key-B firmware

This keyboard is based on [ZMK](https://zmk.dev/) and the [Adafruit nRF2 bootloader](https://github.com/adafruit/Adafruit_nRF52_Bootloader)

## ZMK 

This firmware works with the custom board defined at [Key-B hardware](https://github.com/SaidAlvarado/leftboard-hardware).
And this repository works with the [ZMK github-action template](https://github.com/zmkfirmware/unified-zmk-config-template). So it compiles on the cloud on a github-actions workflow.

### Folder Structure
The `highlighted files` are the modified ones, the rest are the same as the template.

```
.github/
└── workflows/
    └── build.yml  
boards/
├── shields
└── arm/
    └── `keyb/`
        ├── `Kconfig`
        ├── `Kconfig.board`
        ├── `Kconfig.defconfig`
        ├── `board.cmake`
        ├── `keyb.dts`
        ├── `keyb.yaml`
        ├── `keyb.zmk.yml`
        ├── `keyb_defconfig`
        └── zmk.code-workspace
config/
├── `keyb.keymap` (keymap file)
└── west.yml
zephyr/
└── module.yml
`build.yaml`
```

- `keyb/`: Kconfig and DTS files defining the custom board, modified from the [nice!nano board definition](https://github.com/zmkfirmware/zmk/tree/main/app/boards/arm/nice_nano)
- `keyb.keymap`: Keymap file for the keyboard.
- `build.yaml`: Edited to build the `keyb` board.

We are not using a shield with a standard board, so we leave the `shields` folder empty.

### UF2

Pushing code to this repository will trigger a github-actions workflow that will compile ZMK with the configuratin defined in the repo.
You can find the resulting [UF2](https://github.com/adafruit/Adafruit_nRF52_Bootloader#adafruit-nrf52-bootloader) binary [here](https://github.com/SaidAlvarado/leftboard-firmware/actions), in the corresponding workflow tab. 

## Adafruit nRF Bootloader

### Using the Bootloader
Official instructions, here: [Adafruit nRF2 bootloader](https://github.com/adafruit/Adafruit_nRF52_Bootloader)

- BootLoader Mode:
  - Double click reset button
  - ESC + Reset

### Building the Bootloader
I have a fork of the original Adafruit Bootloader [here](https://github.com/SaidAlvarado/Adafruit_nRF52_Bootloader). It is already configured with the information of the Key-B board.

it also has a [fix](https://github.com/adafruit/Adafruit_nRF52_Bootloader/pull/321) for working with gcc version 13

Clone, and Init the repo

```
git clone https://github.com/SaidAlvarado/Adafruit_nRF52_Bootloader
cd Adafruit_nRF52_Bootloader
git submodule update --init
git fetch --tags
```
Build the Key-B board
```
make BOARD=key_b all
```

### Flash the Bootloader
Once the project is built you can find a `uf2` binary in:
```
Adafruit_nRF52_Bootloader/_build/build-key_b/update-key_b_bootloader-0.8.3_nosd.uf2
```

This can be thrown in the `UF2` upgrade folder like any other firmware and it should work.

