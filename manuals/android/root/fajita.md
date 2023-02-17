---
title: Fajita Custom Root + Update Help
description: 
published: true
date: 2023-02-17T19:59:35.508Z
tags: android
editor: markdown
dateCreated: 2023-01-15T18:57:57.353Z
---

# Introduction
Uncategorized links:

- https://github.com/topjohnwu/Magisk/issues/5299
- https://wiki.lineageos.org/devices/fajita/install
- https://download.lineageos.org/fajita
- https://topjohnwu.github.io/Magisk/install.html#patching-images



# Re-Root after update
<br>

## Prerequisites

Make sure you have the following installed on your computer:
- adb
- python =< 3

Make sure you have installed the update and rebooted the device using the default method before you follow the steps.
<br>
<br>

## Steps

1. Download [LineageOS/scripts](https://github.com/LineageOS/scripts) off of Github.
2. Install the [latest update](https://download.lineageos.org/fajita) of LineageOS.
3. Extract `payload.bin` from the .zip and move it to the root directory of the downloaded repo.
4. In the root directory of the repository, execute the following command.

```bash
python ./update-payload-extractor/extract.py payload.bin --output_dir ./output
```

5. Navigate to the `output` folder. 

6. Push your `boot.img` to the device:

```bash
adb push ./boot.img /sdcard
``` 

7. Magisk: patch from file. Select `boot.img`.

8. After it's done, pull your patched image and flash the magisk_patched file.

```
adb pull /sdcard/Download/magisk_patched-25200-<SOME-STRING-HERE>.img
```

```
adb reboot fastboot
```

```
fastboot flash --slot=all boot magisk_patched-<SOME-STRING-HERE>.img
```

9. Finally, reboot the device through the Device's screen. 


