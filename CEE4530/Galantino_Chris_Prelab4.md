```python
from aide_design.play import*
```

## Laboratory 4 Pre Lab Question
### Christopher Galantino

1)	Compare the ability of Cayuga lake and Wolf pond (an Adirondack lake) to withstand an acid rain runoff event (from snow melt) that results in 20% of the original lake water being replaced by acid rain. The acid rain has a pH of 3.5 and is in equilibrium with the atmosphere. The ANC of Cayuga lake is 1.6 meq/L and the ANC of Wolf Pond is 70 µeq/L. Assume that carbonate species are the primary component of ANC in both lakes, and that they are in equilibrium with the atmosphere. What is the pH of both bodies of water after the acid rain input? Remember that ANC is the conservative parameter (not pH!). Hint: You can use the scipy optimize root finding function called brentq. Scipy can’t handle units so the units must be removed using .magnitude

```python
pHrain = 3.5
ANCin = -10**(-pHrain)
restime = .2

ANC_cayuga = 1.6*(10**-3)
ANC_wolf = 70*(10**-6)

ANC_cayuga_after= ANCin*(1-np.exp(-restime))+ANC_cayuga*np.exp(-restime)
print(ANC_cayuga_after)
ANC_wolf_after=ANCin*(1-np.exp(-restime))+ANC_wolf*np.exp(-restime)
print(ANC_wolf_after)
```

2) What is the ANC of a water sample containing only carbonates and a strong acid that is at pH 3.2? This requires that you inspect all of the species in the ANC equation and determine which species are important.

```python
pH = 3.2
concH = 10**(-pH)
ANC = -concH
print('The ANC of water sample is',ANC)
```
3) Bitch
