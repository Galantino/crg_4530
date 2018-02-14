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
theta=theta.to(u.sec)
time = array[1:1255,1]*(u.sec)
restime = time/theta
pH = array[1:1255,3]
## plotting
plt.figure()

plt.plot(restime,pH)
plt.xlabel('Hydraulic Residence Time', fontsize=15)

plt.ylabel('pH', fontsize=15)
plt.show()
```

2) In finding ao, a1, and a2 at the given times

```python
K1 = 10**-6.3
K2 = 10**-10.3
Hconc = 10**(-1*pH)
ao = 1/(1+(K1/Hconc)+((K1*K2)/(Hconc**2)))
a1 = 1/((Hconc/K1)+1+(K2/Hconc))
a2 = 1/(((Hconc**2)/(K1*K2))+(Hconc/K2)+1)
```
In graphing 1.21,1.11

```python
Kh = 10**-1.5
P_CO2 = 10**-3.5
Kw = 10**(-14)
ANCo = .001854
ANCin = -(10**(-3))
ANCcons=ANCin*(1-np.exp(restime*(-1)))+ANCo*np.exp(restime*(-1))
cT4 = ANCo/a1

ANCclosed = cT4*(a1+2*a2)+(Kw/Hconc)-Hconc
cT5 = (P_CO2*Kh)/ao
ANCopen = cT5*(a1+2*a2)+(Kw/Hconc)-Hconc

x = restime
y1 = ANCcons
y2 = ANCclosed
y3 = ANCopen

plt.figure('ax',(10,8))
plt.plot(x,y1, '-b', label = 'Conservative ANC')
plt.plot(x, y2, '-r', label = 'Closed ANC')
plt.plot(x, y3, '-g', label = 'Open ANC')
plt.xlabel('Hydraulic Residence Time', fontsize=15)
plt.ylabel('ANCout', fontsize=15)
plt.legend(loc='upper left')
plt.show()
```

```python

cTCons=ANCin*(1-np.exp(restime*(-1)))+ANCo*np.exp(restime*(-1))
plt.figure('ax',(10,8))
plt.plot(x,y1, '-b', label = 'Conservative cT')
plt.xlabel('Hydraulic Residence Time', fontsize=15)
plt.ylabel('cT', fontsize=15)
plt.legend(loc='upper left')
plt.show()

```



##Conclusions

##Suggestions/comments
