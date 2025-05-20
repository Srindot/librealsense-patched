# librealsense-patced



Custom Arch Linux PKGBUILD for Intel® RealSense™ SDK 2.0 (librealsense), with a patch to fix a missing header file that caused build failures in the official AUR package. This is not an official package.


## Background

The official AUR package for `librealsense2` failed to build due to a missing header file (`<cstdint>`), which resulted in error like:

```txt
/home/pika/.cache/yay/librealsense/src/librealsense-2.55.1/src/core/frame-interface.h:27:19: error: ‘uint8_t’ does not name a type
   27 | virtual const uint8_t * get_frame_data() const = 0;
      |                   ^~~
/home/pika/.cache/yay/librealsense/src/librealsense-2.55.1/src/core/frame-interface.h:6:1: note: ‘uint8_t’ is defined in header ‘<cstdint>’;
this is probably fixable by adding ‘#include <cstdint>’
```

## Installation

1. **Clone this repository:**
    ```bash
    git clone https://github.com/srindot/librealsense-patched.git
    cd librealsense-patched
    ```

2. **Build and install the package:**
    ```bash
    makepkg -si
    ```

## Usage

This package is used to capture video and images from Intel® RealSense™ cameras.

To use your camera:

1. **Connect your Intel RealSense camera** to your computer using a USB 3.0.
2. Once the camera is connected, verify its functionality by running the following command:
    ```bash
    realsense-viewer
    ```
3. The RealSense Viewer application will open, allowing you to view live streams, capture photos, and record videos from your camera.

## Credits

- [Intel RealSense](https://github.com/IntelRealSense/librealsense) for the original SDK
- Community contributors for the patch

## License

This repository contains packaging scripts and patches.  
See the upstream [librealsense license](https://github.com/IntelRealSense/librealsense/blob/master/LICENSE) for details.
   

Make sure your camera is properly connected and detected before launching the viewer.




