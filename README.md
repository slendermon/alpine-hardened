## Developing linux-kernel with hardened patch

Make a custom linux kernel using [this guide.](#custom-kernel) Once you have setup the linux kernel from there, in your current directory ($WORK_DIR/aports/main/linux-lts), gather linux hardened patches via these two CLI commands (Replace "$VERSION" with the current latest version in the releases):

```
wget https://github.com/anthraxx/linux-hardened/releases/download/v$VERSION-hardened1/linux-hardened-v$VERSION-hardened1.patch 0006-linux-hardened-v6.11.10-hardened1.patch
wget https://github.com/anthraxx/linux-hardened/releases/download/v$VERSION-hardened1/linux-hardened-v$VERSION-hardened1.patch.sig 0007-linux-hardened-v6.11.10-hardened1.patch.sig
```

There is some need to remove "-hardened1" in the patch file (not the sig file):
```
-EXTRAVERSION =
+EXTRAVERSION = -hardened1
```
You MUST remove the "EXTRAVERSION" naming ("-hardened1") after it, or compiling with the package "kernel-hooks" would not do anything, as this "extraversion" is not necessary. (Kernel-hooks apk package is necessary to make a secureboot [EFISTUB.](#efistub)) 

Before compiling the kernel, in [the Alpine Linux kernel guide.](#custom-kernel) you must do some kernel module configurations, preferably shorten the amount of kernel modules in the KCONFIG files where possible, to reduce compilation times. You may borrow [this KCONFIG](#linux-hardened-kconfig-file) from linux-hardened as a base, for configuration simplicity sake. (Use the apk package "Kconfig-Hardened-Check" for configuring KCONFIG file as securely as possible.)

After applying this, you may do `abuild -r` to start compiling the kernel.

After compiling kernel, it is also recommended to use the apk package hardened-malloc, and once installed, inside the file `/etc/ld.so.preload`, put this into the file:
`/usr/lib/libhardened_malloc.so`

## External Links:
#### Custom Kernel:
- https://wiki.alpinelinux.org/wiki/Custom_Kernel
#### EFIStub
- https://wiki.alpinelinux.org/wiki/UEFI_Secure_Boot
#### Releases page:
- https://github.com/anthraxx/linux-hardened/releases
#### Some resources for help creating this page:
- https://strfry.github.io/blog/building-alpine-kernel.html
#### Linux-Hardened KCONFIG file
- https://github.com/a13xp0p0v/kernel-hardening-checker/blob/master/kernel_hardening_checker/config_files/distros/Arch_hardened_x86_64.config
