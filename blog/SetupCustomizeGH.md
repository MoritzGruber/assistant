# Setup and Customize your own Google Home

In this article I will show you how to setup your own goolge home on your raspberry pi or any other linux computer. 
Further I will teach you a hack how can create own triggers and hotwords for you assistant. 

## Hardware

Before we start, make sure you have connected a microphone and speakers to your device. A regular usb webcame will also to the trick. 

To check if the devices are actual connected we use the command:

```bash
arecord -l
``` 
To check the microphone and 
```bash
aplay -l
``` 
for the speakers

At this point it is importend that you remember the card number and device number of the microphone and speaker you choosen to use.

This gained numbers we now have to write in our configuartion file under ~/.asoundrc:
```bash
pcm.!default {
    type asym
    playback.pcm {
        type plug
        slave.pcm "hw:1,0"
    }
    capture.pcm {
        type plug
        slave.pcm "hw:0,0"
    }
}
``` 
*Where the two numbers after **hw:** are the card number follwed by the device number and should be replaced by your own values*

More information about the ALSA sound configuration can be found [here](https://wiki.ubuntuusers.de/.asoundrc/)

Now you should be able to record sound with:
```bash
rec test.wav
``` 
and hear you own voice with:
```bash
play test.wav
``` 

## Google Assistant 

### Google API Registeration

### Install Google Assistant Client

### Authentification with google cloud

### Run the sample

## Custom Trigger

### Snowboy

### Create Hotword

### Python3 Support 

### Trigger Google Assistant with Snowboy

