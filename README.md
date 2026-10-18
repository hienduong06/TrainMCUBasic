
# Basic Microcontroller Training

A beginner-friendly introduction to microcontrollers, GPIO, ADC, PWM, UART, and basic circuit protection. This training material helps students understand fundamental microcontroller concepts through theoretical slides and practical simulations.

## Presenter

**Duong Trung Hien**  
Member of the Automotive Powertrain Research Club

## Contents

### 1. Introduction to Microcontrollers
- What is a microcontroller (MCU)?
- Basic MCU architecture and hardware components
- Applications in automotive systems and renewable energy

### 2. Basic MCU Hardware
- ATmega328P and Arduino Uno R3 pinout
- ESP32 GPIO pinout
- Digital and analog pins

### 3. GPIO and Digital Signal Handling
- GPIO Output
- GPIO Input
- Pull-up and pull-down resistors
- Understanding digital HIGH and LOW logic levels

### 4. Analog Input and Communication
- Analog-to-Digital Converter (ADC)
- Pulse Width Modulation (PWM)
- Universal Asynchronous Receiver-Transmitter (UART)

### 5. Basic Circuit Protection
- Voltage divider
- Reverse-polarity protection diode
- Optocoupler for electrical isolation
- Transistor-based output driving

## Practical Exercises

The following Wokwi simulations provide hands-on practice with the concepts covered in the training.

| Topic | Wokwi Simulation |
|---|---|
| GPIO Output | [Open Simulation](https://wokwi.com/projects/478110191827204097) |
| GPIO Input | [Open Simulation](https://wokwi.com/projects/478110864126049281) |
| GPIO Input: External Pull-up and Pull-down | [Open Simulation](https://wokwi.com/projects/478112105509218305) |
| GPIO Input: Internal Pull-up and Pull-down | [Open Simulation](https://wokwi.com/projects/478114146827119617) |
| ADC | [Open Simulation](https://wokwi.com/projects/478119122963112961) |

## Integrated Microcontroller Project

### Project Overview

This final project combines the fundamental concepts covered in the training into an integrated microcontroller application. Learners can choose one of two application domains: automotive systems or renewable energy.

The project can be implemented using Proteus, Tinkercad, or a physical Arduino setup. The objective is to apply analog and digital input processing, output control, PWM, UART communication, and transistor-based output driving in a practical engineering scenario.

### Project Options

| Criteria | Option A: Automotive Systems | Option B: Renewable Energy |
|---|---|---|
| Project Title | Automotive Engine Temperature Warning ECU | Solar Charging Monitoring System |
| Main Controller | Arduino Uno R3 | Arduino Uno R3 |
| Logic Voltage | 0–5 V GPIO | 0–5 V GPIO |
| UART Baud Rate | 9600 bps | 9600 bps |
| Analog Input (ADC) | 5 kΩ or 10 kΩ potentiometer simulating engine temperature from 0–120°C | 5 kΩ or 10 kΩ potentiometer simulating solar irradiance from 0–1200 W/m² |
| Digital Input | Push button for system status requests | Push button for system status requests |
| Digital Outputs | Green LED for normal status; red LED for alarm | Green LED for charging status; red LED for alarm |
| PWM Output | PWM LED simulating cooling fan speed | PWM LED simulating charging power regulation |
| Output Protection | C1815 NPN transistor driving stage | C1815 NPN transistor driving stage |
| Serial Monitoring | Engine temperature and overheat warnings | Solar irradiance and overload warnings |

### Option A: Automotive Systems — Engine Temperature Warning ECU

#### 1. Engineering Background

In a vehicle, the Engine Control Unit (ECU) receives analog signals from the Engine Coolant Temperature (ECT) sensor, processes the measurements, and controls the cooling fan through a PWM signal. When the engine overheats, the ECU also generates a warning for the driver.

In this training project, a potentiometer simulates the temperature sensor, LEDs represent the engine and cooling system status, and the Serial Monitor displays temperature measurements and warning messages.

#### 2. Functional Requirements

- Read the potentiometer's analog signal using the Arduino's 10-bit ADC.
- Convert the ADC reading (0–1023) into an engine temperature range of 0–120°C.
- Read the push button through a digital input using an internal pull-up or an appropriate pull-down circuit.
- Control the green LED through a digital output to indicate normal engine temperature.
- Adjust the brightness of a PWM LED in proportion to engine temperature to simulate cooling fan speed control.
- Transmit the current engine temperature and the `ENGINE OVERHEAT` warning to the computer through UART using the Serial Monitor.
- Implement an output-driving and protection circuit using a C1815 NPN transistor to drive the PWM LED.
- Display the current temperature and engine status immediately when the push button is pressed.

#### 3. System Specifications

**Controller:** Arduino Uno R3

| Component | Arduino Pin | Function |
|---|---|---|
| Potentiometer | A0 | Analog temperature input |
| Push button | D2 | System status request |
| Green LED | D4 | Normal engine status |
| Red LED | D5 | Overheat alarm |
| PWM LED | D6 | Simulated cooling fan speed |
| UART | USB Serial | Temperature and warning messages |

**Communication:** 9600 bps

**ADC resolution:** 10-bit, with readings from 0 to 1023.

**Temperature conversion:**

`Temperature (°C) = ADC Reading × 120 / 1023`

#### 4. Operating Logic

| Engine Temperature | Status | Green LED | Red LED | PWM LED |
|---|---|---|---|---|
| 0–90°C | NORMAL | ON | OFF | OFF |
| Above 90°C to 105°C | HIGH TEMPERATURE | OFF | OFF | Brightness increases from approximately 10% to 100% |
| Above 105°C | ENGINE OVERHEAT | OFF | Blinking | 100% duty cycle |

During the `ENGINE OVERHEAT` condition, the system continuously transmits an overheat warning through UART.

When the push button is pressed, the system immediately reports the current temperature and engine status through the Serial Monitor.

### Option B: Renewable Energy — Solar Charging Monitoring System

#### 1. Engineering Background

In a solar power system, a Maximum Power Point Tracking (MPPT) charge controller monitors operating conditions and adjusts its control strategy to extract available power from photovoltaic panels. The controller regulates a power converter to manage charging of the battery storage system.

In this training project, a potentiometer simulates solar irradiance, while LEDs represent charging status and overload conditions. A PWM LED simulates the adjustment of charging power according to the available solar resource.

**Note:** This is a simplified educational simulation. A potentiometer does not measure actual solar irradiance, and the PWM output does not implement a real MPPT algorithm or directly regulate a physical battery charger.

#### 2. Functional Requirements

- Read the potentiometer's analog signal using the Arduino's 10-bit ADC.
- Convert the ADC reading (0–1023) into a solar irradiance range of 0–1200 W/m².
- Read the push button through a digital input to detect user requests for system information.
- Control the green LED through a digital output to indicate normal charging conditions.
- Adjust the PWM LED brightness in proportion to solar irradiance to simulate charging power regulation.
- Transmit solar irradiance measurements and the `OVERPOWER WARNING` message through UART using the Serial Monitor.
- Implement an output-driving and protection circuit using a C1815 NPN transistor to drive the PWM LED.
- Immediately display the current irradiance and charging status when the push button is pressed.
- Turn off the simulated PWM charging output when the irradiance exceeds the defined safety threshold.

#### 3. System Specifications

**Controller:** Arduino Uno R3

| Component | Arduino Pin | Function |
|---|---|---|
| Potentiometer | A0 | Analog solar irradiance input |
| Push button | D2 | System status request |
| Green LED | D4 | Normal charging status |
| Red LED | D5 | Overload warning |
| PWM LED | D3 | Simulated charging power |
| UART | USB Serial | Irradiance and warning messages |

**Communication:** 9600 bps

**ADC resolution:** 10-bit, with readings from 0 to 1023.

**Irradiance conversion:**

`Irradiance (W/m²) = ADC Reading × 1200 / 1023`

#### 4. Operating Logic

| Solar Irradiance | Status | Green LED | Red LED | PWM LED |
|---|---|---|---|---|
| 0–200 W/m² | LOW IRRADIANCE | OFF | OFF | OFF |
| Above 200 to 1000 W/m² | OPTIMAL CHARGING | ON | OFF | Brightness increases from approximately 10% to 100% |
| Above 1000 W/m² | OVERLOAD RISK | OFF | ON | OFF |

When the irradiance exceeds 1000 W/m², the system disables the simulated PWM charging output and transmits the `OVERPOWER WARNING` message through UART.

When the push button is pressed, the system immediately reports the current solar irradiance and charging status through the Serial Monitor.

#### 5. Implementation Notes

- Use a suitable current-limiting resistor for each LED.
- Connect the potentiometer between 5 V and GND, with its wiper connected to A0.
- Configure the push button consistently with the selected pull-up or pull-down method.
- Use the C1815 transistor as an output-driving stage, with appropriate base and load resistors.
- Verify the transistor pinout against its datasheet before wiring.
- Configure the Serial Monitor to 9600 baud.
- On the Arduino Uno R3, D3, D5, D6, D9, D10, and D11 support hardware PWM.
- Ensure that the transistor's current and power ratings are suitable for the load. A transistor used to drive an LED is not, by itself, a complete protection circuit for a real cooling fan or battery charger.

### Project Deliverables

Learners should submit the following items:

1. **Circuit Design:** A schematic or simulation showing the Arduino Uno R3, potentiometer, push button, LEDs, and transistor-driving stage.
2. **Arduino Source Code:** A complete program implementing ADC conversion, digital input handling, output control, PWM, and UART communication.
3. **Simulation or Hardware Demonstration:** A working project in Proteus, Tinkercad, or on a physical Arduino setup.
4. **Test Results:** Evidence that the system responds correctly to different input values and button presses.
5. **Technical Explanation:** A brief description of the operating logic, pin assignments, ADC conversion, PWM control, and output protection circuit.

### Learning Outcomes

After completing the integrated project, learners should be able to:

- Apply ADC to convert analog input signals into meaningful engineering measurements.
- Implement digital input handling with push buttons and pull-up or pull-down resistors.
- Control LEDs and other simulated outputs through digital GPIO.
- Use PWM to simulate variable-speed or variable-power control.
- Communicate system measurements and warning messages through UART.
- Implement a basic transistor-based output-driving stage.
- Develop a simple embedded monitoring and warning system for an automotive or renewable energy application.
- Test and explain system behavior under normal, warning, and alarm conditions.

## Learning Objectives

After completing this training, learners should be able to:

- Explain the basic structure and applications of a microcontroller.
- Identify common pins and understand their functions.
- Configure GPIO pins for digital input and output.
- Explain the operation of pull-up and pull-down resistors.
- Understand the basic principles of ADC, PWM, and UART.
- Understand common circuit protection techniques.
- Apply microcontroller concepts to an integrated engineering project.
- Practice embedded system design through circuit simulations or physical hardware implementation.

## Tools and Platforms

- **Arduino Uno R3 / ATmega328P:** Main microcontroller platform for the training project.
- **ESP32:** GPIO and embedded application examples.
- **Wokwi:** Online microcontroller simulator for the basic practical exercises.
- **Proteus / Tinkercad:** Alternative platforms for circuit simulation and project implementation.
- **Arduino IDE:** Source code development, compilation, and uploading.
- **Serial Monitor:** UART communication and real-time system monitoring.

## Learning Materials

The accompanying presentation, `TrainMCU.pptx`, contains the training slides and circuit diagrams.

## Project Scope

The integrated project is intended for educational purposes. The automotive option simulates engine temperature monitoring and cooling fan control, while the renewable energy option simulates solar irradiance monitoring and charging status indication. Neither option represents a production-ready automotive ECU or a complete MPPT battery charging controller.

---

*This repository documents basic microcontroller training materials and practical exercises for embedded systems beginners, with applications in automotive electronics and renewable energy.*
