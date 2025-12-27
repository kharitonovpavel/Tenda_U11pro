# AIC8800D80 Fedora 43 Linux Driver
This driver is for the AIC8800D80 chipset, supported by devices such as the Tenda U11 and AX913B.

Added support for devices with Vendor ID 368B (tested).

Tested on Linux kernel 6.17.4-300  with Fedora 43.

Bluetooth not working.

### Disclaimer
I did not develop this software, The code is sourced from the Tenda U11 driver. 
I only made some modifications to the code to adapt it to newer kernel versions. 
Apart from compilation issues, I am unable to address other problems.
This repository was created for myself and in order to share a working driver not for Ubuntu, but for Fedora.

### Attention
Before installing the driver, delete all aic8800-related folders under /lib/firmware. 
Using an incorrect firmware version may cause the system to freeze.

### Installation Steps
Run install_setup.sh

#### Navigate to the driver directory:

Change to the drivers/aic8800 directory:

```bash
cd ./drivers/aic8800
```

#### Compile and Install the Driver:

First, compile the driver:

```bash
make -j4
```
Then, install the driver:

```bash
sudo make install
```

For any kernel updates, you'll need to reinstall the driver:

```bash
make clean
make
sudo make install
```

### Load the Driver
After installation, load the driver with the following command:

```bash
sudo modprobe aic8800_fdrv
```

### Verify the Module is Active
Check if the module is loaded correctly:

```bash
lsmod | grep aic
```
You should see output similar to:

```bash
aic8800_fdrv    536576  0
cfg80211        1146880 1   aic8800_fdrv
aic_load_fw     69632   1   aic8800_fdrv
usbcore         348160  10  xhci_hcd,ehci_pci,usbhid,usb_storage,ehci_hcd,xhci_pci,uas,aic_load_fw,uhci_hcd,aic8800_fdrv
```

After that, plug in your USB wireless network card.

### Verify Wi-Fi Device is Active
To check if the Wi-Fi interface is recognized, run:

```bash
nmcli
```
If the device is still not active, check the kernel logs for any errors related to the driver:

```bash
sudo dmesg
```
