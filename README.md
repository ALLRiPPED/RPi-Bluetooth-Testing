# RPi-Bluetooth-Testing
Experimental Bluetooth support for Windows 10 running on the Raspberry Pi.

## Installation guide
These steps can be done both on the Raspberry Pi or on another PC.
If you're on the Raspberry Pi, assign a letter to the Boot partition in Disk Management.

1. You'll need the following files from this repository:
    * `SerPL011_48MHz.zip`
    * the `RPI_EFI.fd` file inside the `RPi3` or `RPi4` folder (depending on your Pi model)

2. After that, download the latest Bluetooth driver from: https://github.com/worproject/cywbtserialbus/releases (under Assets).

3. Replace the `RPI_EFI.fd` file on the boot partition of your installation with the previously downloaded one.

4. Uninstall SerPL011 (ARM PL011 UART Device Driver), extract the `SerPL011_48MHz.zip` archive and install the new driver.

5. Extract the cywbtserialbus driver and install it.

6. Reboot the board.

## Notes
The PL011 UART driver doesn't support hardware flow control at the moment (WIP), so the Bluetooth driver has a default baud rate of `460800` bps to accommodate for the slowness of Pi 3 (because at higher baud rate and high CPU usage the RX FIFO overruns, we lose packets, the driver will hit an assertion and finally crash the system).

On a Pi 4, we've been able to reliably go as high as `921600 bps` with BT networking and audio playback at the same time.

The baud rate can be changed using `regedit`. 
More details here: https://github.com/worproject/cywbtserialbus#driver-configuration
