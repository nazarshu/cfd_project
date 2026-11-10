# From Jensen (1983) to Katic et al. (1986): turbine wake models

## 1\. A Note on Wind Generator Interaction — N.O. Jensen (1983)

**Notation.** $u$ is the ambient wind velocity, $r\_0$ the rotor radius, $v\_0$ the velocity just behind the rotor, $x$ the downwind distance, $r$ the wake radius at $x$, $v$ the (uniform) velocity inside the wake, $\\alpha$ the entrainment constant (about $0.1$), and $x\_0$ the spacing between generators in a row.

### 1.1 Single wake

**Eq. (1): balance across the wake cross-section**

$$
\pi r_0^2 v_0 + \pi(r^2 - r_0^2)u = \pi r^2 v
$$

The three terms are the flow through the rotor area, the flow through the entrained ring of ambient air, and the total flow through the wake at $x$. Jensen calls it a momentum balance, but it is a balance of volume flow.

**Eq. (2): wake velocity.** Solving (1) for $v$ gives

$$
v = u\left[1 - \left(1 - \frac{v_0}{u}\right)\left(\frac{r_0}{r}\right)^{2}\right].
$$

With a linearly expanding wake, $r = r\_0 + \\alpha x$, and the classical value $v\_0 = u/3$:

$$
v = u\left\lbrace 1 - \frac{2}{3}\left(\frac{r_0}{r_0 + \alpha x}\right)^{2}\right\rbrace
$$

**Eq. (2) with the induction factor ${a}$.** Actuator-disc theory gives $v\_0 = (1-2a) u$, so the **initial velocity deficit** is $\\quad 1 - \\dfrac{v_0}{u} = 2a\\quad$  and 

$$
v = u\left\lbrace1 - 2a\left(\frac{r_0}{r_0 + \alpha x}\right)^{2}\right\rbrace
$$

For the Betz value $a = 1/3$ Jensen's factor becomes $2a = 2/3$.

### 1.2 Multiple wakes in a row

**Eq. (8): velocity in front of generator $N$ in terms of the one before it**

$$
\\frac{v\_N}{u} = 1 - \\left(1 - \\frac{1}{3}\\frac{v\_{N-1}}{u}\\right)\\left(\\frac{r\_0}{r\_0 + \\alpha x\_0}\\right)^{2}
$$

**Eq. (9): shorthand notation**

$$
y\_N = \\frac{v\_N}{u}, \\qquad k = \\left(\\frac{r\_0}{r\_0 + \\alpha x\_0}\\right)^{2}
$$

**Eq. (10): recursion**

$$
y\_N = 1 - k\\left(1 - \\frac{y\_{N-1}}{3}\\right)
$$

Unrolling it:

$$
y\_1 = 1 - \\frac{2k}{3}, \\qquad
y\_2 = 1 - \\frac{2k}{3} - \\frac{2k^2}{9}, \\qquad
y\_3 = 1 - \\frac{2k}{3} - \\frac{2k^2}{9} - \\frac{2k^3}{27}
$$

**Eq. (11): general term**

$$
y\_N = y\_{N-1} - 2\\left(\\frac{k}{3}\\right)^{N}
$$

Combining (10) and (11) gives the explicit expression (a geometric sum):

$$
y\_N = 1 - 2 \\frac{k}{3}\\frac{1 - (k/3)^N}{1 - k/3}
$$

**Eq. (12): asymptotic velocity.** Since $(k/3)^N \\to 0$ quickly, with $\\chi = k/3$ (written $x$ in the paper):

$$
\\frac{v\_\\infty}{u} = 1 - \\frac{2\\chi}{1 - \\chi}
$$

For $r\_0 = 10$ m, $x\_0 = 100$ m and $\\alpha = 0.1$, the paper finds $v\_\\infty \\approx 0.82u$ .

## 2\. A Simple Model for Cluster Efficiency — I. Katic, J. Højstrup, N.O. Jensen (1986)

### 2.1 Model extension

**The thrust coefficient replaces the fixed $v\_0 = u/3$.** Jensen fixes the velocity behind the rotor at one third of the ambient value. Katic lets it depend on the turbine's thrust coefficient $C\_t$. In actuator-disc theory,

$$
C\_t = 4a(1-a), \\qquad U\_r = U(1-2a) = U\\sqrt{1 - C\_t},
$$

because $(1-2a)^2 = 1 - 4a(1-a) = 1 - C\_t$,

solving for the **axial induction factor** $a$:

$$
a = \\frac{1 - \\sqrt{1 - C\_t}}{2}
$$

while the **initial velocity deficit** is defined as

$$
2a = 1 - \\sqrt{1 - C\_t} \\qquad i.e. \\qquad 2a = 1 - \\frac{U_r}{U} = 1 - \\frac{v_0}{u} \\qquad .
$$

From Jensen, the velocity deficit downstream at $x$:

$$
1 - \frac{v}{u} = 2a\left(\frac{r_0}{r_0 + \alpha x}\right)^{2}
$$

which is the initial velocity deficit scaled by the fraction of rotor area inside the wake 

|Jensen (1983)|Katic (1986)|
|-|-|
|$u$|$U$|
|$v\_0$|$U\_r$|
|$v$|$V$|
|$\\alpha$|$k$|



This is the paper's expression for $a$. For the Betz limit, $C\_t = 8/9$, so $\\sqrt{1-C\_t} = 1/3$ and $a = 1/3$, which gives back Jensen's $v\_0 = u/3$.

**The meaning of $a$.** The paper defines $a$ as the *initial velocity deficit*, $1 - U\_r/U$, which is also the axial induction factor of the rotor. Note that its equations then require the deficit to equal $2a = 1 - \\sqrt{1-C\_t}$: strictly, $a$ is the induction factor and the initial deficit is $2a$.

**(c) Wake interaction is handled differently.** Instead of Jensen's generator-by-generator recursion (Eqs. 8–12), Katic adds the squared velocity deficits of the individual wakes. See section 2.3.

### 2.2 Wake velocity and velocity deficit

**Momentum (flow) balance, as in Jensen's Eq. (1) but with diameters:**

$$
D^2 U\_r + (D\_w^2 - D^2),U = D\_w^2, V
$$

**Wake velocity, as in the paper:**

$$
\\frac{V}{U} = 1 - \\frac{2a}{\\left(1 + \\dfrac{2kX}{D}\\right)^{2}}
$$

**Velocity deficit at position $X$, as in the paper (diameter form):**

$$
1 - \\frac{V}{U} = \\frac{1 - \\sqrt{1 - C\_t}}{\\left(1 + \\dfrac{2kX}{D}\\right)^{2}}
$$

**The same deficit written with the rotor radius** ($D = 2r\_0$, so $2kX/D = kX/r\_0$):

$$
1 - \\frac{V}{U} = \\frac{1 - \\sqrt{1 - C\_t}}{\\left(1 + \\dfrac{kX}{r\_0}\\right)^{2}}
= \\left(1 - \\sqrt{1 - C\_t}\\right)\\left(\\frac{r\_0}{r\_0 + kX}\\right)^{2}
$$

This is exactly Jensen's Eq. (2) with the fixed factor $2/3$ replaced by $1 - \\sqrt{1 - C\_t}$ (equal to $2/3$ at $C\_t = 8/9$) and $\\alpha$ renamed $k$.

**Dependence on wind speed.** The paper points out that $C\_t$ normally varies with wind speed, so the initial deficit, and hence this relative deficit, is valid for one wind speed only. This is why the farm efficiency has to be evaluated across the whole range of wind speeds.

### 2.3 Interacting wakes (page 408)

**The last four lines of the first column.** The paper states how interacting wakes are treated: the kinetic energy deficit of the mixed wake is assumed to equal the sum of the energy deficits of each individual wake, evaluated at the downwind position being considered.

**Resulting equation (top of the second column).** For two wakes with original velocities $V\_1$ and $V\_2$:

$$
\\left(1 - \\frac{V}{U}\\right)^{2} = \\left(1 - \\frac{V\_1}{U}\\right)^{2} + \\left(1 - \\frac{V\_2}{U}\\right)^{2}
$$

and for several upstream wakes $i$ acting on the same turbine:

$$
\\left(1 - \\frac{V}{U}\\right)^{2} = \\sum\_i \\left(1 - \\frac{V\_i}{U}\\right)^{2}
$$

(The printed formula adds the *squared velocity deficits*; the kinetic energy deficit itself would be $1 - (V/U)^2$.)

**Saturation of the deficit.** Right after that equation, the paper explains that because the deficits are squared, the total velocity deficit in the wake of a line of turbines, or of several rows, quickly settles at an equilibrium level, typically after about 3–4 turbines or rows, and it reports that this agrees well with wind tunnel results. This echoes Jensen's result in section 1.2: there too the term $(k/3)^N$ dies out quickly, so $v\_N$ converges to the asymptote of Eq. (12) after the first few generators.

\---

## References

1. N.O. Jensen, *A Note on Wind Generator Interaction*, Risø-M-2411, Risø National Laboratory, 1983.
2. I. Katic, J. Højstrup, N.O. Jensen, *A Simple Model for Cluster Efficiency*, EWEC'86 Proceedings, Vol. 1, pp. 407–410, A. Raguzzi, 1986/1987.

