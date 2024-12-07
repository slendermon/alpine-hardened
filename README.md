## Developing linux-kernel with hardened patch
--

Make a custom linux kernel using [this guide.](#Custom_Kernel) Once you have setup the linux kernel from there, gather linux hardened patches via these two cli commands (Replace "$VERSION" with the current version in the releases!!!):

```
wget https://github.com/anthraxx/linux-hardened/releases/download/v$VERSION-hardened1/linux-hardened-v$VERSION-hardened1.patch
wget https://github.com/anthraxx/linux-hardened/releases/download/v$VERSION-hardened1/linux-hardened-v$VERSION-hardened1.patch.sig
```


## Custom Kernel:
- https://wiki.alpinelinux.org/wiki/Custom_Kernel

## Releases page:
- https://github.com/anthraxx/linux-hardened/releases

## Some resources for help creating this page:
- https://strfry.github.io/blog/building-alpine-kernel.html
