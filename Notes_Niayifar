# Niayifar \& Porté-Agel (2016): *Analytical modeling of wind farms: a new approach for power prediction*

*Energies* 9, 741 (2016), doi:10.3390/en9090741. WIRE Lab, EPFL.

The paper turns the single-wake Gaussian model of Bastankhah \& Porté-Agel (2014) into a **wind-farm** model. It keeps the Gaussian deficit unchanged and adds three things:

* 🟢 **\[N1] Linear superposition of deficits scaled by local inflow.** Each wake's deficit is measured relative to the wind reaching the turbine that makes it ($U\_k$), not $U\_\\infty$.
* 🟢 **\[N2] Local turbulence intensity.** It is computed at every rotor from the wakes upstream (Crespo–Hernández model with overlap weighting).
* 🟢 **\[N3] Variable wake growth rate.** $k^*$ becomes a function of local turbulence, $k^* = f(I)$, so each turbine gets its own value.

In the steps below, **\[B14]** marks what comes from Bastankhah 2014 and **\[N1–N3]** marks what Niayifar adds.

\---

## 0\. Inputs

Layout $(X\_j, Y\_j)$, $d\_0$, $z\_h$; inflow $\\theta$, $U\_\\infty$, $I\_0$; curves $C\_T(U)$ and $P(U)$.

## 1\. Rotate and sort

Wind-aligned coordinates ($\\theta$ = direction the wind comes **from**, clockwise from North):

```math
x' = -(X\\sin\\theta + Y\\cos\\theta), \\qquad y' = X\\cos\\theta - Y\\sin\\theta
```

Sort turbines by $x'$. Wakes only act downstream, so **one upstream-to-downstream pass** is enough. Turbines in the first row see $U = U\_\\infty$ and $I = I\_0$.

## 2\. For turbine $i$: loop over every upstream turbine $k$

Turbine $k$ has already been solved, so $U\_k$, $C\_{T,k}$, $a\_k$, $\\varepsilon\_k$ and $k^\*\_k$ are known.

**2a. Wake width \[B14]**, using the growth rate of the turbine that made the wake:

```math
\\sigma\_{ki} = d\_0\\left(k^\*\_k\\,\\frac{\\Delta x\_{ki}}{d\_0} + \\varepsilon\_k\\right)
```

**2b. Wake depth \[B14]:**

```math
C\_{ki} = 1 - \\sqrt{1 - \\frac{C\_{T,k}}{8(\\sigma\_{ki}/d\_0)^2}}
```

**2c. Deficit on rotor $i$, scaled by $U\_k$ 🟢 \[N1]:**

```math
\\Delta U\_{ki} = U\_k\\, C\_{ki}\\,\\overline{\\exp\\!\\left(-\\frac{(y-y'\_k)^2 + (z-z\_h)^2}{2\\sigma\_{ki}^2}\\right)}
```

The bar means the average over the disk of rotor $i$. It matters in partial-wake cases.

**2d. Added turbulence 🟢 \[N2]** (Crespo–Hernández), with $a\_k = \\tfrac12\\left(1-\\sqrt{1-C\_{T,k}}\\right)$:

```math
I\_{+,ki} = 0.73\\,a\_k^{0.8325}\\,I\_0^{0.0325}\\left(\\frac{\\Delta x\_{ki}}{d\_0}\\right)^{-0.32}
```

**2e. Overlap weight 🟢 \[N2].** $A\_{w,ki}$ is the area of rotor $i$ (radius $d\_0/2$) covered by a top-hat wake disk of radius $2\\sigma\_{ki}$ (circle–circle intersection):

```math
w\_{ki} = \\frac{4A\_{w,ki}}{\\pi d\_0^2} \\in \[0,1]
```

## 3\. Combine the wakes at turbine $i$

**3a. Inflow speed, by linear superposition 🟢 \[N1]:**

```math
U\_i = U\_\\infty - \\sum\_k \\Delta U\_{ki}
```

This replaces the quadratic sum $`U\_\\infty - \\sqrt{\\sum (U\_\\infty - U\_{ki})^2}`$ of Katic/Jensen, which overpredicts power deep in the farm.

**3b. Local turbulence 🟢 \[N2].** Only the strongest weighted wake counts, because turbulence is not summed:

```math
I\_{+,i} = \\max\_k\\left(w\_{ki}\\, I\_{+,ki}\\right), \\qquad I\_i = \\sqrt{I\_0^2 + I\_{+,i}^2}
```

## 4\. Outputs of turbine $i$, stored for turbines downstream

**4a. Thrust and initial width \[B14]:**

```math
C\_{T,i} = C\_T(U\_i), \\qquad \\beta\_i = \\frac12\\,\\frac{1+\\sqrt{1-C\_{T,i}}}{\\sqrt{1-C\_{T,i}}}, \\qquad \\varepsilon\_i = 0.2\\sqrt{\\beta\_i}
```

**4b. Wake growth rate 🟢 \[N3]** (fit to V80 LES, valid for $0.065 < I < 0.15$):

```math
k^\*\_i = 0.3837\\, I\_i + 0.003678
```

In B14, $k^\*$ was fitted separately for each case. Farm models of the time used a constant, such as $k = 0.04$ in WAsP.

**4c. Power:** $P\_i = P(U\_i)$ from the power curve.

## 5\. Farm totals

```math
P\_\\text{farm} = \\sum\_i P\_i, \\qquad \\eta = \\frac{P\_\\text{farm}}{N\\,P(U\_\\infty)}
```

To compare with measurements, average over a wind-direction sector (±5° to ±15°). For AEP, weight the results by the wind rose.

\---

## Dependency chain

```math
I\_k \\to k^\*\_k \\to \\sigma\_{ki} \\to
\\begin{cases}
C\_{ki} \\to \\Delta U\_{ki} \\to U\_i \\to C\_{T,i} \\to (a\_i,\\ \\varepsilon\_i),\\ P\_i \\\\
A\_{w,ki} \\to w\_{ki}\\,I\_{+,ki} \\to I\_i \\to k^\*\_i
\\end{cases}
\\;\\Rightarrow\\; \\sigma\_{ij}\\ \\text{for the next turbine}
```

## Key points

* **Validation:** Horns Rev (80 × V80, 8 m/s, $I\_0 = 7.7%$). The model matches LES and SCADA data over wind directions from 173° to 353°. WAsP (top-hat, $k = 0.04$) underpredicts power.
* **Why it works:** Wakes inside the farm see higher turbulence, so they grow faster (larger $k^\*$) and recover sooner. Scaling deficits by $U\_k$ stops them from piling up row after row.
* **Limits:**

  * Only the *linearised* momentum is conserved (revisited by Zong \& Porté-Agel, 2020).
  * A wake keeps its original $k^\*\_k$ even as it passes through regions of higher turbulence.
  * The $k^\*(I)$ fit comes from one turbine type under neutral conditions.
  * There is no blockage or upstream induction.

