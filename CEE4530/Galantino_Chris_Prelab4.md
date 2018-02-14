```python
from aide_design.play import*
```

## Laboratory 4 Pre Lab Question
### Christopher Galantino

1)	Compare the ability of Cayuga lake and Wolf pond (an Adirondack lake) to withstand an acid rain runoff event (from snow melt) that results in 20% of the original lake water being replaced by acid rain. The acid rain has a pH of 3.5 and is in equilibrium with the atmosphere. The ANC of Cayuga lake is 1.6 meq/L and the ANC of Wolf Pond is 70 µeq/L. Assume that carbonate species are the primary component of ANC in both lakes, and that they are in equilibrium with the atmosphere. What is the pH of both bodies of water after the acid rain input? Remember that ANC is the conservative parameter (not pH!). Hint: You can use the scipy optimize root finding function called brentq. Scipy can’t handle units so the units must be removed using .magnitude

```python
pH = 3.5
Kw = 10**(-14)
K1_carbonate = 10**(-6.37)
K2_carbonate = 10**(-10.25)
K_Henry_CO2 = 10**(-1.5)
P_CO2 = 10**(-3.5)
def invpH(pH):
  return 10**(-pH)

def alpha0_carbonate(pH):
   alpha0_carbonate = 1/(1+(K1_carbonate/invpH(pH))*(1+(K2_carbonate/invpH(pH))))
   return alpha0_carbonate

def alpha1_carbonate(pH):
  alpha1_carbonate = 1/((invpH(pH)/K1_carbonate) + 1 + (K2_carbonate/invpH(pH)))
  return alpha1_carbonate

def alpha2_carbonate(pH):
  alpha2_carbonate = 1/(1+(invpH(pH)/K2_carbonate)*(1+(invpH(pH)/K1_carbonate)))
  return alpha2_carbonate
def ANC_closed(pH,Total_Carbonates):
  return Total_Carbonates*(alpha1_carbonate(pH)+2*alpha2_carbonate(pH)) + Kw/invpH(pH) - invpH(pH)

def ANC_open(pH):
  return ANC_closed(pH,P_CO2*K_Henry_CO2/alpha0_carbonate(pH))

ANCin = -10**(-pH)
restime = .2

ANC_cayuga = 1.6*(10**-3)
ANC_wolf = 70*(10**-6)

ANC_cayuga_after= ANCin*(1-np.exp(-restime))+ANC_cayuga*np.exp(-restime)
print(ANC_cayuga_after)
ANC_wolf_after=ANCin*(1-np.exp(-restime))+ANC_wolf*np.exp(-restime)
print(ANC_wolf_after)

import scipy
from scipy import optimize

def ANC_open_unitless(pH):
  return (ANC_open(pH)-ANC_cayuga_after)

def pH_open():
    return optimize.brentq(ANC_open_unitless, 1, 12)
print('The pH of Cayuga after the rainfall is',pH_open())

def ANC_open_unitless(pH):
  return (ANC_open(pH)-ANC_wolf_after)

def pH_open():
      return optimize.brentq(ANC_open_unitless, 1, 12)
print('The pH of Wolf after the rainfall is',pH_open())
```

2) What is the ANC of a water sample containing only carbonates and a strong acid that is at pH 3.2? This requires that you inspect all of the species in the ANC equation and determine which species are important.

```python
pH = 3.2
concH = 10**(-pH)
ANC = -concH
print('The ANC of water sample is',ANC)
```
3) [H+] is not a conserved species because the pH of the water is not low enough to stabilize the [H+] as an independent species in solution. The H+ will continue to possess reactibility as it transforms between different species as carbonic acid, bicarbonate, and free-floating protons. Once the pH decreases low enough and the solution becomes more acidic, the [H+] will remain in solution as protons without undergoing any reversible reactions.
