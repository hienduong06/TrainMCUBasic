
# Basic Microcontroller Training

A beginner-friendly introduction to microcontrollers, GPIO, ADC, PWM, UART, and basic circuit protection. This training material helps students understand fundamental microcontroller concepts through theoretical slides and practical circuit implementation.

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

## Microcontroller Integration Project

This project allows learners to apply GPIO, ADC, PWM, and UART concepts to a practical application. Learners must choose **one of the two project options** below and implement it using physical Arduino hardware or a circuit simulator that supports the required transistor driver circuit.

### Implementation Options

- **Proteus:** Circuit simulation and microcontroller development, provided the required driver circuit can be modeled.
- **Physical Arduino hardware:** Use this option when the required transistor driver circuit cannot be represented accurately in a simulator.

### General Hardware Configuration

The following configuration applies to both project options unless otherwise specified.

| Component | Arduino Pin | Function |
|---|---|---|
| Potentiometer (5–10 kΩ) | A0 | Simulates an analog sensor input |
| Push button | D2 | Requests an immediate measurement report |
| Green LED | D4 | Indicates a normal or optimal operating state |
| Red LED | D5 | Indicates a warning or abnormal state |
| PWM output | D6 for Option A; D3 for Option B | Provides the PWM control signal |
| Transistor driver circuit | Connected to the PWM output circuit | Drives the specified load through the required driver circuit |

**Platform specifications:**
- Arduino Uno R3 with a 5 V logic level.
- 10-bit ADC with readings from 0 to 1023.
- UART communication at 9600 baud.
- Use an appropriate current-limiting resistor for each indicator LED.
- Configure the push button using either pull-up or pull-down logic, with the circuit and code matching the chosen configuration.
- The required transistor driver circuit must be included and tested; an indicator LED alone does not replace the required driver circuit.

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
| Implementation method | Implement the selected project using a simulator that supports the required driver circuit, or a physical Arduino Uno R3. |
| ADC conversion | Correctly map ADC readings to the specified physical quantity and range. |
| State management | Implement the operating rules using clear conditional logic. |
| PWM control | Use a supported Arduino PWM pin and map the input value to the required output duty cycle. |
| Serial monitoring | Display measurements, operating states, and warning messages through the Serial Monitor. |
| Circuit design | Connect the indicator LEDs, push button, potentiometer, and required transistor driver circuit correctly. |
| Testing | Test values below, within, and above each threshold to verify all operating states. Test the transistor driver circuit separately under appropriate conditions. |
| Code quality | Use readable variable names, clear state-handling logic, and comments for important functions. |
| Submission | Submit the source code, circuit diagram or simulation project, and screenshots showing the circuit and test results. |

## Learning Objectives

After completing this training, learners should be able to:

- Explain the basic structure and applications of a microcontroller.
- Identify common pins and understand their functions.
- Configure GPIO pins for digital input and output.
- Explain the operation of pull-up and pull-down resistors.
- Understand the basic principles of ADC, PWM, and UART.
- Understand common circuit protection techniques.
- Build and test basic microcontroller circuits using a suitable simulator or physical hardware.
- Integrate analog inputs, digital inputs, LEDs, PWM outputs, and UART communication into a practical embedded application.
- Implement threshold-based state detection and warning logic.

## Tools and Platforms

- **Arduino Uno R3 / ATmega328P:** MCU hardware examples and project implementation.
- **ESP32:** GPIO and embedded application examples.
- **Proteus:** Circuit simulation platform, subject to support for the required driver circuit.
- **Serial Monitor:** UART output monitoring and debugging.

## Learning Materials

The accompanying presentation, `TrainMCU.pptx`, contains the training slides and circuit diagrams.

---

*This repository documents basic microcontroller training materials and an integration project for embedded systems beginners.*
