# Hacking with Google Assistent

## Table of Content
1. [Hardware](#Hardware)
2. [Change Hotword](#Change Hotword)
3. [Start without Hotword](#example2)
4. [Save Conversation States](#third-example)


## Hardware 
* Raspberry Pi 3
* Usb Microphone
* Speaker
* Ulatrasonic sensor


## Change Hotword   
To give our a Assistent a personal prefered name, we use [snowboy.kitt.ai](www.snowboy.kitt.ai).

* Signup at [snowboy.kitt.ai](www.snowboy.kitt.ai)
* Create your own hotword
* Connect to Rasperry Pi via ssh
* Configure audio devices
	* ```arecord -l``` to get microphone device number
	* ```aplay -l``` to get speaker device number
	* configure ```~/.asoundrc``` whit the device numbers you just got
	```json
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
* Download snowbow tar file from [here](http://docs.kitt.ai/snowboy/#downloads) 
* extract tar file with ```tar -xvf rpi-arm-raspbian-8.0-1.2.0.tar.bz2```
* Install requirement packages:
```
sudo apt-get install python-pyaudio python3-pyaudio sox
sudo apt-get install libatlas-base-dev
pip install pyaudio
```
* Run demo with:
	```
	python demo.py yourtrainedmodel.pmdl
	```
	while yourtrainedmodel.pmdl is the file you downloaded from [snowboy](www.snowboy.kitt.ai)
* Fix possible errors:
	* with PulseAudio
	https://github.com/Kitt-AI/snowboy/issues/9
	* with X11 Display
	```export DISPLAY=:0```



	


## Example2
## Third Example