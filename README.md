# ⚽ Intelligent PEAS Soccer Agent
(Run in Google Colab)

![Python](https://img.shields.io/badge/Python-3.x-blue?style=flat-square)
![AI Concept](https://img.shields.io/badge/AI-PEAS%20Framework-green?style=flat-square)
![Status](https://img.shields.io/badge/Status-Functional-orange?style=flat-square)

## 📖 Project Overview
This project implements a **Rational Intelligent Agent** designed to simulate a soccer player using the **PEAS (Performance, Environment, Actuators, Sensors)** framework. 

The agent operates in a stochastic, dynamic environment (a 2D soccer field) and uses a **Model-Based Reflex Architecture** to balance conflicting goals: scoring goals versus managing stamina resources. The simulation is written in Python and optimized for Google Colab.

---

## 🤖 The PEAS Framework
The agent is designed based on the following formal definition:

| **Component** | **Description** |
| :--- | :--- |
| **(P) Performance** | • +100 Points for scoring a Goal.<br>• +10 Points for Dribbling closer.<br>• Penalty: Reaching 0 Stamina. |
| **(E) Environment** | • 100x60 2D Grid Field.<br>• Dynamic Ball position.<br>• Static Goal at (100, 30). |
| **(A) Actuators** | • `RUN`: Fast movement towards ball (Medium stamina cost).<br>• `DRIBBLE`: Moves ball towards goal (High stamina cost).<br>• `SHOOT`: Attempt to score (Max stamina cost).<br>• `REST`: Recover stamina (Negative cost). |
| **(S) Sensors** | • **GPS:** Detects Agent position $(x,y)$.<br>• **Ball Sensor:** Calculates Euclidean distance to ball.<br>• **Stamina Meter:** Monitors internal energy levels. |

---

## 🧠 Agent Architecture & Logic
The agent follows a **Perception-Action Cycle**. It does not merely react to the ball; it maintains an **Internal State** (Stamina) that influences its decisions.



### Decision Algorithm (Pseudocode)
```text
WHILE Match_Is_Active:
    1. SENSE environment (Get distances to Ball and Goal)
    2. UPDATE Internal State (Check Stamina)
    
    3. DECIDE Action based on Priority:
       IF Stamina < 20% -> PRIORITY: SURVIVAL
          └── Action: REST
          
       ELSE IF Distance_To_Ball > 5 units -> PRIORITY: ACQUISITION
          └── Action: RUN_TO_BALL
          
       ELSE (Agent has Ball) -> PRIORITY: ATTACK
          IF Distance_To_Goal < 25 units:
             └── Action: SHOOT
          ELSE:
             └── Action: DRIBBLE
             
    4. ACT (Update Physics and Score)
