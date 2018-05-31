---
layout: post
title: "Convert .ARW to jpeg and reduce size in a folder"
category: "memo"
date: 2018-05-31 10:09:57
tags:
- osx
---

# Convert all the .ARW images in a specific folder

```
cd path/to/images/folder
for i in *.ARW; do sips -s format jpeg -s formatOptions 70 "${i}" --out "${i%ARW}jpeg"; done
```

# Reduce all images

```
sips -Z 640 *.jpeg
```

# sources

- [Use sips to quickly, easily—and freely—convert image files](https://robservatory.com/use-sips-to-quickly-easily-and-freely-convert-image-files/)
- [Batch Resize Images Quickly in the OS X Terminal](https://lifehacker.com/5962420/batch-resize-images-quickly-in-the-os-x-terminal)

