```python
from aide_design.play import*
```
#### Christopher Galantino
## Laboratory 3 Laboratory Report

##Objectives

##Procedures

##Results and Discussion
**NOTE** We should not keep these in list form. They should be fluid with the final Report

1) In creating the graph of restime (t/theta) versus pH

```python
file = pd.read_csv('Lab3AcidRain_bestdata.csv')
array = np.array(file)
V = 4*(u.L)
Q = 267*(u.mL/u.min)
theta = V/Q
print(theta.to(u.sec))
#theta value was then implemented into the file itself 'Lab3AcidRain_bestdata.csv' because array could not handle units multiplying
restime = array[2:1255,2]
pH = array[2:1255,3]
## plotting
plt.figure('ax',(10,8))
plt.plot(restime,pH)
plt.xlabel('Hydraulic Residence Time', fontsize=15)
plt.ylabel('pH', fontsize=15)
plt.show()
```

2) In finding ao, a1, and a2 at the given times

```python
K1 = 10**-6.3
K2 = 10**-10.3
Hconc = 10**(-pH)
ao = 1/(1+(K1/Hconc)+((K1*K2)/(Hconc**2)))
a1 = 1/((Hconc/K1)+1+(K2/Hconc))
a2 = 1/(((Hconc**2)/(K1*K2))+(Hconc/K2)+1)
```
In graphing 1.21,1.11

```python

#what is cT for the case of 1.11?
cT =
Kw = 10**(-14)

ANCo = 1.854*(u.mmol/u.L)  #is this right?
ANCin = (10**-3)*(u.mol/u.L)  #is this right?
print(restime)
ANCcons = ANCin*(1-np.exp(restime*(-1)))+ANCo*np.exp(restime*(-1))
ANCclosed = cT*(a1+2*a2)+(Kw/Hconc)-Hconc
#NEEDS TO BE IN APPROPRIATE units! ^^

x = restime
y1 = ANCcons
y2 = ANCclosed

plt.figure('ax',(10,8))
plt.plot(x,y1, '-b', label = 'Conservative ANC')

plt.plot(x, y2, '-r', label = 'Closed ANC')
plt.xlabel('Hydraulic Residence Time', fontsize=15)
plt.ylabel('ANCout', fontsize=15)
plt.legend(loc='upper left')
plt.show()
```




##Conclusions

##Suggestions/comments
