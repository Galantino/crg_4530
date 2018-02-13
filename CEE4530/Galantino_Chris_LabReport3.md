```python
from aide_design.play import*
```
#### Christopher Galantino
## Laboratory 3 Laboratory Report
hello

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
# put in your x and y variables
plt.xlabel('Hydraulic Residence Time', fontsize=15)

plt.ylabel('Absorbance', fontsize=15)
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



##Conclusions

##Suggestions/comments
