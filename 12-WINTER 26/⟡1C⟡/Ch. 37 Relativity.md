# invariance of physical laws, simultaneity
- speed of light in vacuum is the same in all inertial frames, and is independent of the motion of the source
- simultaneity is not an absolute concept: events that are simultaneous in one frame are not necessary simultaneous in a second frame moving relative to the first
# time dilation
- if two events occur at the same space point in a particular reference frame, the time interval $\Delta t_0$ between the events measured in that frame is the **proper time interval**
- if this frame moves with constant velocity $u$ relative to a second frame, the time interval $\Delta t$ between the events as observed in the second frame is **longer** than $\Delta t_0$
$$\Delta t=\frac{\Delta t_0}{\sqrt{1-u^2/c^2}}=\gamma\Delta t_0$$
$$\gamma=\frac{1}{\sqrt{1-u^2/c^2}}$$

![300](../pasted_images/Pasted%20image%2020260308011302.png)

# length contraction
- if two points are at rest in a particular reference frame, the distance $l_0$ between the points in that frame is the **proper length**
- if this frame moves with constant velocity $u$ relative to a second frame and the distances are measured parallel to the motion, the distance $l$ between the points in the second frame is shorter than $l_0$
$$l=l_0\sqrt{1-u^2/c^2}=\frac{l_0}{\gamma}$$
![300](../pasted_images/Pasted%20image%2020260308011431.png)

# lorentz transformations
- the Lorentz coordinate transformations relate the coordinates and time of an event in an inertial frame $S$ to those of the same event observed in a second inertial frame $S'$ moving at relative velocity $u$
$$x'=\frac{x-ut}{\sqrt{1-u^2/c^2}}=\gamma(x-ut)$$
$$y'=y,\qquad z'=z$$
$$t'=\frac{t-ux/c^2}{\sqrt{1-u^2/c^2}}=\gamma(t-ux/c^2)$$
$$v_x'=\frac{v_x-u}{1-uv_x/c^2}$$
$$v_x=\frac{v_x'+u}{1+uv'_x/c^2}$$
![300](../pasted_images/Pasted%20image%2020260308011617.png)

# doppler effect for electromagnetic waves
- for a source moving toward observer with speed $u$, the received frequency (in terms of emitted frequency $f_0$) is
$$f=\sqrt{\frac{c+u}{c-u}}f_0$$
![300](../pasted_images/Pasted%20image%2020260308011656.png)

Fractional frequency shift for a **reflected wave**
$$\frac{\Delta f}{f_0}=\frac{2v}{c}$$
# relativistic momentum and energy
- for a particle of rest mass $m$ moving with velocity $\vec v$, the relativistic momentum $\vec p$ is given by
$$\vec p=\frac{m\vec v}{\sqrt{1-v^2/c^2}}=\gamma m\vec v$$
- and the relativistic kinetic energy $K$ is given by
$$K=\frac{mc^2}{\sqrt{1-v^2/c^2}}-mc^2=(\gamma-1)mc^2$$
- $mc^2$ = rest energy, $m$ = rest mass of particle
- total energy $E$ is the sum of $K$ and rest energy $mc^2$
	- can also be expressed in terms of $p$ and $m$:
$$E=K+mc^2=\frac{mc^2}{\sqrt{1-v^2/c^2}}=\gamma mc^2$$
$$E^2=(mc^2)^2+(pc)^2$$
![200](../pasted_images/Pasted%20image%2020260308011912.png)

# approximations
- with $u=(1-\Delta)c$, since $\Delta\ll 1$, $(1-\Delta)^2\approx 1-2\Delta$ so
$$\gamma=\frac{1}{1-(1-\Delta)^2}\approx \frac{1}{\sqrt{2\Delta}}$$
- with $u\ll c$,
$$\sqrt{1-\frac{v^2}{c^2}}\approx 1-\frac{v^2}{2c^2}$$

****
**Lorentz Tranformation**
$K\to K'$ moving at $u$
$t'=\gamma(t-\frac{ux}{c^2})$
$x'=\gamma(x-ut)$

**Velocity addition**
$K\to K'$
$$v_x'=\frac{v_x-u}{1-\frac{v_xu}{c^2}}$$
- $v_x'$ = total velocity
- $v_x$ =reference frame velocity
- $u$ = object velocity
**Doppler shift**
$$f=\sqrt{\frac{c+v}{c-v}}f_0$$
$\lambda$ decreases, $f$ increases

**Relativistic kinetics**
$E_\text{rest}=mc^2$
$E_\text{tot}=\gamma mc^2$
$K=E_\text{tot}-E_\text{rest}=(\gamma-1)mc^2\to \frac{1}{2}mv^2$ (when $v<<c$) 
$\vec p=\gamma m\vec v$
$E_\text{tot}^2=(mc^2)^2+(pc)^2$

