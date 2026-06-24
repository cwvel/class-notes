# 30.1 Mutual Inductance
Change in current in coil 1 $\rightarrow$ changing $\vec B$ and $\Phi_B$ in coil 2 $\rightarrow$ emf (current) in coil 2
![200](Pasted%20image%2020260126154738.png)
$M$, **mutual inductance** between the two coils (proportionality constant)
$$M_{21}=\frac{N_2\Phi_{B2}}{i_1}$$
- $i_1$ = time-varying current through coil 1, producing magnetic field $B$
- $\Phi_{B2}$ = flux through each turn of the coil (or average flux)
- $N_2$ = # of turns in coil 2
- *Note:* $M_{12}=M_{21}$ always
- Units: **henry** (1 H = 1 Wb/A ...)

![Pasted image 20260126154900](Pasted%20image%2020260126154900.png)![Pasted image 20260126155209](Pasted%20image%2020260126155209.png)

# 30.2 Self-Inductance and Inductors
Any circuit with a varying current has an emf induced in it by the variation in its own magnetic field, called a **self-induced emf**, which opposes the change in current that caused the emf.
![Pasted image 20260126155456](Pasted%20image%2020260126155456.png)

![200](Pasted%20image%2020260126155459.png)
Same units as mutual inductance.
$$N\frac{d\Phi_B}{dt}=L\frac{di}{dt}$$
![Pasted image 20260126155528](Pasted%20image%2020260126155528.png)
minus sign reflects Lenz's law

## Inductors as circuit elements
A circuit device designed to have a particular inductance is called an **inductor** or **choke**
![100](Pasted%20image%2020260126155707.png)
Opposes any variation in current through the circuit
For $\vec E_c$ = conservative field, $\vec E_n$ = nonconservative field within the inductor coils,
$$\oint\vec E_n\cdot d\vec l=-L\frac{di}{dt}$$
$$\int_a^b\vec E_n\cdot d\vec l=-L\frac{di}{dt}$$
$\vec E_c+\vec E_n=0$ at each point within the inductor, so $\vec E_n=-\vec E_c$
$$\int_a^b\vec E_c\cdot d\vec l=L\frac{di}{dt}$$
the integral is the same as:
$$V_{ab}=V_a-V_b=L\frac{di}{dt}$$

![300](Pasted%20image%2020260126155821.png)
*The potential difference across a **resistor** depends on the current.*
![300](Pasted%20image%2020260126155828.png)
![300](Pasted%20image%2020260126155834.png)
![300](Pasted%20image%2020260126155838.png)
*The potential difference across an **inductor** depends on the rate of change of the current.*

# 30.3 Magnetic-Field Energy
Instantaneous power $P$ (rate of transfer of energy into the conductor):
$$P=V_{ab}i$$
$$P=\frac{dE(t)}{dt}$$
$E=$ energy
## Energy stored in an inductor
![Pasted image 20260126160515](Pasted%20image%2020260126160515.png)
- As the current increases, energy is stored in the inductor
- As the current decreases from $I$ to $0$, the inductor acts as a source that supplies the amount of energy $\frac{1}{2}LI^2$ to the circuit
*This is different from a resistor, which dissipates energy as heat when current flows through it.*
![300](Pasted%20image%2020260126160652.png)

## Magnetic Energy Density
The energy in an inductor is actually stored in the magnetic field of the coil, just as the energy of a capacitor is stored in the electric field between its plates.
![Pasted image 20260126160747](Pasted%20image%2020260126160747.png)

If the material inside is a material with constant magnetic permeability $\mu=K_m\mu_0$, then
![Pasted image 20260126160750](Pasted%20image%2020260126160750.png)
aka, energy stored in magnetic field (**magnetic field energy**)
# 30.4 R-L Circuit
## Current Growth in an R-L circuit
**R-L circuit**: contains both a resistor and an inductor, and possibly an emf source
Resistor can come from the resistance of the inductor windings
$\implies$ **Exponential approach to steady-state situation**

![300](Pasted%20image%2020260126161347.png)

![300](Pasted%20image%2020260126161423.png)

**time constant** of a circuit: measure of how quickly the current builds towards its final value
![Pasted image 20260126161504](Pasted%20image%2020260126161504.png)

## Current Decay in an R-L Circuit
![300](Pasted%20image%2020260127135117.png)
Voltage across resistor: $v_{ab}=iR$
Voltage across inductor: $v_{bc}=L\frac{di}{dt}$

current $i$ varies with time:
Charging:
$$i=I_0e^{-(R/L)t}$$
Discharging:
$$i=I_0(1-e^{-(R/L)t})$$

![300](Pasted%20image%2020260126161554.png)

# 30.5 The L-C Circuit
A circuit containing an inductor and a capacitor
$\implies$ **Oscillating current and charge**

![Pasted image 20260126161729](Pasted%20image%2020260126161729.png)
In an oscillating L-C circuit, the charge on the capacitor and the current through the inductor both vary **sinusoidally** with time. **Total energy $E$ remains constant.**

Cycle:
1. Capacitor discharges through the inductor
	1. Current starts at 0 and gradually increases
2. Capacitor fully discharged, current at maximum
	1. Energy in capacitor's electric field has fully transferred to inductor's magnetic field
3. Capacitor recharges through the inductor as it slows the current's decreases
4. Repeat

## Electric Oscillations in an L-C Circuit
![300](Pasted%20image%2020260126162438.png)

![Pasted image 20260126162450](Pasted%20image%2020260126162450.png)
Instantaneous current $i=dq/dt$:
$$i=-\omega Q\sin(\omega t+\phi)$$

## Energy in an L-C Circuit
Since the L-C circuit is a conservative system
The sum of all energies (magnetic-field energy + electric-field energy) is the total energy of the system:
$$\frac{1}{2}Li^2+\frac{q^2}{2C}=\frac{Q^2}{2C}$$
When the charge in the capacitor is $q$, the current is
$$i=\pm\sqrt{\frac{1}{LC}}\sqrt{Q^2-q^2}$$
Analogous to simple harmonic motion of an oscillating object (oscillating between KE and PE)
![300](Pasted%20image%2020260126162746.png)

# 30.6 L-R-C Series Circuit
**Damped harmonic motion**
- Can be underdamped, critically damped, or overdamped depending on magnitude of resistance $R$ of the resistor
![300](Pasted%20image%2020260126162855.png)

## Analyzing an L-R-C Series Circuit
![300](Pasted%20image%2020260126162914.png)
Applying **Kirchhoff's loop rule** from a in the direction of abcda:
$$-iR-L\frac{di}{dt}-\frac{q}{C}=0$$
$\iff$
$$\frac{d^2q}{dt^2}+\frac{R}{L}\frac{dq}{dt}+\frac{1}{LC}q=0$$

When $R^2<4L/C$ (***underdamped***), the solution has the form
$$q=Ae^{-(R/2L)t}\cos\left(\sqrt{\frac{1}{LC}-\frac{R^2}{4L^2}t}+\phi\right)$$
where $A$ and $\phi$ are constants.

![Pasted image 20260126162923](Pasted%20image%2020260126162923.png)

# Inductors in circuits
Series: $L_{eq}=L_1+L_2$
Parallel: $L_{eq}=\frac{1}{L_1}+\frac{1}{L_2}$


![300](Pasted%20image%2020260127132300.png)
Connected in series: $L_{eq}=L_1+L_2+2M$
Connected in parallel, with current travelling the same way through both: $L_{eq}=\dfrac{L_1L_2-M^2}{L_1+L_2-2M}$
Parallel with current travelling opposite: $L_{eq}=\dfrac{L_1L_2-M^2}{L_1+L_2+2M}$ ?