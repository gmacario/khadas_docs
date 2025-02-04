title: 编译安卓
---
### 准备
- [x] [搭建开发环境](http://source.android.com/source/initializing.html)
- [x] [下载安卓源码](/zh-cn/edge/DownloadAndroidSourceCode.html)
- [x] [安装Rockchip平台工具链](/zh-cn/edge/InstallToolchains.html)

### 编译
*注意：在开始编译前，确保已经搭建好如上`准备`所述的环境。*

**编译 U-boot：**
```sh
$ cd PATH_YOUR_PROJECT
$ cd uboot
$ make kedge_defconfig
$ make ARCHV=aarch64
```
**编译 kernel：**
```sh
$ cd PATH_YOUR_PROJECT
$ cd kernel
$ make ARCH=arm64 kedge_defconfig -jN
$ make ARCH=arm64 rk3399-khadas-edge-android.img -jN
```
**编译 android：**
```sh
$ cd PATH_YOUR_PROJECT
$ source build/envsetup.sh
$ lunch rk3399_all-userdebug
$ make -jN
$ ./mkimage.sh
```
*注意：替换`N`为你自己电脑实际的线程数。*

**执行`./mkimage.sh`后，在 rockdev/Image-xxx/目录生成完整的固件包(xxx 是具体 lunch的产品名)**
```
rockdev/Image-xxx/
├── boot.img
├── kernel.img
├── misc.img
├── parameter.txt
├── recovery.img
├── resource.img
├── RK3399MiniLoaderAll.bin
├── system.img
├── trust.img
└── uboot.img
```
**打包 update.img：**
```sh
$ cd PATH_YOUR_PROJECT
$ source build/envsetup.sh
$ lunch rk3399_all-userdebug
$ ./pack_image.sh
```

### 参考
* [通过USB数据线升级](/zh-cn/edge/UpgradeViaUSBCable.html)
* [通过TF卡升级](/zh-cn/edge/UpgradeViaTFBurningCard.html)
