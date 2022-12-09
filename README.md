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

## System Diagram **HL**
![](https://github.com/KaiFig/Unit2_project/blob/main/HL-%20System%20diagram.jpg)

**Fig.1** shows the system diagram for the proposed solution (**HL**). The indoor variables will be measured using a Raspberry PI and four DHT11 sensors located inside a room. Four sensors are used to determine more precisely the physical values and include measurement uncertainty. The outdoor variables will be requested to the remote server using a GET request to the API of the server at ```192.168.6.147/readings```. The local values are stored in a CSV database locally and POST to the server using the API and TOKEN authentication. A laptop computer is used for remotely controlling the local Rasberry Pi using a Dekptop sharing application (VNC Viewer). (Optional) Data from the local raspberry is downloaded to the laptop for analysis and processing.

## Flowcharts 
![](https://github.com/KaiFig/Unit2_project/blob/main/Flowchart_1_project_2.jpg)

**Fig.2** shows the flowchart for the posting of the data. The humidity and data is measured inside using the raspberry PI and the four DHT11 sensors. Then it is posted to the DHT11 sensors with its corresponding sensor ID. We use many for loops to prevent bad coding practices of many lines of code so that it is all consolidated into a few lines. With this we manage to fulfill success criteria 4. 


## Record of Tasks
| Task No | Planned Action                                                | Planned Outcome                                                                                                 | Time estimate | Target completion date | Criterion |
|---------|---------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|---------------|------------------------|-----------|
| 1       | Write the Problem context                        | Identitfy the background to a problem at ISAK that relates to our project  | 10min         | Nov 21                 | A         |
| 2       | Write the Problem defition                        | Expand our problem context and identify a customer and their specific problem so that we know what we need to acheive with our project  |  20min         | Nov 21                 | A         |
| 3       | Research how to connect the Raspberry pi to the DHT sensor | We have a clear understanding of how to connect the DHT11 sensors to the Raspberry pi to proceed with our projectly efficiently   | 20 min  |Nov 24               | A         |
| 4       | Make a test circuit with the Raspberry pi and small breadboard | We can start testing the DHT11 sensor to Raspberry pi connection and start doing small tests with the sensors | 20 min   | Nov 26    | B 
|5        | Create lists for each sensor that is connected to our raspberry pi | We are able to see all the readings for humidity and temperature and we are able to start finding the mean, standard deviation, min, max etc so that we are able to fulfill our success criteria number 3  | 20 min | Nov 29 | C   |
|6        | Create CSV files for our data | All of our data is in our CSV file so that when we learn how to upload data to the remote server, we are able to to send all the data right away  | 15 min  | Nov 29 | C  |
|7         | Research crontab | We are able to time our program so that runs every 5 minutes for 48 hours and then stop automatically   | 15 min  | Nov 29  | A  |
|8         | Add time to our CSV data | We are able to accurately see when our program runs and at what time it runs | 10 min | Nov 30 | C  |
|9         | Create graphs for each of our sensors | The graphs accurately show the data that we have gathered from our sensors and we're able to see when it is at an unhealthy level of humidity and temperature for Mr. Sakaguchi    | 45 minutes   | Dec 4  | C         |
|10     | Post our readings to the remote server  | The data that we record is posted to the remote server. Then, we are able to access the data there as a backup and it is also available to everyone as part of all the data that we are collecting      | 30 min    | Dec 6     | C     |
|11     | Make the necessary graphs, listed in Criteria  | We need to make visual representation of the data throught matplotlib. The specfic graphs we need a mean, standad deviation, minimum, maximum, and median for both remote and indoors sensors.      | 120 min    | Dec 8     | C     |
|12     | Create a non-linear model for each of the graphs | For each graph, there is a model for them so that the customer can clearly see the trends present in the graph     | 80 min   | Dec 11     | C |
|13     | Create a prediction for the next 12 hours of each of the graphs   | The customer can see a prediction of how the next 12 hours will be based on the data that we collected over the 48 hours  | 90 min   | Dec 11    | C |
## Test Plan
| Tests | Input                                                         | Expected output
|-------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------
|Record the data from 4 sensor and upload it to the csv file |Data from the 4 DHT11 sensors connnected to the raspberry pi | The data from the DHT11 sensor is uploaded onto the CSV file 
|Run the code with crontab set to run every minute| Data from the DHT11 sensors  | The code runs every minute and it is uploaded to the CSV file 
|Run the code with crontab set to run every 5 minutes for the next 48 hours     | Data from the DHT11 sensors | The data from the DHT11 sensors is uploaded into the CSV file for a total of 48 hours and we end up with around 570 pieces of data from our sensors
|Post a set of readings (without crontab, just to check the posting)    | Data from the DHT11 sensor    | One set of data from the DHT11 sensor is posted to the remote server
|Post a set of readings using crontab  | Data from the DHT11 sensor    | The data is posted for a total of 48 hours to the remote server   |
|Graph each sensors readings, both humidity and temperature     | Data readings from the CSV file       | We are able to see 8 graphs (4 humidity and 4 temperature) of the data that we have in the CSV file   |
# Criteria C: Development

## Minimum viable product 

We created our minimum viable product that we would be able to show to our client (Mr. Sakaguchi) to get feedback from him and test our code. We used the code below to test our sesnors for 48 hours and send all the data that we gatehered into a CSV file. Alomg with the crontab code on terminal, we were able to run the code for every 5 minutes. 
```.py
import Adafruit_DHT
import time
import numpy as np

DHT_SENSOR = Adafruit_DHT.DHT11
pins =[4, 17, 18, 23]
i = 0
data = []
for pin in pins:
    humidity = None
    temperature = None
    while humidity is None or temperature is None:
        humidity, temperature = Adafruit_DHT.read(DHT_SENSOR, pin)

    data.append(humidity)
    data.append(temperature)

datastr = ""
for i in data:
    datastr += str(i) + ","

print(datastr)

data_time = datastr + (time.strftime("%Y-%m-%d %H:%M:%S"))

with open('humidity_data.csv', 'a') as f:
    f.write(data_time+"\n")

print("Done")

```
![](https://github.com/KaiFig/Unit2_project/blob/main/Screenshot%202022-12-04%20at%207.40.57%20AM.png)

**Figx** Below is our CSV file for the first hour and a half.

![](https://github.com/KaiFig/Unit2_project/blob/main/Screenshot%202022-12-04%20at%207.40.50%20AM.png)

**Figx** Below is our CSV file at the end of our 48 hours. Between this and the picture above, we managed to collect a total of 577 pieces of data from the sensors that were all sent to our CSV file. 

## List of techniques used
![Crontab](https://github.com/KaiFig/Unit2_project/blob/main/Crontab_ex.jpg)

**Figx** Attached below is a picture of the crontab commmand we used to run the code for 48 hours. We used crontab since it enabled us to run it every 5 minutes without the fear of the code shutting down. We put the command in the terminal of the raspberry pi and it runs our posting code in the set times. We got the first part of the code from a website called crontab.guru and we got help for the command from Dr. Ruben. 

```.py
data = []
sensor_idhum = [337,338,339,340]
sensor_idtemp = [333,334,335,336]
for pin in pins:
    humidity = None
    temperature = None
    while humidity is None or temperature is None:
        humidity, temperature = Adafruit_DHT.read(DHT_SENSOR, pin)
    data.append(humidity)
    data.append(temperature)
    for id in sensor_idtemp:
        new_record = {"datetime": datetime.isoformat(datetime.now()), "sensor_id":id, "value":temperature}
        r = requests.post('http://192.168.6.142/reading/new', json=new_record, headers=auth)
    for id2 in sensor_idhum:
        new_record2 = {"datetime": datetime.isoformat(datetime.now()), "sensor_id":id2, "value": humidity}
        r2 = requests.post('http://192.168.6.142/reading/new', json=new_record2, headers=auth)
```

**Figx**  Read the data from the DHT11 sensors connected to the raspberry pi and post it to the remote server 

With the above code, we used our prior knowledge and the help of Dr. Ruben and online resources to create the code to post all the data to the remote sensors. We used for loops with variables outside of the for loops so that we did not have 4 almost identical readings from the DHT 11 sensors and 8 almost identical postings to the server. To find out the pins for the raspberry pi, we used an online resource to find a diagram that illustrated which pins on the raspberry pi served which function. Then we were able to find the 5v and GND pin and also know which pins our data was going through. To get the data from the DHT11 sensor we also used an online resource to fidn out how to read the sensors and then we were able to put it in the dictionary. With this piece of code we were able to fill 2 of our success criteria. We used 4 DHT 11 sensors as we are doing the HL part of the project which fulfills success criteria number 2 and by posting the data to the remote sensor we were able to fulfill sucess criteria number 5. 

## Development


# Criteria D: Functionality

A 7 min video demonstrating the proposed solution with narration

# Citations: 
1. Murray, Mike. “Using the DHT11 Temperature Sensor with the Raspberry Pi.” The Geek Pub, 15 Dec. 2019, https://www.thegeekpub.com/236867/using-the-dht11-temperature-sensor-with-the-raspberry-pi/. 
2. “Raspberry Pi Gpio Pinout.” Raspberry Pi GPIO Pinout, https://pinout.xyz/. 

