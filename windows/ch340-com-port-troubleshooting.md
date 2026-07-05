# CH340 COM Port Troubleshooting

## Problem
A device using a CH340 USB-to-Serial chip (such as a 3D printer or Arduino clone) is not recognized on Windows. The COM port does not appear in Device Manager.

## Symptoms
- Device Manager shows an unknown USB device or no new COM port.
- The application cannot connect to the device.
- Installing drivers appears to have no effect.

## Investigation
I checked:
- USB cable and port (tried different cables and ports).
- Device Manager under "Ports (COM & LPT)" and "Other devices".
- Whether CH340 drivers were installed by running the installer and verifying `C:\Windows\System32\Drivers\wchusbserial.sys`.

If the device showed as "USB-SERIAL CH340" with a yellow exclamation mark, I manually updated the driver.

## Solution
1. Download the latest CH340 drivers from the manufacturer or trusted source.
2. Run the installer to add the driver to Windows.
3. If the device appears under "Other devices" in Device Manager, right-click and choose "Update driver" -> "Browse my computer" -> select the CH340 driver folder.
4. Unplug and re-plug the device.
5. Check Device Manager; the device should now appear as "USB-SERIAL CH340" with an assigned COM port number.

On my system, after manually installing the driver, the COM port `COM7` appeared and the device worked.

## What I Learned
Cheap USB-to-Serial adapters often require separate drivers. Manually installing or updating the correct driver resolves most connection issues.
