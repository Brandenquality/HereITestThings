# Project: Hydra 
In this project, we have done a prototype version of smart automatic water container named **Hydra** that is produced by **Bilicra**. This prototype version is a **basic represantation** of actual product and can be used for education purposes. All rights of this project belong to Invgarden. Moreover, you can find all **references** that are used in project at referances folder.

# Introduction
What excatly Hydra is? Hydra is a smart automatic water container that is used for pets.  It has many different tecnologies to filter, sterilization, oxidation the water,  With the help of these tecnologies it can purify and can wipe away 99.7% of bacteries in the water.  Moreover, it can show all these features on the mobile app and you can control them. For example you see remaining water level, charge level ,water quality and temperature at the app and you can control filtering, cleaning, temperature (warm or not) of water and use UV lights.    
# Understanding the Hydra
In this project, we started to reverse engineering Hydra to find out electronical components. After the process, we find these components that are used in Hydra: 
|Electronic Components  | Used For |
|--|--|
|DC Motor  |To mix the water  |
|LED lights|To show power, wifi connection, 4 different fullness level |
|Sensors|Temperature, water level, capacitive occupancy |
|UVC LED|To purify the water|
|Butons| To turn on and off|
|Communication Module|To connect with app|

As we mentioned above, the goal of this project is not making the exact same protype of Hydra but making a simplified version of it. The reason for that are education purposes. Moreover, we will not make any mechanical mechanism or design of it.  Its expected to learn how a embaded system works in such devices and being able to communicate smart devices each other properly. Therefore we only built a system that can transfer temperature data to app and get some commands from app.  

![Hydra made by Bllicra](https://photos.app.goo.gl/JGefE7xcDvm5nJMZ8) ![Prototype made by us](https://photos.app.goo.gl/fMEzrB1zA3G8A78v7)

# Reqiurements

Arcknowledge requirement that are expected to know before starting the project: 
- Some basic knowledge about microcontroller and embaded systems especially STM32 Nucleo boards.
- Some basic knowledge about serial communication protocols like I2C, UART and some knowledge about GPIO pins and Timers.

Hardware Requirements: 
- STM32 Nucleo Board (In this project we used "Nucleo F302R8")
- An USB to Type A Cable  
> **Note:** You might need a different USB cable that depends on your Nucleo board
-   LED Lights 
> **Note:**  The LED lights that are used to take place of some important features of **Hydra**. 
- Breadboard
- 1 kilo Ohm Resistances
- Jumper Cables
- AHT10 Temperature Sensor
>**Note:** You can use a different temperature sensor but you have to know or learn how to use it.
- WBR3 Tuya Module

Software requirements:
- STM32 Cube IDE
- An Serial Communication Port Capture Program (We used Realterm) 
- Tuya Smart App (Needed on Smart Phone)
# Tuya 
You might ask what is exactly Tuya is? Tuya is global IoT devolopment platform service provider that has a goal of making people's live smarter. They provide cloud, products and tecnologies for smart device devolopers and their customers. We used their IoT platform, module, mcu sdk codes and guildes to develop this project. However since this project havent published we do not have the rights to publish this project as a Tuya product. 

# Development of Project

First of all, you need to setup the Tuya platform before doing anything. Here how you can setup your product development in Tuya:
- Go to Tuya IoT Platform Page from [here.](https://auth.tuya.com/?from=https://iot.tuya.com/) Sign up and create an account for yourself. 
- After you sign in, you can see many different features that is provided by Tuya. We will only deal with product development. Therefore, scroll a bit in the page and you can see the developer console. Select smart product development and create a new one.
![Developer Console](https://photos.app.goo.gl/5gUNtXUGLK57TxEK8)
- Then, at select product part, choose "Small Home Appliances" at the standart category. Scroll down until you see **"Animals & Plants"**  menu and then choose **"Pet Fountain"** as product.
![Product](https://prnt.sc/S2y3UTnPErgR)
- After that, it wants us to decide smart mode of project. We will choose **"TuyaOS"** and as solution we only have **"Pet Water Feeder"**. Then complete your product informations. You must choose **"Wifi-Bluetooth"** as your protocol. 
-  Then, it wants us to choose functions that will be used this product. Functions are basically the features that you can see and control in the app. You can choose all of them by clicking all button and then click okay to complete this part.
![Functions](https://prnt.sc/4gn626EPeWNO)
- Afterwards, it will direct us to development page. If you only see the functions, scroll up to most top. Here you can see many different menus like function interaction, device interaction and hardware devolopment. 
- Next, we need to decide control panel of the app. Click **"Device Interaction"** and then at the panel control choose **"All-in One Panel"** as your panel. If you want, you can create your own panel. This completes our app ui and you can test it with Tuya Smart app via QR code. But dont forget we havent done the product yet so its just a visual representation.
- Now, we can pass to **"Hardware Development"**. In this part we will create our source and library files that are need to code our microcontroller. Click and go to page, select "MCU SDK" as  selected cloud access mode. Then it wants us to select cloud access hardware. We choosed **"WBR3 Wi-fi Bluetooth Module"** but if you want to use an another Tuya communication module module, you can select it in here.  Later, if provides you the files that you need to download. You have to download only **"MCU SDK"** files to complete this project but if you want to look at other you can download them too. 
![Needed Codes](https://photos.app.goo.gl/gknreDPt6EcK8WF66)

After these steps, you are pretty much done with Tuya IoT platform. After you complete the project you can comeback to platform and can complete the requirements to publish the product.

