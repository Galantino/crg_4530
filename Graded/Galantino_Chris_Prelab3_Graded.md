```python
from aide_design.play import*
```

## Laboratory 3 Pre Lab Question
### Christopher Galantino

<div class="alert alert-block alert-info">
Grade: 1/1
</div>

How many grams of NaHCO3 would be required to keep the ANC levels in a lake above 50 µeq/L for 3 hydraulic residence times given an influent pH of 3.0 and a lake volume of 4 L, if the current lake ANC is 0 µeq/L?

**Answer** 6.751 grams of NaHCO3

```python
time = 45*u.sec
restime = 15*u.sec
num_restimes = time/restime
ANC_out = 50*(u.umol/u.L)
conc_H =  0.001*(u.mol/u.L)
ANC_in = (-1)*conc_H
ANC_o = (ANC_out-ANC_in*(1-np.exp(-num_restimes)))*np.exp(num_restimes)
conc_NaHCO3 = ANC_o
V = 4*u.L
mass_NaHCO3 = conc_NaHCO3*(84.007*(u.g/u.mol))*V
print(mass_NaHCO3.to(u.g))
```
<div class="alert alert-block alert-success">
Good job!
</div>
