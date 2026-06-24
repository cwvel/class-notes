### 32.1 maxwell's equations and electromagnetic waves
- maxwell's equations: electromagnetic waves propagate in vacuum at the speed of light
- **plane wave:** at any instant, the fields are uniform over any plane perpendicular to the direction of propagation
	- direction of propagation: $\vec E\times \vec B$

![200](../../pasted_images/Pasted%20image%2020260209190220.png)

- electromagnetic wave in a vacuum:
	- ratio between magnitudes of electric and magnetic field: $E=cB$
	- $B=\epsilon_0\mu_0cE$
- speed of electromagnetic waves in a vacuum:
$$c=\frac{1}{\sqrt{\epsilon_0\mu_0}}$$
- **properties of the electromagnetic wave:**
	1. *transverse:* both $\vec E$ and $\vec B$ perpendicular to the direction of propagation, and to each other (direction of propagation = $\vec E\times\vec B$)
	2. wave travels in a *vacuum* with definite and constant speed
- **right-hand-rule**
![250](../../pasted_images/Pasted%20image%2020260209190511.png)

### 32.2 sinusoidal electromagnetic waves
- a sinusoidal plan em-wave traveling in vacuum in $+x$ direction
	- if propagating in $-x$ direction, use $kx+\omega t$ instead
	- $k=2\pi/\lambda$, $\omega=ck=2\pi f$, $f=c/\lambda$
$$\vec E(x,t)=E_\text{max}\cos(kx-\omega t)\hat j$$
$$\vec B(x,y)=B_\text{max}\cos(kx-\omega t)\hat k$$
$$E_\text{max}=cB_\text{max}$$
![200](../../pasted_images/Pasted%20image%2020260228141140.png)
### 32.3 electromagnetic waves in matter
- when the em wave travels through a *dielectric* the wave speed $v$ is less than $c$
$$v=\frac{1}{\sqrt{\epsilon\mu}}=\frac{c}{\sqrt{KK_m}}$$
- thus the wavelength shortens as $f$ stays the same:
$$v=f\lambda$$
### 32.4 energy and momentum in electromagnetic waves
- the energy flow rate (power per unit area) in an em wave in vacuum is given by the **poynting vector** $\vec S$
$$\vec S=\frac{1}{\mu_0}\vec E\times \vec B$$
$$|\vec S|=c\langle u\rangle$$
- intensity of sinusoidal em wave is the time-averaged value of $\vec S$:
$$I=S_\text{av}=\frac{E_\text{max}B_\max}{2\mu_0}=\frac{E_\max^2}
{2\mu_0c}=\frac{1}{2}\sqrt{\frac{\epsilon_0}{\mu_0}}E_\max^2=\frac{1}{2}\epsilon_0cE_\max^2$$
$$I=\frac{P}{A}$$
	- intensity decreases with distance (inverse square law): $I\propto\frac{1}{r^2}$
- electromagnetic waves *carry momentum* and exerts radiation pressure $p_\text{rad}$ when it strikes a surface
	- if surface is perpendicular to propagation direction and is *totally absorbing*: $p_\text{rad}=I/c$
	- if surface is a *perfect reflector*: $p_\text{rad}=2I/c$ (wave totally reflected)
- flow rate of electromagnetic momentum:
$$\frac{1}{A}\frac{dp}{dt}=\frac{S}{c}=\frac{EB}{\mu_0c}$$
- **energy density**
	- in a vacuum:
$$u=\varepsilon_0E^2$$
	- in an electric field, $E$:
$$u_E=\frac{1}{2}\epsilon_0E^2$$
	- in a magnetic field, $B$:
$$u_B=\frac{1}{2}\epsilon_0E^2=\frac{B^2}{2\mu_0}$$
	- average energy density (note, average value of $\sin^2(\alpha)=1/2$):
$$\langle u\rangle=\langle u_E\rangle+\langle u_B\rangle$$
- **poynting vector of a resistor**
![200](../../pasted_images/Pasted%20image%2020260213105747.png)
- at the surface: $B=\frac{\mu_0i}{2\pi r_0}$, $E=\frac{iR}{l}$ $\implies |\vec S|=\frac{i^2R}{l2\pi r_0}$
- integrated across the surface of the resistor (multiplying by the surface area) gives the **power dissipated in a resistor** $P=Ri^2$
- **total power radiated:** integrated over a closed surface, for a sphere:
$$P=I\times 4\pi r^2$$

**Radiation pressure:** photon momentum transfer
- momentum of a photon $p$: $$p=\frac{U}{c}$$ so when an object *absorbs* a photon of energy $U$ it receives momentum $p$.
- total energy of photons striking (a mirror) in time interval $\Delta t$, where $I$ = radiation intensity and $A$ = surface area: $$U=IA\Delta t$$
- when the object *reflects* a photon of energy $U$, the momentum transfer is **twice** as much as absorption (as it must stop the photon and also send it back)
- radiation pressure: $$F_{rad}=\frac{\Delta p}{\Delta t}\left(=\frac{2IA}{c}\right)$$ (on a perfectly reflecting surface at normal incidence)

### 32.5 Standing Electromagnetic Waves
**standing wave.** superposition of an incident wave and a reflected wave (like on a string)

![300](../../pasted_images/Pasted%20image%2020260213110018.png)

**superposition principle of waves principle.**
$$E_y(x,t)=-2E_{max}\sin kx\sin \omega t$$
$$B_z(x,t)=-2B_{max}\cos kx \cos \omega t$$
**nodal planes** are the equivalents of the nodal points of a standing wave, and it is where the fields are 0. same with **antinodal planes**. for $\vec E$ and $\vec B$ they are
$$x=0,\frac{\lambda}{2},\lambda,\frac{3\lambda}{2},\dots\quad(\text{nodal planes of $\vec E$})$$
$$x=\frac{\lambda}{4},\frac{3\lambda}{4},\frac{5\lambda}{4},\dots\quad(\text{nodal planes of $\vec B$})$$
with the antinodal planes midway between any two adjacent nodal planes. the distnance between two nodal points is always $\frac{\lambda}{2}$.

**in a cavity** (equivalent of a string held at both ends) there must be a nodal plane at both conducting planes of the cavity. then the possible wavelengths and frequencies are
$$\lambda_n=\frac{2L}{n},\quad f_n=\frac{c}{\lambda_n}=n\frac{c}{2L}\quad(n=1,2,3,\dots)$$
