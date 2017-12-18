# STM32F3Discovery-meson-example

This is another STM32F3Discovery example Project.

It uses the STM32Cube-f3-meson repo which is optimised for the `meson build system`.

[STM32Cube-f3-meson](https://github.com/hwengineer/STM32Cube-f3-meson)



## Why another build system?
For myself: I hate using eclipse. And also I hate writing Makefiles.
So I had to find another build system to program my precious microcontrollers.

I read about the [mesonbuild](http://mesonbuild.com/) system and though that could be an interesting solution.

>Meson is an open source build system meant to be both extremely fast, and, even more importantly, as user friendly as possible.

Meson uses the so called [ninja](https://ninja-build.org/) back-end.

>Ninja is a small build system with a focus on speed. It differs from other build systems in two major respects: it is designed to have its input files generated by a higher-level build system, and it is designed to run builds as fast as possible.

Both are optimized for speed.

And also I can configure meson to use `llvm`. Which is also just a personal preference of mine.
If I got the time I will also make this script workable with an `arm-none-eabi-gcc` compiler.

## usage (short)

create the build folder, create the meson project and start compilation

      mkdir llvmbuild
      meson --cross-file=cross_file.build
      cd llvmbuild
      ninja

now connect your target and run openocd in a new terminal

      openocd -f interface/stlink-v2.cfg -f target/stm32f3x.cfg

goto your first terminal and start the `gdb` session

      arm-none-eabi-gdb -q llvmbuild/main.elf

Type the following command into the gdb console

      continue

enjoy!

## Toolchain Installation

Of course this only works, if the proper toolchain is installed...

First you have to install the `arm-none-eabi-gcc` toolchain.
On Ubuntu :

      sudo apt-get install binutils-arm-none-eabi gcc-arm-none-eabi gdb-arm-none-eabi  libnewlib-arm-none-eabi libnewlib-arm-none-eabi

### LLVM-5.0

Also we want to install llvm-5.0:

      wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key|sudo apt-key add -
      sudo add-apt-repository -y 'deb http://apt.llvm.org/xenial/ llvm-toolchain-xenial-5.0 main'
      sudo add-apt-repository -y 'deb-src http://apt.llvm.org/xenial/ llvm-toolchain-xenial-5.0 main'

      sudo apt-get update
      sudo apt-get -y install clang-5.0 llvm-5.0 lld-5.0

### Python3 / Meson / Ninja

And of course meson-build

      sudo apt-get -y install python3 python3-pip python3-setuptools ninja-build
      sudo pip3 install --upgrade pip
      sudo pip3 install meson

### git

      sudo apt-get -y install git

### openocd

      sudo apt-get install openocd

You maybe have to add the so called udev rules.
(They should get installed with the openocd package).
After updateing the udev rules use this command to reload the new configs

      sudo udevadm control --reload-rules


### clone this repo

go to your destination folder and clone the repo in

      git clone https://github.com/hwengineer/STM32F3Discovery-meson-example.git
      git submodule update --init --recursive

And no use the commands above for compilation and testing.


## License
Of course the STM32Cube Library is under its own license, all other stuff under my chosen MIT License
