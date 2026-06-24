# (1) measurement and error
- **accuracy:** closeness to *true value*
- **precision:** closeness to *each other* (variance)
- **random error:** vary arbitrarily in sign/magnitude
- **systemic errror:** result from flaws in design/operation/interpretation of experiment, all occurring in the same directly *ex. consistently reading the volume higher on meniscus*

- **absolute error:** same unit and sigfigs as measurement 
$$\Delta A=\pm0.1\text{cm}$$
- **% relative error:**
$$\%\text{ relative error}=\frac{\text{absolute error}}{\text{measurement}}\times 100\%$$
### relative error propagation
- where $\Delta A$ and $\Delta B$ are *absolute errors* in $A$ and $B$
	- $\Delta C$ = absolute error in $C$
	- $\Delta C/C$ = relative error in $C$
- **multiplication:**
$$C=A\times B,\qquad C=A\div B$$
$$\frac{\Delta C}{C}=\frac{\Delta A}{A}+\frac{\Delta B}{B}$$

- **addition:**
$$C=A+B,\qquad C=A-B$$
$$\frac{\Delta C}{C}=\frac{\Delta A}{C}+\frac{\Delta B}{C}$$

# (2) beer-lambert law
- **volumetric glassware** always has sigfigs to the hundredth place in mL units, e.g. 10-mL volumetric pipet $\to$ 10.00 mL
### beer's law
- $I_0$ = incident light intensity
- $I$ = transmitted light intensity
- $\varepsilon$ = molar absorptivity constant (L/mol cm) or (M$^{-1}$cm$^{-1}$)
- C = concentration (M)
- L = depth of solution in cm
$$\text{transmittance} =T= \frac{I}{I_0}=10^{-\varepsilon LC}$$
$$\text{absorbance}=A=\varepsilon LC$$
$$A=-\log T$$
- $\varepsilon$ constant when $A$ is between 0.1 and 1.0
![250](Pasted%20image%2020260313135815.png)
- optimal wavelength: choose at **highest absorbance**
![250](Pasted%20image%2020260313135850.png)
- blanking for background interference: **blank solution** should contain all chemical species except for the one being measured
	- incorrect blank solution $\to$ y-intercept will not be at 0

# (3) pH and Normality
### definitions
- **arrhenius:**
	- acid: produces $H_3O^+$ in water
	- base: produces $OH^-$ in water
	- monoprotic acid: only contains one acidic proton $(HCl, HNO_3)$
	- polyprotic acid: contains more than one acidic proton $(H_2CO_3, H_3PO_4)$
	- monoacidic base: only contains one hydroxide $(NaOH,KOH)$
	- polyacidic base: contains more than one hydroxide $(Mg(OH)_2, Al(OH)_3)$
- **bronsted-lowry:**
	- acid: donates $H^+$
	- base: accepts $H^+$
- **lewis:**
	- acid: accepts an electron pair
	- base: donates an electron pair

### pH, pOH, molarity
- $[.]$ denotes units of molarity
$$pH=-\log[H^+],\qquad pOH=-\log[OH^-]$$
$$[H^+][OH^-]=10^{-14},\qquad pH+pOH=14$$
- sigfigs for log:
	- number of sigfigs in the log argument $\to$ number of sigfigs after the decimal place
	- e.g. $pH=-\log(0.015)=1.82$
- normality requires knowledge of stoichiometric relationship between reactants and products
- normality for an acid:
$$\frac{\text{equivs of $H^+$}}{\text{L of solution}}$$
- normality for a base:
$$\frac{\text{equivs of $OH^-$}}{\text{L of solution}}$$
- in general,
$$N\geq M,\qquad N=xM,\qquad x=1,2,3,\dots$$
### equivalence point vs. end point
- **equivalence point** of an acid
$$N_\text{base}\times V_\text{base}=N_\text{acid}\times V_\text{acid}\qquad\text{OR}\qquad M_\text{base}\times V_\text{base}=M_\text{acid}\times V_\text{acid}$$
- **end point** occurs when the acid-base indicator changes color, does not imply equivalence point
	- we want to choose an indicator that changes color *close* to the equivalence point pH

# (4) equivalent weight
### detergent chemistry
- soap molecule (natural surfactant)
	- has a polar ionic group (hydrophilic) and a large non-polar hydrocarbon group (hydrophobic)
	- the non-polar group will "stick" to grease/oil while the polar group interacts with the aqueous phase
![250](Pasted%20image%2020260313143745.png)
- detergent (synthetic surfactant)
	- modified polar group, does not form insoluble precipitates with calcium and magnesium (found in hard water)
![300](Pasted%20image%2020260313143945.png)

### equivalent weight
- for an acid: weight (grams) of compound containing ONE equivalent of an *acidic proton*
- for a base: weight (grams) of compound containing ONE equivalent of *hydroxide ion*
- related to normality (N), is reaction specific
	- equivalent weight $\le$ molecular weight

# (6) distillation and IMF
- idea of distillation is to separate components by boiling point temperatures
	- lowest bp component should be the first to distill out
	- lower bp = higher vapor pressure
### intermolecular forces
- london forces
- dipole forces
- hydrogen bonding

### raoult's law
- the partial vapor pressure of component $A$ ($P_A$) in the solution is the vapor pressure of *pure* $A$ ($P^0_A$) times its mole-fraction ($X_A$)
$$P_A=P^0_AX_A$$

# (7) chemical kinetics
### rate law
for an overall chemical expression:
$$aA+bB+\dots\xrightarrow{k}\text{products}$$
the general form of the rate law is
$$\text{rate}=k[\text{reactants}]^x\dots=k[A]^m[B]^n\dots$$
- rate has units mole/L s or M/s
- $m$, $n$ are determined experimentally (order of the reactants)
	- overall reaction order is $m+n+\dots$
- $k$ = rate constant (depends on temperature)
	- unit depends on overall reaction order

for an **elementary (single-step) reaction:**
$$aA+bB\longrightarrow\text{products}$$
$$\text{rate}=k[A]^a[B]^b$$
- rate law for a mechanism is dependent on the **rate-determining step**
![500](Pasted%20image%2020260313145955.png)

### method 1: instantaneous initial rates
- hold all initial concentrations fixed except for one
	- then we know change in concentration of one reactant / change in time
![400](Pasted%20image%2020260313150154.png)
comparing trial ratios:
$$\frac{\text{trial \#2 rate}}{\text{trial \#1 rate}}=\frac{k[NO]^x[O_2]^y}{k[NO]^x[O_2]^y}$$
- $[O_2]$ $\times 3$ $\implies$ rate $\times 3$
	- so $O_2$ is 1st order
- $[NO]$ $\times 2$ $\implies$ rate $\times 4$
	- so $NO$ is 2nd order
the final rate law is
$$\text{rate}=k[NO]^2[O_2]$$

### method 2: integrated rate law
- **zero order kinetics:**
	- rate is independent of $[A]$
	- $k=-$ slope, $c=[A]_0$
$$[A]_t=[A]_0-kt$$
$$\text{rate}=-\frac{d[A]}{dt}=k[A]^0=k$$
- **first order kinetics:**
	- $k=-$ slope, $c=\ln[A]_0$
$$\ln[A]_t=-kt+\ln[A]_0$$
$$\text{rate}=-\frac{d[A]}{dt}=k[A]$$
- **second order kinetics:**
	- $k$ = slope, $c=1/[A]_0$
$$\frac{1}{[A]_t}=\frac{1}{[A]_0}+kt$$
$$\text{rate}=-\frac{d[A]}{dt}=k[A]^2$$

# (8) gas chromatography
