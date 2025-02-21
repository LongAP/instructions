# LongAP One Ubuntu 24.04.1 Server Installation Guide

## Warning

**Important:** You will lose access to the security key as the required drivers are not available on the latest Linux kernel.

## Requirements
You will need:
 - A USB drive
 - A USB to RS232 cable 

## Step 1: Prepare the USB Drive

1. Download the Ubuntu 24.04.1 server ISO from the official Ubuntu website.
2. Burn the ISO to a USB drive using a tool like Rufus (Windows) or Etcher (Mac/Linux).

## Step 2: Connect Hardware

1. Connect the serial cable, network cable, and USB drive to the device.
2. Ensure the power is unplugged before connecting the hardware.

## Step 3: Open Serial Console

### On Linux

1. Open a terminal on your PC.
2. Run the following command to open the Serial console:
   ```bash
   screen /dev/ttyUSB0 115200
   ```
3. If using Ubuntu, disable "Enable the menu accelerator key" in the terminal app settings to send F10 to the device.

### On Windows

1. Download and install PuTTY from the official website.
2. Open PuTTY and select "Serial" as the connection type.
3. Set the serial line to `COMx` (replace `x` with the appropriate COM port number).
4. Set the speed to `115200`.
5. Click "Open" to start the serial console.

### On Mac

1. Open a terminal on your Mac.
2. Run the following command to list the available serial devices:
   ```bash
   ls /dev/tty.*
   ```
3. Identify the correct serial device (e.g., `/dev/tty.usbserial-xxxx`).
4. Run the following command to open the Serial console:
   ```bash
   screen /dev/tty.usbserial-xxxx 115200
   ```

## Step 4: Boot from USB Drive

1. Plug in the power to the device.
2. Press F10 to open the boot menu.
3. Select the USB drive to boot from.

## Step 5: Edit Boot Command

1. Press `e` to edit the boot command.
2. Add `console=ttyS0,115200n8` just before the `---` on the line that begins with `linux`. Ensure there's a space before `---`.
3. Press `Ctrl+X` to execute the edited boot command.

## Step 6: Install Ubuntu

1. Wait for the Ubuntu OS to boot and display the serial installer.
2. Follow the installer instructions. If connected to the internet, you may be asked to update the installer.
3. Navigate the screens using `Tab` (cycle options) and `Enter` (select). Select "Done" when prompted.

## Step 7: Configure Storage

1. When prompted for storage configuration, select "Use an entire disk".
2. Ensure the "SATA_SSD" is selected.

## Step 8: Enable OpenSSH Server

1. Enable the OpenSSH server during the installation.
2. Optionally, allow password authentication or import your SSH key(s) from GitHub.

## Step 9: Complete Installation

1. Wait for the installation to complete. This may take a while, and you won't see a progress indicator.
2. When you see "Installation complete" in the top-left corner, remove the USB drive.
3. Select "Reboot now" or unplug the power cable to reboot the device.

## Step 10: First Boot

1. After rebooting (this may take 1-2 minutes), you will see a login prompt or can connect via SSH.

## Step 11: Increase Logical Volume Size

1. Run the following commands to increase the logical volume size:
   ```bash
   sudo lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv
   sudo resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv
   ```

You have successfully installed Ubuntu 24.04.1 server on your device!



