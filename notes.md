# Notes on turbine wake literature

First LaTeX test:

Jensen model:

## Jensen (Park) wake model

**Wake expansion.** The wake grows linearly downstream, with $r_0 = D/2$ the rotor radius and $x$ the distance behind the rotor:

$$
r_w(x) = r_0 + kx \quad\Longleftrightarrow\quad D_w(x) = D + 2kx
$$

**Wake decay constant**, with $z_h$ the hub height and $z_0$ the surface roughness length:

$$
k = \frac{0.5}{\ln\left(z_h / z_0\right)}
$$

Typical values are $k \approx 0.075$ onshore and $k \approx 0.04$ to $0.05$ offshore.

**Axial induction factor** from the thrust coefficient:

$$
a = \frac{1-\sqrt{1-C_T}}{2}
$$

**Velocity deficit.** This comes from conservation of mass (momentum) in the expanding wake, assuming a top-hat velocity profile:

$$
\delta(x) = 1 - \frac{u(x)}{U_\infty} = \left(1-\sqrt{1-C_T}\right)\left(\frac{D}{D+2kx}\right)^2
$$

so the wake velocity is

$$
u(x) = U_\infty\left[1 - \left(1-\sqrt{1-C_T}\right)\left(\frac{D}{D+2kx}\right)^2\right]
$$

**Multiple wakes.** Deficits from the upstream turbines $j$ are combined by a sum of squares at turbine $i$:

$$
\left(1 - \frac{u_i}{U_\infty}\right)^2 = \sum_{j}\left(1 - \frac{u_{ij}}{U_\infty}\right)^2
$$

**Partial wake overlap.** The deficit is scaled by the fraction of rotor area inside the wake, where $A_{\text{overlap}}$ is the rotor area covered by the wake and $A_{\text{rotor}} = \pi D^2/4$:

$$
\delta_{ij} \to \delta_{ij}\,\frac{A_{\text{overlap}}}{A_{\text{rotor}}}
$$

**Power at each turbine:**

$$
P_i = \frac{1}{2}\,\rho\,A\,C_P(u_i)\,u_i^3
$$
