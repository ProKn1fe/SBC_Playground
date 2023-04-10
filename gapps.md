### How to install GAPPS

### Requpments:
- [Magisk](https://github.com/topjohnwu/Magisk)
- [MagiskHideProps](https://github.com/Magisk-Modules-Repo/MagiskHidePropsConf)
- [GAPPS](https://sourceforge.net/projects/magiskgapps/files/) ([difference between versions](https://github.com/wacko1805/MagiskGapps#apps))
- [Termux](https://github.com/termux/termux-app)

I recommend this GAPPS version - [MagiskGApps-a.12L.BASIC.10.16.2022.zip](https://sourceforge.net/projects/magiskgapps/files/android-12L-ALPHA/17.10.2022/MagiskGApps-a.12L.BASIC.10.16.2022.zip/download)

### Steps:
1. Install magisk and termux.
2. Go to magisk and install root (install -> direct install).
3. Reboot.
4. Go to magisk settings and enable `zygisk` and `enforce deny list`. (without it you will get bootloop)
5. Go to magisk -> modules and install `magiskhideprops` zip.
6. Reboot.
7. Now we need to spoof device model, go to termux and write. I use google pixel 6 pro as example, you can choose any device that you want:
   1. su (use root)
   2. props (launch props config)
   3. 1 (spoof device)
   4. f (select device)
   5. 7 (choose vendor)
   6. 29 (choose device)
   7. y (yes)
   8. y (yes)
8. Reboot.
9. Go to magisk -> modules install and install `gapps` zip.
10. Reboot.
11. Enjoy your google services!
