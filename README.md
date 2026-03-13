# Sequential Shape Fields
## A Markov Field Framework for Collective Geometric Interaction

> Minimal instructions can generate complex collective structure.  
> This framework studies how strangers sequentially construct spatial patterns on a shared surface under extremely simple rules.

The project begins with a minimal instruction:

> **Choose one shape and add it anywhere on the paper.**

Each participant adds exactly one shape from a predefined set. Over time the surface accumulates structure. The resulting artifact is modeled as a **sequential stochastic spatial process**.

The central objective is to infer the **local update rule governing participant actions**.

Formally, the goal is to estimate the **transition kernel**

\[
K((q,\ell)\mid X_t)
\]

which describes the probability that a participant chooses shape \(q\) and placement location \(\ell\) given the current field state \(X_t\).

---

# Conceptual Overview

A participant receives an instruction, evaluates the current field, and produces a geometric action.

This action updates the system state:

\[
X_t \rightarrow X_{t+1}
\]

where

- \(X_t\) — system state before the participant acts  
- \(X_{t+1}\) — system state after the participant acts  

For isolated prompts, responses are independent emissions.

For the shared-paper experiment, actions accumulate sequentially:

\[
X_0 \rightarrow X_1 \rightarrow X_2 \rightarrow \dots \rightarrow X_n
\]

Each participant observes the existing field and updates it.

The artifact therefore evolves as a **sequential stochastic process over spatial structure**.

---

# Experimental Grammar

The experimental progression introduces new latent variables in stages.  
Each stage expands the state space of possible responses.

## Level 1 — Single-form generation

Participants generate a single geometric object.

Examples:

- draw a line  
- draw a circle  
- draw a square  
- draw a triangle  

Purpose:

Estimate **single-form emission distributions**.

---

## Level 2 — Same-form relation

Participants generate two objects of the same class.

Examples:

- draw two circles  
- draw two squares  
- draw two triangles  

Purpose:

Estimate **relational geometry distributions**.

---

## Level 3 — Cross-form relation

Participants integrate objects of different geometric classes.

Examples:

- draw a circle and a square  
- draw a circle and a triangle  
- draw a square and a triangle  

Purpose:

Measure **heterogeneous object integration strategies**.

---

## Level 4 — Choice without production

Participants no longer draw shapes.

Instead they choose from a predefined **shape bank**.

Example instruction:

> Choose one shape and add it to the paper.

Purpose:

Isolate

- categorical selection  
- spatial placement  

Motor-production noise is removed.

---

## Level 5 — Collective sequential field

Participants interact with the **same evolving sheet**.

Instruction:

> Each participant adds exactly one shape to the shared paper.

Purpose:

Observe **collective field dynamics**.

---

# Baseline Shape Production

## Circle emission model

Represent a circle drawing as

\[
s = (x,y,r,c,p,v,\theta,\epsilon)
\]

where

| Parameter | Description |
|---|---|
| \(x,y\) | center location |
| \(r\) | radius |
| \(c\) | closure completeness |
| \(p\) | pen pressure |
| \(v\) | drawing velocity |
| \(\theta\) | starting angle |
| \(\epsilon\) | deviation from ideal circle |

Emission model:

\[
s \sim P_{\text{circle}}(\cdot)
\]

Measured tendencies include:

- center bias
- radius distribution
- closure variability
- motor execution variance

---

## Square emission model

Squares introduce polygonal construction.

Unlike circles, squares require:

- vertex planning  
- orthogonal edges  
- angular closure  
- rotation relative to page axes  

Emission model:

\[
s \sim P_{\text{square}}(\cdot)
\]

Typical parameters include side length, orientation, and orthogonality error.

---

## Triangle emission model

Triangles represent the minimal polygon class.

\[
s \sim P_{\text{triangle}}(\cdot)
\]

Parameters include centroid location, scale, orientation, and apex direction.

Triangles often reveal stability and directional biases.

---

# Relational Geometry

## Same-shape relations

Estimate relational distributions:

\[
P(R \mid \text{circle-circle})
\]

\[
P(R \mid \text{square-square})
\]

\[
P(R \mid \text{triangle-triangle})
\]

with

\[
R = (d,\Delta r,o,t,n,a,\sigma)
\]

| Parameter | Meaning |
|---|---|
| \(d\) | center distance |
| \(\Delta r\) | size difference |
| \(o\) | overlap |
| \(t\) | tangency |
| \(n\) | nesting |
| \(a\) | alignment |
| \(\sigma\) | symmetry |

---

## Mixed-shape relations

Example tasks:

- square + circle  
- circle + triangle  
- square + triangle  

Response representation:

\[
s = (s_A,s_B,R,O)
\]

where \(O\) captures order and role structure.

Measured features include containment, scale dominance, and anchor–satellite relationships.

---

# Shape Bank Simplification

To isolate categorical choice, introduce a shape bank:

- circle  
- square  
- triangle  

Instruction:

> Choose one shape and add it to the paper.

Each action becomes

\[
a_t = (q_t,\ell_t)
\]

| Variable | Meaning |
|---|---|
| \(q_t\) | shape category |
| \(\ell_t\) | spatial location |

This removes variation due to drawing execution.

---

# Field State Representation

Let the field configuration at time \(t\) be

\[
X_t = \{(q_1,\ell_1),(q_2,\ell_2),\dots,(q_t,\ell_t)\}
\]

Each participant observes the current field and performs an update:

\[
X_{t+1}=X_t\cup\{(q_{t+1},\ell_{t+1})\}
\]

This produces a **sequential spatial process**.

---

# Markov Field Assumption

The update process is modeled as

\[
P(X_{t+1}\mid X_t,X_{t-1},\dots)\approx P(X_{t+1}\mid X_t)
\]

Participant decisions depend on the **current visible configuration**, which encodes prior history.

---

# Transition Kernel

The fundamental object of inference is the transition kernel

\[
(q_{t+1},\ell_{t+1}) \sim K(\cdot\mid X_t)
\]

This kernel specifies how participants select:

- shape category \(q\)
- spatial placement \(\ell\)

given the existing configuration.

---

# Conditional Intensity Model

A flexible parametric form for the kernel is

\[
P(q,\ell\mid X_t)\propto
\exp(
\beta_1 f_{\text{density}}
+\beta_2 f_{\text{symmetry}}
+\beta_3 f_{\text{match}}
+\beta_4 f_{\text{novelty}}
+\beta_5 f_{\text{edge}}
)
\]

| Feature | Interpretation |
|---|---|
| density | attraction or avoidance of occupied regions |
| symmetry | completion of visible patterns |
| match | category alignment with neighbors |
| novelty | contrast against existing shapes |
| edge | boundary preferences |

---

# Parameter Estimation

Parameters are estimated using **maximum pseudolikelihood methods** for spatial point processes.

Procedure:

1. record all actions \(a_t\)
2. compute local spatial statistics
3. estimate coefficients \(\beta_i\)
4. compare candidate models using

- AIC  
- BIC  
- WAIC  

The model that best reproduces the observed trajectory identifies the most plausible behavioral rule.

---

# Monte Carlo Simulation

Monte Carlo simulation generates synthetic trajectories

\[
X_0 \rightarrow X_1 \rightarrow \dots \rightarrow X_n
\]

Simulated fields are compared against observed artifacts.

Example generative models:

| Model | Mechanism |
|---|---|
| Random | independent uniform placement |
| Cluster | attraction to existing shapes |
| Homophily | shape-category matching |
| Symmetry | balance completion |

Simulation reveals which mechanisms produce structures similar to the empirical field.

---

# Canonical Foundations

This framework connects to established work in several research traditions.

### Emergent collective behavior

The idea that simple local rules can generate large-scale spatial patterns was famously demonstrated by  
:contentReference[oaicite:0]{index=0} in the **Schelling segregation model**.  

In that model, individual agents follow minimal preferences about their immediate neighbors.  
Despite these weak rules, large-scale spatial segregation emerges spontaneously.

Sequential Shape Fields applies the same principle to **geometric artifacts**:

individual decisions  
→ sequential updates  
→ emergent collective structure.

---

### Spatial statistics

The shared-field representation corresponds to a **marked spatial point process**, widely studied in spatial statistics.

---

### Cultural evolution

Sequential accumulation of structure parallels **iterated learning models**, where cultural artifacts evolve through repeated transmission.

---

### Complex systems

The framework also connects to research on **self-organization, collective intelligence, and decentralized decision systems**.

---

# Experimental Pipeline

### Data collection

For each participant record:

- shape category
- coordinates
- order index

### Model fitting

Estimate parameters of candidate kernels.

### Simulation

Generate synthetic trajectories.

### Model comparison

Identify which transition rule best explains the observed field.

---

# Conceptual Summary

The experimental progression follows the ladder

\[
\text{single form}
\rightarrow
\text{relation}
\rightarrow
\text{mixed relation}
\rightarrow
\text{choice}
\rightarrow
\text{placement}
\rightarrow
\text{collective sequential field}
\rightarrow
\text{transition kernel}
\rightarrow
\text{Monte Carlo inference}
\]

Minimal instructions initiate the system.

Sequential local decisions generate the collective artifact.

The scientific objective is to infer the **kernel governing those decisions**.

---

# Minimum Viable Experiment

1. Prepare a shape bank

- circle  
- square  
- triangle  

2. Instruction:

> Choose one shape and add it anywhere on the paper.

3. Each passerby adds exactly one shape.

4. Record

- shape type  
- coordinates  
- order index  

5. Fit the transition model

\[
X_{t+1} \sim K(\cdot \mid X_t)
\]

6. Use Monte Carlo simulation to evaluate candidate mechanisms.

---

# Core Research Goal

Estimate the transition rule

\[
K((q,\ell)\mid X_t)
\]

This kernel describes how strangers collectively generate spatial structure under minimal instructions.

Understanding this rule reveals how **simple local decisions produce complex collective artifacts**.
