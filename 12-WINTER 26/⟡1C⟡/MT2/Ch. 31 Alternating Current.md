### 31.1 Phasors and Alternating Currents
- an alternator/ac source produces an emf that varies sinusoidally with time
- **sinusoidal voltage:** $v=V\cos\omega t$
	- $v$ = instantaneous potential difference
	- $V$ = maximum potential difference
- **sinusoidal alternating current:** $i=I\cos\omega t$
	- $i$ = instantaneous current
	- $I$ = current amplitude (max)
	- $\omega$ = angular frequeency
- can be represented as a **phasor**:
	- vector rotates counterclockwise with constant angular velocity $\omega$
	- projection onto horizontal axis is the instantaneous value
	![100](Pasted%20image%2020260228115421.png)
- **rectified average:** $I_\text{rav}=\frac{2}{\pi}I=0.637I$
	- during any whole # cycles, total $I$ same as if the current were constant $I_\text{rav}$
		- $2/\pi$ = average of $|\cos|$ or $|\sin|$
	- $I$ = current amplitude
- **rms:** $V_\text{rms}=\frac{V}{\sqrt2}$, $I_\text{rms}=\frac{I}{\sqrt2}$
	- represents equivalent DC power
	- $i$ = instantaneous current, then the average of $i^2$ is $I^2/2$, 
$$I_\text{rms}=\sqrt{(i^2)_\text{av}}=\sqrt{\frac{I^2}{2}}=\frac{I}{\sqrt2}$$

### 31.2 Resistance and Reactance
- in general, the instantaneous voltage $v=V\cos(\omega t+\phi)$ between two points in an ac circuit is not *in phase* with the instantaneous current through those points
	- $\phi$ = **phase angle** of voltage relative to current
	![100](Pasted%20image%2020260228115637.png)
- in a **resistor**
	- current and voltage are *in phase*
	- $i=I\cos\omega t$, $v_R=IR\cos\omega t$
	- voltage across a **resistor**: $V_R=IR$
		- $v_R=V_R\cos\omega t$
- in an **inductor**
	- voltage *leads* current ($\phi=90^\circ$)
	- $i=I\cos\omega t$, $v_L=L\frac{di}{dt}=-I\omega L\sin \omega t$
		- $v_L$ proportional to derivative of $i$
	- voltage across an **inductor**: $V_L=IX_L$
		- **inductive reactance:** $X_L=\omega L$ ($\Omega$)
			- describes the self-induced emf that opposes change in current through inductor
			- larger $X_L$ = smaller amplitude of current due to voltage
			- high frequency voltage gives smaller $I$ while lower frequency voltage (of same amplitude) gives larger $I$
- in a **capacitor**
	- voltage *lags* current ($\phi=-90^\circ$)
	- $i=I\cos\omega t$, $v_C=\frac{I}{\omega C}\sin \omega t=\frac{I}{\omega C}\cos(\omega t-90^\circ)$
		- $i$ is proportional to derivative of $v_C$
	- voltage across a **capacitor**: $V_C=IX_C$
		- **capacitive reactance:** $X_C=1/\omega C$ ($\Omega$)
			- tend to pass high-frequency current and block low-frequency currents and dc (opposite of inductors)
	![200](Pasted%20image%2020260228125402.png)
![Pasted image 20260128235423](Pasted%20image%2020260128235423.png)

### 31.3 Impedance and L-R-C series circuit
- the source voltage phasor is the vector sum of $V_R$, $V_L$, $V_C$ phasors
	- $X_L>X_C\implies\phi>0$
	- $X_L<X_C\implies\phi<0$
- the instantaneous total voltage across all components must be the vector sum of the voltage across all three components (*Kirkchhoff's rule*)
- in a general ac circuit, voltage and current amplitudes are related by the **circuit impedance $Z$**
$$V=IZ$$
$$Z=\sqrt{R^2+[\omega L-(1/\omega C)]^2}$$
- $Z_R=R$
- $Z_L=j\omega L$
- $Z_C=\frac{1}{j\omega C}$
$$Z=\sqrt{R^2+(X_L-X_C)^2}$$
$$Z=R+jX,\qquad X=X_L-X_C$$
- in an L-R-C series circuit, the phase angle is determined by $\omega$, $L$, $R$, $C$
$$\tan\phi=\frac{X_L-X_C}{R}=\frac{\omega L-1/\omega C}{R}$$
![200](Pasted%20image%2020260228131130.png)
- **in a parallel RC circuit**
	- resistor branch: $$I_{R,\text{rms}}=\frac{V_\text{rms}}{R}$$
	- capacitor branch: $$I_{C,\text{rms}}=\frac{V_\text{rms}}{X_C}$$
		- where $X_C=1/\omega C$
	- in general: $$I_C(t)=C\frac{dV(t)}{dt}$$
	- total current:
$$I_\text{tot}=\sqrt{I_R^2+I_C^2}$$
	- phase angle:
$$\tan\phi=\frac{I_C}{I_R}=\frac{X_R}{X_C}=\omega CR$$

### 31.4 Power in alternating current circuits
- instantaneous power to a circuit element:
$$p=vi$$
-  **power in general ac circuit**
	- in any AC circuit of resistors, capacitors, and inductors, the voltage $v$ across the entire circuit has some phase angle $\phi$ wrt $i$:
$$p=vi=[V\cos(\omega t+\phi)][I\cos \omega t]$$
	- average power input depends on $V$ and $I$ rms values and $\phi$ (phase angle of voltage relative to current)
		- $\cos\phi$ = **power factor** of the circuit
			- pure resistance: $\phi=0$, $\cos\phi=1$, $P_{av}=V_{rms}I_{rms}$
			- pure inductor/capacitor: $\phi=\pm 90^\circ$, $\cos\phi=0$, $P_{av}=0$
			- for an L-R-C series circuit, $\cos\phi=\frac{R}{Z}$
$$P_\text{av}=\frac{1}{2}VI\cos\phi=V_\text{rms}I_\text{rms}\cos\phi=I_\text{rms}^2R$$
$$p_\text{max}=2P_\text{av}$$
	- when $v$, $i$ are in phase, $\phi=0$, $P_{avg}=0$
	- when $v$ has angle $\phi$ wrt $i$, $P_{avg}=\frac{1}{2}IV\cos\phi$
- **power in a resistor:**
$$P(t)=\frac{V(t)^2}{R}$$
	- average power:
$$P_\text{av}=\frac{1}{2}VI=\frac{V_\text{rms}^2}{R}$$
- **power in an inductor**
	- when $p>0$, energy is going into the m-field of the inductor
	- when $p<0$, m-field is collapsing and supplying energy to source
	- net energy transfer over one cycle is 0
- **power in a capacitor**
	- average power and net energy transfer is 0

### 31.5 Resonance in AC Circuits
- at **resonance angular frequency** $\omega_0$, we get maximum current $I$ at minimum impedance $Z$
	- the frequency at which a voltage can generate the highest amplitude of $I$
- at resonance frequency, $Z=R$ (since no contribution from $L$ and $C$),
$$Z=R\implies I=V_{source}/R$$
- as $\omega$ of source varies, the current amplitude $I=V/Z$ varies and the maximum of $I$ occurrs when impedance $Z$ is minimum
$$\omega_0=\frac{1}{\sqrt{LC}}$$
	- above $w_0$, $V$ lags $I$
		- $X_C<X_L$, $\phi>0$
	- below $w_0$, $V$ leads $I$
		- $X_C>X_L$, $\phi<0$

$$f_0=\frac{w_0}{2\pi}$$
	- frequency of the max current and min impedance
- also at resonance frequency, $X_L=X_C$
	- instantaneous voltages across $L$ and $C$ **cancel out**
- AC circuits can be "tuned" to vary the resonance frequency
![200](Pasted%20image%2020260206113535.png)

### 31.6 Transformers
- ac source causes an **alternating current** in the primary winding $\rightarrow$ **alternating flux** in the core $\rightarrow$ **induced emf** in each windings from Faraday's law $\rightarrow$ induced emf in secondary winding causes **alternating current** in the secondary, which powers the device to which it is connected
- all currents and emfs have the same frequency as the ac source
- from $\mathcal{E}_1=-N_1\frac{d\Phi_B}{dt}$ (and same for 2),
$$\frac{\mathcal{E}_2}{\mathcal{E}_1}=\frac{N_2}{N_1}$$
- in an ideal transformer:
$$\frac{V_2}{V_1}=\frac{N_2}{N_1}$$
	- where $N_1$ = # turns in primary, $N_2$ = # turns in secondary
	- $V_1$ = primary voltage amp/rms, $V_2$ = secondary voltage amp/rms
![200](Pasted%20image%2020260228135332.png)

- by choosing the appropriate turns ration $N_2/N_1$, we can otain any desired secondary voltage from a given primary voltage
	- $N_2>N_1\implies V_2>V_1\implies$ **step-up** transformer
	- $N_2<N_1\implies V_2<V_1\implies$ **step-down** transformer
- For an ideal transformer,
$$\frac{V_1}{V_2}=\frac{N_1}{N_2}=\frac{I_2}{I_1}$$
- **power deliverd to primary = primary taken out of secondary**
$$V_1I_1=V_2I_2$$
$$\frac{V_1}{I_1}=\frac{R}{(N_2/N_1)^2}$$
- when the secondary circuit is completed through a resistance $R$, the result is the same as if the source had been connected directly to the resistance $R$ divided by the square of the ratio, $(N_2/N_1)^2$
- transformer "transforms" voltages, currents, and resistances - transforms the *impedance* of the network to which the secondary circuit is completed
- **Eddy currents can cause energy loss in transformers**
![200](Pasted%20image%2020260206114501.png)
![200](Pasted%20image%2020260206114524.png)
- effects can be minimized using a laminated core -- possible eddy current paths are narrower
![200](Pasted%20image%2020260206114539.png)