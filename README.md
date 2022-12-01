# raspberry_pi400_quectel

1.1. Download AOSP
```
repo init -u https://android.googlesource.com/platform/manifest -b android-13.0.0_r15 --depth=1
```

1.2. Download mark00lui Raspberry PI 400 + Telephony + Quectel device
```
git clone https://github.com/mark00lui/raspberry_pi400_quectel .repo/local_manifests -b arpi-13
```

1.3. Download sourcecode
```
repo sync --no-tags
```

1.4. Ubuntu 22 environment
```
sudo apt-get install git-core gnupg flex bison build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 libncurses5 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z1-dev libgl1-mesa-dev libxml2-utils xsltproc unzip fontconfig
```

1.5 Integrate Quectel Ril
```
https://github.com/mark00lui/raspberry_pi400_quectel/wiki/RIL-for-Quectel
```

1.6 Build AOSP
```
source build/envsetup.sh
lunch rpi400-eng
make ramdisk systemimage vendorimage
```

2.1 Download arpi kernel source code
```
git clone https://github.com/mark00lui/kernel_arpi.git
```

2.2 Build kernel
```
build/build.sh
```

3.1 download mkimg
```
wget https://raw.githubusercontent.com/mark00lui/raspberry_pi400_quectel/arpi-13/mkimg.sh -O mkimg.sh
```

3.2 modify img path
```
# what file name prefix you want
LINEAGEVERSION=rpi13
DATE=`date +%Y%m%d`
IMGNAME=$LINEAGEVERSION-$DATE-rpi4.img

# img size
IMGSIZE=8

# you must modify the path
# i place mkimg.sh at the root , rpi = AOSP , rpi_kernel = kernel
DEVICE="rpi/device/arpi/rpi4"
OUTDIR="rpi/out/target/product/rpi4"
KDIR="rpi_kernel/out/arpi-5.15/dist"

# boot = 128M
# system = 2048M
# vendor = 256M
	echo "Creating partitions..."
	(
	echo o
	echo n
	echo p
	echo 1
	echo
	echo +128M
	echo n
	echo p
	echo 2
	echo
	echo +2048M
	echo n
	echo p
	echo 3
	echo
	echo +256M
	echo n
	echo p
	echo
	echo
	echo t
	echo 1
	echo c
	echo a
	echo 1
	echo w
	) | fdisk $IMGNAME

```

3.3 build img
```
sudo ./mkimg.sh
```

Todo to set raw ip automatically
```
ip link set dev wwan0 down
echo Y > /sys/class/net/wwan0/qmi/raw_ip
ip link set dev wwan0 up
```
