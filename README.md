I have made some changes. First of all, thanks for the great preparatory work!
I have adapted this because of my personal needs.
Hardware:
ESP32-S3 mini

Pinout:
Microphone and amplifier use a common I2S 
GPIO 3 lrclk
GPIO 4 bclrk
GPIO 5 Din of the micro
GPIO 7 Dout of the amplifier
GPIO 8 Din of the (8) LEDs

Thanks to AI support, I have adapted the rest to the current version of ESPHome.

I used a small Halloween skull as the housing, hence the name of the voice assistant.  

Code under V4

Hier is the project I started from: 

# ESP-Assistant
An ESP32 S3 voice assistant for Home Assistant. Light weight and should compile on low end systems.

The main goal of this project was to create a voice assistant (VA) for HA that is not depending on external files*. A second requirement was that for compiling you don't need much resources. This yaml compile many times faster then the ESP32-S3_box version. This version of the voice assistant is also capable to set multiple timers.

_* There is one small dependency in the code if you want a sound when a timer is finished. This dependecy is only there when compiling. A future release may solve this. For now this isn't a big show stopper_

**UPDATE Version 2**

While version 1 works it still suffered from stalls from time to time.
The ESP32-S3-BOX version that I also have showed to be far more stable. Because of this I abandoned to 'no external files' concept and went for the full blown version and took the ESP32-S3-BOX version as start. I stripped everything that deals with the screen and the buttons on the box. I've added my own sensors and other tools. Things I like to see and control in HA such as diagnostics, request and response sensors and timer info. The hisardware stayed the same so this installs directly on the VoicePuck. This version is a lot heavier when compiling. My advise is to start with cleaning your build files and start compiling. When it fails just restart again. File locks will occure but they will be cleared. Files that are already compiled will be skipped so the processor load on lower end systems will handle in the end a full compile.

**UPDATE Version 3**

This the latest version. It is nearly the same as version 2 but this one makes it possible to have a continues conversation.

**Hardware needed**
- CPU: ESP32-S3 mini
- Mic: INMP441
- Amp: MAX98357A
- Led: 3 WS2812B leds.
- Speaker: 40mm Headset Driver Hifi Headphone Speaker Unit 32ohm [AliExpress](https://www.aliexpress.com/item/1005001352277084.html)

I've include the schematic that I used and placed it in the media folder. It follows to general approach for this setup but i had to use 2 diffentent pins to get it working reliably.
Schematic is based on the one found [here](https://smarthomecircle.com/How-to-setup-on-device-wake-word-for-voice-assistant-home-assistant#circuit-diagram-for-esp32-s3-with-inmp441-microphone--max98357a-audio-amplifier)

**UPDATE Version 4**

Pinout: Microphone and amplifier use a common I2S 
- GPIO 3 lrclk 
- GPIO 4 bclrk 
- GPIO 5 Din of the micro 
- GPIO 7 Dout of the amplifier 
- GPIO 8 Din of the (8) LEDs

Thanks to AI support, I have adapted the rest to the current version of ESPHome.

**Requirements**
- Home Assistant
- ESPHome installed

**Setup**
Go to your config/esphome folder
Create a folder and name it sounds
Place the sounds file(s) there

Have a look at the yaml file and change the following substitution for the wake word you want.
At the moment okay_nabu, hey_jarvis and alexa are the available options

_  micro_wake_word_model: okay_nabu _

And don't forget to create your secret SSID een password for the wifi section

  ssid: !secret wifi_ssid
  
  password: !secret wifi_password

  
I've include the 3D print files for the body and the cover. I used a resin printer for these.
Version 2 has a bit better wire management.

![VoicePuck-top](https://github.com/user-attachments/assets/860735a3-23ba-4d62-90ca-2ab0160d5e5d)

![VoicePuck-bottom](https://github.com/user-attachments/assets/b499539f-c70a-4596-942c-3c0e93b9055e)

For comparison this is a Voice puck with with a dark cover which is perforated to let the light shine through.
Left the Google home version, right the ESP Assistant

![VoicePuck-GoogleHome](https://github.com/user-attachments/assets/5bf028dc-2269-41cd-9bdd-1a9a011f9e1a)

You can choose your cover freely. This one has a light wooden vineer cover. 
This thin wood let the light shine through without a problem.

![VoicePuck-white](https://github.com/user-attachments/assets/48c8b008-5497-4cdd-bbc0-d8b4e1e2929a)

![20240810_091030](https://github.com/user-attachments/assets/dab989f1-f182-4e96-a11f-3fbb608e9481)

[Infinity VoicePuck](https://www.youtube.com/shorts/t8ANTnrit_I)

The entities that are available in Home Assistant

![HA-device](https://github.com/user-attachments/assets/dca3b294-eca2-4e0a-87b3-f8b0228a2dab)


**The troubleshooting part**

I had one small issue that was simply my own fault. The speaker and LED's didn't work. I used the 5V pin to get my 5V from but I forgot to add a small solder blob to make the 5V pin an output pin. So make sure you close these pads with a bit of solder

![solderpad](https://github.com/user-attachments/assets/013e3fdf-9ada-4561-8fd3-8d0e5fba6034)
