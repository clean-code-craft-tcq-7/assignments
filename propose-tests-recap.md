
## I need low latency while booking train tickets online = User need

The booking page need to be updated in a maximum period of 1s

Latency shall not exceed 100 milliseconds between booking attempt and application response.

Server must receive user booking info from user page in 8 seconds or less

**Operation profiles**:

Ensure test environment has optimal network speed with at-least 40Mbps. Book the ticket and await for response. Should be less than...

Capture the number of users online and calculate the latency and show that while ticket booking.Also add a suggested timing based on analysis of data for one week.

**Specifications**:

Send a message every 500ms and confirm the reception of two messages every 1s

Verify latency is less than expected. ex less than 3 sec

Send request to server and measure the latency. Verify if response time is < latency_threshold

## I need the embedded software in a public car charger to be reliable = User need

The software of the charger needs to run at least during 3 months without having to restart it.

The charger must run for 12 continuous hours without restarting.

Have a check software capable of detect any potential issue.

Implement an API for firmware validation

**Operation profiles**:

The Charger should be tested in varying environments such as under low , high temperature, Rain ,etc as agreed with the User.

**Specifications**:

A counter integrated in the software, for calculate the running time needs to be greater that 3 months for pass the test  

Apply test load to charger forcing nominal current flow. Ensure current flow is consistent throughout complete testing procedure.

Connect and disconnect charger from the car every 30 minutes, charger should not get restarted.

Send a request from the validation procedure. If firmware is not the updated version, close connection.

Run 500 readouts/per minute while station is connected to car and must have less than 5% variance in data while: charging phase; idle phase; disconnected phase.

## I need to collect data from an IoT temperature sensor to monitor batteries

The data needs to be monitored every 1 second with a precision of 0.1 degrees celsius

Data polling on temperature sensor shall not exceed 200 ms. Threshold of temperature ranges shall have a +-5% tolerance.

Sensor must support temperatures between 0 and 100 °C.

Sensor must output 500 temperature samples per second while temperature sample rate and data variance must not deviate more than 2.5% and 0.125% within temperature range specified in SysReq-171

**Operation profiles**:

Surface temperature / Ambient temperature

Number of sensors

**Specifications**:

Put the sensor in a hot plate, set the plate temperature to 30° C, check the temperature reported by the sensor, increase the temperature, and compare with the measures from the sensor

Increase %6 temperature above high threshold, ensure temperature data indicates "high" in 200ms or less (Considering an ideal scenario, were sensors capture data almost instantly)

Put sensor inside the testing chamber, rise temperature to 100°C, temperature measurement from sensor should be 100°C

Send a request with the battery id to the service and get a response with the information related to the specific battery id (temp, last update, etc)

Run sensor for 1 hour in set temperature, check sampling rate must stay within 2.5% variance, and temperature sample variance within 0.125% variance; use temp ranges given in SysReq-171
