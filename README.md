# Fix UB500 driver problem (Bluetooth 5 devices) on Linux

### Forked from [rogovskyyy/linux-ub500](https://github.com/rogovskyyy/linux-ub500)

## Before you start - make sure you're missing UB500 driver.
```bash
lsusb; dmesg | egrep -i 'blue|firm'
```

If it says something like
```bash
[    6.019483] Bluetooth: hci0: RTL: loading rtl_bt/rtl8761b_fw.bin
[    6.019814] bluetooth hci0: Direct firmware load for rtl_bt/rtl8761b_fw.bin failed with error -2
[    6.019818] Bluetooth: hci0: RTL: firmware file rtl_bt/rtl8761b_fw.bin not found
```
Or something like this:
```bash
[  205.159544] Bluetooth: hci0: RTL: loading rtl_bt/rtl8761bu_fw.bin
[  205.159561] bluetooth hci0: Direct firmware load for rtl_bt/rtl8761bu_fw.bin failed with error -2
[  205.159563] Bluetooth: hci0: RTL: firmware file rtl_bt/rtl8761bu_fw.bin not found
```

Simply put 
```bash
rtl8761b_fw.bin
rtl8761b_config.bin
rtl8761bu_fw.bin
rtl8761bu_config.bin
```
into
```bash
/lib/firmware/rtl_bt
```
and replug the bluetooth module.
(If after replug doesn't work, try restarting the pc)
Voilà

## Tested on `TP-Link UB500` & `Ubuntu 20.04.5 LTS` with `5.15.0-52-generic` Linux Kernel

## Useful link
https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/commit/?id=7118987b2f7aff733573121607bc9640a4880296
