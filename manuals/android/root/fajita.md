---
title: Fajita Custom Root + Root
description: 
published: true
date: 2023-01-24T12:28:20.948Z
tags: 
editor: markdown
dateCreated: 2023-01-15T18:57:57.353Z
---

# Introduction
Your content here

https://github.com/topjohnwu/Magisk/issues/5299

https://wiki.lineageos.org/devices/fajita/install

https://download.lineageos.org/fajita

https://topjohnwu.github.io/Magisk/install.html#patching-images


# Re-Root after update

Download [LineageOS/scripts](https://github.com/LineageOS/scripts) off of Github.

Install the [latest update](https://download.lineageos.org/fajita) of LineageOS.

Extract `payload.bin` from the .zip and move it to the root directory of the downloaded repo.


In the root directory of the repository, execute the following command.

```bash
python ./update-payload-extractor/extract.py payload.bin --output_dir ./output
```

Navigate to the `output` folder. 

Push your `boot.img` to the device:

```bash
adb push ./boot.img /sdcard
``` 

Magisk: patch from file. Select `boot.img`.

After it's done, pull your patched image and flash the magisk_patched file.

```
adb pull /sdcard/Download/magisk_patched-25200-<SOME-STRING-HERE>.img
```

```
adb reboot fastboot
```

```
fastboot flash --slot=all boot magisk_patched-<SOME-STRING-HERE>.img
```

Finally, reboot the device through the Device's screen. 


