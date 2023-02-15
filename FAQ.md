### FAQ

Question: Is WPA3 supported?

Answer: WPA3-SAE is supported. It works well on most modern Linux distros but
not all. Generally the reason for WPA3 not working on Linux distros is that the
distro has an old version of wpa_supplicant or Network Manager. Your options
are to upgrade to a more modern distro (distros released after mid 2022) or
compile and install new versions of wpa_supplicant and/or Network Manager.

-----

Question: I bought two usb wifi adapters based on this chipset and am planning
to use both in the same computer. How do I set that up?

Answer: Realtek drivers do not support more than one adapter with the
same chipset in the same computer. You can have multiple Realtek based
adapters in the same computer as long as the adapters are based on
different chipsets.

-----

Question: Why do you recommend Mediatek based adapters when you maintain
this repo for a Realtek driver?

Answer: Many new and existing Linux users already have adapters based on
Realtek chipsets. This repo is for Linux users to support their existing
adapters but my STRONG recommendation is for Linux users to seek out USB
WiFi solutions based on Mediatek chipsets:

https://github.com/morrownr/USB-WiFi

-----

Question: Will you put volunteers to work?

Answer: Yes. Post a message in `Issues` or `Discussions` if interested.

-----

Question: I am having problems with my adapter and I use Virtualbox?

Answer: This [article](https://null-byte.wonderhowto.com/forum/wifi-hacking-attach-usb-wireless-adapter-with-virtual-box-0324433/) may help.

-----

Secure Boot Information

Question: The driver installation script completed successfully and the
driver is installed but does not seem to be working. What is wrong?

Answer: This question often comes up after installing the driver to a
system that has Secure Boot on. To test if there is a Secure Boot related
problem, turn secure boot off in the system BIOS and reboot.  If the driver
works as expected after reboot, them the problem is likely related to
Secure Boot.

What will increase my chances of having a sucessessful installation on a
system that has Secure Boot on?

First and foremost, make sure Secure Boot is on when you initially install
your Linux distro. If your Linux distro was installed with Secure Boot off,
the easiest solution is likely to do a clean reinstallation with Secure Boot
on.

Ubuntu is used as the example but other distros should be similar to one
degree or another. During the installation there will be a box on one of
installation pages that will appear if the installation program detects
that Secure Boot is on. You will need to check the box and supply a
password. You can use the same password and you use for the system if you
wish. After the installation and reboot completes, the first screen you
should see is the mokutil screen. Mokutil will guide you through the 
process of setting up your system to support Secure Boot

The `install-driver.sh` script currently supports Secure Boot if `dkms`
is installed. Here is a link to the `dkms` website. There is information
regarding Secure Boot in two sections in the `README`.

https://github.com/dell/dkms

Here is a link regarding Debian and Secure Boot:

https://wiki.debian.org/SecureBoot

There is work underway to add Secure Boot suuport for systems that do not
have `dkms` available or if a manual installation is desired.

-----

Question: Can you provide additional information about monitor mode?

Answer: I have a repo that is setup to help with monitor mode:

https://github.com/morrownr/Monitor_Mode

Work to improve monitor mode is ongoing with this driver. Your reports of
success or failure are needed. If you have yet to buy an adapter to use with
monitor mode, there are adapters available that are known to work very well
with monitor mode. My recommendation for those looking to buy an adapter for
monitor mode is to buy adapters based on the following chipsets: mt7921au,
mt7612u, mt7610u, rtl8821cu, rtl8812bu, rtl8812au, and rtl8811au. My specific
recommendations for adapters in order of preference currently are:

ALFA AWUS036ACHM - long range - in-kernel driver

ALFA AWUS036ACM - in-kernel driver

ALFA AWUS036ACU - in-kernel driver (as of kernel 6.2) and [out-of-kernel driver](https://github.com/morrownr/8821cu)

ALFA AWUS036ACH - long range - [driver](https://github.com/morrownr/8812au)

ALFA AWUS036ACS - [driver](https://github.com/morrownr/8821au)

To ask questions, go to [USB-WiFi](https://github.com/morrownr/USB-WiFi)
and post in `Discussions` or `Issues`.

-----

Question: I have an adapter with the 8821cu chipset and it supports
bluetooth. The bluetooth works but the wifi does not. What is wrong?

Answer: There appears to be an issue where adapters can be set up differently
by makers. The fix is to set the driver option ( `rtw_RFE_type` ) in 8821cu.conf.
The easiest way to edit 8821cu.conf is to run the following from the driver
directory:

```
sudo ./edit-options.sh
```

Once in the document, you can scroll down to the documentation about
`rtw_RFE_type`. You will likely have to experiment to find out what setting
works best for your adapter but a good place to start is probably...

```
rtw_RFE_type=7
```

Simply add that option to the end of the `options` line, save and reboot.

-----

Question: How do I disable the onboard WiFi in a Raspberry Pi?

Note: This answer is for the Raspberry Pi OS.

Answer:

Add the following line to `/boot/config.txt`

```
dtoverlay=disable-wifi
```

-----

Question: How do I forget a saved WiFi network on a Raspberry Pi?

Note: This answer is for the Raspberry Pi OS without Network Manager active.

Step 1: Edit `wpa_supplicant.conf`

```
sudo ${EDITOR} /etc/wpa_supplicant/wpa_supplicant.conf
```

Note: Replace ${EDITOR} with the name of the text editor you wish to use.

#### Step 2: Delete the relevant WiFi network block (including the '`network=`' and opening/closing braces).

#### Step 3: Save the file.

#### Step 4: Reboot

-----