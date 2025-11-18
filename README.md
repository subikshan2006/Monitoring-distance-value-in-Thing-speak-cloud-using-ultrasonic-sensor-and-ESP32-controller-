## NAME:Subikshan p
## REG NO:212223240161

# Monitoring distance value in Thing speak cloud using ultrasonic sensor and ESP32 controller

# Uploading ultrasonic sensor data in Thing Speak cloud

# AIM:
To monitor the distance of the obstacle in the Thing speak cloud using ultrasonic sensor and ESP32 controller.
# Apparatus required:
ESP32 Controller,<br>
Ultrasonic Sensor,<br>
Power supply,<br>
Connecting wires,<br>
Bread board<br>
# PROCEDURE:
## Arduino IDE
Step1:Open the Arduino IDE<br>
Step2: Go to sketch- include library – manage libraries file and install esp32 and thing speak library file<br>
Step3:Go to file and select new file option<br>
Step4:Type the program and update the thing speak channel ID, API key, wifi password and ID<br>
Step5:Go to file and select save option to save the program<br>
Step6:Go to sketch and select verify or compile options<br>
Step7:If no error Hex file will be generated in the temporary folder<br>
Step8: Connect all the components as per the circuit diagram<br>
Step9: Connect the programming cable with esp32 and PC.<br>
Step10: Check the jumper position and connect 4 & 5 of P4.<br>
Step11. Upload the program in the esp32.<br>
Step12 Press the boot button in ESP32 and then press and release the reset button after release the boot button<br>
Step13 Check the output in the cloud<br>
## Thingspeak
Step1 Create a ThingSpeak Account<br>
Step2 Log in to your ThingSpeak account<br>
Step3 Create a new channel by navigating to "Channels" and clicking on "New Channel."<br>
Step4 Configure your channel settings, such as Field labels and Channel name<br>
Step5 Copy the Channel ID and API key in the thingspeak and update in the program<br>
Step6 Execute your program to send the sensor value to ThingSpeak<br>
Step7 Check your ThingSpeak channel to verify that the sensor value has been updated<br>
# THEORY:
## Ultrasonic sensor:
The HC-SR04 is a type of ultrasonic sensor which uses sonar to find out the distance of the object from the sensor. It provides an outstanding range of non-contact detection with high accuracy & stable readings. It includes two modules like ultrasonic transmitter & receiver. This sensor is used in a variety of applications like measurement of direction and speed, burglar alarms, medical, sonar, humidifiers, wireless charging, non-destructive testing, and ultrasonography.
### HC-SR04 Ultrasonic Sensor Pin Configuration
This sensor includes four pins and the pin configuration of this sensor is discussed below.

![image](https://github.com/user-attachments/assets/19050fb2-5138-4a32-85d8-f781f705a0df)


•	Pin1 (Vcc): This pin provides a +5V power supply to the sensor.<br>
•	Pin2 (Trigger): This is an input pin, used to initialize measurement by transmitting ultrasonic waves by keeping this pin high for 10us.<br>
•	Pin3 (Echo): This is an output pin, which goes high for a specific time period and it will be equivalent to the duration of the time for the wave to return back to the sensor.<br>
•	Pin4 (Ground): This is a GND pin used to connect to the GND of the system.<br>
### Features
The features of the HC-SR04 sensor include the following
•	The power supply used for this sensor is +5V DC<br>
•	Dimension is 45mm x 20mm x 15mm<br>
•	Quiescent current used for this sensor is <2mA<br>
•	The input pulse width of trigger is10uS<br>
•	Operating current is 15mA<br>
•	Measuring angle is 30 degrees<br>
•	The distance range is 2cm to 800 cm<br>
•	Resolution is 0.3 cm<br>
•	Effectual Angle is <15°<br>
•	Operating frequency range is 40Hz<br>
•	Accuracy is 3mm<br>
### HC-SR04 Ultrasonic Sensor Working
The HC-SR04 Ultrasonic sensor comes with four pins namely Vcc pin, Trigger pin, Echo pin, & Ground pin. This sensor is used to measure the accurate distance between the target and the sensor. This sensor mostly works on the sound waves.
When the power supply is given to this module, it generates the sound waves to travel throughout the air to hit the necessary object. These waves strike and come back from the object, then collects by the receiver module.
Here both the distance as well as time has taken is directly proportional because the time taken for more distance is high. If the trigger pin is kept high for 10 µs, then the ultrasonic waves will be generated which will travel at the sound speed. So it creates eight cycles of sonic burst that will be gathered within the Echo pin. This ultrasonic sensor is interfaced with Arduino to gauge the necessary distance between sensor & object. The distance can be calculated using the following formula.
S = (V x t)/2 <br>
Where the ‘S’ is the required distance<br>
‘V’ is the sound’s speed <br>
‘t’ is the time taken for sound waves to return back after striking the object.<br>
The actual distance can be calculated by dividing its value with 2 as the time will be twice once the waves travel and get back from the sensor.
## What is IoT?
Internet of Things (IoT) describes an emerging trend where a large number of embedded devices (things) are connected to the Internet. These connected devices communicate with people and other things and often provide sensor data to cloud storage and cloud computing resources where the data is processed and analyzed to gain important insights. Cheap cloud computing power and increased device connectivity is enabling this trend.IoT solutions are built for many vertical applications such as environmental monitoring and control, health monitoring, vehicle fleet monitoring, industrial monitoring and control, and home automation.

![image](https://github.com/user-attachments/assets/493f5a4f-9e29-44b4-8ae7-176879daf5e4)

 
Sending Data to Cloud with ESP32 and ThingSpeak
ThingSpeak is an Internet of Things (IoT) analytics platform that allows users to collect, analyze, and visualize data from sensors or devices connected to the Internet. It is a cloud-based platform that provides APIs for storing and retrieving data, as well as tools for data analysis and visualization.The Internet of Things ( or IoT) is a network of interconnected computing devices such as digital machines, automobiles with built-in sensors, or humans with unique identifiers and the ability to communicate data over a network without human intervention.Hello readers, I hope you all are doing great. In this tutorial, we will learn how to send sensor readings from ESP32 to the ThingSpeak cloud. Here we will use the ESP32’s internal sensor like hall-effect sensor and temperature sensor to observe the data and then will share that data cloud.
## What is ThingSpeak?

![image](https://github.com/user-attachments/assets/5a35cd2f-6083-47dd-9b4b-7d18a56a8a3e)

It is an open data platform for IoT (Internet of Things). ThingSpeak is a web service operated by MathWorks where we can send sensor readings/data to the cloud. We can also visualize and act on the data (calculate the data) posted by the devices to ThingSpeak. The data can be stored in either private or public channels.ThingSpeak is frequently used for internet of things prototyping and proof of concept systems that require analytics.
Features Of ThingSpeak
ThingSpeak service enables users to share analyzed data through public channels:
ThingSpeak allows professionals to prepare and analyze data for their businesses:
ThingSpeak updates various ThingSpeak channels using MQTT and REST APIs:
Easily configure devices to send data to ThingSpeak using popular IoT protocols.
Visualize your sensor data in real-time.
Aggregate data on-demand from third-party sources.
Use the power of MATLAB to make sense of your IoT data.
Run your IoT analytics automatically based on schedules or events.
Prototype and build IoT systems without setting up servers or developing web software.

![image](https://github.com/user-attachments/assets/c7746b27-dca6-4b9f-9e71-b24f3e57b6c8)

 
# PROGRAM:
```
#include <Adafruit_Sensor.h>

#include <SoftwareSerial.h>
#include <Adafruit_Sensor.h>
#include <DHT.h>
#include <DHT_U.h>

#define DHTPIN 9                 // Digital pin connected to the DHT sensor 
#define DHTTYPE    DHT11         // DHT 11

DHT_Unified dht(DHTPIN, DHTTYPE);
SoftwareSerial ss(10, 11);       // Arduino RX, TX ,

String inputString = "";         // a String to hold incoming data
bool stringComplete = false;     // whether the string is complete
long old_time=millis();
long new_time;
long uplink_interval=30000;      //ms
bool time_to_at_recvb=false;
bool get_LA66_data_status=false;
bool network_joined_status=false;
float DHT11_temp;
float DHT11_hum;
char rxbuff[128];
uint8_t rxbuff_index=0;

void setup() {
  // initialize serial
  Serial.begin(9600);
   ss.begin(9600);
  ss.listen();
  // reserve 200 bytes for the inputString:
  inputString.reserve(200);
  dht.begin();
  sensor_t sensor;
  dht.temperature().getSensor(&sensor);
  dht.humidity().getSensor(&sensor);
   ss.println("ATZ");//reset LA66
}

void loop() {
  new_time = millis();

  if((new_time-old_time>=uplink_interval)&&(network_joined_status==1)){
    old_time = new_time;
    get_LA66_data_status=false;

  // Get temperature event and print its value.
  sensors_event_t event;
  dht.temperature().getEvent(&event);
  if (isnan(event.temperature)) {
    Serial.println(F("Error reading temperature!"));
    DHT11_temp=327.67;
  }
  else {
    DHT11_temp=event.temperature;
    
    if(DHT11_temp>60){
      DHT11_temp=60;
    }
    else if(DHT11_temp<-20){
      DHT11_temp=-20;
    }
  }
 
 // Get humidity event and print its value.
  dht.humidity().getEvent(&event);
  if (isnan(event.relative_humidity)) {
    DHT11_hum=327.67;
    Serial.println(F("Error reading humidity!"));
  }
  else {
    DHT11_hum=event.relative_humidity;
    
    if(DHT11_hum>100){
      DHT11_hum=100;
    }
    else if(DHT11_hum<0){
      DHT11_hum=0;
    }
  }

    Serial.print(F("Temperature: "));
    Serial.print(DHT11_temp);
    Serial.println(F("°C"));
    Serial.print(F("Humidity: "));
    Serial.print(DHT11_hum);
    Serial.println(F("%"));
    
    char sensor_data_buff[128]="\0";

    snprintf(sensor_data_buff,128,"AT+SENDB=%d,%d,%d,%02X%02X%02X%02X",0,2,4,(short)(DHT11_temp*100)>>8 & 0xFF,(short)(DHT11_temp*100) & 0xFF,(short)(DHT11_hum*100)>>8 & 0xFF,(short)(DHT11_hum*100) & 0xFF);
    
    ss.println(sensor_data_buff);
  }

  if(time_to_at_recvb==true){
    time_to_at_recvb=false;
    get_LA66_data_status=true;
    delay(1000);
    
    ss.println("AT+CFG");    
  }

    while ( ss.available()) {
    // get the new byte:
    char inChar = (char) ss.read();
    // add it to the inputString:
    inputString += inChar;

    rxbuff[rxbuff_index++]=inChar;

    if(rxbuff_index>128)
    break;
    
    // if the incoming character is a newline, set a flag so the main loop can
    // do something about it:
    if (inChar == '\n' || inChar == '\r') {
      stringComplete = true;
      rxbuff[rxbuff_index]='\0';
       
      if(strncmp(rxbuff,"JOINED",6)==0){
        network_joined_status=1;
      }

      if(strncmp(rxbuff,"Dragino LA66 Device",19)==0){
        network_joined_status=0;
      }

      if(strncmp(rxbuff,"Run AT+RECVB=? to see detail",28)==0){
        time_to_at_recvb=true;
        stringComplete=false;
        inputString = "\0";
      }

      if(strncmp(rxbuff,"AT+RECVB=",9)==0){       
        stringComplete=false;
        inputString = "\0";
        Serial.print("\r\nGet downlink data(FPort & Payload) ");
        Serial.println(&rxbuff[9]);
      }
      
      rxbuff_index=0;

      if(get_LA66_data_status==true){
        stringComplete=false;
        inputString = "\0";
      }
    }
  }

   while ( Serial.available()) {
    // get the new byte:
    char inChar = (char) Serial.read();
    // add it to the inputString:
    inputString += inChar;
    // if the incoming character is a newline, set a flag so the main loop can
    // do something about it:
    if (inChar == '\n' || inChar == '\r') {
      ss.print(inputString);
      inputString = "\0";
    }
  }
  
  // print the string when a newline arrives:
  if (stringComplete) {
    Serial.print(inputString);
    
    // clear the string:
    inputString = "\0";
    stringComplete = false;
  }
}



/*function Decoder(bytes,port){
var Temperature=(bytes[0] << 8 | bytes[1])/100;
var Humidity=(bytes[2] << 8 | bytes[3])/100;
return{
Temperature:Temperature,
Humidity:Humidity
};
}*/
```
# CIRCUIT DIAGRAM:
<img width="348" height="706" alt="image" src="https://github.com/user-attachments/assets/5d1f72f6-817e-4c2e-8667-03e22b72795f" />


# OUTPUT:
<img width="1536" height="941" alt="Screenshot 2025-11-14 122328" src="https://github.com/user-attachments/assets/a60e93c1-1685-4a47-9313-c01d598defb9" />
<img width="1886" height="419" alt="Screenshot 2025-11-14 122347" src="https://github.com/user-attachments/assets/4aa20dc1-32a8-4779-afca-13e0e1026b01" />
<img width="1901" height="890" alt="image" src="https://github.com/user-attachments/assets/53aa3dfa-945a-4328-b3c3-e80e9d0a0f86" />



# RESULT:
Thus the distance values are updated in the Thing speak cloud using ESP32 controller.
