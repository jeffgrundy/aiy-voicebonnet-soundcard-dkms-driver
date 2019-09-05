# What is this?

This is the Linux kernel driver for the Google AIY Voice Kit v2 voice bonnet for Ubuntu Server 18 something.

When I tried to follow the instructions in the hacking file ubuntu server throws the error 

Skipping acquire of configured file 'main/binary-arm64/Packages' as repository 'https://dl.google.com/aiyprojects/deb stable InRelease' doesn't support architecture 'arm64'

so I have attempted to build the driver for ubuntu using https://wiki.centos.org/HowTos/BuildingKernelModules#head-d313bd351f90d4f25a2143b7bbcff73f927731f0

DKMS make.log for aiy-voicebonnet-soundcard-0.1 for kernel 4.15.0-1044-raspi2 (aarch64)
Thu Sep  5 01:01:37 UTC 2019
make: Entering directory '/usr/src/linux-headers-4.15.0-1044-raspi2'
  CC [M]  /var/lib/dkms/aiy-voicebonnet-soundcard/0.1/build/snd-aiy-voicebonnet.o
  CC [M]  /var/lib/dkms/aiy-voicebonnet-soundcard/0.1/build/snd-soc-bcm2835-i2s.o
  CC [M]  /var/lib/dkms/aiy-voicebonnet-soundcard/0.1/build/rt5645.o
  CC [M]  /var/lib/dkms/aiy-voicebonnet-soundcard/0.1/build/rl6231.o
/var/lib/dkms/aiy-voicebonnet-soundcard/0.1/build/rt5645.c: In function ‘rt5645_jack_detect’:
/var/lib/dkms/aiy-voicebonnet-soundcard/0.1/build/rt5645.c:3164:20: error: ‘struct rt5645_platform_data’ has no member named ‘jd_invert’
   if (rt5645->pdata.jd_invert)
                    ^
it looks like the member was renamed in the kermel

https://patchwork.kernel.org/patch/9815219/

so i have corrected it here 





Note: the rt6231 and rl5645 codec drivers were copied from the Linux source tree
because the symbols needed in the snd-aiy-voicebonnet driver are not available
in DKMS builds.

These files are identical to the ones in the kernel tree at sound/soc/codecs/
