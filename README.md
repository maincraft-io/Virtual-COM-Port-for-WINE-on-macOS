# Virtual-COM-Port-for-WINE-on-macOS
Guide to configuring a Virtual COM Port using socat (linked with CP2104) on macOS and utilizing it within WINE for development and testing purposes. Compatible with Apple Silicon.

This example is based on CP2104 from Silicon Labs running on macOS 15.1 (Apple Silicon M4 Max).

## Prerequisites
Download the necessary driver from the following link:  
[Silicon Labs USB to UART Bridge VCP Drivers](https://www.silabs.com/developer-tools/usb-to-uart-bridge-vcp-drivers?tab=downloads)  
Alternatively, use the file located in `attachments/SiLabsUSBDriverDisk.dmg`.