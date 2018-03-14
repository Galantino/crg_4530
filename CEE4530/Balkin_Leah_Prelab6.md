```python
from aide_design.play import *
```
#Prelab 6
##Christopher Galantino

**(1)** Calculate the mass of sodium sulfite needed to reduce all the dissolved oxygen in 4 L of pure water in equilibrium with the atmosphere and at 30°C.

```python
DO_at_30C = 7.54*u.mg/u.l
mass_Na2SO3perO2 = 7.875*u.mg/u.mg
mass_DO = (4*u.l)*DO_at_30C
mass_req = mass_DO*mass_Na2SO3perO2
print(mass_req)#units are mgNa2SO3
```
**(2)** Describe your expectations for dissolved oxygen concentration as a function of time during a reaeration experiment. Assume you have added enough sodium sulfite to consume all of the oxygen at the start of the experiment. What would the shape of the curve look like?

As the experiment is reaerated I expect the concentration of dissolved oxygen to increase. According to Equation 1.5, the shape of the curve should be a logarithmic curve.

$\ln(\frac{C^{star}-C}{C^{star}-C_{0}})=-k(t-t_{0})$

The change in concentration is equal to the difference between the equilibrium dissolved gas concentration and the dissolved gas concentration.

$\frac{\text{d}C}{\text{d}t}=\widehat{k}(C^{star}-C)$

Therefore, the higher the concentration becomes, the slower the curve will increase

**(3)** Why is , $\widehat{k}$ not zero when the gas flow rate is zero? How can oxygen transfer into the reactor even when no air is pumped into the diffuser?

Although $\widehat{k}$ depends on time, it is a function of the interface surface area (A), the liquid volume (V), the oxygen diffusion coefficient in water (D), and the thickness of the laminar boundary layer (δ) through which the gas must diffuse before the much faster turbulent mixing process can disperse the dissolved gas throughout the reactor. Therefore, $\widehat{k}$ does not depend on Q and is not zero when the gas flow rate is zero. Oxygen can transfer into the reactor at the surface from the air if the reactor is open.

**(4)** Describe your expectations for, $\widehat{k}$ as a function of gas flow rate. Do you expect a straight line? Why?

By inspecting Equation 1.9, $\widehat{k}$ and Q are linearly related.

$MW_{O_{2}}Q_{air}P_{air}f_{O_{2}}(OTE)=\widehat{k_{v,l}}(C^{star}-C)VRT$

Therefore, I expect the curve for \widehat{k} as a function of gas flow rate to be a straight line.

**(5)** A dissolved oxygen probe was placed in a small vial in such a way that the vial was sealed. The water in the vial was sterile. Over a period of several hours the dissolved oxygen concentration gradually decreased to zero. Why? (You need to know how dissolved oxygen probes work to answer this!)

The dissolved oxygen probe applies a voltage that reduces O2 to H2O which decreases DO over time.
