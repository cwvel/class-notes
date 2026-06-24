Emf $\mathcal{E}$ is voltage across a circuit element. If the equivalent electric field is $\vec E$, then:
$$\mathcal{E}=\int_a^b\vec E\cdot d\vec l$$

**Induced current:** Caused by conductor (ex. coil) experiencing changing magnetic field
**Induced emf**: Corresponding emf required to cause the current

Induced emf is proportional to the rate of change of magnetic flux $\Phi_B$ through the coil.

# 29.2 Faraday's Law
Magnetic flux $d\Phi_B$ through an area element $d\vec A$ in a magnetic field $\vec B$:
$$d\Phi_B=\vec B\cdot d\vec A=B\enspace dA\cos\phi$$
where $\phi$ is the angle between $\vec B$ and $d\vec A$.
Then total magnetic flux through a finite area is:
$$\Phi_B=\int\vec B\cdot d\vec A=\int B\enspace dA\cos\phi$$
![300](../../pasted_images/Pasted%20image%2020260120111922.png)
If $\vec B$ is uniform over a flat $\vec A$, then
$$\Phi_B=BA\cos\phi$$

![500](../../pasted_images/Pasted%20image%2020260120112023.png)

#### Faraday's Law of Induction:
$$\mathcal{E}=-\frac{d\Phi_B}{dt}$$
The induced emf in a closed loop $(\mathcal{E})$ equals the negative of the **time rate of change** of magnetic flux $(d\Phi_B)$ through the loop. 

****
**Direction of Induced emf**
>1. $\vec A$ is pointing in the positive direction.
>2. From $\vec A$ and $\vec B$, determine the sign of $\Phi_B$ and its rate of change $d\Phi_B/dt$
>	**Increasing** flux $(d\Phi_B/dt>0)\rightarrow$ **negative** emf/current
>	**Decreasing** flux $(d\Phi_B/dt<0)\rightarrow)$ **positive** emf/current
>3. Thumb points in the direction of $\vec A$. Positive emf is in the direction of your curled fingers, negative is the opposite.
****

For a coil with $N$ turns and varying flux, the total emf in the coil is:
$$\mathcal{E}=-N\dfrac{d\Phi_B}{dt}$$

# 29.3 Lenz's Law
#### Lenz's Law: 
The **direction** of any magnetic induction effect is such as to oppose the cause of the effect.

In other words the induced EMF opposes the voltage from the source.

![300](../../pasted_images/Pasted%20image%2020260120113213.png)
![300](../../pasted_images/Pasted%20image%2020260120113219.png)

The magnitude of the current still depends on the circuit resistance. *More resistance = less induced current = easier for flux change to take effect.*
**Persistent current**: Zero resistance, so induced current continues to flow after induced emf has disappeared.

# 29.4 Motional emf
$$\mathcal{E}=vBL$$
- $\mathcal{E}$ = motional emf when conductor length and velocity is perpendicular to the uniform $\vec B$
- $v$ = conductor speed
- $B$ = magnitude of uniform magnetic field
- $L$ = conductor length
Direction of the induced emf determined using Lenz's law.
Only valid if the magnetic field is constant across the length of the entire conductor, otherwise you have to integrate.
#### General form of emf of moving conductor
$$\mathcal{E}=\oint(\vec v\times\vec B)\cdot d\vec l$$
- Line integral over all elements of **closed conducting loop**
### Example
![400](../../pasted_images/Pasted%20image%2020260120122925.png)
Battery drives a current $I=\frac{V}{R}$ through the circuit.
Because the rod is carrying a current $I$ in a uniform magnetic field $B$ (out of the page), the rod accelerates left.
As the rod moves left with velocity $v$, it cuts magnetic field lines and develops a motional emf $\mathcal{E}=vBL$
By Lenz's law this EMF opposes the source-driven current ($I=\frac{V-\mathcal{E}}{R}$). The current through the rod generates a force ($F=qvB$) and as the current decreases the force also decreases, so the magnitude of acceleration decreases with time.
Eventually, the rod reaches terminal velocity when $V=\mathcal{E}=vBL$. So $I=0$ and the magnetic force vanishes, so the rod stops accelerating. The velocity of the rod will approach but never exceed a certain terminal velocity

# 29.5 Induced Electric Fields
Induced emf due to changing flux through stationary conductor.
#### Faraday's law for a stationary integration path:
$$\oint \vec E\cdot d\vec l=-\frac{d\Phi_B}{dt}$$
- Line integral of electric field around path = Negative of the time rate of change of magnetic flux through path

# 29.6 Eddy Currents
![300](../../pasted_images/Pasted%20image%2020260120125544.png)
"Loops" of electric current induced in conductors that experience a changing magnetic flux. Eddy currents flow in loops inside the conductor, when there is no well-defined external circuit.

# 29.7 Displacement Current and Maxwell's Equations
## Displacement current
![400](../../pasted_images/Pasted%20image%2020260122102559.png)

Fictitious displacement current in the region between the plates: The changing flux through the bulging surface is equivalent to a conduction current through that surface
Between the capacitors there is no conduction current but there is a "displacement current" that induces a magnetic field
![Pasted image 20260122102544](../../pasted_images/Pasted%20image%2020260122102544.png)


Definition of electric flux:
$$\Phi_E=\int \vec E\cdot d\vec A$$

Generalized Ampere's law:
$$\oint \vec B\cdot d\vec l=\mu_0(i_C+i_D)_{encl}$$
Also, the displacement current density:
$$j_D=\epsilon\frac{dE}{dt}=\frac{I_D}{A}$$

![300](../../pasted_images/Pasted%20image%2020260122102815.png)
A capacitor being charged by a current $i_C$ has a displacement current equal to $i_C$ between the plates. This can be regarded as the source of the magnetic field between the plates.

## Maxwell's Equations of Electromagnetism
![Pasted image 20260122102853](../../pasted_images/Pasted%20image%2020260122102853.png)
![Pasted image 20260122102856](../../pasted_images/Pasted%20image%2020260122102856.png)
![Pasted image 20260122102900](../../pasted_images/Pasted%20image%2020260122102900.png)
![Pasted image 20260122102903](../../pasted_images/Pasted%20image%2020260122102903.png)

### Symmetry
![300](../../pasted_images/Pasted%20image%2020260122102915.png)

# 29.8 Superconductivity
Superconductor: Sudden disappearance of all electrical resistance when the material is cooled below the critical temperature $T_c$.

![200](../../pasted_images/Pasted%20image%2020260122103125.png)

![200](../../pasted_images/Pasted%20image%2020260122103131.png)


![200](../../pasted_images/Pasted%20image%2020260122103138.png)