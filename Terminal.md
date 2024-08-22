# 如何創建光盤映像
# How to create disc image
## DVD
Using terminal command
```bash
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
```bash
# install cdrdao to get device(cd drive) bus information
brew install cdrdao cdrkit
```

#### use drutil to get drive info for parameter dev=1,0,0 in cdrecord
```
drutil status
```
#### use cdrecord to create audio bin file (dump the disc to file)
```bash
sudo cdrecord dev=1,0,0 -dao -v -isosize /volumes/ram/XXXXXXX.bin
```
#### use cdrdao scanbus to get the device hardware information
```bash
cdrdao scanbus
```
#### use cdrdao to output toc from disc image
```bash
cdrdao read-cd --device "IOService:..." --datafile /Volumes/Ram/XXXXXXX.bin /Volumes/Ram/XXXXXXX.toc
```
#### use toc2cue to convert toc to cue 
```bash
toc2cue /Volumes/Ram/VIRIYACDa.toc /Volumes/Ram/VIRIYACDa.cue
```

### 支持從光碟創建映像文件的軟件：
### Software that can create image from disc supporting DVD
[Burn](https://burn-osx.sourceforge.io/Pages/English/home.html)

# 關於截圖
MacOS 預設截圖是 png 格式，好處是畫面質量高，但比較佔用空間。如果想改成 jpeg 格式，可以在終端機 (Terminal) 下輸入：

```bash
defaults write com.apple.screencapture type jpg
```
如果想改回來，只要把 jpg 改成 png 就可以了。

# 與系統設定相關的用法
# System Settings Related
#### 如何在二進制和XML文本格式之間轉換macOS plist設置文件
#### How to convert macOS plist settings file between binary and xml text format
```bash
# convert to plain xml format
plutil -convert xml1 XXXXXX.plist

# convert to binary format
plutil -convert binary1 XXXXXX.plist

# get the menu of plutil
man plutil
```

#### File Operations
#### 檔案處理
```
# Display file type.
file -I ~/Desktop/something

# Network
#### 如果連接埠被使了，想知道甚麼在使用的方法
#### How to check what process is using an exsiting port
```bash
sudo lsof -i -P | grep LISTEN | grep :5000

# example@Sonoma 14.6.1
ControlCe  658       someone   10u  IPv4 0xXXXXXXXXde34f2b      0t0    TCP \***:5000** (**LISTEN**)
ControlCe  658       someone   11u  IPv6 0xXXXXXXXX522241c      0t0    TCP \***:5000** (**LISTEN**)
```

# Conda
#### 建立虛擬 Python 環境的方法
#### Add a virtual python environemnt
```bash
# 使用時，請更改所需的環境名稱和 python 版本
conda create -n ENVIRONMENT_NAME python=3.8.5
```

#### 移除虛擬環境的方法
#### Remove an environment
```bash
conda remove --name ENV_NAME --all
```

#### 將當前 Python 環境的情式包寫入 requirements.txt 的方法
#### How to create the requirements.txt from the current python environment
```bash
pip freeze > requirements.txt
```
