# Amogha_Bharadwaj_Electric_Vehicle_Cruise_Control
Electric Vehicle Cruise Control System using a PI Controller designed in MATLAB and Simulink to maintain constant vehicle speed under varying road conditions. The system includes a road slope disturbance introduced at t=10s to analyze controller stability and disturbance rejection capability
#  Electric Vehicle Cruise Control — PI Control System

> A MATLAB/Simulink project for designing and simulating a PI controller to maintain constant EV speed under varying road conditions, including road slope disturbances.

---

##  Problem Statement

Design a cruise control system for an Electric Vehicle that maintains a constant normalized speed of **1.0** under a road slope disturbance introduced at **t = 10s** to evaluate controller stability and disturbance rejection capability.

The longitudinal vehicle dynamics are approximated by the first-order transfer function:

$$G(s) = \frac{1}{5s + 1}$$

| Signal | Description |
|--------|-------------|
| Input | Motor torque / control effort |
| Output | Normalized vehicle speed |
| Disturbance | Road slope load at t = 10s (step, magnitude −0.2) |

---

##  Control Objectives

The designed controller must satisfy:

-  Overshoot < **10%**
-  Settling time < **10 seconds**
-  Steady-state error ≈ **0**
-  System remains **stable under road slope disturbance**

---

##  Tasks

1. Build and simulate the closed-loop PI control system in Simulink
2. Introduce road slope disturbance at t = 10s and evaluate rejection
3. Analyze speed tracking, control effort, and tracking error signals
4. Run a flyover animation to visualize PI controller response under varying gradient

---

##  Repository Structure

```
EV-CruiseControl/
│
├── EV_Simulink_Advanced.m      # Simulink model builder + simulation runner
├── EV_Hackathon_Advanced.m     # Hackathon variant with same model (extended analysis)
├── EV_Car_Animation.m          # Flyover animation script (run after Simulink script)
├── EV_CruiseControl_Advanced.slx  # Auto-generated Simulink model file
└── README.md                   # This file
```

---

##  PI Controller Parameters

| Parameter | Value |
|-----------|-------|
| Kp (Proportional) | 11.75 |
| Ki (Integral) | 11.25 |

The controller was tuned to achieve fast disturbance rejection with minimal overshoot for the first-order vehicle plant.

---

##  Simulation Results

The MATLAB script (`EV_Simulink_Advanced.m`) builds the Simulink model programmatically and generates the following plots:

| Figure Panel | Description |
|--------------|-------------|
| Panel 1 — Speed Tracking | Actual vehicle speed vs reference (1.0) with ±2% tolerance band |
| Panel 2 — Control Effort | PI controller output signal over time with peak annotation |
| Panel 3 — Tracking Error | Error signal (e = r − y) showing disturbance impact and recovery |

A **scrolling flyover car animation** (`EV_Car_Animation.m`) is also included, showing the EV navigating a flyover ramp. The PI controller corrects speed dips on the ascent and overshoots on the descent in real time.

---

##  Performance Summary

| Metric | Value |
|--------|-------|
| Overshoot (%) | < 10% |
| Steady-State Error | ≈ 0% |
| Disturbance Introduced | t = 10s, magnitude −0.2 |
| Controller Type | PI (Proportional-Integral) |
| Plant Transfer Function | 1 / (5s + 1) |

---

##  Disturbance Testing

Road slope disturbance parameters tested:

-  Pre-disturbance — speed stabilizes at reference (1.0)
-  At t = 10s — step load of −0.2 applied (simulates uphill grade)
-  Post-disturbance — PI controller rejects disturbance and restores speed to reference

---

##  How to Run

### Prerequisites
- MATLAB R2021a or later
- Control System Toolbox
- Simulink (required for `.slx` model generation)

### Steps

1. Clone the repository:
   ```bash
   git clone https://github.com/<your-username>/EV-CruiseControl.git
   cd EV-CruiseControl
   ```

2. Open MATLAB and navigate to the project folder.

3. Run the Simulink model builder and simulation:
   ```matlab
   run('EV_Simulink_Advanced.m')
   ```

4. To run the flyover animation (requires simulation data from Step 3):
   ```matlab
   run('EV_Car_Animation.m')
   ```

5. To open the auto-generated Simulink model directly:
   ```matlab
   open('EV_CruiseControl_Advanced.slx')
   ```

---

##  System Design Overview

```
           r(t)           e(t)         u(t)                   y(t)
Reference ──►[+]──► [ PI Controller ] ──►[+]──► [ Plant G(s) ] ──►── Speed
           ─[−]◄──────────────────────────────────────────────────┘
                          (Unity Feedback)

                                         ↑
                              d(t) = Road Slope at t = 10s
```

**Simulink Model Subsystems:**

| Subsystem | Contents |
|-----------|----------|
| `PI_Controller` | Simulink PID block (PI mode), Kp = 11.75, Ki = 11.25 |
| `Vehicle_Plant` | Transfer Function block: `[1] / [5 1]` |
| `Road_Disturbance` | Step block: triggers at t = 10s, magnitude −0.2 |

---

##  Animation Features

The `EV_Car_Animation.m` script provides a full real-time scrolling animation:

- **Flyover ramp geometry** — smooth cosine-eased ascent and descent
- **Live speed graph** — updated each frame with ascent/descent phase markers
- **HUD overlay** — real-time speed, time, and distance display
- **Status messages** — PI controller actions annotated during ascent and descent phases
- **Pass-2 sync** — animation timing is synchronized precisely with simulation data

---

##  Deliverables

- [x] Transfer function model of EV plant
- [x] PI controller parameters (Kp, Ki)
- [x] Simulink model (auto-generated via MATLAB script)
- [x] Speed tracking, control effort, and error plots
- [x] Road slope disturbance response analysis
- [x] Flyover car animation with live PI feedback visualization

---

##  Event Details

**EV Control Hackathon** — Control Systems Design Challenge  
Organized by **Robostrata Technologies**  
 557, 9th Cross, Jayanagar 7th Block West, Bengaluru 560 070  
 +91 81979 45038 | ✉️ robostratatechnologies@gmail.com

---

## 📄 License

This project was developed as part of a hackathon challenge. Feel free to use and adapt for educational purposes.
