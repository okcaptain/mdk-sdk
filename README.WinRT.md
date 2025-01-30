## MDK: Multimedia Development Kit
### [Changelog](https://github.com/wang-bin/mdk-sdk/blob/master/Changelog.md)
### [API](https://github.com/wang-bin/mdk-sdk/wiki/Player-APIs)

### Features
- [Simple and powerful API set](https://github.com/wang-bin/mdk-sdk/wiki/Player-APIs)
- [Cross platform: Windows(x86, arm), UWP, Linux, macOS, Android, iOS, tvOS, visionOS, Raspberry Pi](https://github.com/wang-bin/mdk-sdk/wiki/System-Requirements)
- [Hardware accelerated decoders](https://github.com/wang-bin/mdk-sdk/wiki/Decoders)
- [0-copy GPU rendering for all platforms and all renderers(Vulkan is WIP.)](https://github.com/wang-bin/mdk-sdk/wiki/Zero-Copy-Renderer)
- [Dynamic OpenGL](https://github.com/wang-bin/mdk-sdk/wiki/OpenGL-Support-Matrix)
- [OpenGL, D3D11, D3D12, Vulkan and Metal rendering w/ or w/o user provided context](https://github.com/wang-bin/mdk-sdk/wiki/Render-API)
- Integrated with any platform native ui apps, gui toolkits or other apps via [OpenGL, D3D11/12, Vulkan and Metal](https://github.com/wang-bin/mdk-sdk/wiki/Render-API) (WinUI3, [OBS](https://github.com/wang-bin/obs-mdk), [Flutter](https://pub.dev/packages/fvp), [Qt](https://github.com/wang-bin/mdk-examples/tree/master/Qt), [SDL](https://github.com/wang-bin/mdk-examples/tree/master/SDL), [GLFW](https://github.com/wang-bin/mdk-examples/tree/master/GLFW), [SFML](https://github.com/wang-bin/mdk-examples/tree/master/SFML), [.NET Avalonia](https://github.com/wang-bin/mdk-examples/tree/master/Avalonia) etc.) easily
- [HDR display, HDR to SDR and SDR to HDR tone mapping](https://github.com/wang-bin/mdk-sdk/wiki/Player-APIs#player-setcolorspace-value-void-vo_opaque--nullptr). You can use HDR display in [Qt6(6.6+ for macOS, 6.x for windows)](https://github.com/wang-bin/mdk-examples/tree/master/Qt/qmlrhi), [OBS Studio](https://github.com/wang-bin/obs-mdk) and more.
- Dolby Vision rendering, including Profile 5. Support HEVC and AV1.
- [Seamless/Gapless media and bitrate switch for any media](https://github.com/wang-bin/mdk-sdk/wiki/Player-APIs#player-setcolorspace-value-void-vo_opaque--nullptr)
- Optimized Continuous seeking. As fast as mpv, but much lower cpu, memory and gpu load. Suitable for [timeline preview](https://github.com/wang-bin/mdk-sdk/wiki/Typical-Usage#timeline-preview)
- Subtitle rendering, including ass, plain text, bitmap, closed caption
- [Smart FFmpeg runtime, dynamic load, compatible with 4.0~7.x abi](https://github.com/wang-bin/mdk-sdk/wiki/FFmpeg-Runtime)
- Professional codecs: GPU accelerated [HAP](https://github.com/wang-bin/mdk-sdk/wiki/Decoders#hap) codec rendering, [Blackmagic RAW](https://github.com/wang-bin/mdk-braw), [R3D](https://github.com/wang-bin/mdk-r3d)


## About SDK for Windows Desktop & UWP
SDK is built by
- latest VS2022 with [FFmpeg win32](https://sourceforge.net/projects/avbuild/files/windows-desktop/ffmpeg-master-windows-desktop-vs2022-lite.7z/download) and [FFmpeg UWP](https://sourceforge.net/projects/avbuild/files/uwp/ffmpeg-master-uwp-vs2022-lite.7z/download)

SDK can be used by any C or C++11 compiler, e.g. vs2015, vs2022, mingw g++, clang

### Use in Visual Studio

#### Install via NuGet (Recommended)
mdk is published on https://www.nuget.org/packages/mdk/. Now you can install it in visual studio.

#### Import from Release Package
mdk sdk can be imported by vs projects. Insert the following line in your vcxproj as the last element of `Project` (assume mdk-sdk is in the same dir as vcxproj)

    <Import Project="mdk-sdk\build\native\MDK.targets" Condition="Exists('mdk-sdk\build\native\MDK.targets')" />


Once installed or imported, necessary compile flags and link flags will be added, runtime dlls will be copied to output dir.

### Use in CMake Projects
```
	include(mdk-sdk-dir/lib/cmake/FindMDK.cmake)
	target_link_libraries(your_target PRIVATE mdk)
```

### Qt qmake project
```qmake
include($$MDK_SDK_DIR/mdk.pri)
```


### Recommended settings
```cpp
    player.setDecoders(MediaType::Video, {"MFT:d3d=11", "D3D11", "hap", "FFmpeg", "dav1d"});
```

### [Runtime Requirements](https://github.com/wang-bin/mdk-sdk/wiki/System-Requirements#uwp)
Optional:
- libEGL.dll, libGLESv2.dll, D3DCompiler_47/43.dll. Qt apps can use qt's dlls

### [Supported Graphics APIs:](https://github.com/wang-bin/mdk-sdk/wiki/Render-API)
- D3D11: recommended
- D3D12
- [OpenGL ES2/3](https://github.com/wang-bin/mdk-sdk/wiki/OpenGL-Support-Matrix): via ANGLE or others. The default if EGL runtime is found.
- Vulkan(No UWP)

### [Supported Decoders:](https://github.com/wang-bin/mdk-sdk/wiki/Decoders)
- [FFmpeg](https://github.com/wang-bin/mdk-sdk/wiki/Decoders#ffmpeg). options: threads=N. e.g. -c:v FFmpeg. -c:v FFmpeg:threads=4
- [MFT](https://github.com/wang-bin/mdk-sdk/wiki/Decoders#mft). options: d3d=0/9/11/12, pool=0/1. e.g. -c:v MFT(software), -c:v MFT:d3d=11(hardware) or MFT:d3d=12.
- [D3D11](https://github.com/wang-bin/mdk-sdk/wiki/Decoders#d3d11): via FFmpeg
- [hap](https://github.com/wang-bin/mdk-sdk/wiki/Decoders#hap)

## Source code:
- [some examples using mdk sdk](https://github.com/wang-bin/mdk-examples)
- [OBS Studio plugin](https://github.com/wang-bin/obs-mdk)
- [QtMultimedia plugin](https://github.com/wang-bin/qtmultimedia-plugins-mdk)
- [MFT decoder module](https://github.com/wang-bin/mdk-mft)
- [dav1d decoder module](https://github.com/wang-bin/mdk-dav1d)
- [Blackmagic RAW](https://github.com/wang-bin/mdk-braw)
- [R3D RAW](https://github.com/wang-bin/mdk-r3d)


Copyright (c) 2016-2025 WangBin(the author of QtAV) <wbsecg1 at gmail.com>
Free for opensource softwares, non-commercial softwares, flutter, QtAV donors and contributors.