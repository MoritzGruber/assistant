# Setup your own Google Home and custom Hotwords

In this article I will show you how to setup your own goolge home on your Raspberry Pi or any other linux computer. 
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
First if you don't have an google account already, create one. After you are logged in to the google devloper console, create a new project. Now we have to enable the [Assistant API](https://console.developers.google.com/apis/api/embeddedassistant.googleapis.com/overview). To create our OAuth ClientID we have to go [here](https://console.developers.google.com/apis/credentials/oauthclient). Select *Other* and when you finshed download the json file. 
You can transfer the file to your Raspberry Pi with:
```bash
scp ~/Downloads/client_secret_client-id.json pi@raspberry-pi-ip-address:/home/pi/
```

### Install Google Assistant Library
To download and install the libarary with a python3 enviroment we use the folling script:
```bash
sudo apt-get update
sudo apt-get install python3-dev python3-venv # Use python3.4-venv if the package cannot be found.
python3 -m venv env
env/bin/python -m pip install --upgrade pip setuptools
source env/bin/activate
python -m pip install --upgrade google-assistant-library
python -m pip install --upgrade google-auth-oauthlib[tool]
```


### Authentification with google cloud
Before we can use the assistant we first have to autherize our application. To do this we call:
```bash
google-oauthlib-tool --client-secrets /path/to/client_secret_client-id.json --scope https://www.googleapis.com/auth/assistant-sdk-prototype --save --headless
```
You will recive a code on a website that you have to enter in the terminal.

### Run the sample
Once you authorized your application, you can now run the sample from google.
```bash
google-assistant-demo
```
You now have a build regular google home and can trigger your assistant with *"OK, Google"* or *"Hey, Google"*.

## Custom Trigger
Since we are building our Google Home on our own, we are open to customization. So we will create our own Trigger. While others use a button to trigger there Assistant, I still want to use voice. I just wasn't so happy with the hotword, so I changed replaced it with something more sympathetic to me: *"Samantha"*, but you can choose anything you like. 

### Snowboy
![Snowboy](./snowboylogo.png)
To create our own personal trained model for hotword detection we use the [Snowboy Engine](https://snowboy.kitt.ai/)

### Create Hotword
Once you are logged in you have the option to choose a existing hotword or create your own. 
In any case you will recive the model as file to download. After downloading you also need to transfer this file to your Raspberry Pi.

### Python3 Support
Unfortunately [Snowboy](https://snowboy.kitt.ai/) just deliver exceutable binarys for Python 2. To work with our Python 3 Google Assistant Library we need to build the binary on our own. To do this we first clone the Snowboy github reporsitory:
```bash
git clone https://github.com/Kitt-AI/snowboy.git
```
First we have make the snowboydetect.py file with swig in the directroy */swig/python3/*

*The following commands may be diffrent for you, depending on your linux distribution and already installed packages.*
```bash
TODO
```
 After successful build you shound run the Snowboy sample under *examples/Python3/* with:
 ```bash
python demo.py your-traine-model.pmdl
 ```    

### Trigger Google Assistant with Snowboy
The Last step is to connect Snowboy with the Google Assistant. That means when Snowboy detects your hotword, it will actevate the Google Assistant, so he starts listening imeadeatly, like you already said *"OK, Google"*. 

![Architecture](./architecturesnowboy.png)

First we change the snowboy demo.py file to call the google library:
```python
TODO
```

After that we modify the google library file at the end in you python enviroment under */TODO///*.
Replace 
```python
TODO
```
with 
```python 
TODO
```
Now you should be able to trigger you assistant with your own hotword by running the snowboy *demo.py*.
You will also find the excact files and the whole project on [Github](TODO)


### Conclusion
Hope you got some inspiration for further expirements with the Google Assistant. Another intresting point is for exaple to jump strait in your own google voice app.
If you want to know how to build a google voice application, check out my other post [here](TODO)

Thanks for reading through my post. For feedback or questions feel free to contact me. 




#### Cheers!

#### Moritz Gruber

[Website]()

[Github]()

[Twitter]()


