```python
from aide_design.play import*
```
#### Christopher Galantino
## Laboratory 3 Laboratory Report


##Objectives

##Procedures

##Results and Discussion

```python
file = pd.read_csv('Lab3AcidRain_bestdata.csv')
array = np.array(file)
V = 4*(u.L)
Q = 267*(u.mL/u.min)
Q = Q.to(u.L/u.s)
theta = V/Q
print(theta)
#theta value was then implemented into the file 'Lab3AcidRain_bestdata.csv' because array could not handle units multiplying

time = array[2:1255,0]
print(time)
pH = array[2:1255,1]

print(pH)
## plotting


plt.figure('ax',(10,8))


plt.plot(restime,pH)
# put in your x and y variables
plt.xlabel('Hydraulic Residence Time', fontsize=15)
plt.ylabel('Absorbance', fontsize=15)
plt.show()
```



##Conclusions

##Suggestions/comments
