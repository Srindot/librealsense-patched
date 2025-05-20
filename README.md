# librealsense-patced



Custom Arch Linux PKGBUILD for Intel® RealSense™ SDK 2.0 (librealsense), with a patch to fix a missing header file that caused build failures in the official AUR package. This is not an official package.


## Background

The official AUR package for `librealsense` failed to build due to a missing header file (`<cstdint>`), which resulted in errors like:

```output
Error
```
