# SeedSigner Emulator (Monero signer fork version)

## This is a fork of the original emulator created by [@EnteroPositivo](https://twitter.com/enteropositivo). The fork is meant to constain any changes made to the new project.


> Allows to execute [SeedSigner](https://github.com/SeedSigner) air-gapped hardware wallet in your desktop (windows/linux/mac)

![](img/ubuntu.png)
![](img/moneroSigner1.png)
![](img/moneroSigner2.png)


## How it works
I made a new display driver that replaces the existing _SeedSigner ST7789 1.3_ driver, making possible to execute the device in a desktop enviroment.

>Use it with the integrated buttons or with your keyboard ( Arrow Keys, Enter, 1,2,3 )

I have tried to make it as non-invasive as possible so that the emulator can be used with other versions of Seedsigner with as little effort as possible.

![](img/demo.gif)



## Launch from source

**1-** Clone [SeedSigner](https://github.com/SeedSigner/seedsigner) repository

```sh
git clone https://github.com/SeedSigner/seedsigner.git
cd seedsigner/src
```

**2-** Convert it into a desktop application

_Option 1_

Download the contents from this respository [Seedsigner emulator (.zip)](https://github.com/enteropositivo/seedsigner-emulator/archive/refs/heads/master.zip) and merge the contents of the folder

![](img/tree_content.png)

with the existing **seedsigner** content you cloned in step 1.


**OR**

_Option 2_

using command line

```sh
git clone http://github.com/enteropositivo/seedsigner-emulator.git
rsync -a seedsigner-emulator/seedsigner ./
```


**3-** Install the following requeriments:
(I am working on freezing these requirements into one repo/in my org to prevent supply chain risk)

The pyzbar fork is the one used by seedsigner. It is a fork of the original package since the original package
does not allow for bytes instead of strings on binary encoded data. 

```sh
python3 -m pip install --upgrade Pillow
python3 -m pip install --upgrade setuptools
sudo apt-get install python3-tk
sudo apt install libzbar0
python3 -m pip install -e git+https://github.com/jreesun/urtypes.git@e0d0db277ec2339650343eaf7b220fffb9233241
python3 -m pip install -e https://github.com/seedsigner/pyzbar.git@c3c237821c6a20b17953efe59b90df0b514a1c03#egg=pyzbar
pip3 install embit dataclasses qrcode tk opencv-python
sudo apt-get install python3-pil python3-pil.imagetk
```
**4-** Launch the emulator
```sh
python3 main.py
```

## ZBar library for Windows

If your are using the code on windows platform you should download ZBar library v0.23.91 from [https://github.com/enteropositivo/pyzbar/releases/tag/v0.1.10-ss](https://github.com/enteropositivo/pyzbar/releases/tag/v0.1.10-ss) and its dependencies to  **/src/pyzbar/pyzbar/**



## Making a standalone executable ( Optional )

You'll need to install PYinstaller to be able to generate an executable for your OS.

```sh
pip3 install pyinstaller
```
go to your proyect main forlder where _main.py_ stands and execute the following command

```sh
pyinstaller --clean --add-data seedsigner\\resources;seedsigner\\resources main.py
```
If you found an error **unable to execute command pyinstaller** try using the following command

```sh
python3 -m pyinstaller --clean --add-data seedsigner\\resources;seedsigner\\resources main.py
```

**Note:** I'll upload releases for linux and windows


## Intalling on TAILS OS

**Use**
```sh
torsocks pip3 install ...
```
**Instead**
```sh
pip3 install ...
```


## :lock: Security tips
- **Don't use it for real transactions**
- This emulator is made for testing Seedsigner source code on your desktop.   
- You can modify or contribute to seedsigner without the need to upload the code to a  Raspberry Pi Zero each time



## Pending Tasks

- [x] Fix screen saver
- [ ] Fix keyboard capture on Linux (on windows works ok)
- [x] Allow desktop webcam
- [ ] Test command to make a **one file** standalone executable
- [ ] Fix reading QR from desktop webcam




## Contact

Follow me on Twitter – [@MoneroSigner](https://twitter.com/MoneroSigner)
