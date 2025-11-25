## NAME:Subikshan p
## REG NO:212223240161

# Update-the-Ultrasonic-sensor-value-in-Things Mate

# AIM:
To upload the Ultrasonic sensor value in the Things mate using Arduino controller.

# Apparatus required:
Arduino Controller  </br>
Indoor gateway</br>
LoRaWAN shield </br>
HC-SR04 Ultrasonic sensor module </br>
Power supply </br>
Connecting wires </br>
Bread board </br>

# PROCEDURE:

### Procedure for gateway setup
	Go to the link http://172.31.255.254:8000 </br>
	Type the user name password </br>
	Go to LoRa and set the frequency plan 865 Mhz </br>
	In LoRa WAN configurations enter the Gate EUI and server address </br>
	Enable the Internet </br>
	Select the Wifi access point </br>
	Type the ssid and password in wifi LAN setting </br>
	Select the internet and IoT service and provide the details. </br>
	Check all the green colour tick marks in gate way and proceed </br>
### Procedure for gateway registration in The thingsMate LoRaWAN Management </br>
	Login https://iot.saveetha.in:4433 and provide the user id and password </br>
	Go to overview and select application server </br>
	Go to gateway and add new gateway </br>
	Enter the gateway id, name, EUI and select frequency plan </br>
	Open Arduino IDE and type the program for the given application </br>
	Compile the program if no error uploads the program in the controller </br>
	Go to gateways in things mate and check the live data </br>
	Create channel by giving channel name and ID </br>
	Add end device and enter the frequency plan, DevEUI, AppEUI, APP key, Select LoRaWAN version </br>
	Enter payload formatters </br>
	Go to the option query and give the new query name </br>
	Go to the option Dashboard and verify the output.</br>  

# THEORY:

### What is IoT?

Internet of Things (IoT) describes an emerging trend where a large number of embedded devices (things) are connected to the Internet. These connected devices communicate with people and other things and often provide sensor data to cloud storage and cloud computing resources where the data is processed and analyzed to gain important insights. Cheap cloud computing power and increased device connectivity is enabling this trend.IoT solutions are built for many vertical applications such as environmental monitoring and control, health monitoring, vehicle fleet monitoring, industrial monitoring and control, and home automation

![image](https://user-images.githubusercontent.com/71547910/235334044-c01d4261-d46f-4f62-b07f-72a7b6fce5d5.png)

### What is LoRaWAN

The LoRaWAN® specification is a Low Power, Wide Area (LPWA) networking protocol designed to wirelessly connect battery operated ‘things’ to the internet in regional, national or global networks, and targets key Internet of Things (IoT) requirements such as bi-directional communication, end-to-end security, mobility and localization services.LoRaWAN® network architecture is deployed in a star-of-stars topology in which gateways relay messages between end-devices and a central network server. The gateways are connected to the network server via standard IP connections and act as a transparent bridge, simply converting RF packets to IP packets and vice versa. The wireless communication takes advantage of the Long Range characteristics of the LoRaÒ physical layer, allowing a single-hop link between the end-device and one or many gateways. All modes are capable of bi-directional communication, and there is support for multicast addressing groups to make efficient use of spectrum during tasks such as Firmware Over-The-Air (FOTA) upgrades or other mass distribution messages.

The specification defines the device-to-infrastructure (LoRa®) physical layer parameters & (LoRaWAN®) protocol and so provides seamless interoperability between manufacturers, as demonstrated via the device certification program.While the specification defines the technical implementation, it does not define any commercial model or type of deployment (public, shared, private, enterprise) and so offers the industry the freedom to innovate and differentiate how it is used.The LoRaWAN® specification is developed and maintained by the LoRa Alliance®: an open association of collaborating members.

![image](https://github.com/anishkumar-Embedded/Update-the-Ultrasonic-sensor-value-in-cloud/assets/71547910/c63c4edd-3b95-4a69-b9c2-4862afb335c3)

### Characteristics of LoRaWAN technology
Long range communication up to 10 miles in line of sight.
Long battery duration of up to 10 years. For enhanced battery life, you can operate your devices in class A or class B mode, which requires increased downlink latency.
Low cost for devices and maintenance.
License-free radio spectrum but region-specific regulations apply.
Low power but has a limited payload size of 51 bytes to 241 bytes depending on the data rate. The data rate can be 0,3 Kbit/s – 27 Kbit/s data rate with a 222 maximal payload size.

### The Things Mate - IoT Cloud Platform

IoT cloud platforms play a pivotal role in the development and deployment of Internet of Things (IoT) applications, connecting devices and enabling seamless data management and analysis. These platforms typically offer a comprehensive suite of services, including device provisioning, secure connectivity, data storage, and advanced analytics.Leading IoT cloud platforms, such as AWS IoT, Azure IoT, and Google Cloud IoT, provide scalable and reliable infrastructure to accommodate diverse IoT deployments. They facilitate device management, allowing users to monitor, update, and control connected devices remotely. Security features are integral, ensuring data integrity and safeguarding against potential threats.

Analytics capabilities enable organizations to derive meaningful insights from the vast amounts of data generated by IoT devices. Machine learning and artificial intelligence integrations further enhance predictive analytics, enabling proactive decision-making.These platforms often offer APIs for seamless integration with other cloud services, supporting a wide range of industries and applications, from smart homes to industrial automation. As the IoT landscape evolves, cloud platforms continue to innovate, contributing to the growth and sophistication of IoT ecosystems worldwide. Choosing the right IoT cloud platform involves considering factors such as scalability, security, and compatibility with specific use cases.

# PROGRAM:
```
#include <SoftwareSerial.h>
#include <Adafruit_Sensor.h>

#define triggerpin 8                 // trigger pin connected to the ultrosonic sensor 
#define echopin 9                   // techo pin connected to the ultrosonic sensor 

int duration, inches, cm;
String inputString = "";         // a String to hold incoming data
bool stringComplete = false;     // whether the string is complete
long old_time=millis();
long new_time;
long uplink_interval=30000;      //ms
bool time_to_at_recvb=false;
bool get_LA66_data_status=false;
bool network_joined_status=false;
char rxbuff[128];
uint8_t rxbuff_index=0;

SoftwareSerial ss(10, 11);       // Create a SoftwareSerial port on Arduino pins 10 (RX) and 11 (TX)

void setup() {
  pinMode(triggerpin,OUTPUT);
  pinMode(echopin,INPUT);
  Serial.begin(9600);
  ss.begin(9600);
  ss.listen();

  inputString.reserve(200);
  sensor_t sensor;
  ss.println("ATZ");//reset LA66
}

void loop() {
new_time = millis();
if((new_time-old_time>=uplink_interval)&&(network_joined_status==1)){
    old_time = new_time;
    get_LA66_data_status=false;
    HC04();      
    char sensor_data_buff[128]="\0";            
    snprintf(sensor_data_buff,128,"AT+SENDB=%d,%d,%d,%02X%02X",0,2,2,(short)(inches),(short)(cm));
    ss.println(sensor_data_buff);
  }
  if(time_to_at_recvb==true){
    time_to_at_recvb=false;
    get_LA66_data_status=true;
    delay(1000);    
    ss.println("AT+CFG");    
  }
    while ( ss.available()) {
    char inChar = (char) ss.read();
     inputString += inChar;
    rxbuff[rxbuff_index++]=inChar;
    if(rxbuff_index>128)
    break;
    
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
    char inChar = (char) Serial.read();
    inputString += inChar;
    if (inChar == '\n' || inChar == '\r') {
      ss.print(inputString);
      inputString = "\0";
    }
  }
 
  if (stringComplete) {
    Serial.print(inputString);
    
    // clear the string:
    inputString = "\0";
    stringComplete = false;
  }
}

void HC04()
{
   digitalWrite(triggerpin, LOW);
   delayMicroseconds(2);
   digitalWrite(triggerpin, HIGH);
   delayMicroseconds(10);
   digitalWrite(triggerpin, LOW);
   duration = pulseIn(echopin, HIGH);
   inches = microsecondsToInches(duration);
   cm = microsecondsToCentimeters(duration);
   Serial.print(inches);
   Serial.print("in, ");
   Serial.print(cm);
   Serial.print("cm");
   Serial.println();
}
long microsecondsToInches(long microseconds) 
{
   return microseconds / 74 / 2;
}
long microsecondsToCentimeters(long microseconds) 
{
   return microseconds / 29 / 2;
}
```
### Uplink Formatter
```
/*function Decoder(bytes, port) {
  // Extract distance from the first two bytes
  var distance = (bytes[0] << 8) + bytes[1];

  // Convert to centimeters (assuming millimeters are being sent)
  var distance_in_cm = distance / 100;

  return {
    "distance": distance_in_cm
  };
}*/
```
# CIRCUIT DIAGRAM:
![USS](https://github.com/user-attachments/assets/475cd2dc-2d4f-4435-aadd-edf439a046cc)


# OUTPUT:
<img width="1472" height="704" alt="screenshot" src="https://github.com/user-attachments/assets/86fc4306-969a-4a8e-a7e0-247f2424b8e6" />
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/5d50eb73-db77-4170-9e87-ba13b5f07338" />
<img width="1472" height="704" alt="screenshot 2" src="https://github.com/user-attachments/assets/7257fda9-50d2-4c1a-80fc-dd198c9d822d" />


# RESULT:
Thus the distance values are updated in the Thing speak cloud using ESP32 controller.
