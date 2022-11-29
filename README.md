![Weather_GIF](https://github.com/KaiFig/Unit2_project/blob/main/cold-weather.gif)
# Unit 2: A Distributed Weather Station for ISAK

## Criteria A: Planning

## Problem definition
Mr. Sakaguchi has been getting sick recently with a sore throat and a cough. As winter is coming, the humidity and the temperature of the house has been getting lower which has coincided with the recent illness. Therefore, Mr. Sakaguchi suspects that this is the cause of his illness, and he has asked us (Zaven and I) to investigate his hypothesis. Currently, he has a thermometer in his room, however, he doesn't check it often and he also cannot check the humidity. Even with the temperature, he doesn't know what temperature is unhealthy and what temperature is healthy. Therefore, he wants us to create a program that shows when he is most vulnerable to illness due to unhealthy levels of humidity and temperature. 
## Proposed Solution
Considering the client requirements an adequate solution includes a low cost sensing device for humidity and temperature and a custom data script that process and anaysis the samples acquired. For a low cost sensing device an adequate alternative is the DHT11 sensor[^1] which is offered online for less than 5 USD and provides adequare precision and range for the client requirements (Temperature Range: 0°C to 50°C, Humidity Range: 20% to 90%). Similar devices such as the DHT22, AHT20 or the AM2301B [^2] have higher specifications, however the DHT11 uses a simple serial communication (SPI) rather than more eleborated protocols such as the I2C used by the alternatives. For the range, precision and accuracy required in this applicaiton the DHT11 provides the best compromise. Connecting the DHT11 sensor to a computer requires a device that provides a Serial Port communication. A cheap and often used alternative for prototyping is the Arduino UNO microcontroller [^3]. "Arduino is an open-source electronics platform based on easy-to-use hardware and software"[^4]. In additon to the low cost of the Arduino (< 6USD), this devide is programable and expandable[^1]. Other alternatives include diffeerent versions of the original Arduino but their size and price make them a less adequate solution.

The 


**Design statement**

[^1]: Industries, Adafruit. “DHT11 Basic Temperature-Humidity Sensor + Extras.” Adafruit Industries Blog RSS, https://www.adafruit.com/product/386. 
[^2]: Nelson, Carter. “Modern Replacements for DHT11 and dht22 Sensors.” Adafruit Learning System, https://learn.adafruit.com/modern-replacements-for-dht11-dht22-sensors/what-are-better-alternatives.   
[^3]:“How to Connect dht11 Sensor with Arduino Uno.” Arduino Project Hub, https://create.arduino.cc/projecthub/pibots555/how-to-connect-dht11-sensor-with-arduino-uno-f4d239.  
[^4]:Team, The Arduino. “What Is Arduino?: Arduino Documentation.” Arduino Documentation | Arduino Documentation, https://docs.arduino.cc/learn/starting-guide/whats-arduino.  

## Success Criteria

1. The solution provides a visual representation of the Humidity and Temperature values inside a dormitory (Local) and outside the house (Remote) for a period of minimum 48 hours. 
1. ```[HL]``` The local variables will be measure using a set of 4 sensors around the dormitory.
2. The solution provides a mathematical modelling for the Humidity and Temperature levels for each Local and Remote locations. ```(SL: linear model)```, ```(HL: non-lineal model)```
3. The solution provides a comparative analysis for the Humidity and Temperature levels for each Local and Remote locations including mean, standad deviation, minimum, maximum, and median.
4. ```(SL)```The Local samples are stored in a csv file and ```(HL)``` posted to the remote server.
5. Create a prediction the subsequent 12 hours for both temperature and humidity.
6. A poster summarizing the visual representations, model and analysis is created and communicated.

# Criteria B: Design

## System Diagram **SL**
![](sysdim_sl.png)

**Fig.1** shows the system diagram for the proposed solution (**SL**). The indoor variables will be measured using an Arduino microprocessor and the sensor DHT11 conencted to the local computer (Laptop) located inside a room. The outdoor variables will be requested to the remote server using a GET request to the API of the server at ```192.168.6.147/readings```. The local values are stored in a CSV database locally.

![](sysdim_hl.png)

**Fig.2** shows the system diagram for the proposed solution (**HL**). The indoor variables will be measured using a Raspberry PI and four DHT11 sensors located inside a room. Four sensors are used to determine more precisely the physical values and include measurement uncertainty. The outdoor variables will be requested to the remote server using a GET request to the API of the server at ```192.168.6.147/readings```. The local values are stored in a CSV database locally and POST to the server using the API and TOKEN authentication. A laptop computer is used for remotely controlling the local Rasberry Pi using a Dekptop sharing application (VNC Viewer). (Optional) Data from the local raspberry is downloaded to the laptop for analysis and processing.


## Record of Tasks
| Task No | Planned Action                                                | Planned Outcome                                                                                                 | Time estimate | Target completion date | Criterion |
|---------|---------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|---------------|------------------------|-----------|
| 1       | Write the Problem context                        | Identitfy the background to a problem at ISAK that relates to our project  | 10min         | Nov 21                 | A         |
| 2       | Write the Problem defition                        | Expand our problem context and identify a customer and their specific problem so that we know what we need to acheive with our project  |  20min         | Nov 21                 | A         |
| 3       | Research how to connect the Raspberry pi to the DHT sensor | We have a clear understanding of how to connect the DHT11 sensors to the Raspberry pi to proceed with our projectly efficiently   | 20 min  |Nov 24               | A         |
| 4       | Make a test circuit with the Raspberry pi and small breadboard | We can start testing the DHT11 sensor to Raspberry pi connection and start doing small tests with the sensors | 20 min   | Nov 26    | B 
|5        | Create lists for each sensor that is connected to our raspberry pi | We are able to see all the readings for humidity and temperature and we are able to start finding the mean, standard deviation, min, max etc so that we are able to fulfill our success criteria number 3  | 20 min | Nov 29 | C   |
|6        | Create CSV files for our data | All of our data is in our CSV file so that when we learn how to upload data to the remote server, we are able to to send all the data right away  | 15 min  | Nov 29 | C  | 
## Test Plan
| Tests | Input                                                         | Expected output
|-------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------
|Record the data from 4 sensor and upload it to the csv file |Data from the DHT11 senosr  | The data from the DHT11 sensor is uploaded onto the CSV file 


# Criteria C: Development

## List of techniques used

## Development


# Criteria D: Functionality

A 7 min video demonstrating the proposed solution with narration

