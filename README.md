# Thanks JLC-PCB


https://user-images.githubusercontent.com/71336632/166524921-9aa6dec7-4ddf-4920-8dc0-d9bbc9dd37d4.mp4


JLCPCB has been one of the most reliable brands in PCB manufacturing and assembly for over a decade. They provide very good quality custom PCBs at a very affordable price. Placing an order is very simple with their one-stop online platform. The customer can get an estimate of the price for manufacturing on the website itself.  JLCPCB also provides its customers with optional placement of a wide variety of components on the PCB. Their collaboration with reliable electrical component providers like Mouser and DigiKey means that they have a very wide variety of high quality parts which they assemble on the PCB for only $0.0017 per joint ($8.00 setup fee extra). All these features make JLCPCB very affordable and convenient to use, and the high quality products speak for themselves.
# About our project
XLR-20, our formula style race car, is designed to be faster, more reliable, and safer as compared to its predecessors. Prime goals for the vehicle are to upgrade the powertrain and reduce weight by 30 kg to 235 kg. Our previous motors were unable to provide enough power required to compete and score well in dynamics apart from the bare minimum score. So, an upgrade in the powertrain system was needed and thus two EMRAX 188 motors are used. To improve dynamic performance, Torque Vectoring based on yaw rate control is implemented. Owing to increased motor voltage, overall tractive system voltage is increased to 400 VDC from last year's 100 VDC, thus more reliable and safe cells are chosen over previous OEM. Liquid-cooling of motors and inverters along with proper validated air cooling of the accumulator is implemented. To complete the low voltage system’s increased power demands, a DC/DC converter is designed to power it from the accumulator. Furthermore, to achieve robustness and reliability, self-designed master-slave topology-based BMS is used. A 4.3 inch LCD display integrated within front communication board, displays parameters like SOC, speed, acceleration and brake line pressure to the driver. Prime goal of the chassis, suspension, brakes, and drivetrain system was to reduce weight without compromise in rigidity, and manufacturing quality. Topology optimized placement of custom dimension tubes increased chassis stiffness over 65 % from its predecessor with a weight reduction of around 4.5 kg. Introduction of CFRP in structural parts of accumulator internal walls yielded weight reduction to 2.3 kg from 4.5 kg while maintaining structural safety factor of more than 2. Shifting from single-stage planetary to stepped planetary gearbox and use of hollow shafts over solid shaft achieved a weight reduction of around 50%. With the integration of Front and Rear U-ARBs, we are able to test our vehicle over a large range of handling characteristics, from understeer to oversteer and vary the roll gradient from 0.58 °/g to 0.84 °/g.
# Cooling Board
![image](https://user-images.githubusercontent.com/71336632/166506296-bb4c042f-219f-4649-9e45-9308614feac9.png)
![image](https://user-images.githubusercontent.com/71336632/166506415-7d83ef74-e54e-4fe6-aec4-00bc214d0811.png)

We use this for optimisation of our fan speed and pump speed for cooling as for different temperatures, we need different fan and pump speed for better optimisation and energy efficiency.
# Front ECU
![image](https://user-images.githubusercontent.com/71336632/166506607-440ccd4e-f3ba-48d1-89d2-2d371163fe9f.png)
![image](https://user-images.githubusercontent.com/71336632/166506662-bac4f0f3-bc30-4d8c-8bd6-c10729f477e3.png)

The frontECU is responsible for collecting data from various sensors like potentiometers, steering sensor, inertial measurement unit, brake pressure sensor etc. The communication with these sensors is done using different protocols like SPI, I2C and CAN. This data is then broadcasted to the CAN lines from where the vehicle control unit takes it and processes the data for logging and controlling the vehicle. 
# Vehicle Control Unit
![image](https://user-images.githubusercontent.com/71336632/166506807-131fb757-4682-4b88-9144-ca4f900030f0.png)
![image](https://user-images.githubusercontent.com/71336632/166506889-c92eba7e-d2ed-48db-9eaa-6c9af6091bf7.png)

As the name suggests, the VCU controls the current supplied to the motors based on the outputs from the algorithms for traction control and torque vectoring. The inputs to these algorithms are given from the front and rear ECUs on the CAN lines. This PCB is equipped with the STM32F429ZIT microcontroller to handle the communication on the CAN line and the inverters, and also to run the traction control and torque vectoring algorithms.
# Telemetry
![image](https://user-images.githubusercontent.com/71336632/166507417-28b5ef78-3d96-4cc8-b909-fc6c8332f8c2.png)
![image](https://user-images.githubusercontent.com/71336632/166507490-19aa9049-0944-4fb3-bd93-bbebfb742b86.png)

It collects data from the sensors installed in the rear of the vehicle and broadcasts them on the CAN line. It will also be used to send the live data to google’s server via 4G. This board is equipped with the STM32F429ZIT microcontroller to handle the communication with various sensors.
# BMS Slave
![image](https://user-images.githubusercontent.com/71336632/166507768-5f8aa655-f5b1-4b92-b914-2b24855c69d3.png)
![image](https://user-images.githubusercontent.com/71336632/166507884-4d1c038f-adf7-42aa-97ef-66a25e534713.png)

8 of these boards collect temperature and voltage data from the vehicle’s battery and send it to the BMS master over the CAN line. These boards use the BQ7694000DBTR voltage sensing ICs to accurately measure cell voltages. This information is used for passive cell balancing through the onboard circuit and also sent to BMS master via CAN. The onboard STMF0 microcontroller is responsible for communication with BQ7694000DBTR over I2C and also for communication with the BMS master.
# BMS Master
![image](https://user-images.githubusercontent.com/71336632/166508272-069df02e-b285-4dc4-8de7-b64b4618cc53.png)

This is the central board of the self designed battery management system. It collects data from the 8 BMS slaves over CAN, processes the data to ensure that the battery is healthy and also logs the data on an on-board SD card using SPI. This board shuts down the vehicle if it detects an unusual behaviour of any of the 196 cells and is one of the most important boards for the car’s and driver’s safety.
# IMD Latch
![image](https://user-images.githubusercontent.com/71336632/166508468-3432230f-33f3-45a4-b0fa-e650edf56a09.png)
![image](https://user-images.githubusercontent.com/71336632/166508528-bf13fa56-d83d-4e75-8c88-fa4dec7e8f5c.png)

The IMD Latch is a latching circuit for the errors given out by an insulation monitoring device (IMD). The IMD ensures a safe separation between the LV and HV circuits, ensuring driver’s safety from the high voltage. The IMD Latch can only be reset manually and latches on to the errors given by IMD.
