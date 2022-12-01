# raspberry_pi400_quectel

1. Download AOSP
```
repo init -u https://android.googlesource.com/platform/manifest -b android-13.0.0_r15 --depth=1
```

2. Download mark00lui Raspberry PI 400 + Telephony + Quectel device
```
git clone https://github.com/mark00lui/raspberry_pi400_quectel .repo/local_manifests -b arpi-13
```

3. Download sourcecode
```
repo sync --no-tags
```

4. Ubuntu 22 environment
```
sudo apt-get install git-core gnupg flex bison build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 libncurses5 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z1-dev libgl1-mesa-dev libxml2-utils xsltproc unzip fontconfig
```

5.1 Integrate Quectel Ril
```
https://github.com/mark00lui/raspberry_pi400_quectel/wiki/RIL-for-Quectel
```

5.2. Build AOSP
```
source build/envsetup.sh
lunch rpi400-eng
make ramdisk systemimage vendorimage
```

6. Download arpi kernel source code
```
git clone https://github.com/mark00lui/kernel_arpi.git
```

7. Build kernel
```
build/build.sh
```

8. mkimg
```

```
