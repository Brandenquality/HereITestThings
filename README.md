# Project: Hydra 
In this project, we have developed a prototype version of a smart automatic water container named **Hydra** that is produced by **Bilicra**. This prototype version is a **basic represantation** of actual product and can be used for educational purposes. All rights to this project belong to Invgarden. Moreover, you can find all **references** that are used in project at referances folder.

# Introduction
What exactly is Hydra? Hydra is a smart automatic water container that is used for pets.  It has many different technologies to filter, sterilize and oxidize the water. With the help of these technologies it can purify and can wipe away 99.7% of bacteria in the water.  Moreover, it can show all these features on the mobile app and you can control them. For example, you see the remaining water level, charge level ,water quality, and temperature in the app and you can control the filtering, cleaning, temperature (warm or not) of water, and use UV lights.    
# Understanding the Hydra
In this project, we started to reverse engineering Hydra to find out its electronic components. After the process, we find these components that are used in Hydra: 
|Electronic Components  | Used For |
|--|--|
|DC Motor  |To mix the water  |
|LED lights|To show power, wifi connection, 4 different fullness level |
|Sensors|Temperature, water level, capacitive occupancy |
|UVC LED|To purify the water|
|Butons| To turn on and off|
|Communication Module|To connect with app|

As we mentioned above, the goal of this project is not making the exact same protype of Hydra but making a simplified version of it. The reason for that are education purposes. Moreover, we will not make any mechanical mechanism or design of it.  Its expected to learn how a embaded system works in such devices and being able to communicate smart devices each other properly. Therefore, we only built a system that can transfer temperature data to an app and get some commands from an app.  

![Hydra made by Bllicra](https://github.com/Brandenquality/SecretFiles/blob/main/Fotolar/110000023109943.jpg) ![Prototype made by us](https://github.com/Brandenquality/SecretFiles/blob/main/Fotolar/Finalproject.jpeg)

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
- You might also need solder, multimeter, oscilloscope, power source, logic analyzer and etc. for testing purposes. 

Software requirements:
- STM32 Cube IDE
- An Serial Communication Port Capture Program (We used Realterm) 
- Tuya Smart App (Needed on Smart Phone)
# Tuya 
You might ask, what exactly Tuya is? Tuya is a global IoT development platform service provider that has a goal of making people's live smarter. They provide cloud services, products, and technologies for smart device devolopers and their customers. We used their IoT platform, modules, mcu sdk codes, and guildes to develop this project. However, since this project hasn't been published, we do not have the rights to publish this project as a Tuya product. 

# Development of Project

First of all, you need to setup the Tuya platform before doing anything. Here is how you can setup your product development in Tuya:
- Go to Tuya IoT Platform Page from [here.](https://auth.tuya.com/?from=https://iot.tuya.com/) Sign up and create an account for yourself. 
- After you sign in, you can see many different features that is provided by Tuya. We will only deal with product development. Therefore, scroll a bit down the page and you will see the developer console. Select smart product development and create a new one.
![Developer Console](https://github.com/Brandenquality/SecretFiles/blob/main/Fotolar/image%20(3).png)
- Then, at the select product part, choose "Small Home Appliances" in the standard category. Scroll down until you see **"Animals & Plants"**  menu and then choose **"Pet Fountain"** as product.
![Product](https://github.com/Brandenquality/SecretFiles/blob/main/Fotolar/indir%20(2)%20(1).png)
- After that, it wants us to decide the smart mode of the project. We will choose **"TuyaOS"** and as solution we only have **"Pet Water Feeder"**. Then complete your product information. You must choose **"Wifi-Bluetooth"** as your protocol. 
-  Then, it wants us to choose functions that will be used in this product. Functions are basically the features that you can see and control in the app. You can choose all of them by clicking all the button and then click okay to complete this part.
![Functions](https://github.com/Brandenquality/SecretFiles/blob/main/Fotolar/indir%20(4)%20(1).png)
- Afterwards, it will direct us to the development page. If you only see the functions, scroll up to the very top. Here you can see many different menus like function interaction, device interaction, and hardware development. 
- Next, we need to decide a control panel for the app. Click **"Device Interaction"** and then at the panel control choose **"All-in One Panel"** as your panel. If you want, you can create your own panel. This completes our app ui and you can test it with Tuya Smart app via QR code. But don't forget we havent done the product yet so its just a visual representation.
- Now, we can pass to **"Hardware Development"**. In this part we will create our source and library files that are need to code our microcontroller. Click and go to page, select "MCU SDK" as  selected cloud access mode. Then it wants us to select cloud access hardware. We choosed **"WBR3 Wi-fi Bluetooth Module"** but if you want to use another Tuya communication module module, you can select it here.  Later, if provides you the files that you need to download. You have to download only **"MCU SDK"** files to complete this project but if you want to look at other you can download them too. 
![Needed Codes](https://github.com/Brandenquality/SecretFiles/blob/main/Fotolar/chooseMcuSDK.jpg)

After these steps, you are pretty much done with Tuya IoT platform. After you complete the project you can comeback to platform and complete the requirements to publish the product.

Now, we can dive into communication between the MCU and the module. As we mentioned before, you need to download STM32 Cube IDE to complete the next parts and a serial monitor program to see the communication. Moreover, you can read the [Tuya Page](https://developer.tuya.com/en/docs/iot/overview-of-migrating-tuyas-mcu-sdk?id=K9hhi0xr5vll9) and [Serial Communication Page of Tuya](https://developer.tuya.com/en/docs/iot/tuya-cloud-universal-serial-port-access-protocol?id=K9hhi0xxtn9cb) for this project, if you want to complete this project by yourself. 

The serial communication protocol between the MCU and Tuya modules is mostly already ready in the "MCU SDK" files we downloaded before. However, we still need to understand how it works and need to specify the communication commands or functions for our microcontroller. After that, we can transfer any data we want and use any transferred data from the module. Lets start with how Tuya module and MCU communicate with each other. Tuya module uses UART communication for it and works synchronously. Generally, one command is sent from one side and received from the other side. The tuya communication procedure begins with the Tuya. Tuya sends the information every 1 second if it is powered. After that, if the initialization steps applied correctly, same message would be sent every 15 seconds. That means your mcu and tuya connected. After this process, you can send data by using the Tuya's built-in library. You can send the updated data everywhere in your code at "main.c" but switch codes have to be sent in "protocol.h" file in the switch function. If you dont see the data that you send via Tuya smart app, the problem might be the time requirements. If you dont give the necessary time for data sending process not possible to see your data safely in your app;
![Serial Communication](https://github.com/Brandenquality/SecretFiles/blob/main/Fotolar/Cat-MCU-Module%20(1).png) 
Thankfully, we don't have to code any protocol to connect to each other. But again, if you want to learn more about this process, you can go and look at the serial communication protocol page of Tuya. All the communication process is already in the files we downloaded like "mcu_api.c" or "wifi.h". 

Now, you can start to code your MCU:
- First, open your STM32 Cube IDE create a new STM32 project from file segment.  Then click board segment, write your own nucleo boards name, write its type choose it below and click next.
 ![Selecting Nucleo Board](https://github.com/Brandenquality/SecretFiles/blob/main/Fotolar/Screenshot_2.jpg)
- Then, give a name to your project. Don't forget to choose **"C"** as your targeted language. Dont change other options, click finnish. You don't have to initialize all peripherals with their default mode, but you need to know which pin your LD2 uses in case you need it later on. 
- After project is built, clear you all pinouts. Go to timers part, click **"TIM16"**, then enable it via clicking **"Enable"** box, at the configuration part, set the **"Prescaler value"** as "3200-1" and **"Counter Period"** as "65536-1". Dont forget to enable **"TIM16 global interrupt"** in the NVIC settings. If you are interested, the formula for timers is "Value / (Prescalar*Counter)". This gives you the frequency value, and 1/frequency is your period.    
- Then, we need to setup the clock speed and debug mode. To do that go to **"System Core"**, click **"RCC"** and then set **"High Speed Clock(HSE) "** as **"Crystal/Ceramic Resonator"**. This setups your base clock speed. Then, to set up the debug mode, click to **"SYS"** in same menu, and set **"Debug"** as **"Serial Wire"**.
- Next, go to the Connectivity part, click I2C1, enable I2C as I2C. At user constants, set the **"I2C Speed Mode"** as fast mode plus, and speed is 1000 kHz. At the same part, click to **"USART1"**, activate its "Mode" as Asynchronous. At user constants, set the **"Baud Rate"** as 115200 Bits/s and you dont have to change any other setting for uart. What we have done here is we enable I2C communication and UART communication. After this, Cube IDE should set the connection pins for you. You can check them out in the pinout view. If you want to change the pins you need to look at the pinouts diagram of your board in the internet and then set them by yourself.
- Afterwards, we need to set the pins that are required to light the LEDs. We need 3 GPIO pins and a LD2 pin to complete this project but if you want to add more, you can. At "Pinout view" find PA5, PA6 and PA7 pins (for f302r8 they are at bottom). Click them and set them as **"GPIO_Output"** If you have a different nucleo board than F302R8 then please sets your own pins by yourself. For LD2 green led you have to know which pin your nucleo board uses so go and check pinout of your nucleo board. Set that pin as "GPIO_Output" too. 
![GPIO Pins](https://github.com/Brandenquality/SecretFiles/blob/main/Fotolar/image%20(1).png)

These settings are enough for your peripheral configurations. Now, you can save your project and it will update and open **"main.c"** file. We are going to use this file a lot, and it is expected that you have some understanding of the structure of this file.

# Coding
Finally, we have reached the most important part of this project, programming. As we mentioned before, we used [Tuya's own developer site](https://developer.tuya.com/en/docs/iot/overview-of-migrating-tuyas-mcu-sdk?id=K9hhi0xr5vll9) to code this project. Therefore, you can check this site and try to code the project by yourself.

Let's first mention the MCU SDK files we downloaded in the previous segment. If you open this file, you will see some library files and some c files in the zip. The one that we will code the most between them is **"protocol.c"**. Protocol file contains functions for processing protocol data. You can add or write your own code to enable the connection between the MCU and Wi-Fi module. After you setup your peripherals and save your project, which was done in the previous segment, you need to import the MCU SDK codes to your own project explorer. There are multiple ways to do that. Firstly, you can directly click and drag the codes to your project explorer. But be careful where you copy the codes. You have to copy the **".c"** files to ">core>Src" folder and your **".h"** or library files to 	"core>Inc" folder. The other way to do that is by directly opening your own workspace and copying the codes one by one.

Before starting the code directly, we want to mention about some functions the HAL library uses:
> X is the value that you specified.
HAL_GPIO_TogglePin(GPIOX, GPIO_PIN_X); This code is going to send your pin that you defined 1s and 0s respectively. 
HAL_GPIO_WritePin(GPIOX,GPIO_PIN_X,SET or RESET) ; This code is going to write 1 or 0 to your pin.
HAL_GPIO_ReadPin(GPIOX,GPIO_PIN_X) ; This code will tell you the status of the pin.

>   You can use the Poll , IT ;
  Polling :
 HAL_UART_Transmit(&huartx, buffer , sizeofbuffer ,exception time ) ; This code is for transmitting the buffer to your serial port.
  You can define the buffer like this: uint8_t bufferTX[x] = "       " ;
  Exception time : This is the time for how much time after the sending process does not send the message properly. 
 HAL_UART_Receive(&huartx,buffer, sizeofbuffer, exception time); 

  >IT : 
 In this mode, we need to call the Uart callback and write the code in it. 
  HAL_UART_Transmit_IT(&huartx,buffer,sizeofbuffer) ; If you write this code, uart callback going to be activated and will do the instructions in it.
  HAL_UART_Receive_IT(&huartx, buffer, sizeofbuffer) ; If you write this code, uart callback going to be activated and goint to do the instructions in it.
    void HAL_UART_TxCpltCallback(UART_HandleTypeDef *huart); You need to use this functions before the while(1);
    void HAL_UART_RxCpltCallback(UART_HandleTypeDef *huart); You need to use this functions before the while(1);

  >-- I2C Codes -- 
  	HAL_I2C_Master_Transmit_IT(&hi2c1, slave_adress, unique send information, size); 
        HAL_I2C_Master_Receive_IT(&hi2c1, slave_adress, unique receive information, size); 
Note : Unique information is information type that special to every individual device. You can only find the information of device in the datasheet.


Now, we can finally code our project:
- The first thing you need to do is include your library files into "main.c". This step is very important and if you miss it, project might not work. You can copy includes below. Copy these includes and paste them after **" USER CODE BEGIN Includes"** at the top of **"main.c"**.

```
#include "wifi.h"
#include "protocol.h"
#include "mcu_api.h"
#include "system.h"
```
- Later on, we need to define some variables that are going to be used for this project. Open your "main.c" file and copy the codes below to "USER CODE BEGIN 0" part, which is under the library includes.
```
//AHT10 variables
uint8_t AHT10_RX_Data[6];
uint32_t AHT10_ADC_Raw;
float AHT10_Temperature=30; //Temperature variable
uint8_t AHT10_TmpHum_Cmd[3]={0xAC, 0x33, 0x00};

#define AHT10_ADRESS (0x38<<1) //AHT10 ADRESS
//aditional variables
uint8_t AHT10_Switcher=255;
long x=0; //used for test purposes you dont have to define this one
```
 - Then, if you check Tuya's site, you can see it explains the macro definitions in **"protocol.h"**. We are not going to mention about them but if you want to check it [here.](https://developer.tuya.com/en/docs/iot/overview-of-migrating-tuyas-mcu-sdk?id=K9hhi0xr5vll9) These macro definations are done by the Tuya IoT platform, so we don't have to change anything manually.
 - Now we can move on to function calls. The first function we need to call is "wifi_protocol_init()". It basically initializes protocols that are required to start wifi. Call this function after peripherals are initialized where it says **"USER CODE BEGIN 2"**.  Also, call some other functions too. "mcu_reset_wifi" function resets the wifi connection, the hal function starts the timer, and "wifi_network_check" is private function that we coded. It checks that does the wifi connection exist or not.  You can copy and paste the code below,
 ```
  wifi_protocol_init();
  mcu_reset_wifi(); 
  HAL_TIM_Base_Start(&htim16); //starts timer
  timer_val=__HAL_TIM_GET_COUNTER(&htim16); //the time value of 	   	timmer at that time
  wifi_network_check(); //our own function check it with f3
```
- You can see the wifi network check below. We have not yet added a function to determine which mode it is in, but you can initiate them yourself. But it is not necessary to complete the project. We only check that does the wifi connection exist or not. 
 ```
void wifi_network_check(void){
	switch(mcu_get_wifi_work_state())
		 {
		  		case SMART_CONFIG_STATE:
		  						   // In EZ mode, the LED flickers quickly.
		  		break;
		  		case AP_STATE:
		  						// In AP mode, the LED flickers slowly.
		  		break;
		  		case WIFI_NOT_CONNECTED:
		  						// The Wi-Fi network has been set up and is connecting to the router. The LED is off.
		  		break;
		  		case WIFI_CONNECTED:
		  						   // The Wi-Fi network is connected to the router. The LED is steady on.
		  			HAL_GPIO_TogglePin(GPIOB,GPIO_PIN_13);
		  		break;
		  		default:break;
		 }
}
```
- The next thing we need to set is the **"uart_transmit_output"** function in the **"protocol.c"** file. Open "protocol.c" file in the "Src" folder and then copy and paste the code below. This code is the UART transmission code for project. We don't have to call "uart_transmit_function" anywhere. Other ".c" files we copied will use it. Dont forget to remove **#error** line otherwise it will send a error to our console. Also to work this code properly we need to include "main.h" library to "protocol.c" file. You can copy it below. Paste these codes to the top of the file. 
 ```
 HAL_UART_Transmit(&huart2, (unsigned char *)&value , 1, 0xffff);
```
```
#include "wifi.h"
#include "main.h"
extern UART_HandleTypeDef huart2;
```
> **Note:** You might sometimes want to define your variables in other files. In such cases, if you use the keyword extern with the variable that you want in the other files it becomes visible at that file and you don't have to declare an exception. Dont add extern keyword in your "main.c" file. Define it in the file that you want to make it visible and add "main.h" header file in it.
  
- Then, we need to start receiving part of UART. You can copy and paste the code below. Paste this code to **"while(1)"** loop in the main function at the "main.c" file.  This code check if there is a received data or not and then starts the function.
```
unsigned char Res=0;
if((USART2->ISR&UART_FLAG_RXNE) != 0)
	{
		Res=USART2->RDR;
		uart_receive_input(Res);
	}
```
- Then, we need to call the function that is required to start wifi services. You can copy and paste them from below. You have to call this function in the "while(1)" loop in the same main body.
```
wifi_uart_service();
```
> Note: After this part, you can test your connection by connecting a serial to usb converter to your circuit. 

  We have caleed the functions that are required to start connection for UART and wifi. Now let's talk about how our data is transmitted to app. As we did before, "uart_transmit_output" function in the "protocol.c" file sends the data to module and module sends this via wifi and bluetooth connection. So we only have to understand how data stored in Tuya. As you remember, when we initialized the project at the Tuya, we selected some functions to use. Within these functions, there are variables called DP data. This DP's already defined in the "protocol.h" so we don't have to define them but you have to know which one is used for which UI at the app. The only one we are going to use here "DPID_TEMP_CURRENT". This DP carries the temperature data to app. 
  - Therefore, the first thing we need to code is measuring the temperature data from AHT10 sensor. You have to use an I2C connection for AHT10 sensor. We already defined some variables that are necessary for us in the above part. So we just have to start the I2C connection. You can copy and paste the code below. This code starts transmitting the temperature data from AHT10. But you can not send this data continuously. You have to add some delays between your readings, but using delays in this project will cause the UART connection to cut.  Therefore, we will use the timer. We already read the time data in above for that moment. If we read the time data from timer again in the "while(1)" loop and subtract these two time data from each other we can measure the time has passed until that time and then we can update the first data time to move on. With the help of the the "if" function we can create a condition of delay without delaying any other process. We are going to check the temperature data every 250 miliseconds. You need to paste this code at the top of **"while(1)"*** loop at the main body. **"AHT10_Temperature"** variable is going to be our temperature data
```
if(__HAL_TIM_GET_COUNTER(&htim16) - timer_val >= 2500){
		  if(AHT10_Switcher){
	  			HAL_I2C_Master_Transmit_IT(&hi2c1,AHT10_ADRESS,(uint8_t*)AHT10_TmpHum_Cmd,3);
	  			}
		  else {
	  			HAL_I2C_Master_Receive_IT(&hi2c1,AHT10_ADRESS,(uint8_t*)AHT10_RX_Data,6);
	  			}
		  if(~AHT10_RX_Data[0] & 0x80){
	  			//Convert temperature
	  			AHT10_ADC_Raw=(((uint8_t)AHT10_RX_Data[3] & 15) << 16) | ((uint8_t)AHT10_RX_Data[4]<<8) | AHT10_RX_Data[5];
	  			AHT10_Temperature = (float)(AHT10_ADC_Raw*200.00/1048576.00)-50.00;

		  	  }
		  AHT10_Switcher = ~AHT10_Switcher;
	  }  
```
- Now, we can send this data as DP to app via the code below. Again we need to make our own delay otherwise the connection between MCU and Tuya will be cutted. We will send this DP at every 1.3 seconds.
```
if(__HAL_TIM_GET_COUNTER(&htim16) - timer_val >= 13000){
		/* x=x+10; // this is for testing purposes dont have to write
		if(x==50){ 
			x=0;
		} */
		mcu_dp_value_update(DPID_TEMP_CURRENT,AHT10_Temperature); //VALUE type data report;
		timer_val=__HAL_TIM_GET_COUNTER(&htim16);
	}
```
- Then, if you check the Tuya developer guide, it wants you to update all the DP's at the "all_data_update()" function at the "protocol.c". However, because this data is already being updated at our main body, we don't need to start anything in this function. 
 Afterwards, you need to get DP commands from the app and take some actions according to this DP's. This receiving data part already done by Tuya so we just have to find the functions we need to use and call the functions required to do action.
 - We will only use **"dp_download_filter_reset_handle"**,  **"dp_download_uv_handle"** and **"dp_download_warm_handle"** functions in this project. Every one of them will light a different LED acourding to readed data from Tuya. You can see which function is for which parameter at below,
 
| Function | Parameter |
|--|--|
|dp_download_filter_reset_handle  | Filter reset condition |
|dp_download_uv_handle | UV working condition|
|dp_download_warm_handle|The warming process condition|

- Now, you need to go to "protocol.c" file and find these functions. You can press control + f to search for them with their names. In these functions, we don't have to change anything but need to add our GPIO functions. You can copy and paste them below. Reset disables the pins, and set enables them.
- This code for "dp_download_filter_reset_handle" function:
```
if(filter_reset == 0) {
        HAL_GPIO_WritePin(GPIOA,GPIO_PIN_7,GPIO_PIN_RESET);
    }else {
        HAL_GPIO_WritePin(GPIOA,GPIO_PIN_7,GPIO_PIN_SET);

    }
```
- This one for "dp_download_uv_handle": 
```
    if(uv == 0) {
        HAL_GPIO_WritePin(GPIOA,GPIO_PIN_5,RESET);
    }else {
    	 HAL_GPIO_WritePin(GPIOA,GPIO_PIN_5,SET);
    
```
- And last one for "dp_download_warm_handle":
```
if(warm == 0) {
    	HAL_GPIO_WritePin(GPIOA,GPIO_PIN_6,RESET);
    }else {
    	HAL_GPIO_WritePin(GPIOA,GPIO_PIN_6,SET);
    }
```

This completes everything we needed to code for this project. You can build your project and debug it after the ping connections are done.
> **Note:** If you get any errors while building the project, go to their line and delete them. Moreover, if you get any error about "SUCCESS", "ERROR" and other declarations, you need to change every "SUCCESS", "ERROR" and other variables in the MCU SDK files we downloaded to something like "SUCCESS2". This error occurs because these variables alread declared in the core files to work the STM32 IDE.

Finally, we just have to build our hardware. You can see the pin diagram below. Make sure the connections are same as your nucleo board. If not then you need to do your own wiring. 
> **Note:** If you have used different pinouts, you need to organize your own pin by yourself. 
![Hardware](https://github.com/Brandenquality/SecretFiles/blob/main/Fotolar/WhatsApp%20Image%202022-08-28%20at%2016.59.55.jpeg)

And now you can debug the code and start it. In this part, you need the **"Tuya Smart"** app to test your work. Download and open it. 
- Then, open the "Home" part at the app, click the button at the right top. Select **"Add Device"**

![Home Menu](https://github.com/Brandenquality/SecretFiles/blob/main/Fotolar/S1.jpg)

- Wait and see if your phone finds the connection. If not, then re-debug your code. If it sees the connection, then click add in the discovering devices.

![Add Device](https://github.com/Brandenquality/SecretFiles/blob/main/Fotolar/S1_2.jpg)

- Then, you wil see your device at add device panel. Click the plus button.

![Add Device 2](https://github.com/Brandenquality/SecretFiles/blob/main/Fotolar/S2.jpg)

- It will want you to connect your device via wifi. Select your wifi and enter your password.

![Wifi Informations](https://github.com/Brandenquality/SecretFiles/blob/main/Fotolar/S3.jpg)

- And finally you are connected...

![Device Panel](https://github.com/Brandenquality/SecretFiles/blob/main/Fotolar/WhatsApp%20Image%202022-08-28%20at%2016.59.20%20(1).jpeg)

Thanks for reading our project. 
Done by Doğukan Yılmaz and Ömer Bektaş
