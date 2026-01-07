# ACT of Insertion: Imitation Learning for Peg Placement  
**Machine Learning for Robotics (RBE 577) – Project 4**

## 📌 Overview
This project implements **Action Chunking Transformer (ACT)** for **robotic peg insertion** using **imitation learning**.  
A **UR10 robotic arm** is trained in **MuJoCo** to perform precise **peg-in-hole insertion** using **multi-modal observations**, including:

- Multi-view RGB images (3 cameras)
- End-effector pose and joint states

Unlike reinforcement learning, the model **learns entirely from expert demonstrations**, enabling safe and efficient policy learning for contact-rich manipulation tasks.

Completed as part of **RBE 577: Machine Learning for Robotics** :contentReference[oaicite:0]{index=0}.

---

## 🎯 Problem Statement
Train a transformer-based policy that maps:
\[
\text{Observations (RGB + Proprioception)} \rightarrow \text{Action Sequences}
\]

to solve **peg insertion** for multiple object geometries (**square and triangle**) without reward signals or environment interaction during training.

---

## 🧠 Methodology

### Action Chunking Transformer (ACT)
ACT is a **transformer-based imitation learning framework** that:
- Predicts **action chunks** instead of single actions
- Uses **DETR-style encoder–decoder attention**
- Incorporates a **VAE latent action space**
- Enables closed-loop control at inference time

ACT combines:
- Vision (multi-camera RGB)
- Robot state
- Temporal context

to generate smooth and robust manipulation trajectories.

---

## 🔁 Pipeline Overview

### 1️⃣ Demonstration Generation
- Scripted expert policies for:
  - Square peg insertion
  - Triangle peg insertion
- Demonstrations collected in **MuJoCo**
- Each episode stored in **HDF5 format**
- Includes:
  - Time-series robot states
  - Multi-view RGB observations
- ~50 demonstrations per peg type
- Randomized initial positions (±1 cm in X/Y)

---

### 2️⃣ ACT Model Training
Key components implemented from scratch:

- **Transformer Encoder & Decoder**
- **Attention mechanisms**
- **Residual & normalization blocks**
- **DETR-VAE architecture**
- **Latent action encoding & decoding**
- **Positional encodings (spatial & temporal)**

Training performed offline using demonstration data only.

Loss terms include:
- Action reconstruction loss
- KL divergence (for latent regularization)

---

### 3️⃣ Evaluation & Analysis
- Closed-loop rollout evaluation
- Success rate across:
  - Peg shapes
  - Initial conditions
- Trajectory smoothness and robustness analysis
- Visual inspection of rollouts and camera feeds

---

## 📊 Results & Evaluation
Evaluation includes:
- Training loss curves
- Success rate metrics
- Trajectory fidelity comparisons
- Rollout visualizations

The ACT policy demonstrates:
- High precision insertion
- Generalization across randomized initial states
- Smooth, temporally consistent actions

---

## 🗂️ Project Structure
