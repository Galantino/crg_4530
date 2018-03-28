```python
from aide_design.play import*
import Environmental_Processes_Analysis as EPA
import importlib
importlib.reload(EPA)
import scipy
from scipy import special
from scipy import stats
from scipy.optimize import curve_fit
import collections
```
# Lab 6 Report
## Chris Galantino, Ben Gassaway, Anna Lawrence
## Gas Transfer Laboratory

## Equations to be used throughout the intro/procedure

$$ln\frac{C^{\star}-C}{C^{\star}-C_{0}} = -\hat{k_{v,l}}(t - t_{0})$$

^can be evaluated using linear regression so that   is the slope of the line.

$$OTE = \frac{\dot{n}_{aq, O_2}}{f_{O_2}\dot{n}_{air}} = \frac{V\hat{k}_{v,l}C^{\star}-C}{f_{O_2}\dot{n}_{air}MW_{O_2}}$$

^ Describes the molar airflow rate is controlled then OTE is based on the ratio of the molar transfer rate of supplied oxygen.

$${C_{eq}} = {P_{{O_2}}}\mathop e\nolimits^{\left( {\frac{{1727}}{T} - 2.105} \right)} $$

$$\ln \frac{{{C_{eq}} - C}}{{{C_{eq}} - {C_0}}} =  - {\hat k_{v,l}}(t - {t_0})$$

## Introduction and Objectives

Gas transfer is a vital unit operation in many environmental engineering processes.  It involves either the desorption or adsorption of gas. The transfer of oxygen to liquid systems is particularly important in oxidation of iron and manganese in water treatment and in the biological treatment of wastewaters. Air stripping to remove toxic volatile organics is another wastewater application. Aeration systems are designed to promote turbulence and break the water into smaller volumes of droplets, increasing the surface area for mass transfer.  Gravity or pressurized flow systems are typically used. Gas transfer means simply the process of allowing any gas to dissolve in a fluid or the opposite of that, promoting the release of a dissolved gas from a fluid.  The gas transfer rate can be modeled as the product of a driving force (the difference between the equilibrium concentration and the actual concentration) and an overall volumetric gas transfer coefficient (a function of the geometry, mixing levels of the system and the solubility of the compound). In a system where air is forced through a tube and a porous diffuser, creating very small bubbles that rise through clean water, the transfer of oxygen takes place through the bubble gas-liquid interface.  If the gas inside the bubble is air, and an oxygen deficit exists in the water, the oxygen transfers from the bubble into the water.  Most gases are only slightly soluble in water; among these are hydrogen, oxygen and nitrogen.  Solubility is influenced by many variables such as the presence of impurities and temperature. Technology has been advanced to augment gas transfer, such as aeration diffusers, packed tower air stripping, and membrane stripping. Each of these technologies creates a high interface surface area to improve gas transfer.


## Procedures


## Results and Discussion


#### Air flow testing
The team moved forward with calculating the flow rate of air from testing the air flow controller. The desired flow rate needed to be 200 uM/s. After calibration, the team tested this flow rate to make sure the numbers were within 10% error.

```python
data_file_path = 'C:\\Users\\en-ce-4530\\github\\crg_4530\\initial_setup200u.xls'
firstrow = 1
time_data = EPA.ftime(data_file_path,firstrow,-1)
pressure_data = EPA.Column_of_data(data_file_path,firstrow,-1,1,'Pa')
plt.plot(time_data.to(u.sec), pressure_data.to(u.Pa),'r')
plt.xlabel(r'$time (sec)$')
plt.ylabel(r'Pressure $\left ({Pa} \right )$')
plt.legend(['Pressure Flow'])
#plt.savefig('C:\\Users\\en-ce-4530\\github\\crg_4530\\Photos\\AirFlowTest.png')
plt.show()
```

Flow rate then needed to be converted from Pa/s to uM/s. This can be done through the Ideal Gas Law. The slope of the best fit line was found to be 539.9 Pa/s. The R constant used was 8.31446 Pa*m^3/K*mol and the volume (V) is 1 L (this was the size of our accumulator). Temperature (T) of the water is 22 C (295 K).

```python
Pflow = 539.9*u.Pa/u.sec
T = 295*u.K
R = 8.31446*((u.Pa*u.m**3)/(u.K*u.mol))
V = 1*u.L
nflow = Pflow*V/(R*T)
nflow.to(u.umol/u.sec)
>>>nflow = 220.118 umol/sec
```
After applying PV = nRT, our experimental molar flow was found to be 220.118 uM/s, which has a percent error of about 10%. From here, we made the airslope of 7.644765M as a constant on ProCoDA.

#### Introducing the data

The team then plots the data of the different flow rates and how they are related to oxygen concentration.

```python
DO_column = 2
filepaths, airflows, DO_data, time_data = EPA.aeration_data(DO_column)

airflows
filepaths
for i in range(airflows.size):
  plt.plot(time_data[i], DO_data[i],'o')

plt.xlabel(r'$time (s)$')
plt.ylabel(r'Oxygen concentration $\left ( \frac{mg}{L} \right )$')
plt.legend(airflows.magnitude)
#plt.savefig('images/aerationdata.png')
plt.show()
```
**Note** We eliminated the 200uM/s flow rate data because something seems to have gone horribly wrong with the data acquisition process. It also appears that the 2000 uM/s does not seem to be calibrated, but we will move forward with this data since it isn't too bad.

The team then proceeded to determine what the experimental saturated DO was using the relationship defined in the Introduction.

```python
Temperature=22*u.degC
Pressure_air = 1*u.atm
O2_sat = EPA.O2_sat(Pressure_air,Temperature)
O2_sat
part_press_ox = 0.21
T = 293
C_star = part_press_ox*np.exp((1727/T)-2.105)
print (C_star)
```
From here, the team wished to know the gas transfer coefficient for each respective data set. The gas transfer coefficient will increase with the interface area and the diffusion coefficient and will decrease with the reactor volume and the thickness of the boundary layer.

```python
Co_array = [0.510,0.509,0.5360,0.511]
dataset = np.array(DO_data)

C20 =np.array(dataset[0])
C110 =np.array(dataset[1])
C1100 =np.array(dataset[2])
C2000 =np.array(dataset[3])
C_array = [C20,C110,C1100,C2000]
#c = [c0[0:219],c1[69:307],c2,c3[109:185],c4[0:54],c5[0:47]]
time = np.array(time_data)
t20 =np.array(time[0])
t110 =np.array(time[1])
t1100 =np.array(time[2])
t2000 =np.array(time[3])

t_array = [t20,t110,t1100,t2000]
C_calculated = [0,0,0,0]
for i in range(4):
  C_calculated[i] = np.log((O2_sat.magnitude-C_array[i])/(O2_sat.magnitude-Co_array[i]))
lindata = [0,0,0,0]
k=[0,0,0,0]
for j in range(4):
  lindata = stats.linregress(-t_array[j],C_calculated[j])
  k[j] = lindata[0]
k=np.array(k)
print (k)
```
It is clear that as the air flow rate increased, there was an increase in the gas transfer coefficient.

This is because

[EXPLAIN HERE]




### Conclusions



### Suggestions/Comments



### Code

1. Calculate the air flow rate from testing the air flow controller and compare with the target value.
2. Eliminate the data from each data set when the dissolved oxygen concentration was less than 0.5 mg/L. This will ensure that all of the sulfite has reacted.

3. Plot a representative data set showing dissolved oxygen vs. time.
4. Calculate   based on the average water temperature, barometric pressure, and the following equation.  $C^{\star}=P_{O_{2}}e^{\frac{1727}{T}-2.105}$ where T is in Kelvin, $P_{O_{2}}$  is the partial pressure of oxygen in atmospheres, and $C^{\star}$ is in mg/L. This equation is valid for 278 K<T<318 K.
5. Estimate $\hat{k}_{v,l}$ using linear regression and equation 1.5 for each data set.
6. Create a graph with a representative plot showing the linearized data,  $ln\frac{C^{\star}-C}{C^{\star}-C_{0}}$ vs. time, and the best-fit line.
7. Plot the reaeration model on the same graph as the dissolved oxygen vs. time data.  This is done by solving equation for C.
8. Plot $\hat{k}_{v,l}$ as a function of airflow rate (μmole/s).
9. Look at each dataset and if necessary (to make more linear plots) eliminate more data from the beginning (or end) of the dataset. You will be able to see when the oxygen level is affected by residual sulfite at the beginning of the experiments.
10. Plot OTE as a function of airflow rate (μmole/s) with the oxygen deficit $(C^{\star}-C)$ set at 6 mg/L.
11. Plot the molar rate of oxygen dissolution into the aqueous phase (μmole/s) as a function of airflow rate (μmole/s).
12. Comment on results and compare with your expectations and with theory.
13. Verify that your report and graphs meet the requirements.






After eliminating the data from each data set where the dissolved oxygen concentration was less than 0.5 mg/L, the results could ensure that all of the sulfite had been completely reacted.

```python


Below is a graphical depiction in which dissolved oxygen is plotted against time.




Below is a representative plot showing the linearized data from $\ln \frac{{{C_{eq}} - C}}{{{C_{eq}} - {C_0}}} against time, and depicting the best-fit line

```python
#6
for p in range(6):
  plt.plot(t[p],y[p])

plt.xlabel(r'$time (s)$')
plt.ylabel(r'Linearized Oxygen conc. $\left ( \frac{mg}{L} \right )$')
plt.legend(airflows.magnitude)
for p in range(6):
  plt.plot(t[p],-t[p]*k[p],"--", color='#808080', label="Best Fit")
plt.show()
```

```python
#7
c_model=[]
for i in range(6):
  val = np.zeros(len(t[i]))
  for j in range(len(t[i])):
    val[j] = (O2_sat.magnitude-((O2_sat.magnitude-co0[i])*(10**(-k[i]*t[i][j]))))
  c_model.insert(i,val)
print (c_model)
```
