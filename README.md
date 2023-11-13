# Custom Rom Build #
This is the Custom Rom build guide for Redmi Note 11 (spes/spesn)

```bash

#Requirements
1. A cloud server
2. Minimum 8-core & 16 GB RAM
3. 500 GB+ storage
4. Device: Redmi Note 11
5. Codename: spes/spesn
6. Stable internet connection
7. OS Ubuntu 20.04 LTS or latest

```

## Build Environment ##

Installing required packages

OS: Ubuntu 18.04 and higher

Version: 64-bit

```bash

sudo apt-get install git-core gnupg flex bison build-essential zip curl zlib1g-dev libc6-dev-i386 libncurses5 x11proto-core-dev libx11-dev lib32z1-dev libgl1-mesa-dev libxml2-utils xsltproc unzip fontconfig

```
<br>

<b>Setting Up Build Environment</b>

```bash

sudo su

```


```bash

add-apt-repository ppa:openjdk-r/ppa && apt-get update && sudo apt-get install git-core gnupg flex bison build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 libncurses5 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z1-dev libgl1-mesa-dev libxml2-utils xsltproc unzip fontconfig && exit

```
<br>

<b>Cloning Akhil Narang Scripts</b>

```bash

mkdir ~/bin && PATH=~/bin:$PATH && cd ~/bin && curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo && chmod a+x ~/bin/repo && git clone https://github.com/akhilnarang/scripts.git scripts && cd scripts && bash setup/android_build_env.sh && cd

```
Directly Copy Paste this 👆 command


## Device Tree ##

```bash
#Device tree contains

1. device_xiaomi_spes
2. kernel_xiaomi_spes
2. vendor_xiaomi_spes

spes is my device codename
It varies phone to phone

```

i will use
device tree / vendor tree from jabiyeff21 and dblenk9

Mi680 kernel from AkiraNoSushi and muralivijay9845

<b>Pre merged Device/Vendor/Kernel Tree</b>

```bash
mkdir rom_name
```

```bash
cd rom_name
```
<br>
 
Here,


<b>-b stands for branch

13 stands for branch name and

device/xiaomi/spes for targeted path

</b>

```bash

git clone https://github.com/ProjectBlaze-Devices/device_xiaomi_spes.git -b 13 device/xiaomi/spes

```

```bash

git clone https://github.com/LineageOS/android_hardware_xiaomi.git -b lineage-20 hardware/xiaomi

```


<b>Now navigate to this path</b> 👇

```bash

cd device/xiaomi/spes

```

```bash

ls

```

<br>


## Bring Up ##

Now, you must have to modify these <b>2</b> files on device tree named

<b>1. AndroidProducts.mk
2. blaze_spes.mk</b>

Each rom use different/same code names likes

<b>Pixel Experience use: aosp

LMODroid use: lmodroid

PixelOS use: aosp

Project Elixir use: aosp</b>

it's available either on their <b>GitHub</b> manifest pages or in <b>Telegram</b> group

<br> <br>

Suppose, i am building <b>LMODroid</b> right now

So, my code name is <b>lmodroid</b>

It could be <b>something else</b> according to your Selected rom

now, open <b>AndroidProducts.mk</b> using <b>nano</b> command

```bash

nano AndroidProducts.mk

```

Where you can see <b>blaze</b>, change it to <b>lmodroid</b>


Now, to save the <b>AndroidProducts.mk</b> press

<b>"ctrl+o"

"enter"

"ctrl+x"</b>

After pressing ctrl+x it will revert back to your current path.


Now, it's time to <b>rename & modify</b> the second file named <b>blaze_spes.mk</b>

For this particular rom, my <b>codename is lmodroid</b>

<b>Now, type this to rename</b>

```bash

mv blaze_spes.mk lmodroid_spes.mk

```

<b>Type</b>

```bash

ls

```

<b>To open "lmodroid_spes.mk", press</b>

```bash

nano lmodroid_spes.mk

```


Change these <b>2</b> things:

1. Inherit some common LineageOS stuff.
$(call inherit-product, vendor/<b>blaze</b>/config/common_full_phone.mk)

2. Product Specifics
PRODUCT_NAME := <b>blaze</b>_spes



It could be something <b>else</b> according to your device tree


<b>Change 1: replace "blaze" with lmodroid

Change 2: replace blaze_spes to lmodroid_spes</b>

I mean, in this two subsection <b>replace the word "blaze" with "lmodroid"</b>

Now, do the same procedure to save and exit as you did to save the <b>AndroidProducts.mk</b>


## Locate Rom Path ##

Now manually type ( cd .. ) to go on your rom directory, or paste this command below 👇

```bash

cd .. && cd .. && cd .. && ls

```

<b>or this</b>

```bash

cd .. && cd .. && cd ..

```

```bash

ls

```


That's it. Now, follow next step to start build the rom.

<br> <br>


## Final Step to Build Rom ##

The <b>clang</b> will be started to clone in your device After paste this command 👇

```bash

. build/envsetup.sh

```


## Gapps & Vanilla ##

If you want <b>gapps</b> build paste this;

If you want <b>vanilla</b> build <b>skip</b> this step & directly paste one of these <b>lunch</b> commands

```bash

exportWITH_GAPPS=true

```

## Lunch Commands ##


```bash

lunch lmodroid_spes-user

```

```bash

lunch lmodroid_spes-userdebug

```

```bash

lunch lmodroid_spes-eng

```

<b> Note: </b>



## Start compilation ##

```bash

m bacon -jX

```

If it's not working for you then you can try these commands below 👇

```bash

make bacon

```

```bash

mka bacon -jX

```

***Here if you paste your cpu core number instead of X then you it wil use all of the cores of your server to compile the rom. I have a 16-core cpu so, the command will be like 👇


```bash

mka bacon -j16

```


This <b>Custom Rom</b> build guide is written by Tanvir Hasan
