
# Basic Microcontroller Training

A beginner-friendly introduction to microcontrollers, GPIO, ADC, PWM, UART, and basic circuit protection. This training material helps students understand fundamental microcontroller concepts through theoretical slides and practical simulations using Wokwi.

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
- GPIO output
- GPIO input
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

## Practical Exercises

The following Wokwi simulations provide hands-on practice with the concepts covered in the training.

| Topic | Wokwi Simulation |
|---|---|
| GPIO Output | [Open Simulation](https://wokwi.com/projects/478110191827204097) |
| GPIO Input | [Open Simulation](https://wokwi.com/projects/478110864126049281) |
| GPIO Input: External Pull-up and Pull-down | [Open Simulation](https://wokwi.com/projects/478112105509218305) |
| GPIO Input: Internal Pull-up and Pull-down | [Open Simulation](https://wokwi.com/projects/478114146827119617) |
| ADC | [Open Simulation](https://wokwi.com/projects/478119122963112961) |

## Microcontroller Integration Project

This project allows learners to apply GPIO, ADC, PWM, and UART concepts to a practical application. Learners must choose **one of the two project options** below and implement it using Wokwi, another circuit simulation tool, or physical Arduino hardware.

### Simulation Resources

- [Wokwi](https://wokwi.com/) — Online Arduino simulator.
- [Proteus](https://www.labcenter.com/) — Circuit simulation and microcontroller development.
- [Tinkercad Circuits](https://www.tinkercad.com/circuits) — Browser-based electronics simulation.

### General Hardware Configuration

The following configuration applies to both project options unless otherwise specified.

| Component | Arduino Pin | Function |
|---|---|---|
| Potentiometer (5–10 kΩ) | A0 | Simulates an analog sensor input |
| Push button | D2 | Requests an immediate measurement report |
| Green LED | D4 | Indicates a normal or optimal operating state |
| Red LED | D5 | Indicates a warning or abnormal state |
| PWM output | D6 for Option A; D3 for Option B | Controls LED brightness or simulates an output control signal |
| C1815 NPN transistor | Connected to the PWM output circuit | Drives a suitable external load when required |

**Platform specifications:**
- Arduino Uno R3 with a 5 V logic level.
- 10-bit ADC with readings from 0 to 1023.
- UART communication at 9600 baud.
- Use an appropriate current-limiting resistor for each LED.
- Configure the push button using either pull-up or pull-down logic, with the circuit and code matching the chosen configuration.

### Option A: Automotive Engine Temperature Warning System

#### 1. Technical Background

The Engine Coolant Temperature (ECT) sensor provides temperature information to the Engine Control Unit (ECU). The ECU uses this information to manage engine cooling and help detect overheating conditions.

In this simplified project, a potentiometer simulates the ECT sensor. Arduino reads the analog input, converts it into an estimated engine temperature, controls the indicator LEDs and PWM output, and sends measurement and warning information through UART.

#### 2. Functional Requirements

| Requirement | Description |
|---|---|
| Temperature simulation | Map ADC readings from 0–1023 to an engine temperature range of 0–120 °C. |
| State detection | Determine the operating state based on the temperature thresholds below. |
| LED indication | Use the green and red LEDs to indicate the current state. |
| PWM control | Increase PWM duty cycle as the temperature rises within the high-temperature range. |
| UART monitoring | Display the current temperature and operating state through the Serial Monitor. |
| Button input | When the button is pressed, immediately print the current temperature and operating state. |
| Overheat warning | Continuously send `ENGINE OVERHEAT` while the engine is in the overheat state. |

#### 3. Operating Rules

| Engine Temperature | Operating State | Green LED | Red LED | PWM Output |
|---|---|---|---|---|
| 0–90 °C | NORMAL | ON | OFF | 0% |
| >90–105 °C | HIGH TEMPERATURE | OFF | OFF | 10–100%, increasing with temperature |
| >105 °C | ENGINE OVERHEAT | OFF | Blinking | 100% |

The Serial Monitor must display the measured temperature and current state. When the temperature exceeds 105 °C, the system must continuously output the warning message `ENGINE OVERHEAT`.

### Option B: Solar Charging Monitoring System

#### 1. Technical Background

Solar charging systems use measurements such as solar irradiance, voltage, and current to evaluate available solar power and manage charging.

In this simplified project, a potentiometer simulates solar irradiance. Arduino converts the analog input into an estimated irradiance value, indicates the charging state through LEDs, adjusts the PWM output when conditions are suitable, and sends monitoring information through UART.

**Note:** This is a basic monitoring and PWM-control simulation, not a complete Maximum Power Point Tracking (MPPT) implementation. A real MPPT controller requires voltage and current measurements and an algorithm to optimize the operating power.

#### 2. Functional Requirements

| Requirement | Description |
|---|---|
| Irradiance simulation | Map ADC readings from 0–1023 to a solar irradiance range of 0–1200 W/m². |
| State detection | Determine the charging state based on the irradiance thresholds below. |
| LED indication | Use the green and red LEDs to indicate the current state. |
| PWM control | Increase PWM duty cycle as irradiance rises within the optimal charging range. |
| UART monitoring | Display the current irradiance and charging state through the Serial Monitor. |
| Button input | When the button is pressed, immediately print the current irradiance and charging state. |
| Overpower warning | Send `OVERPOWER WARNING` when the irradiance exceeds 1000 W/m². |

#### 3. Operating Rules

| Solar Irradiance | Operating State | Green LED | Red LED | PWM Output |
|---|---|---|---|---|
| 0–200 W/m² | LOW IRRADIANCE | OFF | OFF | 0% |
| >200–1000 W/m² | OPTIMAL CHARGING | ON | OFF | 10–100%, increasing with irradiance |
| >1000 W/m² | OVERLOAD RISK | OFF | ON | 0% |

The Serial Monitor must display the measured irradiance and current charging state. When irradiance exceeds 1000 W/m², the system must send `OVERPOWER WARNING`.

### General Implementation Requirements

| Requirement | Description |
|---|---|
| Simulation or hardware | Implement the selected project using Wokwi, Proteus, Tinkercad Circuits, or a physical Arduino Uno R3. |
| ADC conversion | Correctly map ADC readings to the specified physical quantity and range. |
| State management | Implement the operating rules using clear conditional logic. |
| PWM control | Use a supported Arduino PWM pin and map the input value to the required output duty cycle. |
| Serial monitoring | Display measurements, operating states, and warning messages through the Serial Monitor. |
| Circuit design | Connect the LEDs, push button, potentiometer, and transistor driver correctly. |
| Testing | Test values below, within, and above each threshold to verify all operating states. |
| Code quality | Use readable variable names, clear state-handling logic, and comments for important functions. |
| Submission | Submit the source code and circuit diagram or simulation project. Include screenshots or a shareable Wokwi project link when applicable. |

### Wokwi Simulation Guide

1. Open [Wokwi](https://wokwi.com/) and create a new Arduino Uno project.
2. Add the potentiometer, push button, green LED, red LED, and PWM output components.
3. Connect each component according to the pin configuration specified for the selected option.
4. Implement the program in `sketch.ino`.
5. Start the simulation and open the Serial Monitor to observe measurements, state changes, and warning messages.
6. Adjust the potentiometer to test values below, at, and above each threshold.
7. Press the button to verify that the system immediately reports the current measurement and state.
8. Save the project and submit its shareable link along with the source code.

**Simulation note:** Wokwi is suitable for testing Arduino GPIO, ADC, PWM, push-button input, and UART behavior. If a C1815 transistor model is unavailable or unsuitable, use a supported transistor model where appropriate, or verify the transistor driver circuit separately on physical hardware. An LED can be used to verify PWM logic during initial testing, but it does not replace testing the actual driver circuit when one is required.

## Learning Objectives

After completing this training, learners should be able to:

- Explain the basic structure and applications of a microcontroller.
- Identify common pins and understand their functions.
- Configure GPIO pins for digital input and output.
- Explain the operation of pull-up and pull-down resistors.
- Understand the basic principles of ADC, PWM, and UART.
- Understand common circuit protection techniques.
- Build and test basic microcontroller circuits using Wokwi.
- Integrate analog inputs, digital inputs, LEDs, PWM outputs, and UART communication into a practical embedded application.
- Implement threshold-based state detection and warning logic.

## Tools and Platforms

- **Wokwi:** Online microcontroller simulator.
- **Arduino Uno R3 / ATmega328P:** MCU hardware examples and project implementation.
- **ESP32:** GPIO and embedded application examples.
- **Proteus:** Alternative circuit simulation platform.
- **Tinkercad Circuits:** Alternative browser-based electronics simulator.
- **Serial Monitor:** UART output monitoring and debugging.

## Learning Materials

The accompanying presentation, `TrainMCU.pptx`, contains the training slides and circuit diagrams.

---

*This repository documents basic microcontroller training materials, Wokwi simulations, and an integration project for embedded systems beginners.*
