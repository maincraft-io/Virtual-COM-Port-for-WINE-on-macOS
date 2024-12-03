
# Virtual-COM-Port-for-WINE-on-macOS
Guide to configuring a Virtual COM Port using socat (linked with CP2104) on macOS and utilizing it within WINE for development and testing purposes. Compatible with Apple Silicon.

This example is based on CP2104 from Silicon Labs running on macOS 15.1 (Apple Silicon M4 Max).

## Instructions

1. Install the Silicon Labs driver:
   Download it from [Silicon Labs USB to UART Bridge VCP Drivers](https://www.silabs.com/developer-tools/usb-to-uart-bridge-vcp-drivers?tab=downloads)  
   Alternatively, use the file located in `attachments/SiLabsUSBDriverDisk.dmg`.

2. Execute the following command to list available devices:
   ```bash
   ls /dev/cu.*
   ```
   Example output:
   ```
   /dev/cu.Bluetooth-Incoming-Port /dev/cu.SLAB_USBtoUART /dev/cu.debug-console /dev/cu.usbserial-025XXX1F
   ```

3. Copy the path to the device labeled `SLAB_USBtoUART`.

4. Create a virtual COM port using the path from Step 3 by executing the following `socat` command:
   ```bash
   socat -d -d \
   PTY,link=/tmp/virtualport,raw,echo=0,wait-slave,cfmakeraw,ispeed=19200,ospeed=19200,cs8,clocal \
   FILE:/dev/cu.SLAB_USBtoUART,raw,echo=0,cfmakeraw,ispeed=19200,ospeed=19200,cs8,clocal
   ```
   > Note: The `baudrate` in this example is set to `19200`. You can adjust it as per your requirements.

5. Do not close the terminal. Open another terminal window.

6. Ensure you have the latest version of `wine` or `wine@devel` installed.  
   > Instructions for installing Wine are not provided here.

7. Create a physical link for the virtual port to Wine by executing:
   ```bash
   ln -s /tmp/virtualport ~/.wine/dosdevices/com5
   ```
   > Note: The port is named `com5` to be used within WINE.

8. Launch the Wine Registry Editor by executing:
   ```bash
   wine regedit
   ```

9. In the Registry Editor, navigate to:
   ```
   HKEY_LOCAL_MACHINE/Software/Wine/Ports
   ```

10. Create a new String Value in this section:
    - Name: `com5`
    - Value: `/tmp/virtualport`

11. Exit the Registry Editor, launch your Wine application, select `COM5`, and start using it!
