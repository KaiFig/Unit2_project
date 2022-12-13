![Weather_GIF](https://github.com/KaiFig/Unit2_project/blob/main/cold-weather.gif)
# Unit 2: A Distributed Weather Station for ISAK

## Criteria A: Planning

## Problem definition
Mr. Sakaguchi has been getting sick recently with a sore throat and a cough. As winter is coming, the humidity and the temperature of the house has been getting lower which has coincided with the recent illness. Therefore, Mr. Sakaguchi suspects that this is the cause of his illness, and he has asked us (Zaven and I) to investigate his hypothesis. Currently, he has a thermometer in his room, however, he doesn't check it often and he also cannot check the humidity. Even with the temperature, he doesn't know what temperature is unhealthy and what temperature is healthy. Therefore, he wants us to create a program that shows when he is most vulnerable to illness due to unhealthy levels of humidity and temperature. 
## Proposed Solution
Considering the client requirements an adequate solution includes a low cost sensing device for humidity and temperature and a custom data script that process and anaysis the samples acquired. For a low cost sensing device an adequate alternative is the DHT11 sensor[^1] which is offered online for less than 5 USD and provides adequare precision and range for the client requirements (Temperature Range: 0°C to 50°C, Humidity Range: 20% to 90%). Similar devices such as the DHT22, AHT20 or the AM2301B [^2] have higher specifications, however the DHT11 uses a simple serial communication (SPI) rather than more eleborated protocols such as the I2C used by the alternatives. For the range, precision and accuracy required in this applicaiton the DHT11 provides the best compromise. Connecting the DHT11 sensor to a computer requires a device that provides a Serial Port communication. A cheap and often used alternative for prototyping is the Arduino UNO microcontroller [^3]. "Arduino is an open-source electronics platform based on easy-to-use hardware and software"[^4]. In additon to the low cost of the Arduino (< 6USD), this devide is programable and expandable[^1]. Other alternatives include diffeerent versions of the original Arduino but their size and price make them a less adequate solution.

Considering the budgetary constrains of the client and the hardware requirements, the software tool that I proposed for this solution is Python. Python is open source, it is mature and supported in mutiple platforms (platform-independent) including macOS, Windows, Linux and can also be used to program the Arduino microprocessor [^5][^6]. In comparison to the alternative C or C++, which share similar features, Python is a High level programming language (HLL) with high abstraction [^7]. For example, memory management is automatic in Python whereas it is responsability of the C/C++ developer to allocate and free up memory [^7], this could result in faster applications but also memory problems. In addition a HLL language will allow me and future developers extend the solution or solve issues proptly.   


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
![](https://github.com/KaiFig/Unit2_project/blob/main/Raspberry%20pi%204.jpg)

**Fig.1** shows the system diagram for the proposed solution (**HL**). The indoor variables will be measured using a Raspberry PI and four DHT11 sensors located inside a room. Four sensors are used to determine more precisely the physical values and include measurement uncertainty. The outdoor variables will be requested to the remote server using a GET request to the API of the server at ```192.168.6.147/readings```. The local values are stored in a CSV database locally and POST to the server using the API and TOKEN authentication. A laptop computer is used for remotely controlling the local Rasberry Pi using a Dekptop sharing application (VNC Viewer). (Optional) Data from the local raspberry is downloaded to the laptop for analysis and processing.

## Flowcharts 
![](https://github.com/KaiFig/Unit2_project/blob/main/Flowchart_1.jpg)

**Fig.2** shows the flowchart for the posting of the data. The humidity and data is measured inside using the raspberry PI and the four DHT11 sensors. Then it is posted to the DHT11 sensors with its corresponding sensor ID. We use many for loops to prevent bad coding practices of many lines of code so that it is all consolidated into a few lines. With this we manage to fulfill success criteria 4. 

![](https://github.com/KaiFig/Unit2_project/blob/main/Project_2_flowchart_2.jpg)

**Fig.x** Shows the flowchart for getting the data from the remote server. We get the data from the sensors ID: 4 and 5 which are the ones that Dr. Ruben has set up in school. With these sensors, we get the data for a total of 48 hours and then we use a function to smooth the data. Using the remote sensors fulfills success criteria number 1 and we use for loops and functions in this flowchart. With the use of these flowcharts, we have shown our computational thinking skills. First of all, we show decomposition by breaking this problem down into small manageble parts. We first figured out how to get the data from the sensor, then we figured out how to do the smoothing. Additionally, we show our pattern recognition since we used for loops for parts that were repeated in the code and we also used a function since we saw that that particular action was repeated multiple times in the code. Lastly, we showed our algorithim design by making a function for the smoothing of the graphs. 


![](https://github.com/KaiFig/Unit2_project/blob/main/Project_2_flowchart_3.jpg)

**Fig.x** Shows the flowchart for getting the mean of the smoothed data. In this flowchart we are able find the standard deviation, median, min and max of the data. We use a for loop to find the mean of each 5 minute reading of all the sensors. 

## Record of Tasks
| Task No | Planned Action                                                | Planned Outcome                                                                                                 | Time estimate | Target completion date | Criterion |
|---------|---------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|---------------|------------------------|-----------|
| 1       | Write the Problem context                        | Identitfy the background to a problem at ISAK that relates to our project  | 10min         | Nov 21                 | A         |
| 2       | Write the Problem defition                        | Expand our problem context and identify a customer and their specific problem so that we know what we need to acheive with our project  |  20min         | Nov 21                 | A         |
| 3       | Create a bill of materials | We are able to know what materials we need to fulfill this project     | 20 min    | Nov 21   | A |
| 4       | Research how to connect the Raspberry pi to the DHT sensor | We have a clear understanding of how to connect the DHT11 sensors to the Raspberry pi to proceed with our projectly efficiently   | 20 min  |Nov 24               | A         |
| 5       | Pick up materials and sign the scope of work    | We gather all the materials necessary to start with the project and we also get approval from Dr. Ruben via the scope of work     | 20 min    | Nov 24    | A | 
| 6       | Make a test circuit with the Raspberry pi and small breadboard | We can start testing the DHT11 sensor to Raspberry pi connection and start doing small tests with the sensors | 20 min   | Nov 26    | B 
|7        | Create lists for each sensor that is connected to our raspberry pi | We are able to see all the readings for humidity and temperature and we are able to start finding the mean, standard deviation, min, max etc so that we are able to fulfill our success criteria number 3  | 20 min | Nov 29 | C   |
|8        | Create CSV files for our data | All of our data is in our CSV file so that when we learn how to upload data to the remote server, we are able to to send all the data right away  | 15 min  | Nov 29 | C  |
|9         | Research crontab | We are able to time our program so that runs every 5 minutes for 48 hours and then stop automatically   | 15 min  | Nov 29  | A  |
|10         | Add time to our CSV data | We are able to accurately see when our program runs and at what time it runs | 10 min | Nov 30 | C  |
|11       | Create the Minimum Viable Product   | We show the customer our ideas and preliminary solution and we get valuable feedback and experience in how to acheive our success criteria | 40 min   | Nov 30    | C| 
|12         | Create graphs for each of our sensors | The graphs accurately show the data that we have gathered from our sensors and we're able to see when it is at an unhealthy level of humidity and temperature for Mr. Sakaguchi    | 45 minutes   | Dec 4  | C         |
|13       | Register the user on the remote server and get the access token     | We are able to create a secure username and password so that we are able to access the remote server, and the access token enables us to log in and post data to the server   | 20 minutes   | Dec 5 | C | 
|14     | Post our readings to the remote server  | The data that we record is posted to the remote server. Then, we are able to access the data there as a backup and it is also available to everyone as part of all the data that we are collecting      | 30 min    | Dec 6     | C     |
|15     | Make the necessary graphs, listed in Criteria  | We need to make visual representation of the data throught matplotlib. The specfic graphs we need a mean, standad deviation, minimum, maximum, and median for both remote and indoors sensors.      | 120 min    | Dec 8     | C     |
|16     | Create a non-linear model for each of the graphs | For each graph, there is a model for them so that the customer can clearly see the trends present in the graph     | 80 min   | Dec 11     | C |
|17     | Create a prediction for the next 12 hours of each of the graphs   | The customer can see a prediction of how the next 12 hours will be based on the data that we collected over the 48 hours  | 90 min   | Dec 11    | C |
|18     | Create 3 flowcharts from parts of our code    | We are able to showcase pieces of our code with our flowcharts so that the customer can clearly see how the code works. Additionally, if other developers take a look at our code, there are able to see how we did it clearly    | 75 minutes    | Dec 12 | B  |
|19     | Research different levels of healthy/unhealthy levels of humidity and temeprature   | We know how much is dangerous and how much is not based on the information we gather online     | 30 minutes  | Dec 12  |  C | 
|20     | How data is stored  | Upload on github the differnt ways we are storing our data and  | 20 min   | Dec 12    | B | 
|21     | Make test plan    | We have a test plan on github so that we are able to show what we have done | 45 min | Dec 12 | B |
|22     | Record the video   | We can show our customer our final product and explain it well  | 20 min     | Dec 13 | D |
## Test Plan
| Software Test Type | Description | Input | Planned Output  |
|------|-------------|----------|---------|
|Functional test| Record the data from 4 sensor and upload it to the csv file |Data from the 4 DHT11 sensors connnected to the raspberry pi | The data from the DHT11 sensor is uploaded onto the CSV file 
|Functional test | Run the code with crontab set to run every minute| Data from the DHT11 sensors  | The code runs every minute and it is uploaded to the CSV file |
|Functional test| Run the code with crontab set to run every 5 minutes for the next 48 hours     | Data from the DHT11 sensors | The data from the DHT11 sensors is uploaded into the CSV file for a total of 48 hours and we end up with around 570 pieces of data from our sensors
|Non-functional test  | Run the code and see how long it takes for the graphs to load   | Data from the CSV file and the remote server | The graphs are uploaded within 10 seconds of running the code 
|Non-functional test  | Create the poster for the customer  | The graphs and models from our code   | The graphs are displayed in the poster in a way that is easy for the user to read |
|Non-functional test  | Make sure that the graphs are easy to read for the customer | Data readings from the CSV file and sensor 4 and 5 (Dr. Ruben's outdoor sensors)  | We are able to clearly see these values on each graph | 

## How is data stored 

We stored our data in the CSV file and in the remote server 

![](https://github.com/KaiFig/Unit2_project/blob/main/Screenshot%202022-12-04%20at%207.40.57%20AM.png)

**Figx** Above is our CSV file for our data which is stored 



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
| Software/development tools | coding structure tools | Libraries    |
|----------------------------|------------------------|--------------|
| Python/Pycharm             | for loops              | datetime     |
| VNC viewer                 | API requests           | requests     |
|                            | Functions              | csv          |
|                            | While statements       | Adafruit_DHT |
|                            | If statements          | matplotlib   |
|                            |                        | numpy        |


## Development

### Crontab 


![Crontab](https://github.com/KaiFig/Unit2_project/blob/main/Crontab_ex.jpg)

**Figx** Attached below is a picture of the crontab commmand we used to run the code for 48 hours. We used crontab since it enabled us to run it every 5 minutes without the fear of the code shutting down. We put the command in the terminal of the raspberry pi and it runs our posting code in the set times. We got the first part of the code from a website called crontab.guru and we got help for the command from Dr. Ruben. 

### Create the sensors

```.py
import requests
new_user = {"username":"Kai+Zaven", 'password':'r2d2zaven+kai'}
#req = requests.post('http://192.168.6.142/register', json=new_user)
#print(req.json())

req = requests.post('http://192.168.6.142/login', json=new_user)
access_token = req.json()["access_token"]

auth = {"Authorization": f"Bearer {access_token}"}


new_sensor ={ "type": "Temperature","location": "R2-14F", "name": "sensor_kai_temp_1","unit":"C" }
new_sensor2 ={ "type": "Temperature","location": "R2-14F", "name": "sensor_kai_temp_2","unit":"C" }
new_sensor3 ={ "type": "Temperature","location": "R2-14F", "name": "sensor_kai_temp_3","unit":"C" }
new_sensor4 ={ "type": "Temperature","location": "R2-14F", "name": "sensor_kai_temp_4","unit":"C" }
new_sensor5 ={ "type": "Humidity","location": "R2-14F", "name": "sensor_kai_hum_1","unit":"C" }
new_sensor6 ={ "type": "Humidity","location": "R2-14F", "name": "sensor_kai_hum_2","unit":"C" }
new_sensor7 ={ "type": "Humidity","location": "R2-14F", "name": "sensor_kai_hum_3","unit":"C" }
new_sensor8 ={ "type": "Humidity","location": "R2-14F", "name": "sensor_kai_hum_4","unit":"C" }

r = requests.post('http://192.168.6.142/sensor/new', json=new_sensor, headers=auth)
print(r.json())
r2 = requests.post('http://192.168.6.142/sensor/new', json=new_sensor2, headers=auth)
r3 = requests.post('http://192.168.6.142/sensor/new', json=new_sensor3, headers=auth)
r4 = requests.post('http://192.168.6.142/sensor/new', json=new_sensor4, headers=auth)
r5 = requests.post('http://192.168.6.142/sensor/new', json=new_sensor5, headers=auth)
r6 = requests.post('http://192.168.6.142/sensor/new', json=new_sensor6, headers=auth)
r7 = requests.post('http://192.168.6.142/sensor/new', json=new_sensor7, headers=auth)
r8 = requests.post('http://192.168.6.142/sensor/new', json=new_sensor8, headers=auth)
print(r2.json())
print(r3.json())
print(r4.json())
print(r5.json())
print(r6.json())
print(r7.json())
print(r8.json())

```
**Figx**  Create the username for our group, get the access token and create 8 sensors (1 for each humidity and temperature) 

With the above code, we used the information that we learned in class about API endings. With this knowledge, we made a dictionary with our username and password and we used this to get our access token. This is important as without it, we would not have been able to create the new sensor addresses in the remote server. 


### Library


```.py
import requests

def get_sensor(readings:list, id:int)->list:
    T=[]
    for r in readings:
        if r["sensor_id"] == id:
            T.append(r['value'])
    return T

def download(url:str="192.168.6.142/readings")->list:
    req = requests.get(f'http://{url}')
    data = req.json()
    readings = data["readings"][0]
    return readings

def smoothing(data:list,size_window:int=12):
    x = []
    y = []
    for i in range(0,(len(data)-1),size_window):
        segment_mean = sum(data[i:i+size_window])/size_window
        y.append(segment_mean)
        x.append(i//size_window)
    return x,y

```

**Figx** Library with 3 different functions

To better organize our code, we decided to create a library with 3 important functions in it. We used the computational thinking skill of patern recognition to figure out that these were pieces of code that were repeated quite frequently in our data. With this imformation, we used the computational thinking skill of algorithim designing to create these 3 functions. Within these functions, we also used for loops, since we recognized the patterns and we realized that we could simplify the code. We also used the information we learned about getting data from a remote server to complete these functions. Therefore, we partially fulfilled success criteria 4 as we needed to create the sensor id's before posting the data to the remote server. 

### Posting 

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



# Criteria D: Functionality

A 7 min video demonstrating the proposed solution with narration

# Citations: 
1. Murray, Mike. “Using the DHT11 Temperature Sensor with the Raspberry Pi.” The Geek Pub, 15 Dec. 2019, https://www.thegeekpub.com/236867/using-the-dht11-temperature-sensor-with-the-raspberry-pi/. 
2. “Raspberry Pi Gpio Pinout.” Raspberry Pi GPIO Pinout, https://pinout.xyz/. 
3. Cousins, Jonathan. “The Effects of Low Humidity on Your Health and Comfort.” SensorPush, SensorPush, 5 Nov. 2020, https://www.sensorpush.com/articles/the-effects-of-low-humidity-on-your-health-and-comfort. 
