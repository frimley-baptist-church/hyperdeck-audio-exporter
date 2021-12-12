# hyperdeck-audio-exporter

Ever been asked to export an audio file of your ATEM ISO recording? Then this note describes the fastest way to acquire your audio without transferring your USB drive to a computer, without running a video editing application, and to do so quickly and in original ISO recording quality.

## What you'll need
You must have a copy of **FFMPEG** installed somewhere on a computer that has IP connectivity to your ATEM MINI ISO or ATEM MINI EXTREME ISO switcher. Installing FFMPEG is not part of this guide - your favourite search engine will provide appropriate installation details - be your computer choice range from a Raspberry Pi through to any Windows machine, Apple Mac, any Linux server or laptop.

Your computer and ATEM switcher must be on the same network. If you can successfully control your ATEM using BMD's ATEM control software, then you're all set. For ultimate performance, at least with an ATEM EXTREME ISO, use a gigabit network switch to connect the two devices.

## Instructions
### On your computer, run up a 'shell'.
* For Microsoft Windows, that means a CMD BOX. To get one, hit the 'windows' key, type `cmd` and press enter.
* For Apple Mac, that's a Console Terminal window.
* For Linux/Rasperry Pi, a Terminal window/shell.

### Test that ffmpeg runs
* In the 'shell' window, simply type `ffmpeg` and hit return. You should see some terminal output. If you receive a message similar to "application not found", you'll need to revisit your ffmpeg installation procedure.

### Performing the audio extract
* In the example below, my ATEM EXTREME ISO's IP address is 10.183.48.104
* In the example below, my SSD drive was labelled `UNTITLED` - i.e. this is what shows up when plugged into Windows or a Mac as the "drive name".
* In the example below, my recorded ISO file was named FBCLive-20211212-1030.mp4
* In the example below, I am running this command from an Ubuntu Linux 20.04 server, but the experience will be identical regardless of the operating system used.
* In the example below, my network is gigabit throughout.

```
$ ffmpeg -i ftp://a:b@10.183.48.104/UNTITLED/FBCLive-20211212-1030.mp4 -vn -codec copy -y FBCLive-20211212-1030.m4a
ffmpeg version N-94125-gd33414d-8bit_static_linux_x86_64_201906270248 Copyright (c) 2000-2019 the FFmpeg develope                         rs
  built with gcc 5.4.0 (Ubuntu 5.4.0-6ubuntu1~16.04.11) 20160609
  configuration: --extra-version=8bit_static_linux_x86_64_201906270248 --extra-cflags='--static -static ' --extra                         -libs='-static -lpthread -lm' --pkg-config-flags=--static --cross-prefix= --arch=x86_64 --target-os=linux --prefi                         x=/opt/ffbuild --enable-gpl --enable-nonfree --disable-ffplay --disable-dxva2 --enable-openssl --enable-libmp3lam                         e --enable-libspeex --enable-libtheora --enable-libvorbis --enable-libopus --enable-libxvid --enable-libvpx --ena                         ble-libfdk-aac --enable-libx264 --enable-libx265 --enable-libopenjpeg
  libavutil      56. 29.100 / 56. 29.100
  libavcodec     58. 53.100 / 58. 53.100
  libavformat    58. 28.101 / 58. 28.101
  libavdevice    58.  7.100 / 58.  7.100
  libavfilter     7. 55.100 /  7. 55.100
  libswscale      5.  4.101 /  5.  4.101
  libswresample   3.  4.100 /  3.  4.100
  libpostproc    55.  4.100 / 55.  4.100
Input #0, mov,mp4,m4a,3gp,3g2,mj2, from 'ftp://a:b@atem/UNTITLED/fbclive-20211212-1030.mp4':
  Metadata:
    major_brand     : isom
    minor_version   : 1
    compatible_brands: iso4avc1isom
    creation_time   : 2021-12-12T10:30:50.000000Z
    com.apple.proapps.clipID: fbclive-20211212-1030
    com.blackmagic-design.camera.dateRecorded: 2021:12:12
    com.apple.proapps.cameraName: 0
    com.blackmagic-design.camera.uuid: 76A23BD13C934952A87F3FB86B71416F-0
  Duration: 01:17:52.00, start: 0.000000, bitrate: 7085 kb/s
    Stream #0:0(eng): Video: h264 (Main) (avc1 / 0x31637661), yuv420p(tv, bt709, progressive), 1920x1080, 6950 kb                         /s, SAR 1:1 DAR 16:9, 50 fps, 50 tbr, 50 tbn, 100 tbc (default)
    Metadata:
      creation_time   : 2021-12-12T10:30:50.000000Z
      handler_name    : ?Apple Video Media Handler
      encoder         : H264/AVC
      timecode        : 10:30:50:14
    Stream #0:1(eng): Data: none (tmcd / 0x64636D74) (default)
    Metadata:
      creation_time   : 2021-12-12T10:30:50.000000Z
      handler_name    : ?Time Code Media Handler
      timecode        : 10:30:50:14
    Stream #0:2(eng): Audio: aac (LC) (mp4a / 0x6134706D), 48000 Hz, stereo, fltp, 128 kb/s (default)
    Metadata:
      creation_time   : 2021-12-12T10:30:50.000000Z
      handler_name    : ?Apple Sound Media Handler
      timecode        : 10:30:50:14
Output #0, ipod, to 'fbclive-20211212-1030.m4a':
  Metadata:
    major_brand     : isom
    minor_version   : 1
    compatible_brands: iso4avc1isom
    com.blackmagic-design.camera.uuid: 76A23BD13C934952A87F3FB86B71416F-0
    com.apple.proapps.clipID: fbclive-20211212-1030
    com.blackmagic-design.camera.dateRecorded: 2021:12:12
    com.apple.proapps.cameraName: 0
    encoder         : Lavf58.28.101
    Stream #0:0(eng): Audio: aac (LC) (mp4a / 0x6134706D), 48000 Hz, stereo, fltp, 128 kb/s (default)
    Metadata:
      creation_time   : 2021-12-12T10:30:50.000000Z
      handler_name    : ?Apple Sound Media Handler
      timecode        : 10:30:50:14
Stream mapping:
  Stream #0:2 -> #0:0 (copy)
Press [q] to stop, [?] for help
size=   73857kB time=01:17:51.97 bitrate= 129.5kbits/s speed=72.9x
video:0kB audio:73000kB subtitle:0kB other streams:0kB global headers:0kB muxing overhead: 1.174151%
$
```

In my case, the audio extract to a .m4a file completed in 65 seconds. As shown toward the end of the above log, that was around 73x real-time.

In our scenario, we then process that audio file and release it as, effectively, a podcast on our church website.
