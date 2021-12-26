# AltServer-Linux
AltServer for AltStore, but on-device

## Build Instruction

- Preparation: `git clone --recursive https://github.com/D-06/AltServer-Linux`

- Install corecrypto_static
  - https://developer.apple.com/security/
        - Download corecrypto source (2020 OS Releases)
    ```
    cd corecrypto; sed -i "/mach_time.h/d" corecrypto_test/include/ccshadow_decls.h
    mkdir b; cd b; CC=clang CXX=clang++ cmake ..; make; sudo make install; cd ../..
    ```
- need to install this
  ```
  sudo apt install libcpprest-dev xxd uuid-dev libzip-dev usbmuxd libimobiledevice6 libimobiledevice-utils 
  ```
- Build Configuration 1 (AltServer): Simple AltServer running on normal Linux host, working through usbmuxd
  ```
  make NO_USBMUXD_STUB=1 NO_UPNP_STUB=1
  ```
  
- Build Configuration 2 (AltServerNet): AltServer running on normal Linux host, working through manually specifying IP
  ```
  make NO_UPNP_STUB=1
  ```

- Build Configuration 3 (AltServerUPnP): AltServer running on iSH, working through manually specifying IP in a UPnP enabled router
  ```
  make
  ```

## Usage

- For build configuration 1 (AltServer): Works just like a normal AltServer on windows
  - Install IPA: `./AltServer -u [UDID] -a [AppleID account] -p [AppleID password] [ipaPath.ipa]`
  - Running as AltServer Daemon: `./AltServer`
- For build configuration 2 (AltServerNet): AltServer over Network
  - Install IPA: `./AltServerNet -u [UDID] -P [jitterbug pair file] -i [device IP] -a [AppleID account] -p [AppleID password] [ipaPath.ipa]`
  - Running as AltServer Daemon not supported
- For build configuration 2 (AltServerUPnP): AltServer over Network
  - Install IPA: `./AltServerUPnP -u [UDID] -P [jitterbug pair file] -i [device IP] -a [AppleID account] -p [AppleID password] [ipaPath.ipa]`
