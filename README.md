# pi-pd-synth
A uni project: the movie: the game: the sequel.

- [Things you'll need](#things-youll-need)
- [Installation guide](#installation-guide)
  - [Baking Pi](#step-1-baking-pi)
  - [Making a connection](#step-2-making-a-connection)
  - [Entering the Pi-trix](#step-3-entering-the-pi-trix)
  - [Changing the rules](#step-4-changing-the-rules)
  - [Gorgeous VNC Viewer ahead](#step-5-gorgeous-vnc-viewer-ahead)
  - [Pure Data](#step-6-pure-data)
  - [Midi and Audio](#step-7-midi-and-audio)
  - [Synth-time](#step-8-synth-time)
  
# Things you'll need
- Raspberry Pi (we used the fourth iteration of the microprocessing unit commonly known as the Raspberry Pi)
- adapter to power your Pi
- micro SD card, at least 8gb
- ethernet cable
- usb to ethernet adapter
- audio interface (we used a Focusrite Scarlett 2i4)
- midi controller of some sort
- a device – or more precisely: a transducer – that converts sound into an electrical signal (you might call it a microphone)
- speakers

# Installation guide
#### Step 1: Baking Pi
Download a Raspbian image from the [Raspberry Pi site](https://www.raspberrypi.org/downloads/raspbian/). We recommend Raspbian Buster with desktop. Write your downloaded image to your SD card. On Windows you can use [Rufus](https://rufus.ie/). To enable SSH you'll need to a make an empty file called `ssh` (without an extension!) and place it in the root of your SD card. That's it, really.

#### Step 2: Making a connection
Now it's time to grab your ethernet cable and usb to ethernet adapter. Connect the ethernet cable to your adapter and Pi. Connect the usb to your already working computer. To allow your Raspberry Pi to connect to the internet, you'll need to share your already working computer's internet connection with your Pi. On Windows you'll need to change your adapter properties like this:

![haha](https://github.com/nooisy/pi-pd-synth/blob/master/img/share.png)

#### Step 3: Entering the Pi-trix
Open up your favorite terminal. You can use PowerShell if you're on Windows (perhaps consider changing the [color scheme](https://draculatheme.com/powershell/) to make it actually readable). Stretch your fingers, we're going to start typing!
```
ssh pi@raspberrypi.local
```
The default password is `raspberry`. You won't see letters or * appearing when typing your password - don't worry, your keyboard is still working! You'll probably get a prompt yabbering about so-called [ECDSA fingerprints](https://en.wikipedia.org/wiki/Public-key_cryptography). To shut it up, answer with a confident `yes`. If all went well you'll now be logged into your Pi!

<p align="center">
  <img src="https://github.com/nooisy/pi-pd-synth/blob/master/img/pitrix.png" alt="haha">
</p>

#### Step 4: Changing the rules
Let's make our stay a more comfy one by configuring some options. It's handy to maximize your terminal window for the coming steps. We're going to run a program requiring special security privileges. That means that we need to prepend our command with the `sudo` ([superuser do](https://en.wikipedia.org/wiki/Sudo)) command:
```
sudo raspi-config
```
You'll be greeted by a big menu:

![haha](https://github.com/nooisy/pi-pd-synth/blob/master/img/bigmenu.png)

You can navigate through the menu with the arrow keys. Select option 5 and enable `P3 VNC`. You could also consider other options like changing your password and locale, or enabling Wi-Fi. This is not in the scope of this manual though, so let us move on!

#### Step 5: Gorgeous VNC Viewer ahead
First things first, [download](https://www.realvnc.com/en/connect/download/viewer/) and install VNC Viewer on your already working computer. 

If you were wondering how the last step made our stay more comfy: fret not, you'll find out right now. Escape the big menu and return to the regular terminal environment. To start VNC Viewer, simply type `vncserver` (on a Pi 4 you might run into some resolution problems, `vncserver-virtual -randr=1920x1080` may solve that). Your terminal will spit out a bunch of text, but we only need the last bit:
```
New desktop is raspberrypi:1 (*IP-address:port*)
```
Your desktop might have a different name. Make sure to use that one and not the one above. Open up VNC Viewer and let's connect to your Pi.

![haha](https://github.com/nooisy/pi-pd-synth/blob/master/img/vnc.png)

Login with your username and password. Now you can comfyily navigate your Pi!

![haha](https://github.com/nooisy/pi-pd-synth/blob/master/img/desktop.png)

#### Step 6: Pure Data
Installing Pure Data is easy as Pi:
```
sudo apt-get install pd
```
If you want a more up-to-date and extensive version of Pure Data, we can recommend [Purr Data](https://github.com/agraef/purr-data/wiki/Installation#raspbian) (which is also slightly less easy to install).

#### Step 7: Midi and Audio
To configure midi we need to use a program called `aconnectgui`. You might not have it installed, so just in case:
```
sudo apt-get install aconnectgui
```
You can plug-in your midikeyboard now and start Pure Data. Open the preferences window (Ctrl + P) to select your audio interface as I/O and make sure that you're using the ALSA audio api.

<p align="center">
  <img src="https://github.com/nooisy/pi-pd-synth/blob/master/img/pdaudio.png" alt="haha">
</p>

Hop over to the MIDI tab, set the midi api to the ALSA one and both ports to channel 1.

<p align="center">
  <img src="https://github.com/nooisy/pi-pd-synth/blob/master/img/pdmidi.png" alt="haha">
</p>

To make use of these channels we need to run `aconnectgui` to connect them to your midikeyboard. You can do this by clicking on the cable-icon and drawing the right lines between the corresponding channels.

<p align="center">
  <img src="https://github.com/nooisy/pi-pd-synth/blob/master/img/alsa.png" alt="haha">
</p>

#### Step 8: Synth-time
Almost there! Download this repository using `git`:
```
git clone https://github.com/nooisy/pi-pd-synth.git
```
Open the `main.pd` patch and start having fun!

![haha](https://github.com/nooisy/pi-pd-synth/blob/master/img/pdend.png)
