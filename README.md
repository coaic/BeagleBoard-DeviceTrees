# Syncing Source

### Syncing script directory

https://git.kernel.org/pub/scm/linux/kernel/git/devicetree/devicetree-rebasing.git/tree/scripts

```
scripts/
```

### Syncing include directory

https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/tree/include/dt-bindings

```
include/
```

### Device Trees, sync with mainline and patch on top

https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/tree/arch (and local pull requests)

```
src/
```

### Local pull request:

local pull requests

```
tools/
```

# Building

```
make
```

# Installing on am335x and am57xx:

```
sudo make install_arm
```

# Installing on BBAI-64

```
sudo make install_arm64
```

# LLM Current Context

Context summary (confirmed working state):

Hardware:
- Board: BeagleBone Black + BeagleWire
- Flash: Macronix MX25L3273E (32 Mbit / 4 MiB)
- Flash SPI bus shared with iCE40 FPGA

Electrical:
- FPGA CRESET on P9_25 (GPIO3_21) must be held LOW to tri-state SPI bus
- SPI pins:
  - SCK  = P9_31 (GPIO3_14)
  - MISO = P9_29 (GPIO3_15)
  - MOSI = P9_30 (GPIO3_16)
  - CS#  = P9_28 (GPIO3_17)

Software (known-good):
- Kernel: 6.16.12-bone26
- SPI master: spi-gpio
- spidev bound via driver_override at boot
- Stable speed: 500 kHz
- Verified full read + verify with flashrom

Working command:
flashrom -p linux_spi:dev=/dev/spidev2.0,spispeed=500 -c MX25L3233F/MX25L3273E