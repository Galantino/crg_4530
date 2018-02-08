```python
from aide_design.play import*
```
## Laboratory 2 Pre Lab Questions
### Christopher Galantino

###1.

I chose Zinc Nitrate Zn(NO3)2 which has a molecular weight of 189.36 g/mol and zinc has a molecular weight of 65.38 g/mol. Knowing that I need 100 mL of 1 uM Zinc solution, I need to see how many grams of zinc per liter this 1 uM solution will need to contain. I multiply the molecular weight by 1 uM and get the following:

```python
weightZinc = 65.38*u.g/u.mol
sol_Goal = 1*u.umol/u.l
massPerLiter = weightZinc*sol_Goal
print(massPerLiter.to(u.g/u.L))

```
Then I see how much zinc is present in 100 mL of this solution and therefore its moles:

```Python
mass = massPerLiter*100*u.mL
moleZinc = mass/weightZinc
print(moleZinc.to(u.mol))
```
From here I wished to see the smallest amount of volume I could add of an unknown stock solution to obtain this many moles in 100 mL. I chose 10 uL since that's the smallest volume we can use:

```Python
Conc = moleZinc/(10*u.uL)
print(Conc.to(u.mol/u.l))
```

I then see how much Zinc Nitrate needs to be added to 1 liter of water to get this stock concentration:

```python
weightZN = 189.36*(u.g/u.mol)
massToAdd = Conc*weightZN
print(massToAdd.to(u.g/u.l))
```
####Procedure
Therefore, 1.894 grams of zinc nitrate shall be added to 1 L of distilled water. This is the stock solution. Ensure a good mixing period. From there, 10 uL will be removed using a pipette and added to a 100 mL graduated cylinder. Then, this will be diluted with distilled water until the volume in the flask is 100 mL, giving the appropriate concentration of 1 micro molar zinc solution.

###2.

The density of sodium chloride solutions as a function of concentration is approximately 0.6985C + 998.29 kg/m^3. Refer to the following math:

```Python
molweight = 58.4*(u.g/u.mol)
molConc = 1*(u.mol/u.l)
Conc = molweight*molConc
density=(0.6985*Conc.to(u.kg/u.m**3))+998.29*(u.kg/u.m**3)
print(density)
```
So the density of a 1 M solution of sodium chloride is 1039 kg/m^3.
