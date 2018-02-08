```python
from aide_design.play import*
```
## Laboratory 1 Pre Lab Questions
### Christopher Galantino

1. Why are contact lenses hazardous in the laboratory?

Contact lenses are hazardous in the lab
because they may hold chemical vapors, prevent the removal of
foreign material, and prove difficult to remove in a splashing incident.

2. What is the minimum information needed on the label for each chemical? When are Right-To-Know labels required?

The minimum information needed on the label for each chemical is the full
chemical name, concentration, and date prepared. Right-To-Know labels are required
if a chemical is deemed as a hazardous material by the definition provided by OSHA.

3. Why is it important to label a bottle even if it only contains distilled water?


It is important to label a bottle even if it contains just distilled water
because it adds a sense of mystery for those who don't know it's distilled water.
This leads to disposal issues and unwanted stress.

4. Find an SDS for sodium nitrate.

a. Who created the SDS?

ScienceLab.com created this SDS

b. What is the solubility of sodium nitrate in water?

The solubility of sodium nitrate in water is 92.1 g/100 ml @ 25 deg C or 180 g/100 ml @ 100 deg C

c. Is sodium nitrate carcinogenic?

 Sodium nitrate is NOT carcinogenic

d. What is the LD50 oral rat?

The LD50 oral rat is 1267 mg/kg.

e. How much sodium nitrate would you have to ingest to give a 50% chance of death (estimate from available LD50 data).

```python
mymass = 86*u.kg
LD50 = 1267*u.mg/u.kg
amount = mymass*LD50
print(amount.to(u.mg))
```

f. How much of a 1 M solution would you have to ingest to give a 50% chance of death?


```python
Weight = 84.9947*u.g/u.mol
sol_Conc = 1*u.mol/u.l
req_Vol = amount/(sol_Conc*Weight)
print(req_Vol.to(u.l))
```
g. Are there any chronic effects of exposure to sodium nitrate?

As for chronic effects, the substance may be toxic to blood. Repeated or prolonged exposure to the substance can produce organ damage.

5. You are in the laboratory preparing chemical solutions for an experiment and it is lunchtime. You decide to go to CTB to eat. What must you do before leaving the laboratory?

First, make sure all your chemicals are properly labeled. Ensure that your lab space is cleared and your hands are thoroughly washed. If you have an experiment running, let someone in the lab know you'll be doing so.
