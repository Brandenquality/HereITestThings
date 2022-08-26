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
- Some knowledge about C programming.

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

After these steps, you are pretty much done with Tuya IoT platform. After you complete the project you can comeback to platform and complete the requirements to publish the product.

Now, we can dive into communication between MCU and the module. As we mentioned before, you need to download STM32 Cube IDE to complete next parts and a serial monitor program to see does the communication or not. Also you can read the [Tuya Page](https://developer.tuya.com/en/docs/iot/overview-of-migrating-tuyas-mcu-sdk?id=K9hhi0xr5vll9) and [Serial Communication Page of Tuya](https://developer.tuya.com/en/docs/iot/tuya-cloud-universal-serial-port-access-protocol?id=K9hhi0xxtn9cb) for this project, if you want to complete this project by yourself. 

The serial communication protocol between MCU and Tuya modules mostly already ready in the "MCU SDK" files we downloaded before. However we still need to undestand how it works and need to spesify the communication commands or function for our microcontroller. After that we can transfer any data we want and use any transfered data from module. Lets start with how Tuya module and MCU communicates with each other. Tuya module uses UART communication for it and works synchronously. Generally, one command is sent by one side and received by other side. One sides send a command and then waits for a response from other side. If sender does not receive a correct response within a spcific time period, the transmission times out. You can see it in the following figure.
![Serial Communication](https://photos.app.goo.gl/rTvqYAmkp2mhJbNE6) 
Thankfully, we dont have to code any protocol to connect them each other. But again If you want to learn more about this process you can go and look the serial communication protocol page of Tuya. All communication process is already at   the files we downloaded like mcu_api.c or wifi.h. 

Now, you can start to code your MCU:
- First, open your STM32 Cube IDE create a new STM32 project from file segment.  Then click board segment, write your own nucleo boards name, write its type choose it at below and click next.
 ![Selecting Nucleo Board](https://photos.app.goo.gl/xHwghZhkhctndrK58)
- Then, give a name to your project. Dont forget to choose **"C"** as your targeted language. Dont change other options, click finnish. You dont have to	 initialize all peripherals with their defult mode but you need to know which pin your LD2 uses in case if you need it later on. 
- After project is built, clear you all pinouts. Go to timers part, click **"TIM16"**, then enable it via clicking **"Enable"** box, at the configuration part, set the **"Prescaler value"** as "3200-1" and **"Counter Period"** as "65536-1". Dont forget to enable **"TIM16 global interrupt"** in the NVIC settings.  
![Timer Settings](https://photos.app.goo.gl/aWLcTsTscxtBWGtN9)  
- Then, we need to setup the clock speed and debug mode. To do that go to **"System Core"**, click **"RCC"** and then set **"High Speed Clock(HSE) "** as **"Crystal/Ceramic Resonator"**. This setups your base clock speed. Then to set up the debug mode click to **"SYS"** in same menu, and set **"Debug"** as **"Serial Wire"**.
- Next, go to Connectivity part, click I2C1, enable I2C as I2C. At user constants, set the **"I2C Speed Mode"** as fast mode plus and speed is 1000 kHz. At same part, click to **"USART1"**, activate its "Mode" as Asynchronous. At user constants, set the **"Baud Rate"** as 115200 Bits/s and you dont have to change any other setting for uart. What we have done in here is we enables I2C communication and UART communication. After this, Cube IDE should set the connection pins for you. You can check them in pinout view. If you want to change the pins you need to look at the pinouts diagram of your board in the internet and then set them by yourself.
- Afterwards, we need to set the pins that are required to light the LEDs. We need 3 GPIO pins and a LD2 pin to complete this project but if you want to add more you can. At "Pinout view" find PA5, PA6 and PA7 pins (for f302r8 they are at bottom). Click them and set them as **"GPIO_Output"** If you have a different nucleo board than F302R8 then please sets your own pins by yourself. For LD2 green led you have to know which pin your nucleo board uses so go and check pinout of your nucleo board. Set that pin as "GPIO_Output" too. 
![GPIO Pins](https://photos.app.goo.gl/uxtUkPot9NZ6f9Sd7)

These setting are enough for your peripherals configuration. Now, you can save your project and it will update and open **"main.c"** file. We are going to use this file a lot and its expected to you have some understanding about the structure of this file.

Now, 
**Waiting for codes please update here later on**

# Coding
Finally we have reach the most important part of this project, programming. As we mentioned before, we used [Tuya's own developer site](https://developer.tuya.com/en/docs/iot/overview-of-migrating-tuyas-mcu-sdk?id=K9hhi0xr5vll9) to code this project. Therefore, you can check this site and try to code the project by yourself.

Lets first mention about the MCU SDK files we downloaded in previous segment. If you open this file you see some library files and some c files in the zip. The one that we will code the most between them is **"protocol.c"**. Protocol file contains functions for processing protocol data, you can add or write your own code to enable the connection between MCU and Wi-Fi module. After you setup your peripherals and save your project which is done at previous segment, you need to import the MCU SDK codes to your own project explorer. There are multiple ways to do that. Firstly, you can dirrectly click and drag the codes to your project explorer. But be carefull where you copy the codes. You have to copy the **".c"** files to ">core>Src" folder and your **".h"** or library files to 	"core>Inc" folder. The other way to do that directy opening you own workspace and copying the codes one by one. 

Before starting the codding directly, we want to mention about about some function HAL library uses.

**WAIT FOR REMAININ THEN COPPY HERE THANKS**

Now, we can finally code our project:
- First thing you need to do is including your library files to "main.c". This step is very important and if you miss it, project might not work. You can copy includes below. Copy these includes after **" USER CODE BEGIN Includes"** 

```
#include "wifi.h"
#include "protocol.h"
#include "mcu_api.h"
#include "system.h"
#include <stdio.h>
#include <string.h>
#include <stdio.h>
```
 
