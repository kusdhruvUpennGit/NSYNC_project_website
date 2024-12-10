# NSYNC-Project-Website
NSYNC Project Report

## 1. Abstract

### 1.1 Overview

<p>Swarm analysis investigates the collaborative dynamics of multiple autonomous agents working collectively to achieve shared objectives. Rooted in natural systems such as ant colonies, bee hives, and bird flocks, the field explores how simple, local interactions among individual agents give rise to complex, efficient, and adaptive group behaviors. This decentralized approach, wherein agents follow straightforward rules and interact locally, enables swarms to adapt to environmental changes and maintain functionality even when individual components fail. These principles ensure robustness, resilience, and adaptability in both natural and engineered systems, particularly in robotics.</p>

<p>Drawing inspiration from biological and ecological systems, swarm analysis examines how social insects and animals exhibit sophisticated group behaviors that allow them to perform critical tasks like foraging, building, and protection. Ants, for instance, employ pheromone trails for efficient resource discovery, while bees utilize the "waggle dance" for directing hives toward nectar sources. Similarly, flocking birds exhibit coordinated movements that enhance predator evasion and energy conservation. These natural systems demonstrate the power of decentralized, self-organized behaviors, where simple individual actions culminate in achieving complex group objectives, offering a model for robust, adaptive, and scalable systems.</p>

### 1.2 Swarm analysis in robotics and warehouse application

<p>Swarm robotics leverages principles inspired by nature to enable groups of autonomous robots to perform tasks collaboratively using simple rules and local interactions. This decentralized approach ensures dynamic task allocation, scalability, and robust adaptability to failures or environmental changes. By minimizing human intervention, swarm systems enhance efficiency, resilience, and sustainability in complex operational settings.</p>

<p>This project implements swarm robotics in a warehouse environment using a two-robot system. Each robot, powered by an ATmega328P microcontroller, is coordinated through an Xbee-based central controller that ensures synchronization and prevents task overlaps. The robots navigate, allocate tasks, and optimize energy usage, triggering alerts when batteries are low. This showcases the potential of scalable, efficient, and resilient robotic systems to improve warehouse automation and overall productivity through collaboration and energy-aware operations.</p>


## 2. Motivation 

<p>The rapid expansion of e-commerce and logistics industries has driven a significant demand for efficient and automated warehouse solutions. To meet rising consumer expectations and navigate the complexities of modern supply chains, businesses increasingly rely on automation to streamline operations and reduce costs.</p>

<p>Swarm robotics presents an innovative approach to enhancing warehouse efficiency by reducing human intervention and improving overall operational effectiveness. The collaborative capabilities of swarms enable optimized task distribution and resource utilization, facilitating seamless workflows. By harnessing swarm intelligence, warehouses benefit from task allocation, accelerated decision-making, and improved scalability, achieving enhanced performance and efficient resource management.</p>

## 3. Goals

<p>The goals for this project have been revised to reflect updates in the hardware and functionality. Initially, the project intended to use ESP32 and ATmega328PB microcontrollers; however, the implementation now employs Pololu 3pi robots equipped with ATmega328P microcontrollers. The revised goals are as follows:</p>

1.	Wireless Control: Enable seamless control of the robots using XBee RF modules for wireless communication.<br>
2.	Synchronized Bot Operations: Develop a two-bot system capable of executing synchronized tasks based on user inputs, including moving forward, backward, rotation, or line-following.<br>
3.	Battery Monitoring: Integrate real-time monitoring of each bot's battery level to ensure operational efficiency.<br>
4.	Low Battery Alert and Task Reallocation: Implement a system where a buzzer alerts when a bot’s battery is low, causing the bot to stop its wheels after a few seconds and reassign its tasks to the other bot to maintain uninterrupted operation.<br>

## 4. Block Diagram

![alt text](Images/1_BlockDiagram.png)

 * This block diagram shows the setup for a single Pololu 3pi bot, highlighting key components like sensors, motors, LEDs, and communication with the laptop using XBee modules.<br>
 * The project now integrates two such bots, both controlled wirelessly, working in sync to share and complete tasks while autonomously managing battery levels and task reassignment.


## 5. Software Requirments Specifications

The software system is designed to facilitate efficient wireless communication, monitoring, and task management between XBee modules, Pololu 3pi robots, and ATmega328P microcontrollers.

<table>
  <thead>
    <tr>
      <th>SRS</th>
      <th>Objective</th>
      <th>Specifications</th>
      <th>Expected Outcome</th>
      <th>Result</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>SRS 1</td>
      <td>Create a mesh network between XBee Coordinator and XBee Endpoints</td>
      <td>
        <ul>
          <li>Configure 1 XBee Coordinator and 2 XBee End Devices as routers.</li>
          <li>Set all devices to the same PAN ID for communication.</li>
        </ul>
      </td>
      <td>The Coordinator successfully sends commands to the End Devices.</td>
      <td><strong>Pass</strong>: The Coordinator successfully communicated with the End Devices, achieving the intended functionality.</td>
    </tr>
    <tr>
      <td>SRS 2</td>
      <td>Wirelessly control the Pololu 3pi bots through the serial monitor via XBee Coordinator.</td>
      <td>
        <ul>
          <li>Command <code>1</code>: Control Pololu Robot 1 to perform its task (rotate).</li>
          <li>Command <code>2</code>: Control Pololu Robot 2 to perform its task (rotate).</li>
          <li>Ignore other commands.</li>
        </ul>
      </td>
      <td>
        <ul>
          <li>Robot 1 rotates upon receiving Command <code>1</code>.</li>
          <li>Robot 2 rotates upon receiving Command <code>2</code>.</li>
          <li>Other commands have no effect.</li>
        </ul>
      </td>
      <td><strong>Pass</strong>: Robot 1 and Robot 2 performed their tasks correctly, while other commands had no effect.</td>
    </tr>
    <tr>
      <td>SRS 3</td>
      <td>Use buttons on ATmega328PB microcontroller to wirelessly control Pololu 3pi bots via XBee network.</td>
      <td>
        <ul>
          <li>Button <code>1</code>: Send a command to Robot 1 to perform its task.</li>
          <li>Button <code>2</code>: Send a command to Robot 2 to perform its task.</li>
          <li>Ensure communication between ATmega328PB and Pololu 3pi bots over XBee network.</li>
        </ul>
      </td>
      <td>
        <ul>
          <li>Robot 1 performs its task when Button <code>1</code> is pressed.</li>
          <li>Robot 2 performs its task when Button <code>2</code> is pressed.</li>
        </ul>
      </td>
      <td><strong>Not Completed</strong>: Baud rate mismatch between ATmega328PB (16 MHz) and Pololu 3pi bots (20 MHz). XBee communication at 115200 baud was unsuccessful.</td>
    </tr>
  </tbody>
</table>

#### Process of Configuring Xbee Modules and Wireless Communication

To achieve seamless wireless communication between the two Pololu 3pi bots and the laptop, we utilized the XBee S2C modules. The system was configured with one module as the Coordinator and the other two modules as Routers, following the process described below.<br>

Configuration Process:<br>
1. Hardware Setup:<br>
    • The XBee S2C modules were connected to USB XBee adapters and linked to the laptop via USB ports. XCTU software was used to configure the modules.<br>
    • The Coordinator and Router roles were assigned to the modules using XCTU.<br>

2. Coordinator Configuration: <br>
        The first module was set as the Coordinator with the following parameters:<br>
        • PAN ID: 1234 (common network ID for all modules).<br>
        • CE (Coordinator Enable): Enabled.<br>
        • Destination Address DL: Set to FFFF (broadcast mode to communicate with all devices in the PAN ID).<br>
        • The configuration was saved by clicking the "Write" button in XCTU.<br>
3.	Router Configuration: The other two modules were configured as Routers with the following parameters:<br>
• PAN ID: 1234 (same as the Coordinator).<br>
• CE (Coordinator Enable): Disabled.<br>
• Destination Address DL: Defaulted to 0 (addressing the Coordinator).<br>
• Configuration was saved for each module.<br>

4.	Testing Communication:<br>

    • Two instances of XCTU software were opened on the laptop, one for the Coordinator and the other for a Router.<br>
    • The Terminal mode in XCTU was used to test communication between the devices. Messages typed in one module's terminal were successfully transmitted and displayed on the other module's terminal, confirming proper configuration and functionality.<br>
    • The communication was reliable, with transmitted messages appearing in blue and received messages in red, as seen in the attached screenshots.<br>

Below screenshots show the configuration of xbee modules:

![alt text](Images/2_XbeeCoordinator.png)

![alt text](Images/3_XbeeRouter.png)


## 6. Hardware Requirments


<table>
  <thead>
    <tr>
      <th>HRS</th>
      <th>Objective</th>
      <th>Specifications</th>
      <th>Expected Outcome</th>
      <th>Result</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>HRS 1</td>
      <td>Configuring the Pololu 3pi bot</td>
      <td>Flash a test code using avrdude via Pololu USB AVR programmer v2 to check the bot's functionality.</td>
      <td>Flash the .hex file at 115200 baud and verify proper functionality of the Pololu 3pi bot.</td>
      <td><strong>Pass</strong>: The .hex file was successfully flashed, and the bot worked as expected.</td>
    </tr>
    <tr>
      <td>HRS 2</td>
      <td>Configuring the Pololu 3pi bot LEDs and Buzzers</td>
      <td>Test the working of LEDs and buzzers for integration with further implementations.</td>
      <td>Successfully blink LEDs and ring the buzzer with a square wave pulse.</td>
      <td><strong>Pass</strong>: LEDs blinked and the buzzer rang as expected.</td>
    </tr>
    <tr>
      <td>HRS 3</td>
      <td>Configure the motors</td>
      <td>Control the motors to make the bot rotate in a specific direction.</td>
      <td>Make the bot rotate by configuring the left and right motors to move in opposite directions.</td>
      <td><strong>Pass</strong>: The bot rotated as intended.</td>
    </tr>
    <tr>
      <td>HRS 4</td>
      <td>Configuring the QTR sensors</td>
      <td>Test the QTR IR sensors by toggling LEDs when a black line is detected.</td>
      <td>Toggle LEDs based on sensor readings: stop the red LED for right sensors and green LED for left sensors.</td>
      <td><strong>Pass</strong>: LEDs toggled as expected based on sensor readings.</td>
    </tr>
    <tr>
      <td>HRS 5</td>
      <td>Configuring the XBee modules with the Pololu 3pi bot</td>
      <td>Connect XBee routers to Pololu 3pi bots and send a simple print message to the XBee Coordinator.</td>
      <td>Establish communication to display "Hello from pololu 3pi" on the serial monitor.</td>
      <td><strong>Pass</strong>: Communication was established and the message was successfully displayed via UART.</td>
    </tr>
    <tr>
      <td>HRS 6</td>
      <td>Controlling the movement of the bots by giving controls in the serial monitor</td>
      <td>Allow user to enter commands (1 for Bot 1, 2 for Bot 2) to control motor rotation and LED blinking.</td>
      <td>Bot 1 rotates on command 1, and Bot 2 rotates on command 2, with LED feedback.</td>
      <td><strong>Pass</strong>: Bots rotated and LEDs blinked as intended based on user input.</td>
    </tr>
    <tr>
      <td>HRS 7</td>
      <td>Send battery monitoring details from Pololu 3pi bot to the XBee Coordinator</td>
      <td>Read battery voltage using ADC6 on the Pololu 3pi bot and transmit data to the XBee Coordinator.</td>
      <td>Display battery voltage in millivolts on the XBee Coordinator serial monitor.</td>
      <td><strong>Pass</strong>: Battery voltage was successfully transmitted and displayed.</td>
    </tr>
    <tr>
      <td>HRS 8</td>
      <td>Try configuring a smart battery monitoring system</td>
      <td>Signal low battery with a buzzer and stop the motors when voltage falls below 4000mV.</td>
      <td>Ring buzzer for 5 seconds, stop motors, blink RED LED, and display a low battery message on the serial monitor.</td>
      <td><strong>Pass</strong>: System behaved as expected under low battery conditions.</td>
    </tr>
    <tr>
      <td>HRS 9</td>
      <td>Try implementing line following as part of task demonstration</td>
      <td>Integrate QTR sensors, motors, and push buttons to enable line-following functionality.</td>
      <td>Bot follows a line after configuration via button presses.</td>
      <td><strong>Partially Achieved</strong>: Motors and sensors were configured, but calibration issues affected line-following performance.</td>
    </tr>
  </tbody>
</table>


## 8. Main Issues Faced

### 8.1 Baud Rate Mismatch

During the configuration and testing of the XBee communication with the ATmega328P microcontroller, we encountered a significant issue with the baud rate. Despite configuring the system to operate at a baud rate of <b>115200</b>, we observed an error in data transmission. The data received was inconsistent and appeared to be sent at approximately <b>140000 baud</b>, leading to about <b>20% error in UART communication.</b>

• <b>Root Cause:</b>

After thorough debugging, we realized that the ATmega328P microcontroller was operating at a 20 MHz clock frequency instead of the expected 16 MHz. The incorrect assumption of the clock frequency had resulted in inaccurate prescaler calculations for the UART baud rate, causing the mismatch.

• <b>Resolution</b>:To resolve this issue:

• <b>Prescaler Adjustment:</b> We recalculated the prescaler value for the UART baud rate based on the 20 MHz clock frequency, ensuring accurate baud rate settings.

• Verification with <b>Saleae Logic Analyzer:</b>
    We used a Saleae Logic Analyzer to analyze the transmitted and received UART signals.
    The logic analyzer allowed us to confirm the actual baud rate being transmitted and verify that the adjusted prescaler correctly aligned the transmission rate with the configured baud rate of 115200.


## 9. Power Management

![alt text](Images/4_PowerManagement.png)

<p>• The power management system in the 3pi robot is a sophisticated design that ensures optimal performance for the device, even as battery voltage fluctuates during operation. The system addresses the challenge of inconsistent battery voltage from four AAA cells, which can range between 3.5 V and 5.5 V (or even up to 6 V for alkaline batteries). This variability makes direct voltage regulation to 5 V impractical. To overcome this, the 3pi employs a dual-regulation approach, utilizing both a switching regulator and a linear regulator.</p>

<p>• First, the switching regulator boosts the battery voltage to a stable 9.25 V (Vboost), which is used to power the motors and IR LEDs in the line sensors. Then, a linear regulator reduces Vboost to 5 V (VCC), supplying the microcontroller and digital circuitry. This dual-regulation method provides several advantages. The motors benefit from higher voltage and, consequently, more power without increased current demand, enabling consistent performance regardless of battery depletion. Additionally, the regulated voltage ensures that motor speeds remain constant, simplifying programming tasks such as timed turns. Furthermore, the higher voltage enables the IR LEDs to be powered in series, minimizing power consumption.</p>

<p>• The system also incorporates a voltage monitoring circuit to help track battery status. This is achieved using a voltage divider, which scales the battery voltage to a level safely below the microcontroller's 5 V maximum analog input. This scaled voltage is fed to an ADC input and converted into the actual battery voltage using a simple formula. We monitored the battery voltage by a function, read_battery_millivolts_3pi(), that automates this process by averaging ten ADC samples and returning the battery voltage in millivolts.</p>

![alt text](Images/5_PowerPin.png)

• In summary, the 3pi’s power management system ensures maximum performance until the battery is fully drained, offering regulated voltage for reliable operation of all components while monitoring battery health for proactive power management.

## 10. Detailed Explaination of Hardware Implementation

### 10.1 Motors

The Pololu 3pi robot uses brushed DC motors with a gear ratio of 30:1, which are ideal for the lightweight and agile design of the 3pi robot. The details are as follows:<br>

### Motor Design and Characteristics:<br>
•Brushed DC Motor: The motors operate with permanent magnets and electromagnetic coils, offering a reliable mechanism for the small and efficient Pololu 3pi.<br>
#### Key Specifications:<br>
• Free-Running Speed: 700 rpm (rotations per minute) without any load.<br>
• Free-Running Current: 60 mA, ensuring low power consumption during operation.<br>
• Stall Torque: 6 oz-in (ounce-inches), providing sufficient force for the robot to overcome minor obstacles.<br>
• Stall Current: 540 mA, which the motor draws under maximum load conditions.<br>

#### Gear Ratio and Torque:<br>
• A 30:1 gear ratio is employed, which reduces the speed and increases the torque by a factor of 30. This is crucial for tasks like:<br>
    Precise movement during line-following.<br>
    Overcoming resistance from friction or uneven surfaces.<br>
•The gear ratio ensures that even though the motor spins rapidly, the robot achieves smooth and controlled movements.
Differential Drive System:<br>
•Each wheel of the 3pi robot is connected to an independent motor, enabling tank-style movement:<br>
    Both motors moving forward at the same speed: The robot moves straight.<br>
    One motor faster than the other: The robot turns.<br>
    Motors moving in opposite directions: The robot spins in place.<br>
•This setup allows the robot to make sharp turns and maintain a steady trajectory along the line.<br>
PWM Control:<br>
•Pulse Width Modulation (PWM): The motor speed is controlled by varying the duty cycle of the PWM signal.<br>
•The onboard TB6612FNG motor driver chip generates PWM signals linked to the Timer2 in the ATmega328 microcontroller.<br>
•By changing the PWM duty cycle, the motors achieve:<br>
    Smooth acceleration and deceleration: Gradual adjustments in speed ensure stability.<br>
    Precise directional control: The robot follows curves with minimal overshooting.<br>

### 10.2 Sensors

The Pololu 3pi uses five reflectance sensors mounted underneath the chassis for line detection. These sensors are critical for determining the position of the robot on a line and ensuring accurate navigation. Here's a detailed breakdown:<br>
Reflectance Sensor Design:<br>
•Phototransistor-Based Sensors: The sensors use phototransistors to measure reflected light intensity. Bright surfaces reflect more light, while dark surfaces reflect less.<br>
•The key components include:<br>
    Infrared Emitter: Sends light to the surface.<br>
    Phototransistor Detector: Measures the amount of reflected infrared light.<br>
Operation of Reflectance Sensors:<br>
•The reflectance sensors are connected to the microcontroller’s digital inputs, such as PC0 (Port C).<br>
•A capacitor discharge mechanism is used:<br>
    The sensor pin is charged to 5V and then set to an input.<br>
    The capacitor discharges through the phototransistor, and the rate of discharge depends on the reflectance.<br>
    The microcontroller measures the time taken for the pin to drop below a certain threshold voltage.<br>
•Output Range:<br>
    White surfaces cause rapid discharge and low sensor values.<br>
    Black surfaces cause slow discharge and high sensor values.<br>
Sensor Layout and Coverage:<br>
•Five sensors are arranged in a row beneath the robot, ensuring wide coverage of the line.<br>
•This layout allows the robot to detect curves and edges effectively, maintaining its trajectory even in complex paths.<br>

### 10.3 Mircrocontroller and H-Bridge Motor Driver

Microcontroller: ATmega328<br>
•The ATmega328P microcontroller handles motor control, sensor data processing, and high-level decision-making.<br>
•Timers and Ports Used:<br>
    Timer2: Generates PWM signals for motor speed control.<br>
    Port C (PC0-PC4): Interfaces with the reflectance sensors.<br>
H-Bridge Motor Driver:<br>
•The onboard TB6612FNG motor driver chip uses H-Bridge circuits to control motor direction.<br>
•Directional Logic:<br>
    Motors are controlled by toggling the logic levels of PD5, PD6 (Motor 1) and PD3, PB3 (Motor 2).<br>
    Example configurations:<br>
    PD5 = 1, PD6 = 0: Motor 1 moves forward.<br>
    PD5 = 0, PD6 = 1: Motor 1 reverses.<br>
•Coasting and Braking:<br>
    Motors can be set to coast (no movement) or brake (immediate stop) by configuring the H-Bridge logic.<br>
4. Buttons and Additional Inputs<br>
Buttons for User Control:<br>
•PB4 (Button B): Used for toggling between starting and stopping the robot.<br>
    The button is connected with a pull-up resistor to avoid floating input values.<br>
    Pressing the button sets the corresponding input to logic low (0), triggering the desired functionality in the firmware.<br>



### 11. Video Implementations

Video link to final demo:
[Link](https://drive.google.com/file/d/18RFZoYMZ_O98KFYrI4eGMwchdLWHGtCn/view?usp=drive_link)



Link showing interfacing led and pushbuttons:
[Link](https://drive.google.com/file/d/1S4Z-eInoQ7wf2noCODETjuOZ1mt6ME1N/view?usp=sharing)


Link to showing working of buzzer and led blinking:
[Link](https://drive.google.com/file/d/1IsLDWu6bf9tx6z9PqTOx2AZyhzqks5P4/view?usp=drive_link)

Link to video showing working of IR sesnosrs:
[Link](https://drive.google.com/file/d/1L7b0nwyDtBVQVn3g3IIqXnq-lpMjQe97/view?usp=drive_link)

Link to video showing wirless communication between 2 xbees:
[Link](https://drive.google.com/file/d/1N9SaClY3qcYWlyZ3d0JNDajOq4S42tjL/view?usp=sharing)


Link showing wireless communication from xbee to atmega:
[Link](https://drive.google.com/file/d/1um7ZsDng7-yxWcuwBKc0DoomefzdZ1Ut/view?usp=drive_link)


Link showing wireless communication from atmega to xbee:
[Link](https://drive.google.com/file/d/19bvlWNmOn_qIHddz2FfXGzltxhePZOj-/view?usp=drive_link)


Link to a video showcasing the wireless control of the bot's motors:
 [Link](https://drive.google.com/file/d/1foPRAMkwSOQCrFttxfK9oeal0Zd3ZwFI/view?usp=drive_link)


Link to a video showing Motor and QTR sensors working together (Facing Calibration Issues):
  [Link](https://drive.google.com/file/d/1ZaagUqCAhBXo545llPBmGqV77pNaJmeO/view?usp=drive_link)


### 12.  Hardware Implementation

