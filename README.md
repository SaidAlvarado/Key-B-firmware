# Key-B firmware

This keyboard is based on [ZMK](https://zmk.dev/) and the [Adafruit nRF2 bootloader](https://github.com/adafruit/Adafruit_nRF52_Bootloader)

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
git clone https://github.com/adafruit/Adafruit_nRF52_Bootloader
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