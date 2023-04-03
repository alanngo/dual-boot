<img src="./assets/linux/ubuntu-logo.png" width='25' align='right'>
<img src="./assets/windows/windows-logo.png" width='25' align='left'>


<div align="center">

# Dual Booting Windows 10 & Ubuntu 22.04 in 2023

</div>

## Growing Pains & Resolutions

### [Slow Wifi](#slowifi)
### [Audio not Working](#noaudio)
### [Wrong Time in Windows](#wrongtime)
### [Uninstalling Nvidia Drivers](#nvidiadrivers)



<div id='slowwifi'>

## 🐢 Slow Wifi in Ubuntu 
**Cause:** Ubuntu may set network configurations to power-saving mode, thus throttling wifi

1. Test by going to https://www.speedtest.net/
2. Open Terminal
3. Run the following command
```bash
$ sudo vim /etc/NetworkManager/conf.d/default-wifi-powersave-on.conf
```
4. Set the value of ``wifi.powersave`` to 2.

<img src="./assets/linux/wifi.png">

5. Reboot into Ubuntu
6. Run the speed test again https://www.speedtest.net/

### wifi.powersave values
- 0: Use default settings
- 1: ignore
- 2: DISABLE power saving **(YOU WANT THIS SETTING)**
- 3: ENABLE power saving

source: https://www.youtube.com/watch?v=N_e82SuiAYc&list=LL&index=1

</div>

<div id="noaudio">

## 🔇 Ubuntu Audio Not Working 
**Cause:** ``pulseaudio`` has not properly started

1. Open Terminal
2. Run the following commands

```bash
$ sudo pulseaudio --kill
$ sudo pulseaudio --start
```
3. Test: https://www.youtube.com/watch?v=eZ2PtEx9-ls


<div id="wrongtime">

## 🕰️ Wrong Time in Windows
**Cause:** Windows and Linux store their times differently in UEFI firmware, causing clock desynchronization
1. Boot into Ubuntu
2. Open Terminal
3. Run the following commands

```bash
$ sudo timedatectl set-local-rtc 1 --adjust-system-clock
```
4. Reboot into Windows
5. Go to ``Start``  > ``Settings``  > ``Time & language`` > ``Date & time``.
6. Set your timezone if necesarry
7. Disable and renable ``Set time automatically`` in one step
<img src="./assets/windows/datetime.png">
8. Reboot system to Windows

source: https://www.youtube.com/watch?v=A70s-C-yWTQ&list=LL&index=4

</div>

<div id="nvidiadrivers">

## 🖥️ Uninstalling Nvidia Drivers

**Cause:** You might be installing an Nvidia driver, but after rebooting, you get greeted by a black screen of death

1. Boot your system in recovery mode by selecting ``Advanced options for Ubuntu``

<img src="./assets/linux/grub.png">

2. Select the first option that lists ``(recovery mode)``

<img src="./assets/linux/recoverymode.png">

3. Select ``resume``

<img src="./assets/linux/resume.webp">

4. Once you arrive to your desktop, open your terminal and use these commands.

```bash
$ dpkg -l | grep -i nvidia 
$ sudo apt-get remove --purge '^nvidia-.*' 
$ sudo apt-get install ubuntu-desktop 
$ echo 'nouveau' | sudo tee -a /etc/modules
```

5. Reboot your system

source: https://askubuntu.com/questions/206283/how-can-i-uninstall-a-nvidia-driver-completely

</div>