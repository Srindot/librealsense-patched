# librealsense-patced



Custom Arch Linux PKGBUILD for Intel® RealSense™ SDK 2.0 (librealsense), with a patch to fix a missing header file that caused build failures in the official AUR package. This is not an official package.


## Background

The official AUR package for `librealsense` failed to build due to a missing header file (`<cstdint>`), which resulted in errors like:

```Error
In file included from /home/pika/.cache/yay/librealsense/src/librealsense-2.55.1/src/core/frame-holder.h:5,
                 from /home/pika/.cache/yay/librealsense/src/librealsense-2.55.1/src/core/matcher-factory.cpp:5:
/home/pika/.cache/yay/librealsense/src/librealsense-2.55.1/src/core/frame-interface.h:27:19: error: ‘uint8_t’ does not name a type
   27 | virtual const uint8_t * get_frame_data() const = 0;
      |                   ^~~
/home/pika/.cache/yay/librealsense/src/librealsense-2.55.1/src/core/frame-interface.h:6:1: note: ‘uint8_t’ is defined in header ‘<cstdint>’; this is probably fixable by adding ‘#include <cstdint>’
    5 | #include <librealsense2/h/rs_frame.h>
  +++ |+#include <cstdint>
    6 | #include <memory>
make[2]: *** [CMakeFiles/realsense2.dir/build.make:79: CMakeFiles/realsense2.dir/src/core/matcher-factory.cpp.o] Error 1
make[1]: *** [CMakeFiles/Makefile2:1023: CMakeFiles/realsense2.dir/all] Error 2
make: *** [Makefile:136: all] Error 2
==> ERROR: A failure occurred in build().
    Aborting...
-> error making: librealsense-exit status 4
==> Making package: monado 25.0.0-1 (Fri 09 May 2025 10:07:16 PM CDT)
==> Checking runtime dependencies...
==> Checking buildtime dependencies...
==> Missing dependencies:
  -> librealsense
==> ERROR: Could not resolve all dependencies.
-> error making: monado-exit status 8
-> Failed to install the following packages. Manual intervention is required:
librealsense - exit status 4
```
