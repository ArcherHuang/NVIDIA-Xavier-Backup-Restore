# NVIDIA® Jetson AGX Xavier™ Backup & Restore

## Contents
- [Prerequisites](#prerequisites)
- [NVIDIA Xavier - front view ( left ) & rear view ( right )](#nvidia-xavier---front-view--left---rear-view--right-)
- [Physical Connection](#physical-connection)
- [Ubuntu HOST PC Setup Process - Install NVIDIA SDK Manager](#ubuntu-host-pc-setup-process---install-nvidia-sdk-manager)
- [Backup the image of Jetson AGX Xavier](#backup-the-image-of-jetson-agx-xavier)
- [Restore Custom Image to NVIDIA Jetson AGX Xavier](#restore-custom-image-to-nvidia-jetson-agx-xavier)
- [License](#license)
- [Reference](#reference)

## Prerequisites
* Make sure you have all of the following prerequisites：
  * Hardware
    * Host pc with [Ubuntu 18.04 LTS Desktop](https://releases.ubuntu.com/18.04/) ( Internet Connection ) - 1 pc
    * [NVIDIA® Jetson AGX Xavier™](https://developer.nvidia.com/embedded/jetson-agx-xavier-developer-kit) - 1 pc
    * AC Adapter for NVIDIA® Jetson AGX Xavier™ - 1 pc
    * USB Type-C to Type-A Cable for NVIDIA® Jetson AGX Xavier™ & PC - 1 pc
    * HDMI Monitor for NVIDIA® Jetson AGX Xavier™ & PC - 2 pcs
    * HDMI Cable for NVIDIA® Jetson AGX Xavier™ & PC - 2 pcs
    * USB keyboard & mouse for NVIDIA® Jetson AGX Xavier™ & PC - 2 pcs
  * Software
    ```
    ├── sdkmanager_1.8.4-10431_amd64.deb
    ├── system.img
    └── ubuntu-18.04.6-desktop-amd64.iso
    ```

|           Device           | Ubuntu 18.04 LTS | AC Adapter | USB Type-C to Type-A Cable | HDMI Monitor | HDMI Cable | USB keyboard & mouse |
|:--------------------------:|:----------------:|:----------:|:--------------------------:|:------------:|:----------:|:--------------------:|
|           Host PC          |         ●        |            |              ●             |       ●      |      ●     |           ●          |
| NVIDIA® Jetson AGX Xavier™ |                  |      ●     |              ●             |       ●      |      ●     |           ●          |

## NVIDIA Xavier - front view ( left ) & rear view ( right )
![](./Images/NVIDIA-Xavier.png)

## Physical Connection
* Use the `USB Type-A` cable to connect the `Ubuntu HOST PC` to the `front USB Type-C` connector on the `NVIDIA® Jetson AGX Xavier™`.

![](./Images/NVIDIA-Xavier-Connect-PC.png)

## Ubuntu HOST PC Setup Process - Install NVIDIA SDK Manager
【 Step 1 】 Change the working directory in the HOST terminal to the `sdkmanager_1.8.4-10431_amd64.deb` file

【 Step 2 】 Copy `sdkmanager_1.8.4-10431_amd64.deb` to `~`
* Enter the following command in the HOST terminal.
```
cp sdkmanager_1.8.4-10431_amd64.deb ~
```

【 Step 3 】 Install NVIDIA SDK Manager
* Enter the following command in the HOST terminal.
```
cd ~
sudo apt update
sudo apt install -y ./sdkmanager_1.8.4-10431_amd64.deb
```

【 Step 4 】 Open NVIDIA SDK Manager
* Enter the following command in the HOST terminal.
```
sdkmanager
```

【 Step 5 】Install Jetson OS
* Click `LOGIN` Button
![](./Images/sdkmanager-1.png)
![](./Images/sdkmanager-2.png)

* Input `Email Address`
![](./Images/sdkmanager-3.png)

* Input `Password` or Click `More Login Options`
![](./Images/sdkmanager-4.png)

* Click `Log in with Google` ( Authenticate Using Google )
![](./Images/sdkmanager-5.png)

* Input `Google Account` ( Authenticate Using Google )
![](./Images/sdkmanager-6.png)

* Input `Authenticator Code` ( Authenticate Using Google )
![](./Images/sdkmanager-7.png)

* Login Success
![](./Images/sdkmanager-8.png)

* Click `No, disable usage collection`
![](./Images/sdkmanager-9.png)

* Click `OK`
![](./Images/sdkmanager-10.png)

* Select Items
  * `PRODUCT CATEGORY` field
    * Select `Jetson`
  * `HARDWARE CONFIGURATION` field 
    * Select `Target Hardware Jetson AGX XAVIER modules`
  * `TARGET OPERATING SYSTEM` field
    * Select `Linux JetPack 4.6.1`
  * When the input is complete, please click `CONTINUE` button.
![](./Images/sdkmanager-11.png)

* In progress
  * Choose only `Jetson OS`
![](./Images/sdkmanager-12.png)
![](./Images/sdkmanager-13.png)

* Click `Create`
![](./Images/sdkmanager-14.png)

* Input `sudo password`
![](./Images/sdkmanager-15.png)

* Click `OK`
![](./Images/sdkmanager-16.png)

* In progress
![](./Images/sdkmanager-17.png)
![](./Images/sdkmanager-18.png)

* Click `Skip`
![](./Images/sdkmanager-19.png)

* Finish
  * Click `FINISH AND EXIT`
![](./Images/sdkmanager-20.png)

## Backup the image of Jetson AGX Xavier
【 Step 1 】 Connect Ubuntu PC to NVIDIA Jetson AGX Xavier
* Ref [Physical Connection](#physical-connection)

【 Step 2 】 Change NVIDIA® Jetson AGX Xavier™ Mode
* Press and Hold the `Power Button` and `Force Recovery Button`, now Wait for `5 second` and Release the `Power Button` and `Force Recovery Button`.

![](./Images/NVIDIA-Xavier-Bottom-View.png)

【 Step 3 】 Check Connect Status
* Enter the following command in the HOST terminal. If connected, you'll see the device name listed as a `NVidia Corp.`
```
lsusb
```

![](./Images/lsusb.png)

【 Step 4 】 Changing to another directory
* Enter the following command in the HOST terminal.
```
cd ~/nvidia/nvidia_sdk/JetPack_4.6.1_Linux_JETSON_AGX_XAVIER_TARGETS/Linux_for_Tegra
```

【 Step 5 】 Create Custom Image
* Enter the following command in the HOST terminal. If command executed successfully, you'll see the `backup.img` and `backup.img.raw` in `~/nvidia/nvidia_sdk/JetPack_4.6.1_Linux_JETSON_AGX_XAVIER_TARGETS/Linux_for_Tegra`
```
sudo ./flash.sh -r -k APP -G backup.img jetson-xavier mmcblk0p1
```

【 Step 6 】 System backup succeeded
* Rename `backup.img` to `system.img` in `~/nvidia/nvidia_sdk/JetPack_4.6.1_Linux_JETSON_AGX_XAVIER_TARGETS/Linux_for_Tegra`.

## Restore Custom Image to NVIDIA Jetson AGX Xavier
【 Step 1 】Copy `system.img` to `~/nvidia/nvidia_sdk/JetPack_4.6.1_Linux_JETSON_AGX_XAVIER_TARGETS/Linux_for_Tegra/bootloader`

【 Step 2 】Connect Ubuntu PC to NVIDIA Jetson AGX Xavier
* Ref [Physical Connection](#physical-connection)

【 Step 3 】Change NVIDIA® Jetson AGX Xavier™ Mode
* Press and Hold the `Power Button` and `Force Recovery Button`, now Wait for `5 second` and Release the `Power Button` and `Force Recovery Button`.

![](./Images/NVIDIA-Xavier-Bottom-View.png)

【 Step 4 】Check Connect Status
* Enter the following command in the HOST terminal. If connected, you'll see the device name listed as a `NVidia Corp.`
```
lsusb
```

![](./Images/lsusb.png)

【 Step 5 】Changing to another directory
* Enter the following command in the HOST terminal.
```
cd ~/nvidia/nvidia_sdk/JetPack_4.6.1_Linux_JETSON_AGX_XAVIER_TARGETS/Linux_for_Tegra
```

【 Step 6 】Restore custom image
* Enter the following command in the HOST terminal.
```
sudo ./flash.sh -r jetson-xavier mmcblk0p1
```

【 Step 7 】System restore succeeded
* Please reboot your NVIDIA® Jetson AGX Xavier™.

## License
This sample is licensed under the [MIT](./LICENSE) license.

## Reference
* https://developer.nvidia.com/nvidia-sdk-manager
* https://developer.nvidia.com/embedded/jetpack-sdk-46#collapseAllJetson
* https://releases.ubuntu.com/18.04/