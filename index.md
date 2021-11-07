## What is the DashPi?
The DashPi at is a Raspberry Pi based Car Computer which can be customised to perform a wide variety tasks such as Car Diagnostics, GPS Navigation, Dash Recording, and even object detection.

### Inspiration

Smart cars are cool, but I'm a college student that can barely afford fuel. For the time being, I'm stuck with my dumb 2007 Subaru Impreza, but that doesn't mean I can't try and make it smarter myself!  

<img src="https://upload.wikimedia.org/wikipedia/commons/d/d9/2007_Subaru_Impreza_%28GD9_MY07%29_Luxury_sedan_%282010-11-28%29.jpg" width="500" height="250">  

### Required Hardware  

The physical aspect of this project can be as full fledged as you like. With a bigger budget, you could buy a GPS module with a higher baud rate, a higher definition webcam, or even a more powerful mini computer. This guide will only serve as a tutorial for these specific components, but other components will require a very similar setup procedure.  

**Raspberry Pi 4**  
<img src="https://upload.wikimedia.org/wikipedia/commons/f/f1/Raspberry_Pi_4_Model_B_-_Side.jpg" width="200" height="100">  
[$100](https://raspberry.piaustralia.com.au/products/raspberry-pi-4?src=raspberrypi)  

**Raspberry Pi Touchscreen**  
<img src="https://core-electronics.com.au/media/catalog/product/cache/1/image/650x650/fe1bcd18654db18f328c2faaaf3c690a/5/i/5inch_hdmi_lcd_h_.jpg" width="200" height="100">  
[$80](https://core-electronics.com.au/waveshare-5inch-lcd-800x480.html?utm_source=google_shopping)  

**USB Webcam**  
<img src="https://www.thetelecomshop.com/au/media/catalog/product/cache/9cd8ad701df57b45fe03cf4988b4e1eb/image/212069b75f/grandstream-full-hd-1080p-30fps-usb-webcam-guv3100-grndguv3100bn.jpg" width="200" height="100">  
[$30](https://www.amazon.com/Microphone-NexiGo-Computer-110-degree-Conferencing/dp/B088TSR6YJ/ref=sr_1_3?_encoding=UTF8&c=ts&keywords=Webcams&qid=1636068048&qsid=141-1752746-3911824&s=pc&sr=1-3&sres=B088TSR6YJ%2CB084ZJFNKN%2CB01LXCDPPK%2CB08BHX7GYY%2CB01N5UOYC4%2CB07M6Y7355%2CB004FHO5Y6%2CB08931JJLV%2CB01BGBJ8Y0%2CB08LKZ27C9%2CB01DPNPJ72%2CB088D3VXC6%2CB006JH8T3S%2CB09B9MXT35%2CB09B9RWZMN%2CB004YW7WCY%2CB08T1MWX6J%2CB08FDM4DHF%2CB08BNJPVXG%2CB08VJ25PL1&srpt=CAMCORDER&ts_id=172511)  

**USB GPS Reciever**  
<img src="https://www.shop.nctechimaging.com/wp-content/uploads/IMG_2426.jpg" width="200" height="100">  
[$60](https://www.amazon.com.au/GlobalSat-BU-353-S4-USB-Receiver-Black/dp/B008200LHW/ref=asc_df_B008200LHW/?tag=googleshopdsk-22&linkCode=df0&hvadid=341792355995&hvpos=&hvnetw=g&hvrand=18146161714122481599&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=1000142&hvtargid=pla-318320054786&psc=1)  

**OBD2 Adapter**  
<img src="https://m.media-amazon.com/images/I/61pNHKSSYTL.jpg" width="200" height="100">  
[$20](https://www.remoteoz.com/product/usb-elm327-elm-obdii-obd2-diagnostic-scanner-for-pc-engine-scan-tool-code-reader/)  

**USB C Cigarette Port Charger**  
<img src="https://www.jaycar.com.au/medias/sys_master/images/images/9524103020574/MP3684-usb-type-c-car-charger-5-4a-total-outputImageMain-515.jpg" width="200" height="100">  
[$40](https://www.jaycar.com.au/usb-type-c-car-charger-5-4a-total-output/p/MP3684) 

**Battery Pack (optional)**  
<img src="https://cdn.shopify.com/s/files/1/0735/0383/products/1566-11_800x.jpg?v=1632041088" width="200" height="100">  
[$70](https://www.pakronics.com.au/products/usb-battery-pack-for-raspberry-pi-10000mah-2-x-5v-outputs-ada1566?currency=AUD&utm_medium=cpc&utm_source=google&utm_campaign=Google%20Shopping) 

**Make sure your power supply can provide a minimum of 3 amps to power the Pi and it's components.**

Total Project Cost ≈ $250 
<br>
<br>
### Configuring the GPS
The Hardware portion of this system is quite simple. Simply plug in your GPS into one of the blue USB 3.0 ports on the Pi. A red light should appear on the device and begin blinking.

***TIP*** - GPS Modules can take anywhere from 30 seconds to 5 minutes to fully boot and obtain a signal. Make sure your GPS module is placed in a location that recieves optimal connection. You can use your phone's service bar as an indicator of a spot with a good signal. 


Once booted, you can check if the GPS signal is working by installing the GPSD client on your Pi. To do this, run ```sudo apt-get install gpsd```

You can then run the test daemon by running ```sudo cgps -s```. This will display the GPS ouput from your GPS adapter. If you are not recieving a full GPS signal, try running the daemon with the flag ```-s```. This will prevent GPSD from interfering with the signal, which can break cheaper GPS modules such as the GlobalSat BU-353-S4.

![image](https://user-images.githubusercontent.com/90184008/140636878-9e3dcde2-527e-4c3e-8167-1c0ebca9e7ff.png)

Once you have a stable GPS connection, it's time to set up Navit.

### Setting up Navit

To install the Navit client, run ```sudo apt-get install Navit```. You can now launch the software by exectuing the command ```navit```. Upon launching, you will probably be met with a blank screen. This is because Navit doesn't have any map data to display your GPS coordinates on. To create map data for your desired area, go to http://maps9.navit-project.org/. Using this tool, select your local area and download the bin file.

![image](https://user-images.githubusercontent.com/90184008/140631810-9c191958-c2e0-4af0-909f-1cf844016374.png)

Once you have the bin file downloaded, extract it to the /home/pi/maps/map.bin, then edit the navit configuration file with ```sudo nano /navit/navit.xml```

To enable the custom map data you extracted, search for this line ```<map type="binfile" enabled="yes" data="/home/pi/maps/map.bin"/>```, and replace the data tag with the directory to your map file.

![image](https://user-images.githubusercontent.com/90184008/140636395-27a03c14-00e3-464a-a913-2ae4c09864a5.png)

Sweet. You've got a working map and GPS. Looks pretty ugly though. Let's fix that.

To edit the layout and design of Navit, you can edit the XML design structure within Navit.xml. This can be a pretty tedious process if you're not experienced with XML, so I've saved you some time and provided you with my very own sexy custom Navit theme. Just replace the code in Navit.xml with my file, then select "Daniel's  A e s t h e t i c  Theme" from the layout menu in Navit.

![image](https://user-images.githubusercontent.com/90184008/140636414-4b4171ed-ca71-4dc7-bdd6-b7604354c625.png)

Navit can also read out the directions when navigating. You can enable voice output by installing ESpeak with ```sudo apt-get install espeak```, then searching for this line ```<speech type="cmdline" data="echo 'Fix the speech tag in navit.xml to let navit say:' '%s'" cps="15"/>``` and changing it to ```<speech type="cmdline" data="espeak '%s'" cps="15"/>```

### Dash Recording  
Having footage of your Dash can save you a lot of time and money if you ever get into an accident. Here's how you can implement DashCam functionality into the DashPi.

To begin, you will need to uninstall the default version of FFMPEG that comes pre installed on the Raspberry Pi. This is because the default version is outdated, and can't perform the majority of functions we will need for our Dashcam. You can do this by running ```sudo apt-get purge FFMPEG```.

Once uninstalled, you will need to run an FFMPEG setup script specifically designed for the Raspberry Pi. You can find this script here. Simply download it to your Pi, and execute it with ```sudo ./setup```.

***TIP*** - This installation can take HOURS, and your Pi will be at maximum CPU usage for nearly the entire time.

After you've succesfully installed the latest version of FFPMEG, you can launch the help menu with ```ffmpeg -h```. Through here, you can find all of the options needed to record video from your USB Camera. To save you many hours of your life, I'll share the command I came up with:

```ffmpeg -f alsa -ac 2 -i hw:2,0 -f video4linux2 -i /dev/video0 -acodec ac3 -ab 128k -f matroska -s 1280x720 -f avi -vcodec mpeg4 -qp 16 -f segment -segment_time 00:00:03 -strftime 1  /home/pi/Videos/%Y-%m-%d-%H-%M-%S.avi```

This command will begin recording footage through the device linked @ /dev/video0, as well as recording the microphone audio from the Camera. It will save the video into the /home/pi/Videos/ directory every 3 seconds, with the date and time as the filename. This should be enough to serve as a functional DashCam. Going further, you could implement a system that automatically deletes old videos once the Pi's storage fills up, but I was unable to do so myself.

![image](https://user-images.githubusercontent.com/90184008/140637166-273d1074-bf9f-4f06-ad90-68b346608510.png)

![image](https://user-images.githubusercontent.com/90184008/140637191-7cdb9ab4-d0ef-4b2e-ad15-46a0c0ed531f.png)

Example Output ^^

### OBD2 Diagnostics
Since 2006, it has become a requirement that all Australian cars are fitted with a on board diagnostics port (OBD2), which allows mechanics to read car information such as internal errors, RPM, speed, temperature, etc. You can tap into this wealth of information with a cheap OBD2 adapter.

First of all, you will need to find out where the OBD2 port is located in your car. Using this website, you can find the location for pretty much any car compatible with OBD2. 

After locating the port, simply plug the adapter in, making sure it is oriented the right way up. While some cars will require the ignition to be turned to boot the device, some may boot automatically. It is recommended you use a USB adapter if it is powered while the car is off, as there are many bluetooth vulnerabilities which could be exploited by an attacker.

After either connecting to your OBD device through bluetooth or USB, install the python3 OBD module with ```python3 pip3 install OBD```

Using this, we can easily connect to and read the device data with a simple python script, which I have provided here.

### Object Detection
While object detection wasn't in the original scope of my project, a similar project by TinkerNut has shown it to be entirely possible. 


