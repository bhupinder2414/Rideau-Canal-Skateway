# Rideau Canal Skateway Monitoring System
### 1. Introduction
The Rideau Canal Skateway, a historic attraction in Ottawa, requires constant monitoring to ensure skater safety. Our team has been commissioned by the National Capital Commission (NCC) to create a real-time monitoring system that tracks vital weather and ice conditions using Internet of Things (IoT) sensors, giving actionable insights to identify dangerous skating conditions.

The three main locations—Dow's Lake, Fifth Avenue, and NAC—are used by this system to mimic Internet of Things sensors that produce data on ice thickness, surface temperature, snow accumulation, and external temperature. Azure IoT Hub and Azure Stream Analytics are used to process the data in real time, while Azure Blob Storage is used to store the data for analysis and reporting.

### 2. Overview
The Rideau Canal Skateway Monitoring System ensures the safety of skaters by continuously monitoring ice and weather conditions at key locations along the canal. Using simulated IoT sensors, Azure IoT Hub, Azure Stream Analytics, and Azure Blob Storage, this system processes and stores real-time data for further analysis

### 3. System Architecture
The following diagram illustrates the architecture and data flow:

1. IoT Sensors: Generates data every 10 seconds for ice thickness, surface temperature, snow accumulation, and external temperature.
2. Azure IoT Hub: Receives data from simulated sensors.
3. Azure Stream Analytics: Processes data in real time, calculating:
   
      - Average ice thickness over 5 minutes.
   
      - Maximum snow accumulation over 5 minutes.
5. Azure Blob Storage: Stores processed data for analysis.

### 4. Architecture Diagram
![image](https://github.com/user-attachments/assets/a2cffdff-1724-4e72-b364-571ffc1ea57e)

### 5. Key Files:
Sensor simulation files Dows_Lake_sensor.py,Fifth_Avenue_sensor.py and NAC_sensor.py

     -Located in the sensor-simulation/ folder
**Running the Simulation:**

1. Install dependencies:
   
        -pip install azure-iot-device
   
2. Run the script:

       -python3 Dows_Lake_sensor.py
       -python3 Fifth_Avenue_sensor.py
       -python3 NAC_sensor.py
   
### 6. Implementation Details

#### 1. IOT Sensor Simulation
The simulated IoT sensors are actual equipment positioned at three strategic points along the Rideau Canal Skateway: the NAC, Fifth Avenue, and Dow's Lake. These sensors are intended to keep an eye on important ice-related and environmental parameters, protecting skaters.

### How It Works:
1. Data Generation: For every metric, the script produces a random value within a plausible range.
   
2. Payload Creation: A JSON payload is created by packaging data.
   
3. Transmission: The IoTHubDeviceClient is used to send the payload to Azure IoT Hub.
   
4. Continuous Data Flow: New data is pushed every ten seconds as the script runs endlessly.

### 2. IOT Hub Configuration
1. Device Registration with Device id (dows_lake, fifth_avenue, nac_sensors)

2. Connection string to send the data

3. Message routing for downstream processing.

### Outcome
Real-time data is received by the IoT Hub, processed by Azure Stream Analytics, aggregated, and stored in Azure Blob Storage.

### 3. Azure Stream Analytics Job
Azure IoT Hub serves as the primary ingestion point for the simulated IoT sensor data, and the input for the Stream Analytics job is set up to receive data from it.

1. Aggregates data over a minute window for each location.

2. It shows average thickness and maximum snow accumulation.

### Outcome
After processing, the results are sent to Azure Blob Storage for additional examination and preservation.

### 4. Azure Blob Storage
1. The processed data is stored in Azure Blob Storage in JSON format.

2. Set up this container as the output destination for Stream Analytics.

3. Browse and download saved data for additional analysis using the Azure Portal.
