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
OR
```markdown
$ xz -d -v linux-5.1.2.tar.xz
```

### Step 3. Copy existing Linux kernel config file
Before start building the kernel, one must configure Linux kernel features. You must also specify which kernel modules (drivers) needed for your system. The task can be overwhelming for a new user. I suggest that you copy existing config file using the cp command:
```markdown
$ cd linux-5.1.2
$ cp -v /boot/config-$(uname -r) .config
```
