# Bastankhah & Porté-Agel (2014): *A new analytical model for wind-turbine wakes*

*Renewable Energy* (2014), doi:10.1016/j.renene.2014.01.002. WIRE Lab, EPFL.

The model replaces the **top-hat** deficit of Jensen and Frandsen with a **Gaussian** deficit. Its amplitude comes from mass and momentum conservation, and the wake grows linearly with distance. The only free parameter is the wake growth rate.

---

## 1. The wake model (Section 2 of the paper)

### 1.1 Momentum balance

If viscous and pressure terms are neglected, mass and momentum conservation applied to the wake give

$$
\rho \int U_w\,(U_\infty - U_w)\, dA = T, \qquad (8)
$$

where $\rho$ is the air density, $U_\infty$ the incoming wind speed, $U_w$ the streamwise velocity in the wake, $dA$ an element of the wake cross-section, and $T$ the thrust force on the turbine. The left-hand side is the momentum flux the wake has lost. The thrust is

$$
T = \tfrac{1}{2}\, C_T\, \rho\, A_0\, U_\infty^2, \qquad (9)
$$

where $C_T$ is the thrust coefficient and $A_0 = \pi d_0^2/4$ the rotor swept area, with $d_0$ the rotor diameter.

### 1.2 Self-similar Gaussian deficit

$$
\frac{\Delta U}{U_\infty} = C(x)\, f\!\left(\frac{r}{\delta(x)}\right), \qquad (10)
$$

$\Delta U/U_\infty = (U_\infty - U_w)/U_\infty$ is the normalised velocity deficit and $x$ the downwind distance. $C(x)$ is the maximum normalised deficit at each $x$, which occurs on the wake centreline. $r$ is the radial distance from the wake centre, $\delta(x)$ a characteristic wake width, and $f$ a shape function that is the same at every $x$ (that is what "self-similar" means). Choosing a Gaussian for $f$:

$$
\frac{\Delta U}{U_\infty} = C(x)\, e^{-\frac{r^2}{2\sigma^2}}, \qquad (11)
$$

where $\sigma(x)$ is the standard deviation, i.e. the width, of the Gaussian deficit profile. It is a spatial width and has nothing to do with turbulent fluctuations. The wake velocity is then

$$
U_w = U_\infty\left(1 - C(x)\, e^{-\frac{r^2}{2\sigma^2}}\right). \qquad (12)
$$

### 1.3 Amplitude of the deficit

Substituting (9) and (12) into (8) and integrating over $r$ from $0$ to $\infty$ gives a quadratic in $C$:

$$
8\left(\frac{\sigma}{d_0}\right)^2 C(x)^2 - 16\left(\frac{\sigma}{d_0}\right)^2 C(x) + C_T = 0. \qquad (13)
$$

The physical root is the one whose deficit gets smaller further downstream:

$$
C(x) = 1 - \sqrt{1 - \frac{C_T}{8\,(\sigma/d_0)^2}}. \qquad (14)
$$

### 1.4 Linear wake expansion

$$
\frac{\sigma}{d_0} = k^*\,\frac{x}{d_0} + \varepsilon, \qquad (15)
$$

$k^* = \partial\sigma/\partial x$ is the wake growth rate, and $\varepsilon$ is the value of $\sigma/d_0$ as $x \to 0$. $k^*$ is not the same as Jensen's $k_{wake}$, which is the growth rate of the top-hat wake radius.

### 1.5 Full velocity-deficit field

Inserting (14) and (15) into (11):

$$
\frac{\Delta U}{U_\infty} = 
\left(1 - \sqrt{1 - \frac{C_T}{8\left(k^* x/d_0 + \varepsilon\right)^2}}\right)
\exp\!\left(-\frac{1}{2\left(k^* x/d_0 + \varepsilon\right)^2}
\left[\left(\frac{z - z_h}{d_0}\right)^2 + \left(\frac{y}{d_0}\right)^2\right]\right) \qquad (16)
$$

Here $y$ is the spanwise coordinate, $z$ the vertical coordinate, and $z_h$ the hub height, so that $r^2 = y^2 + (z - z_h)^2$.

### 1.6 Determining $\varepsilon$

To find $\varepsilon$, the authors equate the **total mass-flow deficit rate** at $x = 0$,

$$
\int \frac{\Delta U}{U_\infty}\, dA,
$$

computed two ways: with the Frandsen model and with Eq. (16). Eq. (16) cannot capture the real, roughly uniform profile right behind the rotor, but both models rest on the same conservation laws, so this integral should agree. The result is

$$
\varepsilon = 0.25\,\sqrt{\beta}, \qquad (19)
$$

where $\beta$ is the wake-area expansion ratio from actuator-disk theory, i.e. the area of the wake once its pressure has recovered, divided by $A_0$:

$$
\beta = \frac{1}{2}\,\frac{1 + \sqrt{1 - C_T}}{\sqrt{1 - C_T}}. \qquad (6)
$$

---

## 2. Qualitative interpretation of Eq. (16)

Eq. (16) is **amplitude × shape**.

- **Shape (the exponential).** The deficit is largest on the hub axis and fades smoothly towards the edge, with no sharp wake boundary. Since $\sigma$ grows linearly with $x$, the wake is a widening cone with soft edges.
- **Amplitude $C(x)$.** The rotor removes a fixed momentum flux, equal to $T \propto C_T$. Turbulent mixing does not remove this deficit. It spreads it over a cross-section that grows like $\sigma^2$, so the centreline deficit must fall. More thrust gives a deeper wake; a wider wake gives a shallower one. Far downstream, $C \approx C_T / [16(\sigma/d_0)^2] \propto 1/x^2$.
- **$k^*$ is the turbulence knob.** More ambient turbulence means more mixing, a larger $k^*$ and faster wake recovery.
- **Validity.** The square root is real only when $8(\sigma/d_0)^2 \ge C_T$. This is my own check, not stated in the paper: for $C_T = 0.8$ it fails within roughly the first 2 diameters, so this is a far-wake model.

---

## 3. Results (short)

- **Self-similarity.** Wind-tunnel and LES deficit profiles collapse onto one Gaussian for $x/d_0 \gtrsim 3$. The data cover one miniature turbine and a V80 over four terrain roughnesses.
- **Linear growth.** $\sigma/d_0$ grows roughly linearly for $2 < x/d_0 < 15$, not like the classical $x^{1/3}$. The reason is that ambient turbulence speeds up wake growth. Higher turbulence gives a larger $k^*$, which the authors fit to the data for each case.
- **Correction to $\varepsilon$.** Extrapolating the LES fits back to $x = 0$ shows that Eq. (19) has the right trend (higher $C_T$ gives larger $\varepsilon$) but overestimates the value. The cause is Frandsen's assumption that the expanded wake area applies right at $x = 0$, when it really applies slightly downstream. The authors recommend

$$
\varepsilon = 0.2\,\sqrt{\beta}. \qquad (21)
$$

- **Accuracy.** The Gaussian model matches the hub-height deficit and vertical profiles well. The top-hat models (Jensen, Frandsen) underestimate the deficit at the wake centre and overestimate it at the edge.
- **Power.** Available power scales with $U_w^3$, so profile errors are amplified. At $x/d_0 = 7$, a $5^\circ$ change in wind direction changes the top-hat models' power error by 15–30% or more. For the Gaussian model it changes by only 3–7%. This matters a lot for wind-farm layout optimisation.
- **Neglected effects.** The ground effect changes the hub-height deficit by less than 0.01, and wake rotation is weak for $x/d > 5$, so both are neglected.
