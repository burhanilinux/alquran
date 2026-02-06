# Windows packaging

This directory contains the Qt Installer Framework (QtIFW) configuration for
building the **online** Windows installer.

## Prerequisites

- Qt 6.x (with Qt Multimedia and image formats)
- CMake + MSVC build tools
- [Qt Installer Framework](https://doc.qt.io/qtinstallerframework/)

## Build the application

```powershell
mkdir build
cd build
cmake.exe -DCMAKE_PREFIX_PATH="C:\Qt\6.x.x\msvc_2019" -DCMAKE_BUILD_TYPE=Release ..
cmake.exe --build . --config Release
```

## Prepare the online installer

1. Update the version numbers in:
   - `dist/windows/online-installer/config/config.xml`
   - `dist/windows/online-installer/packages/com.zer0x.qurancompanion/meta/package.xml`
2. Ensure the remote repository in `config.xml` points at the published Windows
   package feed.
3. Create the installer with `binarycreator`:

```powershell
binarycreator.exe ^
  --config dist\windows\online-installer\config\config.xml ^
  --packages dist\windows\online-installer\packages ^
  Quran_Companion_Online_Installer.exe
```

The output executable is a lightweight online installer that downloads the
application components from the configured repository.
