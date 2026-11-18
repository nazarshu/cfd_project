# Niayifar & Porté-Agel (2016): *Analytical modeling of wind farms: a new approach for power prediction*

The paper turns the single-wake Gaussian model of Bastankhah & Porté-Agel (2014) into a **wind-farm** model. It keeps the Gaussian deficit unchanged and adds three things:

- **[N1] Linear superposition of deficits scaled by local inflow.** Each wake's velocity deficit is measured relative to the wind reaching the turbine that makes it ($U_k$), not $U_\infty$.
- **[N2] Local turbulence intensity.** It is computed at every rotor considering the largest added streamwise turbulence intensity from the wakes upstream (Crespo–Hernández model with overlap weighting).
- **[N3] Variable wake growth rate.** $k^{\ast}$ becomes a function of local turbulence, $k^{\ast} = f(I)$, so each turbine gets its own value.

In the steps below, **[B14]** marks what comes from Bastankhah 2014 and **[N1–N3]** marks what Niayifar adds.


## 0. Inputs

Layout $(X_j, Y_j)$, $d_0$, $z_h$; 

Inflow $\theta$, $U_\infty$, $I_0$; 

Curves $C_T(U)$ and $P(U)$.

## 1. Rotate and sort

Wind-aligned coordinates ($\theta$ = direction the wind comes **from**, clockwise from North):

```math
x' = -(X\sin\theta + Y\cos\theta), \qquad y' = X\cos\theta - Y\sin\theta
```

Sort turbines by $x'$. 

Wakes only act downstream, so **one upstream-to-downstream pass** is enough. 

Turbines in the first row see $U = U_\infty$ and $I = I_0$.

## 2. For turbine $i$: loop over every upstream turbine $k$

Turbine $k$ has already been solved, so $U_k$, $C_{T,k}$, $a_k$, $\varepsilon_k$ and $k^*_k$ are known.

**2a. Wake width [B14]**, using the growth rate of the turbine that made the wake:

```math
\sigma_{ki} = d_0\left(k^*_k\,\frac{\Delta x_{ki}}{d_0} + \varepsilon_k\right)
```

**2b. Wake depth [B14]:**

```math
C_{ki} = 1 - \sqrt{1 - \frac{C_{T,k}}{8(\sigma_{ki}/d_0)^2}}
```

**2c. Deficit on rotor $i$, scaled by $U_k$ [N1]:**

```math
\Delta U_{ki} = U_k\, C_{ki}\,\overline{\exp\!\left(-\frac{(y-y'_k)^2 + (z-z_h)^2}{2\sigma_{ki}^2}\right)}
```

<!--
\Delta U_{ki} = U_k\, C_{ki}\,\frac{1}{A_0}\iint_{A_i} \exp\!\left(-\frac{(y-y'_k)^2 + (z-z_h)^2}{2\sigma_{ki}^2}\right) dA
-->

The bar means the average over the disk of rotor $i$. It matters in partial-wake cases.

**2d. Added turbulence [N2]** (Crespo–Hernández), with $a_k = \tfrac12\left(1-\sqrt{1-C_{T,k}}\right)$:

```math
I_{+,ki} = 0.73\,a_k^{0.8325}\,I_0^{0.0325}\left(\frac{\Delta x_{ki}}{d_0}\right)^{-0.32}
```

**2e. Overlap weight [N2].** $A_{w,ki}$ is the area of rotor $i$ covered by a top-hat wake disk of radius $2\sigma_{ki}$ (circle–circle intersection):

```math
w_{ki} = \frac{4A_{w,ki}}{\pi d_0^2} \in [0,1]
```

## 3. Combine the wakes at turbine $i$

**3a. Inflow speed, by linear superposition [N1]:**

```math
U_i = U_\infty - \sum_k \Delta U_{ki}
```

This replaces the quadratic sum of Katic/Jensen, which overpredicts power deep in the farm.

**3b. Local turbulence [N2].** Only the strongest weighted wake counts, because turbulence is not summed:

```math
I_{+,i} = \max_k\left(w_{ki}\, I_{+,ki}\right), \qquad I_i = \sqrt{I_0^2 + I_{+,i}^2}
```

## 4. Outputs of turbine $i$, stored for turbines downstream

**4a. Thrust and initial width [B14]:**

```math
C_{T,i} = C_T(U_i), \qquad \beta_i = \frac12\,\frac{1+\sqrt{1-C_{T,i}}}{\sqrt{1-C_{T,i}}}, \qquad \varepsilon_i = 0.2\sqrt{\beta_i}
```

**4b. Wake growth rate [N3]** (fit to V80 LES, valid for $0.065 < I < 0.15$):

```math
k^*_i = 0.3837\, I_i + 0.003678
```

In [B14], $k^*$ was fitted separately for each case. Farm models of the time used a constant, such as $k = 0.04$ in WAsP.

**4c. Power:** $P_i = P(U_i)$ from the power curve.

## 5. Farm totals

```math
P_\text{farm} = \sum_i P_i, \qquad \eta = \frac{P_\text{farm}}{N\,P(U_\infty)}
```

To compare with measurements, average over a wind-direction sector (±5° to ±15°). For AEP, weight the results by the wind rose.

## Dependency chain

```math
I_k \to k^*_k \to \sigma_{ki} \to
\begin{cases}
C_{ki} \to \Delta U_{ki} \to U_i \to C_{T,i} \to (a_i,\ \varepsilon_i),\ P_i \\
A_{w,ki} \to w_{ki}\,I_{+,ki} \to I_i \to k^*_i
\end{cases}
\;\Rightarrow\; \sigma_{ij}\ \text{for the next turbine}
```

## Key points

- **Validation:** Horns Rev (80 × V80, 8 m/s, $I_0 = 7.7\%$). The model matches LES and SCADA data over wind directions from 173° to 353°. WAsP (top-hat, $k = 0.04$) underpredicts power.
- **Why it works:** Wakes inside the farm see higher turbulence, so they grow faster (larger $k^*$) and recover sooner. Scaling deficits by $U_k$ stops them from piling up row after row.
- **Limits:**
  - Only the *linearised* momentum is conserved (revisited by Zong & Porté-Agel, 2020).
  - A wake keeps its original $k^*_k$ even as it passes through regions of higher turbulence.
  - The $k^*(I)$ fit comes from one turbine type under neutral conditions.
  - There is no blockage or upstream induction.
