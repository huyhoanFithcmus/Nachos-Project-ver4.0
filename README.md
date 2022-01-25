# How to install Nachos on Ubuntu 18.04
## The install procedure is as follows:
### Login to Ubuntu 18.04 with your account
- Install and compile the basic toolkit
``` 
sudo apt-get install build-essential 
```
- Computer 32/64 check
- Check that the system is a 64-bit kernel,
```
dpkg --print-architecture
```
- Execute the above command. If the output shows amd64, it means that your Linux distribution is a 64-bit kernel, and you need to perform the second step;
- Turn on support for 32 positions
```
sudo dpkg --add-architecture i386
```
- Install c, c++ multi-platform library
```
sudo apt-get install gcc-multilib g++-multilib
```
- Install 32-bit environment library
```
sudo apt-get install lib32ncurses5 lib32z1
```
- Install a version lower than gcc5.0
```
sudo apt-get install gcc-4.8 gcc-4.8-multilib g++-4.8 g++-4.8-multilib
```
- Switch the low version gcc and g++ to the current active version
```
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 40
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.8 40
```
- Check if the version is correct
```
gcc -v
```
- You should see the following message:
```
Using built-in specs.
COLLECT_GCC=gcc
COLLECT_LTO_WRAPPER=/usr/lib/gcc/x86_64-linux-gnu/4.8/lto-wrapper
Target: x86_64-linux-gnu
Configured with: ../src/configure -v --with-pkgversion='Ubuntu 4.8.5-4ubuntu8' --with-bugurl=file:///usr/share/doc/gcc-4.8/README.Bugs --enable-languages=c,c++,go,d,fortran,objc,obj-c++ --prefix=/usr --program-suffix=-4.8 --enable-shared --enable-linker-build-id --libexecdir=/usr/lib --without-included-gettext --enable-threads=posix --with-gxx-include-dir=/usr/include/c++/4.8 --libdir=/usr/lib --enable-nls --with-sysroot=/ --enable-clocale=gnu --enable-libstdcxx-debug --enable-libstdcxx-time=yes --enable-gnu-unique-object --disable-libmudflap --enable-plugin --with-system-zlib --enable-objc-gc --enable-multiarch --disable-werror --with-arch-32=i686 --with-abi=m64 --with-multilib-list=m32,m64,mx32 --with-tune=generic --enable-checking=release --build=x86_64-linux-gnu --host=x86_64-linux-gnu --target=x86_64-linux-gnu
Thread model: posix
gcc version 4.8.5 (Ubuntu 4.8.5-4ubuntu8)
```
```
 g++ -v
```
- You should see the following message:
```
Using built-in specs.
COLLECT_GCC=g++
COLLECT_LTO_WRAPPER=/usr/lib/gcc/x86_64-linux-gnu/4.8/lto-wrapper
Target: x86_64-linux-gnu
Configured with: ../src/configure -v --with-pkgversion='Ubuntu 4.8.5-4ubuntu8' --with-bugurl=file:///usr/share/doc/gcc-4.8/README.Bugs --enable-languages=c,c++,go,d,fortran,objc,obj-c++ --prefix=/usr --program-suffix=-4.8 --enable-shared --enable-linker-build-id --libexecdir=/usr/lib --without-included-gettext --enable-threads=posix --with-gxx-include-dir=/usr/include/c++/4.8 --libdir=/usr/lib --enable-nls --with-sysroot=/ --enable-clocale=gnu --enable-libstdcxx-debug --enable-libstdcxx-time=yes --enable-gnu-unique-object --disable-libmudflap --enable-plugin --with-system-zlib --enable-objc-gc --enable-multiarch --disable-werror --with-arch-32=i686 --with-abi=m64 --with-multilib-list=m32,m64,mx32 --with-tune=generic --enable-checking=release --build=x86_64-linux-gnu --host=x86_64-linux-gnu --target=x86_64-linux-gnu
Thread model: posix
gcc version 4.8.5 (Ubuntu 4.8.5-4ubuntu8)
```

- Create a directory called "nachos" for creating the environment of NachOS and then change directory into "nachos" directory
```
mkdir nachos
```
```
cd nachos
```
- Download the source code
- Download NachOS source code:
```
nachos> wget https://www.fit.hcmus.edu.vn/~ntquan/os/assignment/nachos_40.tar.gz
```
-Download the source code of MIPS cross-compiler:
```
nachos> wget https://www.fit.hcmus.edu.vn/~ntquan/os/assignment/mips-decstation.linux-xgcc.gz
```
-Download the patch for Linux:
```
nachos> wget https://www.fit.hcmus.edu.vn/~ntquan/os/assignment/nachos-gcc.diff.gz
```

- Extract the zipped files and patch the Makefiles for the environment of Linux
- Extract NachOS source code:
```
nachos> tar zxvf nachos_40.tar.gz
```
- Extract the source code of MIPS cross-compiler:
```
nachos> tar zxvf mips-decstation.linux-xgcc.gz
```
- Extract patch file:
```
nachos> tar zxvf nachos-gcc.diff.gz
```
- Patch Makefiles:
```
nachos> patch -p0 < nachos-gcc.diff
```
- Compile NachOS:
```
nachos> cd NachOS-4.0
nachos/NachOS-4.0> cd code/build.linux
nachos/NachOS-4.0/code/build.linux> make depend
nachos/NachOS-4.0/code/build.linux> make
```
- Test Nachos:
```
nachos/NachOS-4.0/code/build.linux> ./nachos
```
- You should see the following message:
```
Machine halting!

Ticks: total 10, idle 0, system 10, user 0
Disk I/O: reads 0, writes 0
Console I/O: reads 0, writes 0
Paging: faults 0
Network I/O: packets received 0, sent 0
```

- Build the tool to transfer COFF format to NOFF format (The output executible file is coff2noff.x86Linux):
```
nachos/NachOS-4.0/code/build.linux> cd ../../coff2noff
nachos/NachOS-4.0/coff2noff> make
```
- Compile the "test" user applications for NachOS:
```
nachos/NachOS-4.0/coff2noff> cd ../code/test
nachos/NachOS-4.0/code/test> make
```

- Use the application program "halt" to test running appliction on NachOS:
```
nachos/NachOS-4.0/code/test> ../build.linux/nachos -x halt
```
You should see the following message:
```
Machine halting!

Ticks: total 22, idle 0, system 10, user 12
Disk I/O: reads 0, writes 0
Console I/O: reads 0, writes 0
Paging: faults 0
Network I/O: packets received 0, sent 0
```
# Congratulations!!! You've succeeded.
