# ZOROZORO Experiments

This repository contains the experimental code for the ZOROZORO project, which controls 256 toio cubes simultaneously.

![toio260_1126](https://user-images.githubusercontent.com/27694/143378054-eb7cffa7-544f-4d6e-9711-e092c7f7c5f6.gif)

https://twitter.com/Saqoosha/status/1333233470143774720

## Architecture
The system works as the following steps:
1. Scanner and Bridges connects to Controller.
2. Scanner finds unconnected cube.
3. Scanner tells it to the Controller.
4. Controller finds Bridge which has capacity to connect to the cubes.
5. Controller sends cube address to Bridge to connect it.
6. After the connection is established, Controller can send commands to cubes.
![image](https://user-images.githubusercontent.com/27694/143379123-c8bad323-9bec-4a0f-b77d-f4c1f9a01e32.png)

| Module          | Role                                                                                              | Source code                                                                    |
| --------------- | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| Cube Controller | Collects information from the Scanner and Bridge and sends out appropriate commands to each cube. | [`14-cubecontroller`](14-cubecontroller)                                       |
| Bridge          | Make a BLE connection with toio cubes and relay with Controller through TCP socket.               | [`13-unitycontroller2/PlatformIO/bridge/`](13-unitycontroller2/PlatformIO/bridge/)   |
| Scanner         | Detects a cube emitting an advertising signal and tells the contoller.                            | [`13-unitycontroller2/PlatformIO/scanner/`](13-unitycontroller2/PlatformIO/scanner/) |

## Installation Instruction
### Upgrade Bootloader thourgh CLI
Go to [Adafruit_nRF52_Bootloader Github](https://github.com/adafruit/Adafruit_nRF52_Bootloader/releases/tag/0.6.3) and download the latest bootloader

<b>On Linux</b>, install _adafruit-nrfutil_
```
$ pip3 install --user adafruit-nrfutil
```
<b>On mac</b>, if you have pip3 installed, you can use the aforementioned command. Otherwise, you can download the source file [here](https://github.com/adafruit/Adafruit_nRF52_nrfutil/releases/tag/0.5.3.post17)

Plug in nRF52840 board through usb cable. You should able to see the drive on your desktop.

type
```
ls /dev/cu.*
```

You should able to find your board with name (something similar to _/dev/cu.usbmodem411_). This is your board name.

Navigate to the folder where you download adafruit-nrfutil-macos and run adafruit-nrfutil

```
./adafruit-nrfutil-macos --verbose dfu serial --package feather_nrf52840_express_bootloader-0.2.9_s140_6.1.1.zip -p [board name] -b 115200 --singlebank --touch 1200
```

Lastly, check the INFO_UF2.TXT file inside your board drive, the version should change from 0.2.x to 0.6.1 or newer.


## Hardware

- [Adafruit Feather nRF52840 Express](https://www.adafruit.com/product/4062)
- [Adafruit Ethernet FeatherWing](https://www.adafruit.com/product/3201)
- Ethernet Hub
- 5V/10A AC Adapter
- [Custom power distribution board](10-powerpcb/)

![IMG_5856](https://user-images.githubusercontent.com/27694/143379298-fea5e6da-6c5a-4b97-9892-152cacb88424.jpeg)

Credit: Saqoosha & Whatever Inc