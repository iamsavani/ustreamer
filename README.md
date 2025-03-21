### µStreamer

[µStreamer](https://github.com/pikvm/ustreamer) µStreamer is a lightweight and fast MJPEG video streaming service that can stream MJPEG video on V4L2 devices to the network. This video format is supported by major browsers and most video players such as mplayer and VLC. It is part of the [PiKVM](https://github.com/pikvm/pikvm) project and aims to transmit VGA or HDMI video data over the network with the highest possible resolution and frame rate.

The author branched and modified µStreamer : adding libx264 video encoder to support H.264 video encoding on platforms other than Raspberry Pi.


### Compile

Based on Ubuntu/Debian distribution, directly compile the required dependencies:

```bash
apt install  build-essential libssl-dev libffi-dev libevent-dev libjpeg-dev libbsd-dev libudev-dev git pkg-config
```
`WITH_PYTHON=1` Additional dependencies required to enable the option:
```bash
apt install python3-dev python3-build
```
`WITH_JANUS=1` Additional dependencies required to enable the option:
```bash
apt install janus-dev libasound2-dev  libspeex-dev libspeexdsp-dev libopus-dev
sed --in-place --expression 's|^#include "refcount.h"$|#include "../refcount.h"|g' /usr/include/janus/plugins/plugin.h
```
`WITH_LIBX264=1` Additional dependencies required to enable the option：
```bash
apt install libx264-dev libyuv-dev
```


```bash
git clone --depth=1 https://github.com/iamsavani/ustreamer
cd ustreamer
make
#make WITH_PYTHON=1 WITH_JANUS=1 WITH_LIBX264=1
./ustreamer --help
```


-----
### use

Basic usage example: Capture `/dev/video0` the video stream of the device and `0.0.0.0:80` provide web services on it:
```bash
./ustreamer --device=/dev/video0 --host=0.0.0.0 --port=80
```

Example of using libx264 to encode H.264 video:


```bash
./ustreamer \
    --format=mjpeg \
    --encoder=LIBX264-VIDEO \
    --persistent \
    --h264-sink=test.h264 #

./ustreamer-dump \
    --sink test.h264 \
    --output test.h264
```
Use ```ustreamer --help``` to see a complete list of options.

-----
### Copyright Notice
Copyright (C) 2018-2024 by Maxim Devaev mdevaev@gmail.com

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see https://www.gnu.org/licenses/.
