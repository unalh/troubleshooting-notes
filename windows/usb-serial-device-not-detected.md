# USB Serial Device Not Detected

## Problem
After flashing a microcontroller or connecting a USB serial adapter, Windows does not detect the device and no COM port appears. The board powers on but no serial device is listed.

## Symptoms
- No new COM port in Device Manager.
- Device appears under "USB devices" but not under "Ports".
- Tools (Arduino IDE, flashing software) cannot connect.

## Investigation
Steps taken:
- Tested with different cables and USB ports.
- Checked Device Manager for any unknown devices.
- Verified that the board's bootloader was intact by double-tapping the reset button to enter bootloader mode.
- Looked for new entries under "Universal Serial Bus controllers".

Sometimes the device enumerates as a composite or HID device; drivers may be missing.

## Solution
1. Ensure the USB cable supports data transfer (not charge-only).
2. Enter bootloader mode (if applicable) by pressing reset twice; the device should appear as a different USB device.
3. Install the correct USB-to-Serial driver (e.g., CH340, CP210x) if the board uses one.
4. Use `zadig` or manufacturer tools to replace generic "USB Serial" driver with WinUSB if required.
5. Restart the computer after driver installation.

After installing the CP210x driver and using a new cable, Windows recognized the board and assigned a COM port.

## What I Learned
Many connection issues are due to power-only cables or missing drivers. Always test with a known good cable and install device-specific drivers.
