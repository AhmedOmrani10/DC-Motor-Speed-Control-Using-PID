# DC Motor Speed Control Using PID – MATLAB/Simulink

This project implements a closed-loop speed control system for a separately excited DC motor using a PID controller in MATLAB/Simulink.  
The goal is to maintain a desired reference speed under different load conditions by adjusting the motor's armature voltage.

---

## 🚀 Project Overview

This model contains:
- A DC motor (5 HP, 240 V, 1750 RPM, Field = 150 V)
- A PID controller for feedback control
- A Controlled Voltage Source driving the armature
- A Load Torque input (TL)
- A closed-loop system: measurement → feedback → PID → motor
- Speed measurement converted from rad/s to RPM
- Reference tracking for target speed

---

## ⚡ DC Motor Model

### Motor Terminals

| Terminal | Function |
|----------|----------|
| A+ / A- | Armature voltage input |
| F+ / F- | Field voltage input |
| TL      | Load torque input |
| M       | Mechanical output bus |

### Mechanical Output Bus (M)

```
M.w  → angular speed (rad/s)
M.Te → electromagnetic torque (N·m)
M.th → rotor position (rad)
```

---

## 📐 Motor Mathematical Model

### 1. Electrical Armature Equation

```math
Va = Ra * ia + La * dia/dt + Ke * ω
```

### 2. Electromagnetic Torque

```math
Te = Kt * ia
```

### 3. Mechanical Dynamics

```math
J * dω/dt + B * ω + TL = Te
```

---

## 🔁 Closed-Loop Speed Control

### Speed Conversion (rad/s → RPM)

```matlab
RPM = omega * 60 / (2*pi);
```

### Error Signal

```matlab
error = speed_ref - speed_measured;
```

### PID Control Law

```matlab
Va = Kp * error + Ki * integral(error) + Kd * derivative(error);
```

### Application to Motor

The PID output is fed into the Controlled Voltage Source connected to:

```
A+ / A-
```

---

## 🏋️ Load Torque (TL)

Rated torque calculation:

```matlab
P = 5 * 746;              
omega_rated = 1750 * 2*pi/60;
T_rated = P / omega_rated;   % ≈ 20.3 N·m
```

Simulation example:

```matlab
TL = 12; % N*m
```

---

## 📊 Simulation Results

### With PID Controller
- Fast response
- Low overshoot
- Stable speed regulation
- Handles load disturbances well

### Without PID
- Large steady-state error
- Slower response
- Oscillation

---
