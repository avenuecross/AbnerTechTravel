本篇文章转载自一个外文网站。

平时使用Linux系统常使用发行版，如果想要运行源码或者自己定制的系统需要自己去编译内核。

## How to compile and install Linux Kernel
The procedure to build (compile) and install the latest Linux kernel from source is as follows:
1. Grab the latest kernel from kernel.org
2. Untar the kernel tarball
3. Copy existing Linux kernel config file
4. Compile and build Linux kernel
5. Install Linux kernel and modules (drivers)
6. Update Grub configuration
7. Reboot the system

### Step 1. Get the latest Linux kernel source code
Visit the official project site and download the latest source code. Click on the big yellow button that read as “Latest Stable Kernel“

### Step 2. Extract tar.xz file
```markdown
$ unxz -v linux-5.1.2.tar.xz
```
Or
```markdown
$ xz -d -v linux-5.1.2.tar.xz
```

### Step 3. Copy existing Linux kernel config file
Before start building the kernel, one must configure Linux kernel features. You must also specify which kernel modules (drivers) needed for your system. The task can be overwhelming for a new user. I suggest that you copy existing config file using the cp command:
```markdown
$ cd linux-5.1.2
$ cp -v /boot/config-$(uname -r) .config
```

### Step 4. Compile and build Linux kernel
You must have development tools such as GCC compilers and related tools installed to compile the Linux kernel.
Now you can start the kernel configuration by typing any one of the following command in source code directory:
* $ make menuconfig – Text based color menus, radiolists & dialogs. This option also useful on remote server if you wanna compile kernel remotely.
* $ make xconfig – X windows (Qt) based configuration tool, works best under KDE desktop
* $ make gconfig – X windows (Gtk) based configuration tool, works best under Gnome Dekstop.
For example, run make menuconfig command launches following screen:
```markdown
$ make menuconfig
```
You have to select different options as per your need. Each configuration option has HELP button associated with it so select help button to get help. Please note that ‘make menuconfig’ is optional. I used it here to demonstration purpose only. You can enable or disable certain features or kernel driver with this option. It is easy to remove support for a device driver or option and end up with a broken kernel. For example, if the ext4 driver is removed from the kernel configuration file, a system may not boot. When in doubt, just leave support in the kernel.

Start compiling and tocreate a compressed kernel image, enter:
```markdown
$ make
```
To speed up compile time, pass the -j as follows:
```markdown
## use 4 core/thread ##
$ make -j 4
## get thread or cpu core count using nproc command ##
$ make -j $(nproc)
```
Compiling and building the Linux kernel going take a significant amount of time. The build time depends upon your system’s resources such as available CPU core and the current system load. So have some patience.

### Step 5. Install Linux kernel and modules (drivers)
```markdown
$ sudo make modules_install
```
So far we have compiled the Linux kernel and installed kernel modules. It is time to install the kernel itself:
```markdown
$ sudo make install
```
It will install three files into /boot directory as well as modification to your kernel grub configuration file:
* initramfs-5.1.2.img
* System.map-5.1.2
* vmlinuz-5.1.2

### Step 6. Update Grub configuration
You need to modify Grub 2 boot loader configurations. Type the following command at a shell prompt as per your Linux distro:

(Debian/Ubuntu Linux)
The following commands are optional as make install does everything for your but included here for historical reasons only:
```markdown
$ sudo update-initramfs -c -k 5.1.2
$ sudo update-grub
```

### Step 6. Reboot the system
You have compiled a Linux kernel. The process takes some time, however now you have a custom Linux kernel for your system. Let us reboot the system.
```markdown
# reboot
```
Verify new Linux kernel version after reboot:
```markdown
$ uname -mrs
```
Configurations! You completed various steps to build the Linux kernel from source code and compiled kernel should be running on your system. I strongly suggest that you always keep backup of essential data and visit the kernel.org page here for more info.
