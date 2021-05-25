# Cardano stake pool guide
tips, gotchas and other learnings

## Hardware
* 2 x raspberry pi 4 model b, 8GB RAM: https://www.canakit.com/raspberry-pi-4-starter-kit.html
* 2 x samsung 970 evo SSD M.2 NVMe, minimum 250GB: https://www.amazon.com/Samsung-970-EVO-250GB-MZ-V7E250BW/dp/B07BN5FJZQ
* 2 x icy box SSD enclosure: https://www.amazon.com/Icy-Box-External-Type-C-Enclosure/dp/B07Z4BKTQG/ref=sr_1_3?crid=2Y0W4MG08XD27&dchild=1&keywords=icy+box+ssd+enclosure&qid=1621606795&sprefix=icy+box+ssd+enc%2Celectronics%2C201&sr=8-3
* 2 x powered usb hub: https://www.amazon.com/Sabrent-4-Port-Individual-Switches-HB-UM43/dp/B00JX1ZS5O
* any monitor that can connect with the raspberry 🥮 (micro HDMI): https://projects.raspberrypi.org/en/projects/raspberry-pi-setting-up/1

## Raspberry Pie 🥮 setup (AcceptanceCriteria = bootloading Ubuntu from the USB storage rather than the microSD card slot $ because faster | cheaper | [better](https://www.zdnet.com/article/booting-my-raspberry-pi-4-from-a-usb-device/))
- headless setup on both pies 🥮
  - https://www.tomshardware.com/reviews/raspberry-pi-headless-setup-how-to,6028.html
  - https://www.raspberrypi.org/software/
  - https://www.raspberrypi.org/documentation/configuration/wireless/headless.md
- install Ubuntu on SSD flash drive
  - https://ubuntu.com/blog/how-to-install-ubuntu-with-the-new-raspberry-pi-imager
  - https://www.raspberrypi.org/software/
- boot load from USB (SSD $ flash drive (Samsung 970 M.2)) instead from the microSD slot
  - https://jamesachambers.com/raspberry-pi-4-ubuntu-20-04-usb-mass-storage-boot-guide/ (hardware recommended from this article)
  - https://www.tomshardware.com/how-to/boot-raspberry-pi-4-usb
  - https://linuxhint.com/how_to_boot_raspberry_pi_4_from_usb_ssd/#:~:text=From%20the%20Raspberry%20Pi%20OS,re%20done%2C%20click%20on%20Start. 


## Build and configure the cardano node
* resource followed: https://www.coincashew.com/coins/overview-ada/guide-how-to-build-a-haskell-stakepool-node
* the following tools do not come packaged with ubuntu so you need to install them via apt: git, llvm, libnuma-dev, make, libtool, jq, net-tools, fail2ban
* during the libsodium build step
  * run the configure bash script with the following argument: ./configure --disable-dependency-tracking
* correctly set the LD_LIBRARY_PATH, the guide has it set incorrectly: export LD_LIBRARY_PATH=$(llvm-config --libdir):$LD_LIBRARY_PATH

## Harden Ubuntu on both raspberry pies 🥮
* follow most of the guide
* add the swap file step if necessary: https://cardano-node-installation.stakepool247.eu/adding-swap-virtual-memory
