# HTCShiftX9500Lubuntu
Install notes for Lubuntu 18.10 on HTC Shift X9500

##Steps

1. Download [Lubunu 18.10](https://lunbuntu.me) and create an installable boot image using something Like [Unetbootin](https://unetbootin.github.io) or [Etcher](https://www.balena.io/etcher/).

2. Ensure you have a USB Hub as you will that can accommodate the USB Boot Disk and Micro Wifi USB (The default Marvell Adaptor will not be recognised).

3. Start the Shift and Press F10 on startup to get to the boot menu and choose the USB Boot

4. Choose to start Lubuntu

5. Once Lubuntu has started, connect to a Wifi network (assuming that your micro USB Wifi card is recognised - Lubuntu is pretty good at recognising modern day cards. I used one that was lying around that I had used for my Raspberry Pi)

6. Once Wifi is setup then choose to install Lubuntu.

7. When navigating the installer screen you will not be able to click the 'Next' button to get to the next screen of the installer because it is not visible. Press Alt and left mouse click and then move the screen up so you can see the buttons and proceed.

8. The installer will take some time to complete and don't panic ig it seems to get stuck on the regional settings. It seems to download all of the regional settings as part of the install so can take some time.

9. Once done remove the USB stick and reboot and login to Lubuntu. Your wifi should be detected and should connect.

10. Click the windows button to launch the start menu and type in 'qterminal' to launch the terminal.

11. Update the packages:

```
sudo apt-get update
sudo apt-get upgrade
```

12. The default Lubuntu store has never worked well for me so it is better to install the Snap store IMO opinion. To do that:

```
sudo snap install snapd
sudo snap install snap-store
```

13. Next lets sort out the Shift Touchpad / mouse issues. Moving around with the right hand touchpad causes the virtual desktops to switch constantly. To fix this:

```
cd ~/.config/openbox
cp lubuntu-rc.xml lubuntu-rc.xml.bak
leafpad lubuntu-rc.xml
```

Delete the following lines:

```
<mousebind button="UP" action="click">
 <action name="DesktopPrevious" />
<mousebind button="Down" action="click">
 <action name="DesktopNext" />
```
  
  Log out and log back in again

Now if you wish to switch between desktops use Cntrl-Alt-Left and Cntrl- Alt-Right

14. Now lets enable double tap for the right hand touchpad to make life easier. Drop out to QTerminal in Lubuntu and enter:

```
sudo leafpad /etc/X11/xorg.conf.d/30-touchpad.conf
```

enter the following content:

```
Section "InputClass"
  Identifier "touchpad"
  Driver "libinput"
  MatchisTouchpad "on"
  Option "Tapping" "on"
EndSection
```
