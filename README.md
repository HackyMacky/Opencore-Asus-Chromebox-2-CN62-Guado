# Opencore-Asus-Chromebox-2-CN62-Guado
A repository of Opencore configuration for Asus Chromebox 2 CN62 Guide

## DISCLAIMER 
I will not be held responsible for any damage, permanent loss of data or any sorts of consequences that may arise by using my configuration files on your devices. Please use at your own risk.

## Current Release
- Opencore 0.8.6
- Monterey 12.6.1 (Recommended)
- Ventura 13.0.1 (Read Ventura footnote below)
- All latest kexts as of Nov 10, 2022

## Notebook Specifications

| Specification  | Model |  Remark  |
| ------------- | ------------- | ------------- |
| FW  | Mr.Chromebox's CoreBoot | 4.18  |
| CPU  | Intel i7-5500U  |
| iGPU  | Intel HD 5500 | 
| Storage  | Transcend 512GB M.2 2242 SSD  |
| RAM  | 16GB (2x4GB) PC3L |
| Ethernet  | Realtek RTL8111 |
| Wi-Fi  | Fenvi BCM94360NG + Fenvi F-C25NG (Mini PCIe to M.2 adapter)  |
| Bluetooth  | Intel Bluetooth   |
| Audio  | HD5500 + Realtek   |


## What's working
- AppleID and iServices
- Apple continuity and handoff features (requires a native wifi NIC)
- Wi-Fi & Bluetooth, Ethernet
- Display outputs (DP + HDMI)
- Hardware acceleration (Monterey and below)
- Headphone jack, microphone
- USB ports mapping
- Sleep/Wake
- SD Card reader

## What's not working
- Hardware acceleration (Ventura and newer)

## Not tested
- N/A

## Quirks/issues
- Prior to using Fenvi F-C25NG (Mini PCIe to M.2 adapter), I used a generic oem adapter to connect my Fenvi BCM94360NG. This worked fine for wifi but bluetooth and continuity/handoff features were really poor or unreliable. After switching to Fenvi F-C25NG adapter, everything worked well and Airpods and other bluetooth connectivity has been excellent. I would highly recommend using this adapter.

- Hardware acceleration on Ventura does not work. Only way to fix is to patch via OCLP but with some tradeoffs (not recommended). See Ventura footnote below.

## Ventura Footnote
1. You can upgrade or directly install Ventura (tested with 13.0.1 as of Nov 10, 2022) but you will not have hardware acceleration as Broadwell graphics tend to stop being supported in Ventura.
2. To get hardware acceleration on Ventura, you can perform a root patch using Opencore Legacy Patcher (OCLP) however you will loose SIP & AMFI
3. If OCLP requires to disable SIP, AMFI and Secure Boot, you will need to change the following values in config.plist
- Misc > Security > SecureBootModel > Disabled
- NVRAM > Add > 7C436110-AB2A-4BBB-A880-FE41995C9F82 > boot-args > amfi_get_out_of_my_way
- NVRAM > Add > 7C436110-AB2A-4BBB-A880-FE41995C9F82 > csr-active-config > FF0F0000
4. Once the above values have been changed, restart and reset NVRAM
5. Once back in macOS, you can proceed to root patch using OCLP and restart. 
6. Hardware acceleration should work after restart.
7. Do take note, that you cannot enable back SIP or remove the amfi_get_out_of_my_way boot-args. You can however enable back secureboot. If you try to revert back the changes done in Step 3 (for SIP and AMFI), the hackintosh will not boot to macOS.

## Credits
- All credits & rights goes to the maintainers, contributors and developers of the Opencore project and respective kernel extensions.
- MrChromebox for Coreboot/Tianocore
- Apple Inc.
