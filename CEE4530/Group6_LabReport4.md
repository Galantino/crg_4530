```python
from aide_design.play import*
```
### Group 6 (Ben Gassaway, Anna Lawrence, Christopher Galantino)
## Laboratory 4 Lab Report



##Introduction and Objectives


##Procedures



##Results and Discussion


####1
*Plot measured pH of the lake versus hydraulic residence time (t/theta).*

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
plt.savefig('./Photos/HydraulicResTimevspH.png')
plt.show()
```
####2, 3, and 4

In graphing conservative, closed, and open ANC on the same plot...

```python
K1 = 10**-6.3
K2 = 10**-10.3
Hconc = 10**(-1*pH)
ao = 1/(1+(K1/Hconc)+((K1*K2)/(Hconc**2)))
a1 = 1/((Hconc/K1)+1+(K2/Hconc))
a2 = 1/(((Hconc**2)/(K1*K2))+(Hconc/K2)+1)

Kh = 10**-1.5
P_CO2 = 10**-3.5
Kw = 10**(-14)
ANCo = .001854
ANCin = -(10**(-3))
ANCcons = ANCin*(1-np.exp(restime*(-1)))+ANCo*np.exp(restime*(-1))

cT4 = ANCo
ANCclosed = ANCo*(a1+2*a2)+(Kw/Hconc)-Hconc

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
plt.savefig('./Photos/ANC_plot_Lab4.png')
plt.show()
```
####5
*Analyze the data from the 2nd experiment and graph the data appropriately. What did you learn from the 2nd experiment?*

```python
file = pd.read_csv('Lab3AcidRain_baddata.csv')
array = np.array(file)
V = 4*(u.L)
Q = 267*(u.mL/u.min)
theta = V/Q
theta=theta.to(u.sec)
time = array[1:1223,1]*(u.sec)
restime = time/theta
pH = array[1:1223,2]
## plotting
plt.figure()
plt.plot(restime,pH)

plt.xlabel('Hydraulic Residence Time', fontsize=15)
plt.ylabel('pH', fontsize=15)
plt.show()
```

```python
K1 = 10**-6.3
K2 = 10**-10.3
Hconc = 10**(-1*pH)
ao = 1/(1+(K1/Hconc)+((K1*K2)/(Hconc**2)))
a1 = 1/((Hconc/K1)+1+(K2/Hconc))
a2 = 1/(((Hconc**2)/(K1*K2))+(Hconc/K2)+1)

Kh = 10**-1.5
P_CO2 = 10**-3.5
Kw = 10**(-14)
ANCo = .001854
ANCin = -(10**(-3))
ANCcons=ANCin*(1-np.exp(restime*(-1)))+ANCo*np.exp(restime*(-1))

cT4 = ANCo
ANCclosed = ANCo*(a1+2*a2)+(Kw/Hconc)-Hconc

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
plt.savefig('./Photos/ANC_plot_Lab4.png')
plt.show()
```
Because it wasn't mixed properly, the pH trend did not track as tightly as the effect should have been displayed. This was due to the uneven distribution of the carbonate in the reservoir. The ANC appeared to be buffering the solution well, but after one residence time, pH dropped dramatically.

Furthermore, the ANC is skewed and does not signify the exponential decay. This is a trend that is consistent with our first set of data.  

##Conclusions



##Suggestions/comments
