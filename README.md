# librealsense-patced



Custom Arch Linux PKGBUILD for Intel® RealSense™ SDK 2.0 (librealsense), with a patch to fix a missing header file that caused build failures in the official AUR package. This is not an official package.


## Background

The official AUR package for `librealsense2` failed to build due to a missing header file (`<cstdint>`), which resulted in error like:

```txt
/home/pika/.cache/yay/librealsense/src/librealsense-2.55.1/src/core/frame-interface.h:27:19: error: ‘uint8_t’ does not name a type
   27 | virtual const uint8_t * get_frame_data() const = 0;
      |                   ^~~
/home/pika/.cache/yay/librealsense/src/librealsense-2.55.1/src/core/frame-interface.h:6:1: note: ‘uint8_t’ is defined in header ‘<cstdint>’; this is probably fixable by adding ‘#include <cstdint>’
```

## Installation

1. **Clone this repository:**
    ```
    git clone https://github.com/srindot/librealsense-patched.git
    cd librealsense-patched
    ```

2. **Build and install the package:**
    ```
    makepkg -si
    ```

