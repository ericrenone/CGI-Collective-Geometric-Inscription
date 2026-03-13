# Sequential Shape Fields

## A Markov Field Framework for Collective Geometric Interaction

> Minimal instructions can generate complex collective structure.

This framework studies how strangers sequentially construct spatial patterns on a shared surface under extremely simple rules.

The project begins with a single minimal instruction:

> **Choose one shape and add it anywhere on the paper.**

Each participant adds exactly one shape from a predefined set. Over time the surface accumulates structure. The resulting artifact is modeled as a **sequential stochastic spatial process**.

The central scientific objective is to infer the **local update rule** that governs participant actions. Formally, the goal is to estimate the **transition kernel**

\[
K((q,\ell) \mid X_t)
\]

which gives the probability that a participant selects shape category \(q\) and placement location \(\ell\) given the current field state \(X_t\).

---

## Conceptual Overview

A participant receives the instruction, observes the current field, and produces a geometric action. This action updates the system state:

\[
X_t \rightarrow X_{t+1}
\]

where  
- \(X_t\) is the system state before the action,  
- \(X_{t+1}\) is the system state after the action.

For isolated prompts, responses are independent emissions. In the shared-paper experiment, actions accumulate sequentially:

\[
X_0 \rightarrow X_1 \rightarrow X_2 \rightarrow \dots \rightarrow X_n
\]

Each participant observes the existing field and updates it. The artifact therefore evolves as a **sequential stochastic process over spatial structure**.

---

## Experimental Grammar

The experimental progression systematically introduces new latent variables, expanding the state space of possible responses stage by stage.

### Level 1 — Single-form generation
Participants generate a single geometric object.  
**Examples:** draw a line, draw a circle, draw a square, draw a triangle.  
**Purpose:** Estimate single-form emission distributions.

### Level 2 — Same-form relation
Participants generate two objects of the same class.  
**Examples:** two circles, two squares, two triangles.  
**Purpose:** Estimate relational geometry distributions.

### Level 3 — Cross-form relation
Participants integrate objects of different geometric classes.  
**Examples:** circle + square, circle + triangle, square + triangle.  
**Purpose:** Measure heterogeneous object integration strategies.

### Level 4 — Choice without production
Participants no longer draw shapes. Instead they choose from a predefined **shape bank** (circle, square, triangle).  
**Instruction:** “Choose one shape and add it to the paper.”  
**Purpose:** Isolate categorical selection and spatial placement decisions. Motor-production noise is eliminated.

### Level 5 — Collective sequential field
Participants interact with the **same evolving sheet**.  
**Instruction:** “Each participant adds exactly one shape to the shared paper.”  
**Purpose:** Observe emergent collective field dynamics.

---

## Baseline Shape Production

### Circle emission model
A circle is represented as
\[
s = (x,y,r,c,p,v,\theta,\epsilon)
\]
where

| Parameter | Description                  |
|-----------|------------------------------|
| \(x,y\)   | center location              |
| \(r\)     | radius                       |
| \(c\)     | closure completeness         |
| \(p\)     | pen pressure                 |
| \(v\)     | drawing velocity             |
| \(\theta\)| starting angle               |
| \(\epsilon\)| deviation from ideal circle |

Emission model: \(s \sim P_{\text{circle}}(\cdot)\).  
Measured tendencies include center bias, radius distribution, closure variability, and motor execution variance.

### Square emission model
Squares introduce polygonal construction (vertex planning, orthogonal edges, angular closure, rotation relative to page axes).  
Emission model: \(s \sim P_{\text{square}}(\cdot)\).  
Typical parameters: side length, orientation, orthogonality error.

### Triangle emission model
Triangles represent the minimal polygon class.  
Emission model: \(s \sim P_{\text{triangle}}(\cdot)\).  
Parameters include centroid location, scale, orientation, and apex direction. Triangles often reveal stability and directional biases.

---

## Relational Geometry

### Same-shape relations
Relational distributions are estimated as

\[
P(R \mid \text{circle-circle}),\quad
P(R \mid \text{square-square}),\quad
P(R \mid \text{triangle-triangle})
\]

with relation vector

\[
R = (d,\Delta r,o,t,n,a,\sigma)
\]

| Parameter | Meaning                  |
|-----------|--------------------------|
| \(d\)     | center distance          |
| \(\Delta r\)| size difference        |
| \(o\)     | overlap                  |
| \(t\)     | tangency                 |
| \(n\)     | nesting                  |
| \(a\)     | alignment                |
| \(\sigma\)| symmetry                |

### Mixed-shape relations
Tasks combine different classes (e.g., square + circle).  
Response representation: \(s = (s_A, s_B, R, O)\), where \(O\) encodes order and role structure.  
Measured features include containment, scale dominance, and anchor–satellite relationships.

---

## Shape Bank Simplification

To isolate categorical choice and placement, the experiment uses a fixed shape bank:

- Circle
- Square
- Triangle

**Instruction:** “Choose one shape and add it to the paper.”

Each action is recorded as
\[
a_t = (q_t, \ell_t)
\]

| Variable | Meaning             |
|----------|---------------------|
| \(q_t\)  | shape category      |
| \(\ell_t\)| spatial location   |

Motor-production noise is removed.

---

## Field State Representation

The field configuration at time \(t\) is

\[
X_t = \{(q_1,\ell_1),\ (q_2,\ell_2),\ \dots,\ (q_t,\ell_t)\}
\]

Each participant observes \(X_t\) and performs the update
\[
X_{t+1} = X_t \cup \{(q_{t+1},\ell_{t+1})\}.
\]

This produces a **sequential spatial process**.

---

## Markov Field Assumption

The update process is modeled as

\[
P(X_{t+1} \mid X_t, X_{t-1}, \dots) \approx P(X_{t+1} \mid X_t).
\]

Participant decisions depend only on the current visible configuration (which implicitly encodes prior history).

---

## Transition Kernel

The fundamental object of inference is the transition kernel

\[
(q_{t+1},\ell_{t+1}) \sim K(\cdot \mid X_t).
\]

This kernel fully specifies how participants select shape category \(q\) and spatial placement \(\ell\) given the existing field.

---

## Conditional Intensity Model

A flexible parametric form for the kernel is the conditional intensity

\[
P(q,\ell \mid X_t) \propto \exp\bigl(
\beta_1 f_{\text{density}} +
\beta_2 f_{\text{symmetry}} +
\beta_3 f_{\text{match}} +
\beta_4 f_{\text{novelty}} +
\beta_5 f_{\text{edge}}
\bigr).
\]

| Feature    | Interpretation                              |
|------------|---------------------------------------------|
| density    | attraction or repulsion from occupied regions |
| symmetry   | completion of visible patterns              |
| match      | category alignment with neighbors           |
| novelty    | contrast against existing shapes            |
| edge       | boundary or margin preferences              |

---

## Parameter Estimation

Parameters \(\beta_i\) are estimated via **maximum pseudolikelihood** for spatial point processes:

1. Record every action \(a_t\).
2. Compute local spatial statistics at each step.
3. Estimate coefficients \(\beta_i\).
4. Compare candidate models using AIC, BIC, and WAIC.

The model that best reproduces the observed trajectory identifies the most plausible behavioral rule.

---

## Monte Carlo Simulation

Synthetic trajectories are generated via Monte Carlo:

\[
X_0 \rightarrow X_1 \rightarrow \dots \rightarrow X_n
\]

Simulated fields are statistically compared with empirical artifacts.

| Model      | Mechanism                              |
|------------|----------------------------------------|
| Random     | independent uniform placement          |
| Cluster    | attraction to existing shapes          |
| Homophily  | shape-category matching                |
| Symmetry   | balance / pattern completion           |

Simulation reveals which local mechanisms produce structures statistically indistinguishable from the observed collective field.

---

## Canonical Foundations

This framework connects to several established research traditions.

### Emergent collective behavior
The principle that simple local rules generate large-scale spatial structure was demonstrated by **Thomas C. Schelling** in [*Dynamic Models of Segregation* (1971)](https://acoustique.ec-lyon.fr/chaos/Schelling71.pdf) and [*Micromotives and Macrobehavior* (1978)](https://openlibrary.org/books/OL4729113M/Micromotives_and_macrobehavior). 

In Schelling’s model, individual agents follow minimal neighborhood preferences, yet global segregation patterns emerge (see [Schelling’s model of segregation on Wikipedia](https://en.wikipedia.org/wiki/Schelling%27s_model_of_segregation)). Sequential Shape Fields extends the same logic from residential segregation to **geometric artifacts**: local decision rules → sequential spatial updates → emergent collective structure.

### Spatial statistics
The shared-field representation is a **marked spatial point process**, a core model in spatial statistics.

### Cultural evolution
Sequential accumulation mirrors **iterated learning** models in cultural transmission.

### Complex systems
The framework also aligns with research on self-organization, collective intelligence, and decentralized decision systems.

---

## Experimental Pipeline

1. **Data collection**  
   For each participant record: shape category, coordinates, and order index.

2. **Model fitting**  
   Estimate parameters of candidate transition kernels.

3. **Simulation**  
   Generate synthetic trajectories under competing mechanisms.

4. **Model comparison**  
   Identify the transition rule that best explains the observed collective field.

---

## Conceptual Summary

The experimental ladder proceeds as

\[
\text{single form} \to
\text{same-form relation} \to
\text{mixed relation} \to
\text{categorical choice} \to
\text{spatial placement} \to
\text{collective sequential field} \to
\text{transition kernel} \to
\text{Monte Carlo inference}.
\]

Minimal instructions initiate the system. Sequential local decisions generate the collective artifact. The scientific goal is to recover the **kernel governing those decisions**.

---

## Minimum Viable Experiment

1. Prepare shape bank: circle, square, triangle.
2. Instruction:  
   > Choose one shape and add it anywhere on the paper.
3. Each passerby adds exactly one shape.
4. Record: shape type, coordinates, order index.
5. Fit the transition model \(X_{t+1} \sim K(\cdot \mid X_t)\).
6. Use Monte Carlo simulation to evaluate candidate mechanisms.

---

## Core Research Goal

Estimate the transition rule

\[
K((q,\ell) \mid X_t).
\]

This kernel reveals how strangers, under minimal instructions, collectively generate spatial structure. Understanding the rule illuminates how **simple local decisions produce complex collective artifacts**.
