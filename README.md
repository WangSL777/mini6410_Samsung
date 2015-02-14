# mini6410_Samsung

How to install and build linux on local machine to make use of existing mini6410 module drivers

1) First download two packages...
    
    a) Toolchain to cross compile for the Mini6410 - arm-linux-gcc-4.5.1-v6-vfp-20101103.tgz
    b) Linux Kernel - linux-2.6.38-20110718.tar.gz
    
    To download above packages,
    Please go to FriendlyARM's FTP site: ftp://162.251.81.100/ to download all the materials
    Username: downloaduser
    password: 12345
    
    Or you can get both these packages from SD card which come along with your Samsung mini6410 board. So simply copy      those files into your ubuntu machine.
    
2) You can copy those packages into /home/$YOUR_MACHINE_NAME/mini6410/ .

3) Now enter in your terminal as Super User.
    sudo su
    
3) Now extract those packages into /opt directory. For that run following commands.
    tar -xvzf arm-linux-gcc-4.5.1-v6-vfp-20101103.tgz -C /
    mkdir /opt/FriendlyARM/mini6410
    mv /opt/FriendlyARM/toolschain /opt/FriendlyARM/mini6410
    tar -xvzf linux-2.6.38-20110718.tar.gz -C /opt/FriendlyARM/mini6410/  (or whatever linux version package you have                                                                                                            installed)

4) Add path of Arm Cross compiler to .bashrc file. Add below sentence to top of the file.
    gedit ~/.bashrc & 
    export PATH=$PATH:/opt/FriendlyARM/mini6410/toolschain/4.5.1/bin
    
    Now close the terminal and reopen it for reexecution of that .bashrc file. It's necessary.
    
5) You got all extracted packages, Now build kernel 2.6.38 , enter into linux-2.6.38 directory.
    cd /opt/FriendlyARM/mini6410/linux-2.6.38/
    make
    
    This command will build all necessary object files and kernel drivers. It will take approxomately 10 minutes for       execution process.

6) To see existing examples you have to extract those files into /opt/FriendlyARM/mini6410/linux-2.6.38/ directory.
    tar -xvzf /home/$YOUR_MACHINE_NAME/mini6410/examples-mini6410-20110104.tgz -C /opt/FriendlyARM/mini6410/linux-2.6.38/
    cd /opt/FriendlyARM/mini6410/linux-2.6.38/examples/
    ls
    
    By executing above command it will list all existing exmples like leds,pwm,buttons,i2c,adc-test,led-player etc.
    
7) Now it's time to see existing char devices in our machine. First install necessary packages.
    apt-get install ncurses-dev
    cd /opt/FriendlyARM/mini6410/linux-2.6.38/
    make menuconfig
    
    So you will get one popup blue-white screen named Linux/arm 2.6.38 Kernel Configuration. Go Device Drivers -> Character devices ->   there you will get mini6410 device samples.
    
    
Here you go........ Now enjoy changes into kernel drivers and test those into your hardware board by copying .ko and application file into samsung board and insert that module into kernel by insmod and run that application.
