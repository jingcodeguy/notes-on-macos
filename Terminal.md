# 如何創建光盤映像
# How to create disc image
## DVD
Using terminal command
```
# start to burn

# to check your dvd drive path
diskutil list # eg dev/disk2

# unmount the disk so that it will not be used by any app
diskutil unmountdisk /dev/disk2
dd if=/dev/disk2 of=XXXXXXXX.iso bs=2048

# after finish
diskutil eject /dev/disk2
```

## Audio CD
Using terminal command

To obtain bin and cue files like Windows famous tools imgburn does, can use the following method (So far, cannot find other GUI tools to achieve the same thing)
1. install CDRDAO  CDRKIT
2. use drutil to get drive info for parameter dev=1,0,0 in cdrecord
3. use cdrecord to create audio bin file
4. use cdrdao scanbus to get the device hardware information
5. use cdrdao to output toc from disc image
6. use toc2cue to convert toc to cue (toc2cue included in cdrkit)

#### install CDRDAO  CDRKIT
```
# install cdrdao to get device(cd drive) bus information
brew install cdrdao cdrkit
```

#### use drutil to get drive info for parameter dev=1,0,0 in cdrecord
```
drutil status
```
#### use cdrecord to create audio bin file (dump the disc to file)
```
sudo cdrecord dev=1,0,0 -dao -v -isosize /volumes/ram/XXXXXXX.bin
```
#### use cdrdao scanbus to get the device hardware information
```
cdrdao scanbus
```
#### use cdrdao to output toc from disc image
```
cdrdao read-cd --device "IOService:..." --datafile /Volumes/Ram/XXXXXXX.bin /Volumes/Ram/XXXXXXX.toc
```
#### use toc2cue to convert toc to cue 
```
toc2cue /Volumes/Ram/VIRIYACDa.toc /Volumes/Ram/VIRIYACDa.cue
```

### 支持從光碟創建映像文件的軟件：
### Software that can create image from disc supporting DVD
[Burn](https://burn-osx.sourceforge.io/Pages/English/home.html)



# 與設定相關的用法
# Settings Related
#### 如何在二進制和XML文本格式之間轉換macOS plist設置文件
#### How to convert macOS plist settings file between binary and xml text format
```
# convert to plain xml format
plutil -convert xml1 XXXXXX.plist

# convert to binary format
plutil -convert binary1 XXXXXX.plist

# get the menu of plutil
man plutil
```
