本篇文章转载自一个外文网站。

平时使用Linux系统常使用发行版，如果想要运行源码或者自己定制的系统需要做更多的工作。

##How to compile and install Linux Kernel
The procedure to build (compile) and install the latest Linux kernel from source is as follows:
1. Grab the latest kernel from kernel.org
2. Verify kernel
3. Untar the kernel tarball
4. Copy existing Linux kernel config file
5. Compile and build Linux kernel
6. Install Linux kernel and modules (drivers)
7. Update Grub configuration
8. Reboot the system

###Step 1. Get the latest Linux kernel source code
Visit the official project site and download the latest source code. Click on the big yellow button that read as “Latest Stable Kernel“

###Step 2. Extract tar.xz file
'''markdown
$unxz -v linux-5.1.2.tar.xz
'''
