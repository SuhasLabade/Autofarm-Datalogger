# Autofarm Datalogger 
### Project objective : 
To design and fabricate a device that collects and store temperature and relative humidity data 
to analyze and maintain plant health inside controlled envirnoment.  

### Project description and Need : 




### System sketch and design:

This device system mainly consisiting Sensor part ,Main controller board, 
data trnsmission unit and cloud storage. Sensor part includes BOSCH make BME280 Temperature and relative humidity 
sensor, considering its best performance in this envirnoment.ESP32 controller is brain of this system,considered its latest features like onchip bluetooth ,wifi connectivity. 
Its also suitable for furure modifications at software level.GSM SIM800L module used for transmitiing data in GPRS mode on thingspeak cloud.Thingspeak
cloud storage displaying this data in graphical format and if possible, we can do mathematical analysis using thingspeak. Its also available to download 
CSV sheet format.This whole system is powered with Solar energy with battery backup considering remote farm locations without electric supply.   



### Electronic design:

Electronics design part mainly consisting four parts - 
1. Sensory system 
2. Main control unit 
3. Cloud storage 
4. Power supply 

#### Sensor selection : 
Here to measure temperature and relative humidity parameters BOSCH make BME280 sensor selected.
This module self-heats a little bit and the temperature measurements can be 1 or 2 degrees above the real temperature value.
However, the BME280 is also the temperature sensor that gave more stable temperature readings without many oscillations between readings.
 This has to do with the resolution of the sensor. It can detect changes up to 0.01ºC.  
 
On below link most commonly used temparture sensors are compared and its showing BME280 is most suitable for this type of application. 
https://randomnerdtutorials.com/dht11-vs-dht22-vs-lm35-vs-ds18b20-vs-bme280-vs-bmp180/

Refering these results to use BME280 for this project.

Temperature sensors comparision            |  Comparision graph
:---------------------------:|:-------------------------:
![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/BME4.png)  |  ![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/BME5.png)

Although temperature sensor selection is dependent on your applications. 

##### BME280 Temperature and Humidity sensor : 

The BME280 is temperature, Humidity and Pressure sensor based on proven principle. 
Here sensor works in I2C protocol using SDA and SCL pin connections for communication.
![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/BME3.png)
  
Following are parameters of BME 280, Opearating voltage, minimum and maximum temperature and relative Humidity range values given here: 

![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/BME1.png)

How sensor works ? 

BME 280 mainly measures following parameters in terms of :
- Pressure : Resistance 
- Temperature : Diode Voltage 
- Humidity : Capacitanace 


![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/BME2.png)

and giving these values to Analog to digital converter (ADC) and generates logic level signals to show relative values of Temperature, humidity and Presssure. 
More details of this sensor vailable here: 
Datasheet : BME280 
https://ae-bst.resource.bosch.com/media/_tech/media/datasheets/BST-BME280-DS002.pdf




#### Main control unit :

ESP32 xtensa microcontroller unit used in this system.ESP32 is latest product by EPRESSIF system with robust design and 
advanced callibration circuitary. Its ultra- low power consumption mode suits perfect for this application.Compare to Atmega 328 , 
ESP32 comes with on chip bluetooth and wifi interface and able to use in diffrent modes.  
![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/ESP2.png)
For this application we need to use diffrent modes depends on geographic location and electricity/ Wifi availability.
Its easy to customize hardware with ESP32 and  perform complex application at software level. So selected ESP32 microcontroller for this device. 
Following are specifications of ESP32 Wroom 32 developement kit :
![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/ESP1.png)
Refered details given here for connections and to write program: 
https://randomnerdtutorials.com/getting-started-with-esp32/

Datasheet : https://www.espressif.com/sites/default/files/documentation/esp32_datasheet_en.pdf

Here ESP 32 takes input from BME280 sensor thorugh I2C protocol and procesess it to send it to Thingspeak webserver. 


#### SIM800L GSM module : 
Here to use this device in all possible ways- where internet and electricty issues are there,
used SIM800L module to connect this device using GPRS to Thingspeak webserver. SIM800L is GSM/GPRS module uses SIMcard to 
connect with cellular network, with calling , SMS and internet facilities. For this device SIM800L works in GPRS mode to connect with Internet. 

To connect this module with ESP32 microcontroller it uses serial communication protocol, which sends or receive data using TX and Rx pins. 
Module details given below: 

Pinouts: 
![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/Sim2.png)

Specifications: 
![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/SIm800L1.png)

Datasheet : https://img.filipeflop.com/files/download/Datasheet_SIM800L.pdf

(Note : This module is very sensitive to power supply, ensure first wheather your supply is stable and correct)  
 

#### Thingspeak cloud:

ThingSpeak is an IoT analytics platform service that allows you to aggregate, visualize, and analyze live data streams in the cloud. 
You can send data to ThingSpeak from your devices, create instant visualization of live data, 
and send alerts. Here to meausre, analyze and to keep datalog used this IoT platform.It mainly shows temperature 
and humidity readings on two different channels in graphical format. We can also export all channel data in exel format. Few mathematical 
tools are free on this to analyze data and generate results. To use this you need to out chnenel API keys into program. 

To setup thingspeak server and creat channels and to get API keys reffered this tutorial given here: 
https://www.mathworks.com/help/thingspeak/getting-started-with-thingspeak.html

  




#### Power supply: 

This devivce is powered with solar energy which stored in battery, considering remote farm locations with electricit unavailability. 

Power consumption of this device is around 1.65W/Hr  - 2W/Hr maximum.To power up this device used here 18650
Lithium Ion battery with 3.7 Voltage and 2800mAh capacity. To charge this with regulated voltage 
and current used charging module with battery saving IC. Solar panel with load volatge 8V and current 1.37A charging this bettery. This whole system designed to give backup around 6-8 hours.If we kept data transmission every half hour then its giving backup around 8 hours. 

Details and connection diagram given below: 
Charging module and battery connection             |  Solar panel
:---------------------------:|:-------------------------:
![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/Charger.png)  |  ![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/Solar%20panel.jpg)


#### Circuit daigarm :
![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/connection%20diagram.png)

To asemble all these modules on single PCB , designed PCB shiled i n Eagle PCB design software and printed on SRM 20 milling machine .

Schematic             |  Board design 
:---------------------------:|:-------------------------:
![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/Charger.png)  |  ![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/Solar%20panel.jpg)

Printed PCB shield           |  Assembled PCB 
:---------------------------:|:-------------------------:
![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/Charger.png)  |  ![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/Solar%20panel.jpg)


PCB layout schematic and board design files given below. 




#### Programming : 

Arduino IDE platform used to program ESP32 board. Its possible to use arduino envirnoment for this.
Reffered this tutorial to add ESP32 board in arduino IDE patform. Following libararies need ]s to download for this program 

- SoftwareSerial
- Wire.h
- Adafruit_BME280

Libraries and variables declaration :
![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/program1.png)

Read sensor values : 
![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/program2.png)

Thingspeak API keys declaration: 
![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/program3.png)


Download whole program from here: 


Packaging : 

To package this whole pcb here used ABS box with demensions 130mm x 130mm x 80mm. Following dimensions are used to mount ON/OFF toggle 
switch and solar panel power jack. 

Box design             |  Box design  
:---------------------------:|:-------------------------:
![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/Charger.png)  |  ![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/Solar%20panel.jpg)

Dimensions          | Actual ABS casing
:---------------------------:|:-------------------------:
![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/Charger.png)  |  ![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/Solar%20panel.jpg)


  Assembleing 1         |    Assembleing 2
:---------------------------:|:-------------------------:
![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/Charger.png)  |  ![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/Solar%20panel.jpg)

Final Hero shot : 

![](https://github.com/SuhasLabade/my-projects-/blob/master/Images/Solar%20panel.jpg)


Installation : 

Polyhouse photo 


Thingspeak results link : 

Graphs : 



