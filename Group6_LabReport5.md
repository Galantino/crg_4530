```python
from aide_design.play import*
import Environmental_Processes_Analysis as EPA
import importlib
importlib.reload(EPA)
import scipy
from scipy import special
from scipy.optimize import curve_fit
import collections
```

### Group 6 (Ben Gassaway, Christopher Galantino, Anna Lawrence)
## Laboratory 5 Lab Report

###Equations to be added throughout the report
$E_{(t)} = \frac{C_{t}V_{r}}{C_{tr}V_{tr}} = e^{(-t/\theta)}$

$Pe = \frac{UL}{D_{d}}$

$t^{\star} = \frac{tU}{L}$

$E_{N_{(t^{\star})}} = \frac{N^{N}}{(N-1)!}(t^{\star})^{N-1}e^{(-Nt^{\star})}$

$d_{orifice} = \sqrt{\frac{4Q_{reactor}}{\pi n_{orifice}K_{orifice}\sqrt{2g\Delta h}}}$

integral formula for finding F using E

$$\int_{0}^{t^{\star}} E_{(t^{\star})dt^{\star}}$$

### Introduction and Objectives
In order to test specific natural or engineered processes, reactors can be set up to simulate these chemical, biological, and physical processes and provide insight as to how a certain system would act in different scenarios. Specifically, a reactor can be described as a boundary, literally or figuratively, that physically controls the processes under specific constraints. One gets to decide what they want their system to be, where they want their boundaries to be, what inputs will go into the system, and what is to be measured. Reactors give the user more control over chemical, biological and physical reactions, including temperature control of the vessel contents, measurement of parameters such as pH or pressure, and mixing and dispersing applications. There are a number of different types of reactors, including stirred, high-pressure, and mini reactors. Continuous flow tubular reactors can be externally heated or jacketed with a circulating fluid. Although many different types of reactors, all of these reactors fall under three categories, CMFR (completely mixed flow reactor), PFR (plug-flow reactor) or Batch Reactor. CMFRs are control volumes for which spatially uniform properties may be assumed. They are also reactors with flow, are completely mixed and can attain steady state. Some examples include a room in a building or a small pond. A batch reactor varies from a CMFR for it has no flow. Material is added, mixed, given time for reaction to occur, but then the reactor is drained. Steady state is not attained. PFR, or plug flow reactors, has flow, however, there is no mixing in lateral direction. Properties may vary through the PFR. When modeling a PFR, it is important that it is split into a series of sequential control volumes. The plug flow reactor is an idealized extreme not attainable in practice. All real reactors fall under the category of Batch or CMFR.

### Procedure:
Day 1: Calibration and Set-Up (CMFR)
Our goal was to perform a mass balance on red dye through a reactor of length 30 cm and width 15 cm. We limited our depth to a maximum of 5 cm and used a container with a volume of 4L. We also set our pumping rate to 380 mL/min, giving us a residence time of approximately 6 minutes. Once our reactor was set up to the pump with the correct pipes leading to the influent and effluent, we added tracer directly into the first chamber of our reactor. The red dye allowed us to qualitatively observe the advection and dispersion in the reactors. We calculated our data using ProCoDA II software and a photometer. To calibrate the photometer, our objective was to have a total volume of 1 L circulating through the reactor system. We connected the pump, a 1 L bottle, and the vertically positioned photometer in a closed loop with one another via 18” pipes. 1 L of tap water was added to the bottle and the pump was turned on to 380 mL/min. We set our voltage to 5V on ProCoDA II and confirmed that it was reading values between -1.3V when the light in the photometer is off and +3.5V when it is on. Using a 40 g/L stock solution of Red Dye, we made our calibration curve for our photometer by calculating the volume of red dye that will be needed to generate a calibration with points at 0, 1, 2, 5, 10, 20, 30, 40, and 50 mg/L. The first calibration point, 0 mg/L, was used as our standard and was a record of our voltage prior to adding any red dye. We then added red dye to make the concentration of the reactor 1mg/L and continued to add dye until and recorded all of the standards have been read and formed a linear plot. Once we finished our calibration, we set up a CMFR reactor for our experiment. We connected a pump from a 20L Jerrican filled with tap water to the influent of your reactor and placed our reactor on a stir plate. We connected a 3/8” push-connect fitting is on the effluent side of your reactor and connected the effluent to the drain through a short tube. A second pump head was set up to pull a sample from weir through the photometer and then to the drain. We confirmed our system worked by running the pump at 380 rev/min to check to see if our ProCoDA software was reading a stable voltage of about +3.5V and checking that the volume in the remained constant. For each test, we wanted to measure the reactor volume, residual reactor red dye concentration, and the flow rate. We added a volume of red dye #40 stock until the maximum concentration of the tracer was about 30 mg/L near the influent of the reactor. We calculated data until the majority of the tracer has exited the reactor. Once we terminated the experiment, we poured the contents of the reactor into a container and weighted it to determine the exact volume of the reactor. We used this information to obtain the average concentration in the reactor and to further perform a mass balance on the red dye.

Day 2: Baffles
The ideal CMFR model assumes that the fluid in the reactor is perfectly mixed and that there are no concentration gradients inside the reactor. However, in a real-world stirred tank reactor, there most likely will not be perfect mixing and will be concentration gradients present. Baffles contribute additional disturbance to the flow created by the mixer, and provide more effective mixing. We used the set up from the prior week to continue with this part of the lab. For this part if the experiment, we included baffles in order to bring our reactor closer to the ideal of perfect mixing in each of the baffle zones. We also experimented with baffles with different sized pores to achieve mixing within zones. Our objective was to determine the diameter and spacing of the pores required to achieve adequate mixing by measuring the Peclet number. An additional constraint regarding pore design that we took into consideration is that the head loss through the pores does not get too excessive. We tested 3 different baffle designs:
1.     No holes
2.     Small holes on the first baffle but no holes on the second baffle
3.     Small holes on both baffles
We dropped red dye into the first section of the reactor and calculated the concentration of the red dye at the effluent using ProCoDA software.  

Day 3: Coiling
We used full coil tubing connected on one end to a pump and a Jerrican filled with tap water and on the other end an effluent tube. In order to determine concentration of the red dye, we first needed to measure the volume of the tubes. We measured the tube absent of anything as 1240g and then filled with water as 2015g. These values were used to calculate the mass of the water inside the tubing, 775g. This corresponds to a volume of 775 mL. Since the diameter of the tube was 3/8 inch tubing, dividing the volume by the cross sectional area gives us a length of 35.7 feet. One our system was set up, we added a pulse of .05 mL (20mg/L) of 100g/L red dye into the coiled tube (pump running at 380 rev/min pump).

### Results and Discussion

The first experiment was a simple CMFR setup in order to serve as our constant. There were no baffles installed and an added pulse was able to slowly dissipate until the dye experienced a full residence time.

We used multivariable nonlinear regression to obtain the best fit between experimental data and the appropriate model. These functions, either an CMFR solver and/or an Advective-Dispersion (AD) solver will minimize the error by varying average residence time, (mass of tracer/reactor volume), and either the number of CMFR in series or a Peclet number.

The first experiment only utilized the CMFR model.


```python
data_file_path = 'C:\\Users\\en-ce-4530\\github\\crg_4530\\Lab5Part2(CMFR_Final).xls'
print(EPA.notes(data_file_path))

#I eliminate the beginning of the data file because this is a CMFR and the first data was taken before the dye reached the sensor.
firstrow = 36
time_data = EPA.ftime(data_file_path,firstrow,-1)
concentration_data = EPA.Column_of_data(data_file_path,firstrow,-1,1,'mg/L')
V_CMFR = 4*u.L
Q_CMFR = 380 * u.mL/u.min
theta_guess = (V_CMFR/Q_CMFR).to(u.s)
C_bar_guess = np.max(concentration_data)
#The Solver_CMFR_N will return the initial tracer concentration, residence time, and number of reactors in series.
#This experiment was for a single reactor and so we expect N to be 1!
CMFR = EPA.Solver_CMFR_N(time_data, concentration_data, theta_guess, C_bar_guess)
#use dot notation to get the 3 elements of the tuple that are in CMFR
CMFR.C_bar
CMFR.N
CMFR.theta
#create a model curve given the curve fit parameters.
CMFR_model = CMFR.C_bar * EPA.E_CMFR_N(time_data/CMFR.theta,CMFR.N)

plt.plot(time_data.to(u.min), concentration_data.to(u.mg/u.L),'r')
plt.plot(time_data.to(u.min), CMFR_model,'b')

plt.xlabel(r'$time (min)$')
plt.ylabel(r'Concentration $\left ( \frac{mg}{L} \right )$')
plt.legend(['Measured dye','CMFR Model'])
#plt.savefig('C:\\Users\\en-ce-4530\\github\\crg_4530\\Photos\\reactorplotCMFR.png')
plt.show()
```
![CMFR](https://github.com/Galantino/crg_4530/blob/master/Photos/reactorplotCMFR.png?raw=true)

In order to observe the effects of a set of baffles, specifically Experiment 1 with no holes, the same analysis was performed as before but both the CMFR and AD fit were applied to the measured dye concentration.

```python
data_file_path1 = 'C:\\Users\\en-ce-4530\\github\\crg_4530\\Baffle1.txt'
data_file_path1
#time initiates at pulse addition
start = 367
pd.read_csv(data_file_path1,delimiter='\t')
time_data1 = EPA.ftime(data_file_path1,start,-1)
concentration_data = EPA.Column_of_data(data_file_path1,start,-1,1,'mole/L')
V_CMFR = 4*u.L
Q_CMFR = 380 * u.mL/u.min
theta_guess = (V_CMFR/Q_CMFR).to(u.s)
C_bar_guess = np.max(concentration_data)
CMFR1 = EPA.Solver_CMFR_N(time_data1, concentration_data, theta_guess, C_bar_guess)
CMFR1.C_bar
CMFR1.N
CMFR1.theta.to(u.min)
CMFR1_model = (CMFR1.C_bar*EPA.E_CMFR_N(time_data1/CMFR1.theta, CMFR1.N)).to(u.mole/u.L)
#use solver to get the advection dispersion parameters
AD1 = EPA.Solver_AD_Pe(time_data1, concentration_data, theta_guess, C_bar_guess)
AD1.C_bar
AD1.Pe
AD1.theta.to(u.min)
#Created the advection dispersion model curve based on the solver parameters
AD1_model = (AD1.C_bar*EPA.E_Advective_Dispersion((time_data1/AD1.theta).to_base_units(), AD1.Pe)).to(u.mole/u.L)
plt.plot(time_data1.to(u.min), concentration_data.to(u.mole/u.L),'-')
plt.plot(time_data1.to(u.min), CMFR1_model,'b')
plt.plot(time_data1.to(u.min), AD1_model,'g')
plt.xlabel(r'$time (min)$')
plt.ylabel(r'Concentration $\left ( \frac{mg}{L} \right )$')
plt.legend(['Measured dye','CMFR Model', 'AD Model'])
#plt.savefig('C:\\Users\\en-ce-4530\\github\\crg_4530\\Photos\\reactorplot1.png')
plt.show()
```
![Exp1](https://github.com/Galantino/crg_4530/blob/master/Photos/reactorplot1.png?raw=true)

The next set of baffles were then installed (Experiment 2) with the CMFR and AD models fitting the measured data.

```python
data_file_path2 = 'C:\\Users\\en-ce-4530\\github\\crg_4530\\Baffle2.txt'
#time initiates at pulse addition
start = 18
time_data2 = EPA.ftime(data_file_path2,start,-1)
concentration_data = EPA.Column_of_data(data_file_path2,start,-1,1,'mole/L')
V_CMFR = 4*u.L
Q_CMFR = 380 * u.mL/u.min
theta_guess = (V_CMFR/Q_CMFR).to(u.s)
C_bar_guess = np.max(concentration_data)
CMFR2 = EPA.Solver_CMFR_N(time_data2, concentration_data, theta_guess, C_bar_guess)
CMFR2.C_bar
CMFR2.N
CMFR2.theta.to(u.min)
CMFR2_model = (CMFR2.C_bar*EPA.E_CMFR_N(time_data2/CMFR2.theta, CMFR2.N)).to(u.mole/u.L)
#use solver to get the advection dispersion parameters
AD2 = EPA.Solver_AD_Pe(time_data2, concentration_data, theta_guess, C_bar_guess)
AD2.C_bar
AD2.Pe
AD2.theta.to(u.min)
#Created the advection dispersion model curve based on the solver parameters
AD2_model = (AD2.C_bar*EPA.E_Advective_Dispersion((time_data2/AD2.theta).to_base_units(), AD2.Pe)).to(u.mole/u.L)

plt.plot(time_data2.to(u.min), concentration_data.to(u.mole/u.L),'-')
plt.plot(time_data2.to(u.min), CMFR2_model,'b')
plt.plot(time_data2.to(u.min), AD2_model,'g')
plt.xlabel(r'$time (min)$')
plt.ylabel(r'Concentration $\left ( \frac{mg}{L} \right )$')
plt.legend(['Measured dye','CMFR Model', 'AD Model'])
#plt.savefig('C:\\Users\\en-ce-4530\\github\\crg_4530\\Photos\\reactorplot2.png')
plt.show()
```
![Exp2](https://github.com/Galantino/crg_4530/blob/master/Photos/reactorplot2.png?raw=true)

The next set of baffles were then installed (Experiment 3) with the CMFR and AD models fitting the measured data.

```python
data_file_path3 = 'C:\\Users\\en-ce-4530\\github\\crg_4530\\Baffle3.txt'
#time initiates at pulse addition
start=34
time_data3 = EPA.ftime(data_file_path3,start,-1)
concentration_data = EPA.Column_of_data(data_file_path3,start,-1,1,'mole/L')
V_CMFR = 4*u.L
Q_CMFR = 380 * u.mL/u.min
theta_guess = (V_CMFR/Q_CMFR).to(u.s)
C_bar_guess = np.max(concentration_data)
CMFR3 = EPA.Solver_CMFR_N(time_data3, concentration_data, theta_guess, C_bar_guess)
CMFR3.C_bar
CMFR3.N
CMFR3.theta.to(u.min)
CMFR3_model = (CMFR3.C_bar*EPA.E_CMFR_N(time_data3/CMFR3.theta, CMFR3.N)).to(u.mole/u.L)
#use solver to get the advection dispersion parameters
AD3 = EPA.Solver_AD_Pe(time_data3, concentration_data, theta_guess, C_bar_guess)
AD3.C_bar
AD3.Pe
AD3.theta.to(u.min)
#Created the advection dispersion model curve based on the solver parameters
AD3_model = (AD3.C_bar*EPA.E_Advective_Dispersion((time_data3/AD3.theta).to_base_units(), AD3.Pe)).to(u.mole/u.L)
plt.plot(time_data3.to(u.min), concentration_data.to(u.mole/u.L),'-')
plt.plot(time_data3.to(u.min), CMFR3_model,'b')
plt.plot(time_data3.to(u.min), AD3_model,'g')
plt.xlabel(r'$time (min)$')
plt.ylabel(r'Concentration $\left ( \frac{mg}{L} \right )$')
plt.legend(['Measured dye','CMFR Model', 'AD Model'])
#plt.savefig('C:\\Users\\en-ce-4530\\github\\crg_4530\\Photos\\reactorplot3.png')
plt.show()
```
![Exp3](https://github.com/Galantino/crg_4530/blob/master/Photos/reactorplot3.png?raw=true)

The team then devised a new experiment (the Coiling experiment) in order to observe the effects of a long coiled system on dispersion.

```python
data_file_path4 = 'C:\\Users\\en-ce-4530\\github\\crg_4530\\lab5_week3_coil.xls'
print(EPA.notes(data_file_path4))
#time initiates at pulse addition
start=346
time_data4 = EPA.ftime(data_file_path4,start,-1)
concentration_data = EPA.Column_of_data(data_file_path4,start,-1,1,'mole/L')
V_CMFR = 4*u.L
Q_CMFR = 380 * u.mL/u.min
theta_guess = (V_CMFR/Q_CMFR).to(u.s)
C_bar_guess = np.max(concentration_data)
CMFR4 = EPA.Solver_CMFR_N(time_data4, concentration_data, theta_guess, C_bar_guess)
CMFR4.C_bar
CMFR4.N
CMFR4.theta.to(u.min)
CMFR4_model = (CMFR4.C_bar*EPA.E_CMFR_N(time_data4/CMFR4.theta, CMFR4.N)).to(u.mole/u.L)
#use solver to get the advection dispersion parameters
AD4 = EPA.Solver_AD_Pe(time_data4, concentration_data, theta_guess, C_bar_guess)
AD4.C_bar
AD4.Pe
AD4.theta.to(u.min)
#Created the advection dispersion model curve based on the solver parameters
AD4_model = (AD4.C_bar*EPA.E_Advective_Dispersion((time_data4/AD4.theta).to_base_units(), AD4.Pe)).to(u.mole/u.L)
plt.plot(time_data4.to(u.min), concentration_data.to(u.mole/u.L),'-')
plt.plot(time_data4.to(u.min), CMFR4_model,'b')
plt.plot(time_data4.to(u.min), AD4_model,'g')
plt.xlabel(r'$time (min)$')
plt.ylabel(r'Concentration $\left ( \frac{mg}{L} \right )$')
plt.legend(['Measured dye','CMFR Model', 'AD Model'])
#plt.savefig('C:\\Users\\en-ce-4530\\github\\crg_4530\\Photos\\reactorplotCoil.png')
plt.show()

```

![Coil](https://github.com/Galantino/crg_4530/blob/master/Photos/reactorplotCoil.png?raw=true)

We then took the Peclet numbers and the estimated number of CMFR's each system simulated and analyzed them side by side. For our coil experiment where the length of the tube was much greater than the diameter, we expected low dispersion and a high CMFR number value.

```python
AD1.Pe
>>1.9508928723811871
CMFR1.N
>> 2.1613709603431954

AD2.Pe
>> 0.78162661414059287
CMFR2.N
>> 1.5980665401945651

AD3.Pe
>> 1.1872478888720472
CMFR3.N
>> 1.8357328657739764

AD4.Pe
>>204.3959422679807
CMFR4.N
>>103.02205755390601
```

The trends, when drawing a comparison between 1 and 2 or 1 and 3 make sense because the presence of holes will result in a decrease in dispersion. The experiments were carried out first as a no-hole baffled system, then with one baffle with holes and one without, and finally a system with holes in both baffles. Despite the dispersions being less than that of trial one as expected, there is a discrepancy in the results for Experiments 2 and 3.

Since the inclusion of holes from Experiment 1 to 2 decreased the dispersion within the system, the results of 3 did not prove correlation for the presence of holes as a source of decreased dispersion. Given a system with more holes, the third trial should hypothetically have produced the highest dispersion values. The reason for this is because the presence of holes allows a pulse of dye to bypass an otherwise longer route (which would have made for a higher length to width ratio and thus lower dispersion). Another source of error can be attributed

The source of this discrepancy could be attributed to a potential inconsistency in the sealant between the walls of the baffles. For instance, there may have been points in the system in which the dye leaked past the tape and gave an inflated value for the concentration during one or more of the experiments.

Our Coil experiment was the most successful representation of a PMFR. Due to its large length to width ratio, there was little dispersion (a Peclet number of 204!) and a simulation of about 103 CMFRs in sseries.

In addition to our dispersion analysis, it appears that the lower the dispersion (higher the Peclet number) correlated with a higher number of respective CMFR in series. Experiment 3 is the only discrepancy with errors considered above.

##### 4) *Report the values of $t^\star$ at F = 0.1 for each of your experiments. Do they meet your expectations?*
$\overline{t}$ is theta , $t^{\star}$ is t over $\overline{t}$

AD.theta about t bar

```python
t_star1 = time_data1/AD1.Pe
t_star1 = t_star1.magnitude
t_star2 = time_data2/AD2.Pe
t_star2 = t_star2.magnitude
t_star3 = time_data3/AD3.Pe
t_star3 = t_star3.magnitude
t_star4 = time_data4/AD4.Pe
t_star4 = t_star4.magnitude

e1 = EPA.E_Advective_Dispersion(t_star1, AD1.Pe)
e2 = EPA.E_Advective_Dispersion(t_star2, AD2.Pe)
e3 = EPA.E_Advective_Dispersion(t_star3, AD3.Pe)
e4 = EPA.E_Advective_Dispersion(t_star4, AD4.Pe)

from scipy.integrate import quad

def integrand(x, t_star1, AD):
  return (AD/(4*np.pi*t_star1))**(0.5)*np.exp((-AD*((1-t_star1)**2))/(4*t_star1))

I = quad(integrand, 0, np.inf, args=(t_star1,Pe))

#F = integration of e (in epa)
```
##### 5) *Evaluate whether there is any evidence of “dead volumes” or “short circuiting” in your reactor.*

inconsistencies in the residence times  of the system so no uniform mixing or transport

##### 6) *Make a recommendation for the design of a full scale chlorine contact tank. As part of your recommendation discuss the parameter you chose to vary as part of your experimentation and what the optimal value was determined to be.*

## Conclusions
