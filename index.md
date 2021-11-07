## What is the DashPi?

The DashPi at is a Raspberry Pi based GPS Dashcam which can be customised to perform a wide variety tasks such as Car Diagnostics, Media playing, or even object detection.

This site aims to act as a guide for anyone who wishes to build their own version of this project. 

###INSPIRATION  

Smart cars are cool, but I'm a college student that can barely cover the costs for fuel. For the time being, I'm stuck with my dumb 2007 Subaru Impreza, but that doesn't mean I can't try and make it smarter myself!  

<img src="https://upload.wikimedia.org/wikipedia/commons/d/d9/2007_Subaru_Impreza_%28GD9_MY07%29_Luxury_sedan_%282010-11-28%29.jpg" width="500" height="250">  

### Required Hardware  

The physical aspect of this project can be as full fledged as you like. Personally, I was on a tight budget and time constraints, so I used cheaper modules and did not build a chassis for the components. With more money and resources, you could buy a better GPS module, mini computer, and webcam. The specific parts used should't matter, as they should all have a relatively similar process of setting up.  

**Raspberry Pi 4**  
<img src="https://upload.wikimedia.org/wikipedia/commons/f/f1/Raspberry_Pi_4_Model_B_-_Side.jpg" width="200" height="100">  
[Link](https://raspberry.piaustralia.com.au/products/raspberry-pi-4?src=raspberrypi)  

**USB Webcam**  
<img src="https://www.thetelecomshop.com/au/media/catalog/product/cache/9cd8ad701df57b45fe03cf4988b4e1eb/image/212069b75f/grandstream-full-hd-1080p-30fps-usb-webcam-guv3100-grndguv3100bn.jpg" width="200" height="100">  
[Link](https://www.amazon.com/Microphone-NexiGo-Computer-110-degree-Conferencing/dp/B088TSR6YJ/ref=sr_1_3?_encoding=UTF8&c=ts&keywords=Webcams&qid=1636068048&qsid=141-1752746-3911824&s=pc&sr=1-3&sres=B088TSR6YJ%2CB084ZJFNKN%2CB01LXCDPPK%2CB08BHX7GYY%2CB01N5UOYC4%2CB07M6Y7355%2CB004FHO5Y6%2CB08931JJLV%2CB01BGBJ8Y0%2CB08LKZ27C9%2CB01DPNPJ72%2CB088D3VXC6%2CB006JH8T3S%2CB09B9MXT35%2CB09B9RWZMN%2CB004YW7WCY%2CB08T1MWX6J%2CB08FDM4DHF%2CB08BNJPVXG%2CB08VJ25PL1&srpt=CAMCORDER&ts_id=172511)  

**USB GPS Reciever**  
<img src="https://www.shop.nctechimaging.com/wp-content/uploads/IMG_2426.jpg" width="200" height="100">  
[Link](https://www.amazon.com.au/GlobalSat-BU-353-S4-USB-Receiver-Black/dp/B008200LHW/ref=asc_df_B008200LHW/?tag=googleshopdsk-22&linkCode=df0&hvadid=341792355995&hvpos=&hvnetw=g&hvrand=18146161714122481599&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=1000142&hvtargid=pla-318320054786&psc=1)  

**USB C Cigarette Port Charger (optional)**  
<img src="https://www.jaycar.com.au/medias/sys_master/images/images/9524103020574/MP3684-usb-type-c-car-charger-5-4a-total-outputImageMain-515.jpg" width="200" height="100">  
[Link](https://www.jaycar.com.au/usb-type-c-car-charger-5-4a-total-output/p/MP3684)  
  
  
### Configuring Hardware
The Hardware portion of this system is quite simple. Simply plug in your GPS into one of the blue USB 3.0 ports on the Pi. A red light should appear on the device and begin blinking.

**PRO TIP** - GPS Modules can take anywhere from 30 seconds to 5 minutes to fully boot and obtain a signal. Please be patient, and make sure your GPS module is placed in a location that recieves optimal connection. You can use your phone's service bar as an indicator of a spot with a good signal. 


Once booted, you can check if the GPS signal is working by installing the GPSD client on your Pi. To do this, run ```sudo apt-get install gpsd```

Once installed, you can run the test daemon by running ```sudo cgps -s```

Note - The S flag

If you are not recieving a full GPS signal, try editing the default gpsd configuration file with ```sudp nano gpsd.rc```

Once opened
- Safe flag
- Specify port
