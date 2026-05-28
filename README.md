# LogixPRO PLC Ladder Logic - Process Automation Projects

🏆 **Part of 1st Place Ranking - IEEE ASUB Workshop Final Assessment (Score: 98.2%)**

A comprehensive collection of Process Automation projects developed in LogixPRO PLC simulation software. These projects demonstrate practical ladder logic programming, sequential control, sensor integration, and industrial automation workflows.

**Workshop:** IEEE ASUB Workshop - Automation & Industrial Control  
**Software:** LogixPRO (Allen-Bradley PLC Simulator)  
**Programming Language:** Ladder Logic (IEC 61131-3)  
**Focus Area:** PLC Programming & Process Automation  
**Developed by:** Ali Mohamed Ahmed, Mechatronics & Robotics Engineering Student (Ain Shams University)

---

## 💼 Technical Expertise

This repository represents hands-on PLC programming projects developed during intensive training in:
- **Ladder Logic Programming** - IEC 61131-3 standard compliance
- **PLC Fundamentals** - Input/Output handling, memory, scan cycles
- **Sequential Control** - State machines and process sequences
- **Sensor Integration** - Digital and analog input processing
- **Actuator Control** - Motor control, solenoid operations, valve control
- **Timers & Counters** - Timing logic and event counting
- **Data Handling** - Register manipulation and data storage
- **Simulation & Testing** - Real-time PLC simulation and debugging

**Related Skills:** CAD Simu electrical schematics, MATLAB/Simulink, SolidWorks CAD/CAM (CSWA), CNC Operations

---

## 📋 Overview

LogixPRO is an industry-standard PLC simulator that allows engineers and students to develop and test ladder logic programs in a safe virtual environment. This collection showcases 6+ process automation projects demonstrating real-world automation scenarios including:

- Sequential machine operations
- Conveyor system control
- Liquid level monitoring and control
- Traffic light coordination
- Motor sequencing and interlocking
- Multi-sensor data processing
- Process safety and fault detection

Each project includes complete ladder logic code, documentation, and simulation results.

---

## 🎯 Key Projects

### Project 1: Basic Motor Control - Start/Stop with Latching Logic
![stop](images/stop)  
**Description:** Fundamental PLC exercise demonstrating start/stop motor control with latching relay logic using basic contacts and coils.  
**Key Components:**
- Start button (I:1/0) - Initiates motor operation
- Stop button (I:1/1) - Halts motor operation
- Output coil (O:2/0) - Motor control output
- Latching mechanism - Holds motor in RUN state
- Output indicator showing active status

**Complexity Level:** Beginner  
**Runtime:** < 1 second  
**Key Learning Outcomes:**
- Input/output addressing (I:x/y, O:x/y format)
- Latching coil operation
- Basic motor start/stop logic
- Contact series and parallel combinations
- Real-time output visualization

**Control Logic:**
```
When START button (I:1/0) is pressed:
  └─ Energize output coil (O:2/0)
  └─ Latch coil to maintain state

When STOP button (I:1/1) is pressed:
  └─ De-energize output coil
  └─ Reset latched state
```

**I/O Configuration:**
- **Input I:1/0:** Start button (NO contact)
- **Input I:1/1:** Stop button (NC contact)
- **Output O:2/0:** Motor output control

---

### Project 2: Multi-Motor Forward/Reverse Control
![start_stop](images/start_stop)  
**Description:** Advanced motor control demonstrating forward/reverse operation with mechanical interlocks to prevent simultaneous activation.  
**Key Components:**
- Forward button (start control)
- Reverse button (stop control)
- Multiple output paths for FWD/REV operations
- Protective logic preventing both directions active simultaneously
- Status outputs (O:2/0, O:2/1, O:2/2)

**Complexity Level:** Intermediate  
**Runtime:** 10-15 seconds  
**Key Learning Outcomes:**
- Bidirectional motor control patterns
- Electrical interlocking logic
- Prevention of hazardous conditions
- Output multiplexing
- Safety-first control design

**Control Logic:**
```
Forward Path:
  START → Enable forward contactor (FWD)
  └─ Prevent REV output simultaneously

Reverse Path:
  START (alternate) → Enable reverse contactor (REV)
  └─ Prevent FWD output simultaneously

STOP:
  └─ De-energize both FWD and REV outputs
```

**Safety Features:**
- Mutual exclusion logic (FWD OR REV, never both)
- Clear output indication
- Emergency stop capability

---

### Project 3: Complex Batch Mix Simulator with Multi-Sensor Integration
 
![simple_batch](images/simple_batch)
**Description:** Industrial-grade process automation controlling a batch mixing system with multiple pumps, flowmeters, heater, and level sensors.  
**Simulated Equipment:**
- **Flowmeter 1 (I:1/05):** Measures inlet flow
- **Flowmeter 2 (I:1/06):** Monitors alternative inlet
- **Pump 1 (O:2/01):** Primary inlet pump
- **Pump 2 (O:2/02):** Secondary inlet pump
- **Pump 3 (O:2/03):** Outlet/drain pump
- **Mixer (O:2/00):** Mixing motor control
- **Heater (O:2/04):** Temperature control element
- **Flowmeter 3 (I:1/07):** Exit flow monitoring
- **HI-LEVEL (I:1/04):** Tank fill level sensor
- **LO-LEVEL (I:1/03):** Tank empty level sensor
- **Thermostat (I:1/02):** Temperature monitoring

**Complexity Level:** Advanced  
**Runtime:** 3-5 minutes (full batch cycle)  
**Key Learning Outcomes:**
- Multi-sensor data acquisition and interpretation
- Process sequencing and timing
- Pump interlocking to prevent dangerous combinations
- Temperature monitoring and control
- Level-based conditional logic
- Real-time process visualization
- Industrial automation best practices

**Batch Process Sequence:**
```
1. INITIALIZATION
   └─ Check LOW-LEVEL sensor
   └─ Verify all outputs ready

2. FILLING PHASE
   └─ Activate Pump 1 (primary inlet)
   └─ Monitor Flowmeter 1
   └─ Check for HIGH-LEVEL threshold
   └─ Stop Pump 1 when full

3. HEATING PHASE
   └─ Enable Mixer motor
   └─ Activate Heater element
   └─ Monitor Temperature via Thermostat
   └─ Wait for target temperature

4. MIXING PHASE
   └─ Maintain Mixer operation
   └─ Continue heating if needed
   └─ Monitor temperature stability

5. DRAIN PHASE
   └─ Stop Mixer and Heater
   └─ Activate Pump 3 (outlet)
   └─ Monitor Flowmeter 3
   └─ Verify LOW-LEVEL signal
```

**I/O Mapping:**
| Address | Component | Type | Function |
|---------|-----------|------|----------|
| I:1/02 | Thermostat | Input | Temperature feedback |
| I:1/03 | LO-LEVEL | Input | Tank empty detection |
| I:1/04 | HI-LEVEL | Input | Tank full detection |
| I:1/05 | Flowmeter 1 | Input | Inlet flow monitoring |
| I:1/06 | Flowmeter 2 | Input | Secondary inlet |
| I:1/07 | Flowmeter 3 | Input | Outlet flow monitoring |
| O:2/00 | Mixer | Output | Mixing motor control |
| O:2/01 | Pump 1 | Output | Primary inlet pump |
| O:2/02 | Pump 2 | Output | Secondary inlet pump |
| O:2/03 | Pump 3 | Output | Outlet pump |
| O:2/04 | Heater | Output | Heating element |

**Safety Interlocks:**
- ✅ Prevent pump operation without level sensors
- ✅ Prevent heater without mixer running
- ✅ Prevent simultaneous inlet/outlet operation
- ✅ Automatic shutdown on temperature overshoot
- ✅ Emergency stop functionality

**Real-time Monitoring:**
- Live tank visualization
- Temperature display (Thermostat I:1/02)
- Flowmeter readings
- Motor status indicators
- System state feedback

---

### Project 4: Advanced Batch Processing with Comparison Logic
![Advanced Batch] 
**Description:** Enhanced batch system demonstrating advanced comparison operations, threshold detection, and conditional branching for complex process control.  
**Key Components:**
- **Comparison blocks:** LEQ (Less Than or Equal), GEQ (Greater Than or Equal)
- **Multiple threshold detection:** Lower, upper, and safety limits
- **Conditional outputs:** Different actions based on value ranges
- **Data source blocks:** T4:0 ACC and T4:0 ACC2 (analog data)
- **Multi-stage logic:** Sequential decision making

**Complexity Level:** Advanced  
**Runtime:** 5-10 minutes  
**Key Learning Outcomes:**
- Comparison instruction (LEQ, GEQ, LES, GRT)
- Threshold-based control logic
- Multi-condition decision trees
- Analog value processing
- Source B parameter usage
- Complex conditional branching
- Industrial measurement integration

**Comparison Logic Implemented:**
```
Source Values:
  ├─ Source A: T4:0 ACC (Primary measurement)
  └─ Source B: 50, 30, or 0018h (threshold values)

Comparison Operations:
  ├─ LEQ (Less Than or Equal): Output TRUE if Source A ≤ Source B
  ├─ GEQ (Greater Than or Equal): Output TRUE if Source A ≥ Source B
  └─ GRT (Greater Than): Output TRUE if Source A > Source B

Output Actions:
  ├─ O:2/1: Triggered by LEQ condition
  ├─ O:2/2: Triggered by GEQ condition
  └─ O:2/3: Triggered by combined logic
```

**Safety Features:**
- Multiple threshold levels for process control
- Cascading comparisons for fail-safe operation
- Hysteresis to prevent oscillation
- Emergency override logic

---

### Project 5: Advanced Timer-Based Sequencing System
**File:** Multi-timer sequencing project  
**Description:** Sophisticated control system using 4 Timer On Delay (TON) blocks to create complex sequential operations with precise timing control.  
**Key Components:**
- **Timer T1 (TON):** Initial delay/startup phase
  - Preset: 30 (0.1 second base = 3 seconds)
  - Time Base: 0.1 seconds
- **Timer T2 (TON):** Inter-stage delay
  - Preset: 30 (3 seconds)
  - Accumulator: Tracking current time
- **Timer T3 (TON):** Main operation timing
  - Preset: 30 (3 seconds)
  - Monitors M1 activation
- **Timer T4 (TON):** Extended duration control
  - Preset: 15 (1.5 seconds with 0.1 base)
  - Extended accumulation

**Complexity Level:** Advanced  
**Runtime:** 20-30 seconds (complete sequence)  
**Key Learning Outcomes:**
- TON (Timer On Delay) instruction programming
- Cascading timer logic
- Time-base configuration (0.1 second precision)
- Sequential activation with delays
- Accumulator monitoring
- Stage completion detection
- Multi-step process automation

**Sequencing Timeline:**
```
t=0.0s   ├─ START button pressed
         └─ T1 begins timing

t=3.0s   ├─ T1 completes (preset 30 × 0.1s)
         ├─ T2 begins
         └─ First output activated

t=6.0s   ├─ T2 completes
         ├─ T3 begins
         ├─ Mixer/Motor M1 starts
         └─ T4 begins in parallel

t=7.5s   ├─ T4 completes (preset 15)
         └─ Secondary operation triggered

t=9.0s   ├─ T3 completes
         ├─ All motors stop
         └─ Sequence ready for reset
```

**I/O Configuration:**
- **Inputs:** Start/Stop controls, Timer feedback
- **Outputs:** M1 (motor), M2 (secondary), operational flags
- **Timers:** T1, T2, T3, T4 with synchronized presets

**Key Features:**
- ✅ Precise 0.1 second resolution
- ✅ Overlapping timer operations for parallel activities
- ✅ Accumulator tracking for diagnostics
- ✅ Clear timing visualization in simulation
- ✅ Scalable to longer durations

---

### Project 6: Multi-Motor Coordination with Timer Interlocking
**File:** Advanced sequencing session  
**Description:** Complex automation controlling multiple motors (M1, M2, M3) with interlock timing, preventing simultaneous operation and ensuring safe sequential activation.  
**Key Components:**
- **Motor M1:** Primary motor with timer control (T4:ON logic)
- **Motor M2:** Secondary motor with cascade logic
- **Motor M3:** Tertiary motor with dependent timing
- **Timers T4, T5, T6:** Sequential operation control
- **Interlock Coils:** T1, T2, M1, M3 preventing unsafe combinations
- **Safety Logic:** Ensures only one motor active per phase

**Complexity Level:** Advanced  
**Runtime:** 30-45 seconds  
**Key Learning Outcomes:**
- Multi-motor safety interlocking
- Timer-based motor sequencing
- Cascade activation logic
- Preventing simultaneous motor startup
- State machine implementation
- Fault tolerance design
- Industrial sequencing standards

**Operational Sequence:**
```
Phase 1: Motor M1 Only
  ├─ T4:ON energizes M1
  ├─ T1 prevents M2 activation
  └─ Duration: 5-10 seconds

Phase 2: M1 Off, M2 Active
  ├─ T4 times out
  ├─ T5 triggers M2
  ├─ Interlock prevents M1 re-activation
  └─ Duration: 5-10 seconds

Phase 3: M2 Off, M3 Active
  ├─ T5 times out
  ├─ T6 triggers M3
  ├─ Both M1 and M2 interlocked
  └─ Duration: 5-10 seconds

Phase 4: All Motors Off
  ├─ All timers expire
  ├─ System reset ready
  └─ Safe for next cycle
```

**Safety Interlocks:**
- ✅ NO two motors simultaneously active
- ✅ T1/T2 coils prevent backward transitions
- ✅ M1/M3 coils block conflicting operations
- ✅ Cascade failure prevents stuck states
- ✅ Clear emergency stop path

---

### Project 7: Advanced Comparison Logic with Multi-Path Branching
**File:** Session 5 - Advanced comparison operations  
**Description:** Sophisticated control system utilizing comparison instructions (LEQ, GEQ) with multiple parallel evaluation paths for complex decision-making.  
**Key Components:**
- **LEQ Blocks (Rung 002-004, 006):** Less Than or Equal comparisons
  - Source A: Various inputs (T4:0 ACC, measurement data)
  - Source B: Multiple thresholds (50, 30, 0018h)
  - Outputs: O:2/1, O:2/2, O:2/3, O:2/4
- **GEQ Blocks (Rung 003):** Greater Than or Equal comparisons
  - Complex nested logic
  - Multi-condition evaluation
- **Output Combinations:** 6 different comparison paths generating 4 outputs
- **Advanced Triggering:** B3:0/1 control bits manage output state

**Complexity Level:** Advanced+  
**Runtime:** 3-5 minutes  
**Key Learning Outcomes:**
- LEQ (Less Than or Equal) instruction mastery
- GEQ (Greater Than or Equal) instruction mastery
- Parallel comparison evaluation
- Multi-source data handling
- Output priority and sequencing
- Complex decision logic implementation
- Industrial process optimization
- Data-driven control systems

**Comparison Matrix:**
```
Rung 002:
  ├─ LEQ: T4:0 ACC ≤ 50 → O:2/1
  └─ GEQ: T4:0 ACC ≥ 30 → O:2/2

Rung 003:
  ├─ LEQ: T4:0 ACC ≤ 30 → O:2/2
  └─ GEQ: T4:0 ACC ≥ 0018h → O:2/3

Rung 004:
  ├─ GEQ: T4:0 ACC ≥ 50 → O:2/4
  └─ Multiple source B options (50, 30, 0018h)

Rung 006:
  ├─ Combined LEQ/GEQ logic
  └─ Final output states determined
```

**Outputs Generated:**
| Output | Trigger Condition | Application |
|--------|-------------------|-------------|
| O:2/1 | Value ≤ 50 | Low threshold response |
| O:2/2 | 30 ≤ Value ≤ 50 | Mid-range operation |
| O:2/3 | Value ≥ 0018h | High threshold action |
| O:2/4 | Value > 50 | Overshoot protection |

**Practical Applications:**
- ✅ Temperature-based equipment control
- ✅ Pressure regulation systems
- ✅ Flow rate management
- ✅ Level monitoring with hysteresis
- ✅ Load balancing systems
- ✅ Multi-stage process automation

---

## 🎯 Mini Projects & Quick Wins

This section showcases smaller, focused automation projects and specialized work that complement the 7 main LogixPRO projects.

### Mini Project 1: Simple Start/Stop Logic
**Description:** Foundational PLC exercise demonstrating basic input/output control without timing logic.  
**Key Concepts:**
- Single input switch controlling single output
- NO and NC contact combinations
- Direct coil energization
- Immediate response without delays

**Complexity Level:** Beginner  
**Runtime:** < 1 second  
**Key Learning:** Understanding PLC I/O basics

---

### Mini Project 2: Indicator Light Control
**Description:** Multi-input logic controlling indicator light states based on system conditions.  
**Key Concepts:**
- Combining multiple inputs with AND/OR logic
- Output logic based on system state
- Status indication best practices
- Conditional light activation

**Complexity Level:** Beginner  
**Runtime:** Immediate  
**Key Learning:** Multi-input decision logic

---

### Mini Project 3: Simple Alarm Logic
**Description:** Threshold-based alarm generation with acknowledgment capability.  
**Key Concepts:**
- Threshold detection
- Alarm triggering and reset
- Acknowledgment button logic
- Alert output control

**Complexity Level:** Beginner  
**Runtime:** 2-5 seconds  
**Key Learning:** Alarm system fundamentals

---

### Mini Project 4: Pulse Generator
**Description:** Creates timed pulse signals for triggering periodic events.  
**Key Concepts:**
- Using timers to create pulses
- Frequency control
- Duty cycle manipulation
- One-shot logic implementation

**Complexity Level:** Intermediate  
**Runtime:** Continuous (5+ minutes)  
**Key Learning:** Pulse timing and frequency

---

### Mini Project 5: Toggle Switch Logic
**Description:** Single button that toggles output on/off with latching relay logic.  
**Key Concepts:**
- Latching coil operation
- Unlatching (reset) coil
- Toggle mechanism
- Memory-based control

**Complexity Level:** Beginner-Intermediate  
**Runtime:** Immediate  
**Key Learning:** Latching and state retention

---

### Mini Project 6: Light Dimming Sequencer
**Description:** Progressive brightness control using multiple light outputs.  
**Key Concepts:**
- Sequential output activation
- Cascading logic patterns
- Brightness simulation via output sequence
- Timer-controlled progression

**Complexity Level:** Intermediate  
**Runtime:** 10-15 seconds  
**Key Learning:** Sequential light activation

---

### Mini Project 7: Temperature Threshold Alert
**Description:** Simulated temperature monitoring with upper/lower limit detection.  
**Key Concepts:**
- Analog signal interpretation (simulated)
- Upper and lower threshold logic
- Hysteresis to prevent oscillation
- Dual-state alarm output

**Complexity Level:** Intermediate  
**Runtime:** 3-5 minutes  
**Key Learning:** Threshold detection patterns

---

### Mini Project 8: Pump Run Counter
**Description:** Counts number of pump operation cycles for maintenance tracking.  
**Key Concepts:**
- Counter up instruction (CTU)
- Reset after threshold
- Cycle tracking
- Data accumulation

**Complexity Level:** Intermediate  
**Runtime:** 5+ minutes  
**Key Learning:** Counter usage and data tracking

---

### Mini Project 9: Safety Interlock Demo
**Description:** Demonstrates critical safety logic preventing dangerous simultaneous operations.  
**Key Concepts:**
- Mechanical safety interlocks
- Electrical interlock logic
- Priority-based control
- Safe shutdown procedures

**Complexity Level:** Intermediate  
**Runtime:** 10 seconds  
**Key Learning:** Safety-first design principles

---

### Mini Project 10: Blinking Light Pattern
**Description:** Creates repeating light blink patterns using timer logic.  
**Key Concepts:**
- Timer-based On/Off cycling
- Pattern creation
- Frequency adjustment
- Visual feedback simulation

**Complexity Level:** Beginner  
**Runtime:** Continuous  
**Key Learning:** Oscillating signals with timers

---

## 📋 Mini Projects Quick Reference

| # | Project Name | Skills | Complexity | Runtime |
|---|--------------|--------|-----------|---------|
| 1 | Start/Stop Logic | I/O Basics | ⭐ | <1s |
| 2 | Indicator Light Control | Multi-input Logic | ⭐ | Immediate |
| 3 | Simple Alarm Logic | Thresholds | ⭐ | 2-5s |
| 4 | Pulse Generator | Timers | ⭐⭐ | 5+ min |
| 5 | Toggle Switch Logic | Latching | ⭐⭐ | Immediate |
| 6 | Light Dimming Sequencer | Sequential Logic | ⭐⭐ | 10-15s |
| 7 | Temperature Threshold Alert | Threshold Detection | ⭐⭐ | 3-5 min |
| 8 | Pump Run Counter | Counters | ⭐⭐ | 5+ min |
| 9 | Safety Interlock Demo | Safety Logic | ⭐⭐ | 10s |
| 10 | Blinking Light Pattern | Timer Oscillation | ⭐ | Continuous |

---

## 📁 Project Structure

```
LogixPRO_Projects/
├── README.md (This file)
│
├── Main_Projects/
│   ├── Project_1_Basic_Fundamentals/
│   │   ├── BasicLogic.l5x
│   │   ├── README.md
│   │   ├── Ladder_Diagram.pdf
│   │   └── Documentation/
│   │
│   ├── Project_2_Traffic_Light_Controller/
│   │   ├── TrafficLight.l5x
│   │   ├── README.md
│   │   └── Documentation/
│   │
│   ├── Project_3_Conveyor_Belt_Control/
│   │   ├── ConveyorControl.l5x
│   │   ├── README.md
│   │   └── Documentation/
│   │
│   ├── Project_4_Tank_Level_Control/
│   │   ├── TankLevel.l5x
│   │   ├── README.md
│   │   └── Documentation/
│   │
│   ├── Project_5_Multi_Motor_Sequencing/
│   │   ├── MultiMotorSequence.l5x
│   │   ├── README.md
│   │   └── Documentation/
│   │
│   ├── Project_6_Process_Control_DataLogging/
│   │   ├── ProcessControl.l5x
│   │   ├── README.md
│   │   └── Documentation/
│   │
│   └── Project_7_Fault_Detection_Redundancy/
│       ├── FaultDetection.l5x
│       ├── README.md
│       └── Documentation/
│
├── Mini_Projects/
│   ├── Mini_1_StartStop_Logic/
│   │   ├── StartStop.l5x
│   │   └── README.md
│   ├── Mini_2_Indicator_Light/
│   │   ├── IndicatorLight.l5x
│   │   └── README.md
│   ├── Mini_3_Alarm_Logic/
│   │   ├── AlarmLogic.l5x
│   │   └── README.md
│   ├── Mini_4_Pulse_Generator/
│   │   ├── PulseGenerator.l5x
│   │   └── README.md
│   ├── Mini_5_Toggle_Switch/
│   │   ├── ToggleSwitch.l5x
│   │   └── README.md
│   ├── Mini_6_Light_Dimmer/
│   │   ├── LightDimmer.l5x
│   │   └── README.md
│   ├── Mini_7_Temp_Threshold/
│   │   ├── TempThreshold.l5x
│   │   └── README.md
│   ├── Mini_8_Pump_Counter/
│   │   ├── PumpCounter.l5x
│   │   └── README.md
│   ├── Mini_9_Safety_Interlock/
│   │   ├── SafetyInterlock.l5x
│   │   └── README.md
│   └── Mini_10_Blinking_Pattern/
│       ├── BlinkingLight.l5x
│       └── README.md
│
└── Resources/
    ├── Standards_References.md
    ├── Troubleshooting_Guide.md
    └── Learning_Path.md
```

---

## 🚀 Getting Started

### Prerequisites
- **LogixPRO Software** (Allen-Bradley PLC simulator)
  - Download from: [Rockwell Automation](https://www.rockwellautomation.com/)
  - Supports Windows XP SP3 and later
  - Requires ~50MB disk space
- **Basic understanding** of electrical circuits and relay logic
- **Familiarity** with PLC concepts (scan cycle, I/O, memory)

### Installation Steps

1. **Download and Install LogixPRO:**
   ```
   - Visit Rockwell Automation's official website
   - Download LogixPRO setup file
   - Run installer and follow default installation
   - Launch LogixPRO from Start Menu
   ```

2. **Clone or Download This Repository:**
   ```bash
   git clone https://github.com/alimo2004-creator/logixpro-automation.git
   cd logixpro-automation
   ```

3. **Open a Project:**
   - Launch LogixPRO
   - Go to File → Open
   - Navigate to desired project folder
   - Open the `.l5x` file (LogixPRO project file)
   - Review the ladder logic diagram
   - Run simulation by clicking the RUN button

4. **Experiment & Learn:**
   - Modify input values using on-screen controls
   - Observe real-time output changes
   - Review ladder logic step-by-step
   - Check memory/register values in data view

---

## 🔧 LogixPRO Features & Capabilities

### Ladder Logic Elements Used

| Element | Symbol | Function |
|---------|--------|----------|
| **Input Contact (NO)** | `-\|-` | Read input status |
| **Input Contact (NC)** | `-//-` | Negated input logic |
| **Output Coil** | `-(O)-` | Energize output |
| **Latching Coil** | `-(L)-` | Set and hold output |
| **Unlatching Coil** | `-(U)-` | Reset held output |
| **Timer On Delay** | `TON` | Delay before activation |
| **Timer Off Delay** | `TOF` | Delay after deactivation |
| **Counter Up** | `CTU` | Increment on trigger |
| **Counter Down** | `CTD` | Decrement on trigger |
| **Compare Equal** | `EQU` | Test equality condition |
| **Compare Greater** | `GRT` | Test greater-than condition |
| **Compare Less** | `LES` | Test less-than condition |
| **Move Block** | `MOV` | Copy data between registers |
| **Add Block** | `ADD` | Arithmetic addition |

### Instruction Types

**Timer Instructions:**
- **TON (Timer On Delay):** Accumulates time while input is TRUE
- **TOF (Timer Off Delay):** Accumulates time while input is FALSE
- **RTO (Retentive Timer):** Maintains accumulated time through scan cycles

**Counter Instructions:**
- **CTU (Count Up):** Increments accumulated count on rising edge
- **CTD (Count Down):** Decrements accumulated count on rising edge
- **Reset Instruction:** Clears timer/counter accumulated value

**Data Instructions:**
- **MOV (Move):** Transfers data from source to destination
- **ADD, SUB, MUL, DIV:** Basic arithmetic operations
- **Comparison Blocks:** EQU, GRT, LES, GEQ, LEQ, NEQ

---

## 📊 Technical Specifications

| Aspect | Details |
|--------|---------|
| **Software** | LogixPRO (Allen-Bradley PLC Simulator) |
| **Programming Language** | Ladder Logic (IEC 61131-3) |
| **File Format** | `.l5x` (LogixPRO native format) |
| **PLC Type Simulated** | Allen-Bradley CompactLogix/MicroLogix |
| **Simulation Type** | Real-time discrete and combinatorial logic |
| **Number of Projects** | 7 comprehensive process automation projects |
| **Complexity Range** | Beginner to Advanced |
| **Runtime Environment** | Windows (XP SP3 and later) |

---

## 💡 Key Concepts Demonstrated

### Fundamental Ladder Logic Concepts
- ✅ Series (AND) logic combinations
- ✅ Parallel (OR) logic combinations
- ✅ Input contact addressing and status
- ✅ Output coil energization and control
- ✅ Latching and unlatching circuits
- ✅ Normally Open (NO) and Normally Closed (NC) contacts

### Timing & Sequencing
- ✅ Timer On Delay (TON) for delayed activation
- ✅ Timer Off Delay (TOF) for delayed deactivation
- ✅ Retentive Timer (RTO) for persistent timing
- ✅ Multi-stage sequencing with staggered starts
- ✅ Pulse generation and one-shot logic
- ✅ Cyclical operation timing

### Counting & Data Management
- ✅ Up counters (CTU) for event tracking
- ✅ Down counters (CTD) for countdown operations
- ✅ Counter reset and accumulation
- ✅ Register manipulation and data transfer
- ✅ Arithmetic operations (ADD, SUB, MUL, DIV)
- ✅ Data comparison and threshold detection

### Process Control
- ✅ Sequential process automation
- ✅ Pump/valve interlocking
- ✅ Motor soft-start and soft-stop
- ✅ Level and temperature monitoring
- ✅ Dual-state machine implementation
- ✅ Hysteresis control for stability

### Safety & Fault Handling
- ✅ Emergency stop logic (hard-wired and software)
- ✅ Overload protection and detection
- ✅ Watchdog timer for system health
- ✅ Redundancy and voting logic
- ✅ Graceful degradation modes
- ✅ Error detection and recovery

### Advanced Topics
- ✅ State machine design patterns
- ✅ Multi-output coordination
- ✅ Sensor data fusion
- ✅ Alarm prioritization
- ✅ Diagnostic and self-test logic
- ✅ Memory management and registers

---

## 🎓 Learning Path & Progression

### Phase 1: Fundamentals (Projects 1-2)
**What You'll Learn:**
- Basic ladder logic syntax and symbols
- Input and output addressing
- Contact and coil operations
- Simple combinatorial logic
- Timer fundamentals (TON, TOF)
- State-based sequencing

**Time to Complete:** 4-6 hours  
**Recommended Order:** Project 1 → Project 2

### Phase 2: Intermediate Automation (Projects 3-4)
**What You'll Learn:**
- Motor control logic patterns
- Multi-sensor integration
- Safety interlock design
- Pump/valve sequencing
- Hysteresis and threshold logic
- Status indication and monitoring

**Time to Complete:** 8-10 hours  
**Recommended Order:** Project 3 → Project 4

### Phase 3: Advanced Process Control (Projects 5-7)
**What You'll Learn:**
- Complex state machines
- Multi-component coordination
- Counter and data register usage
- Fault detection patterns
- Redundancy and voting logic
- System diagnostics

**Time to Complete:** 12-16 hours  
**Recommended Order:** Project 5 → Project 6 → Project 7

**Total Learning Time:** 24-32 hours for complete mastery

---

## 📝 How to Use These Projects

### For Learning & Understanding:

1. **Study the Ladder Logic:**
   - Open the `.l5x` file in LogixPRO
   - Review the complete ladder diagram
   - Identify input contacts and output coils
   - Trace logic paths through the circuit
   - Understand the control flow and sequences

2. **Simulate & Experiment:**
   - Switch LogixPRO to RUN mode
   - Toggle input switches using the simulator panel
   - Observe real-time output changes
   - Watch timer and counter accumulation
   - Test edge cases and error conditions

3. **Modify & Test:**
   - Change timer preset values
   - Adjust counter targets
   - Modify threshold values
   - Add new logic branches
   - Document your changes
   - Test thoroughly before implementation

4. **Reference the Documentation:**
   - Read project-specific READMEs
   - Review logic explanation documents
   - Check simulation results and test cases
   - Study state machine diagrams
   - Reference component descriptions

### For Industry Applications:

- **Adapt circuits** for your specific automation tasks
- **Use as templates** for similar process automation
- **Study safety patterns** for interlock design
- **Reference best practices** in ladder logic
- **Implement diagnostics** from fault detection projects
- **Apply sequencing logic** to multi-machine systems

### For Teaching & Training:

- **Use progressively** from beginner to advanced projects
- **Show simulation results** for classroom demonstrations
- **Have students modify** projects to understand concepts
- **Reference diagrams** in presentations and materials
- **Discuss design choices** and alternative approaches

---

## 🔌 Ladder Logic Conventions

### Addressing Scheme (Allen-Bradley Style)

| Address Type | Format | Example | Meaning |
|--------------|--------|---------|---------|
| **Input Bit** | `I:x/y` | `I:0/0` | Input module 0, bit 0 |
| **Output Bit** | `O:x/y` | `O:0/0` | Output module 0, bit 0 |
| **Internal Bit** | `B3/x` | `B3/1` | Internal bit memory location 1 |
| **Timer** | `T4:x` | `T4:0` | Timer element 0 |
| **Counter** | `C5:x` | `C5:0` | Counter element 0 |
| **Integer Register** | `N7:x` | `N7:5` | Integer register 5 |

### Scan Cycle Operation

LogixPRO operates on a continuous scan cycle:

```
1. INPUT SCAN
   └─ Read all input values

2. LOGIC SCAN
   └─ Execute ladder logic from top to bottom
   └─ Evaluate all contacts and coils
   └─ Update internal memory and timers

3. OUTPUT SCAN
   └─ Write all output values
   └─ Update physical I/O (or simulator)

4. REPEAT
   └─ Return to step 1
```

**Scan Time:** Typically 10-50 ms depending on program complexity

---

## 🛠️ Troubleshooting & Tips

### Common Issues

| Problem | Cause | Solution |
|---------|-------|----------|
| **Output not energizing** | Input contact not TRUE | Verify input logic path; check contact status |
| **Timer not timing** | Rung not powered or improper setup | Verify timer enable condition; check preset value |
| **Counter not counting** | Missing rising-edge trigger | Ensure counter trigger comes from powered rung |
| **Latching not holding** | Unlatching coil energizing immediately | Add logic to prevent immediate reset |
| **Simulation too fast/slow** | Scan time setting incorrect | Adjust simulation speed in menu |

### Best Practices

✅ **Clear Naming:** Use descriptive labels for contacts, coils, timers  
✅ **Documentation:** Comment complex logic sections  
✅ **Modular Design:** Organize logic into functional sections  
✅ **Testing:** Verify all input combinations before deployment  
✅ **Safety First:** Always include emergency stop logic  
✅ **Redundancy:** Use redundant logic for critical functions  
✅ **Error Handling:** Plan for unexpected input conditions  
✅ **Memory Efficient:** Avoid unnecessary duplicate logic  

---

## 📊 Expected Learning Outcomes

After completing these 7 projects, you will be able to:

- ✅ Write complete ladder logic programs from specifications
- ✅ Design timer-based sequential control systems
- ✅ Implement multi-sensor data acquisition logic
- ✅ Create robust safety interlock circuits
- ✅ Develop state machines for complex processes
- ✅ Debug and troubleshoot ladder logic programs
- ✅ Optimize logic for clarity and efficiency
- ✅ Implement fault detection and recovery logic
- ✅ Design redundant systems with voting logic
- ✅ Create professional PLC documentation
- ✅ Prepare ladder logic for real hardware implementation

---

## 🤝 Contributing

Contributions and improvements welcome! Help expand this collection.

### How to Contribute:

1. **Fork the repository:**
   ```bash
   git clone https://github.com/alimo2004-creator/logixpro-automation.git
   ```

2. **Create a feature branch:**
   ```bash
   git checkout -b feature/new-automation-project
   ```

3. **Add your project:**
   - Create new project folder with clear naming
   - Include `.l5x` LogixPRO file
   - Add detailed README explaining the automation
   - Document all ladder logic sections
   - Include PDF export of ladder diagram
   - Test thoroughly in simulation
   - Document expected behavior and test cases

4. **Commit and push:**
   ```bash
   git add .
   git commit -m 'Add: [Project Name] - [Brief Description]'
   git push origin feature/new-automation-project
   ```

5. **Open a Pull Request**

### Contribution Guidelines:
- ✅ Use clear, commented ladder logic
- ✅ Follow Allen-Bradley addressing conventions
- ✅ Include comprehensive documentation
- ✅ Test all scenarios before submission
- ✅ Provide state machine diagrams where applicable
- ✅ Document safety considerations
- ✅ Include simulation results

---

## 📋 Documentation Checklist

For each project submission:
- [ ] `.l5x` LogixPRO project file
- [ ] Project-specific README.md
- [ ] PDF export of ladder diagram
- [ ] Logic explanation document
- [ ] State machine or sequence diagram (if applicable)
- [ ] Component/I/O description list
- [ ] Test cases and expected results
- [ ] Simulation screenshots/results
- [ ] Safety and interlock documentation
- [ ] Troubleshooting guide

---

## 📄 License

[MIT License](LICENSE) - Feel free to use, modify, and distribute these educational PLC projects.

---

## 🙏 Acknowledgments

- **IEEE ASUB Workshop** - Comprehensive training in automation and industrial control
- **Rockwell Automation** - LogixPRO simulator and educational resources
- **Allen-Bradley** - Industry-standard PLC programming conventions
- **PLC Community** - Best practices in ladder logic design
- **Workshop Instructors & Peers** - Collaborative learning environment

---

## 👤 Author

**Ali Mohamed Ahmed**  
Mechatronics & Robotics Engineering Student | Ain Shams University  
**Email:** alimohamedahmedhassan2004@gmail.com  
**Phone:** +20 1020120158  
**Location:** Nasr City, Cairo, Egypt  

**Certifications:**
- 🏆 IEEE Automation & Industrial Control - Ranked 1st (98.2%)
- 🏆 CSWA (Certified SolidWorks Associate)
- 🏆 OSHA Occupational Health & Safety
- 🏆 PMI Project Management

**GitHub:** [alimo2004-creator](https://github.com/alimo2004-creator)  
**LinkedIn:** [Ali Mohamed Ahmed](https://www.linkedin.com/in/ali-mohamed-ahmed)  

---

## 📞 Support & Contact

### Getting Help:
- 📧 **Email:** alimohamedahmedhassan2004@gmail.com
- 💬 **GitHub Issues:** Report bugs or ask questions
- 💡 **Discussions:** Share ideas and solutions
- 🔗 **LinkedIn:** [Connect with me](https://www.linkedin.com/in/ali-mohamed-ahmed)
- 📱 **WhatsApp:** +20 1020120158

### Frequently Asked Questions:

**Q: How do I simulate these programs in LogixPRO?**  
A: Open the `.l5x` file in LogixPRO, press the RUN button, and use the simulator panel to toggle inputs. Observe output changes in real-time.

**Q: Can I export ladder diagrams to PDF?**  
A: Yes! In LogixPRO, go to File → Print → Print to PDF to generate professional diagrams.

**Q: What Allen-Bradley PLC models are compatible?**  
A: LogixPRO simulates CompactLogix and MicroLogix platforms. Code adapts to other Allen-Bradley platforms with minor modifications.

**Q: Can I use these programs on real hardware?**  
A: Yes, but verify I/O addressing and add necessary safety checks. Test thoroughly before production use.

**Q: How can I modify timer values or thresholds?**  
A: Double-click the timer or comparison block, edit the preset/threshold values, and recompile.

**Q: What's the difference between TON and TOF?**  
A: **TON** (On Delay) counts while enabled and resets when disabled. **TOF** (Off Delay) continues counting after disabling. Choose based on your sequence needs.

---

## 📅 Repository Information

**Created:** 2026  
**Last Updated:** [Update with your date]  
**Version:** 1.0  
**Status:** Active Development  

---

## 🚀 Future Enhancements

Planned additions to the repository:
- [ ] Video tutorials for each project
- [ ] Interactive simulation walkthroughs
- [ ] Conversion to RSLogix 500/Studio 5000 formats
- [ ] CompactLogix hardware implementation guides
- [ ] Advanced analog I/O projects
- [ ] Network communication projects
- [ ] Human-Machine Interface (HMI) integration
- [ ] Energy monitoring and optimization circuits
- [ ] Predictive maintenance logic

---

## 📊 Repository Statistics

- **Total Projects:** 7 comprehensive process automation projects
- **Total Ladder Logic Rungs:** 100+ interconnected logic elements
- **Complexity Levels:** Beginner to Advanced+
- **Simulation Time Required:** 24-32 hours for mastery
- **Real-World Applications:** 50+

---

**⭐ If you find these PLC projects helpful and educational, please consider leaving a star!**

**🔗 Share your learning journey using #LogixPRO #PLCProgramming #IEEEASUBWorkshop #LadderLogic**

---

## 📚 Additional Learning Resources

### Official Documentation
- [Rockwell Automation LogixPRO Documentation](https://www.rockwellautomation.com/)
- [Allen-Bradley PLC Programming Manual](https://ab.rockwellautomation.com/)
- IEC 61131-3 Standard Specification

### Recommended Textbooks
- **"Programmable Logic Controllers"** by Frank Petruzella
- **"Industrial Control Electronics"** by Joseph Chapple
- **"Automation and Robotics"** - IEEE ASUB Workshop materials

### Online Communities
- Allen-Bradley User Community
- PLCdev Forum
- Automation and Control Forum

---

**Last Section Updated:** May 28, 2026
