# SIR Model Study: Optimal Vaccination Control

This project presents a mathematical study and numerical simulation of the **SIR (Susceptible-Infected-Removed) epidemic model**, extended with a vaccination rate optimized through **Control Theory**.

The work was developed as a formal report for the course *"Introduction to the Physics of Complex Systems"* at the University of Bologna, taught by professor Bazzani.

---

## 📋 Table of Contents
* [Introduction](#-introduction)
* [The SIR Model](#-the-sir-model)
* [Vaccination & Herd Immunity](#-vaccination--herd-immunity)
* [Optimal Control Theory](#-optimal-control-theory)
* [Simulation & Results](#-simulation--results)
* [Technical Implementation](#-technical-implementation)

---

## 🦠 Introduction
The project analyzes a "compartmental model" where the population is divided into three classes:
* **Susceptible ($S(t)$):** Individuals who have not contracted the disease and are at risk.
* **Infected ($I(t)$):** Individuals who have the disease and are contagious.
* **Removed ($R(t)$):** Individuals who have recovered and are no longer infectable.

The dynamics assume a constant population $N = S(t) + I(t) + R(t)$ and a unidirectional flow ($S \to I \to R$).

---

## 📐 The SIR Model
The temporal evolution is described by a system of differential equations:

$$
\begin{cases}
\dot{S}(t) = -m \cdot I(t) \cdot S(t) \\
\dot{I}(t) = m \cdot I(t) \cdot S(t) - \gamma \cdot I(t) \\
\dot{R}(t) = \gamma \cdot I(t)
\end{cases}
$$

### Key Parameters:
* **$m$ (Sociality):** Represents the contact rate and probability of transmission.
* **$\gamma$ (Recovery Rate):** The reciprocal of the average time an individual remains infectious.
* **$R_0$ (Basic Reproduction Number):** Defined as $m/\gamma$. If $R_0 > 1$, the epidemic spreads.



---

## 💉 Vaccination & Herd Immunity
By adding a vaccination rate $u(t)$, susceptible individuals can move directly to the "Removed" class without being infected.

### Herd Immunity Threshold
The study defines the minimum fraction of the population ($V$) that must be vaccinated to prevent the disease from spreading:
$$V_{soglia} = 1 - \frac{1}{R_0}$$

---

## ⚖️ Optimal Control Theory
The vaccination rate $u(t)$ is treated as a time-dependent control variable to minimize a **Cost Functional** $J$:

$$J(S, I, u) = \int_{0}^{T} \left( I(t) + \frac{A}{2}u^2(t) \right) dt$$

* **$I(t)$:** Represents human/social costs (hospitalizations).
* **$\frac{A}{2}u^2(t)$:** Represents economic costs of the vaccination campaign.
* **$A$:** A parameter quantifying the relative cost between vaccines and hospital stays.

Using Hamiltonian mechanics and the Lyusternik theorem, the optimal control $\overline{u}(t)$ is derived as:
$$\overline{u}(t) = \frac{\overline{S}(t) \cdot \lambda_1(t)}{A}$$



---

## 📈 Simulation & Results
The model was simulated using Python, with parameters calibrated on **Covid-19 data from Bologna (2020)**:
* **$\gamma = 1/3$:** Average infectious period of 3 days.
* **$u(t)$ range:** Values of the order $10^{-3}$ (approx. 1000 vaccines/day for 900,000 people).
* **$A = 5000$:** Based on the estimated 1:100 ratio between vaccination and hospitalization costs.

### Conclusions
* The optimal control strategy provides a vaccination rate consistent with real-world logistical capabilities.
* However, the peak of infected individuals ($ \approx 0.2$) under this control still exceeds the actual hospital capacity ($\approx 10^{-3}$), indicating that vaccination must be supported by other measures.

---

## 🛠 Technical Implementation
* **Language:** Python.
* **Solver:** `scipy.integrate.odeint` using the LSODA method (BDF and Adams-Bashforth-Moulton algorithms).
* **Mathematical Framework:** Hamiltonian Mechanics and Functional Analysis.

---
**Course:** Introduzione alla Fisica dei Sistemi Complessi  
**Author:** Marco Maltoni 
