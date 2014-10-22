## RTL8812AU

This is the driver supplied by Realtek, version 4.3.8_12175.20140902 with a small patch to make it build on Raspberry Pi as well.

For building on Raspberry Pi, you must install a Debian-style kernel.

```bash
sudo apt-get install linux-image-rpi-rpfv linux-headers-rpi-rpfv linux-source-3.12
```

You must enable the kernel in /boot/config.txt. If you don't do this, it will boot the kernel supplied by the The Raspberry Pi Foundation (the one that's provided by rpi-update). This kernel is provided without the source and the headers, hence it's easier to switch to a kernel provided by Raspbian. Append these lines at the end of the file:

```
kernel=vmlinuz-3.12-1-rpi
initramfs initrd.img-3.12-1-rpi followkernel
```

If the kernel version changes, you need to update /boot/config.txt. The `linux-source` meta-package points to linux-source-3.2, therefore you need to manually specify the latest version.

Now you can take the steps for getting this driver:

 * Reboot your Raspberry Pi
 * Clone this repository
 * Edit the Makefile in order to pick the Raspberry Pi target
 * Change CONFIG_PLATFORM_I386_PC to n
 * Change CONFIG_PLATFORM_ARM_RPI to y
 * Save the Makefile
 * Type `make`, grab a cup of coffee; the build is going to take a while
 * Install the module with `sudo make install`
 * Load the module with `modprobe 8812au`

PS: Please do not ask me to patch various stuff in this driver. I am not smart enough to maintain this.
