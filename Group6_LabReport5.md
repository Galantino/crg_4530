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

### Introduction
In order to test specific natural or engineered processes, reactors can be set up to simulate these chemical, biological, and physical processes and provide insight as to how a certain system would act in different scenarios. Specifically, a reactor can be described as a boundary, literally or figuratively, that physically controls the processes under specific constraints. One gets to decide what they want their system to be, where they want their boundaries to be, what inputs will go into the system, and what is to be measured. Reactors give the user more control over chemical, biological and physical reactions, including temperature control of the vessel contents, measurement of parameters such as pH or pressure, and mixing and dispersing applications. There are a number of different types of reactors, including stirred, high-pressure, and mini reactors. Continuous flow tubular reactors can be externally heated or jacketed with a circulating fluid. Although many different types of reactors, all of these reactors fall under three categories, CMFR (completely mixed flow reactor), PFR (plug-flow reactor) or Batch Reactor. CMFRs are control volumes for which spatially uniform properties may be assumed. They are also reactors with flow, are completely mixed and can attain steady state. Some examples include a room in a building or a small pond. A batch reactor varies from a CMFR for it has no flow. Material is added, mixed, given time for reaction to occur, but then the reactor is drained. Steady state is not attained. PFR, or plug flow reactors, has flow, however, there is no mixing in lateral direction. Properties may vary through the PFR. When modeling a PFR, it is important that it is split into a series of sequential control volumes. The plug flow reactor is an idealized extreme not attainable in practice. All real reactors fall under the category of Batch or CMFR.

### Procedure:
Day 1: Calibration and Set-Up (CMFR)
Our goal was to perform a mass balance on red dye through a reactor of length 30 cm and width 15 cm. We limited our depth to a maximum of 5 cm and used a container with a volume of 4L. We also set our pumping rate to 380 mL/min, giving us a residence time of approximately 6 minutes. Once our reactor was set up to the pump with the correct pipes leading to the influent and effluent, we added tracer directly into the first chamber of our reactor. The red dye allowed us to qualitatively observe the advection and dispersion in the reactors. We calculated our data using ProCoDA II software and a photometer. To calibrate the photometer, our objective was to have a total volume of 1 L circulating through the reactor system. We connected the pump, a 1 L bottle, and the vertically positioned photometer in a closed loop with one another via 18” pipes. 1 L of tap water was added to the bottle and the pump was turned on to 380 mL/min. We set our voltage to 5V on ProCoDA II and confirmed that it was reading values between -1.3V when the light in the photometer is off and +3.5V when it is on. Using a 40 g/L stock solution of Red Dye, we made our calibration curve for our photometer by calculating the volume of red dye that will be needed to generate a calibration with points at 0, 1, 2, 5, 10, 20, 30, 40, and 50 mg/L. The first calibration point, 0 mg/L, was used as our standard and was a record of our voltage prior to adding any red dye. We then added red dye to make the concentration of the reactor 1mg/L and continued to add dye until and recorded all of the standards have been read and formed a linear plot. Once we finished our calibration, we set up a CMFR reactor for our experiment. We connected a pump from a 20L Jerrican filled with tap water to the influent of your reactor and placed our reactor on a stir plate. We connected a 3/8” push-connect fitting is on the effluent side of your reactor and connected the effluent to the drain through a short tube. A second pump head was set up to pull a sample from weir through the photometer and then to the drain. We confirmed our system worked by running the pump at 380 rev/min to check to see if our ProCoDA software was reading a stable voltage of about +3.5V and checking that the volume in the remained constant. For each test, we wanted to measure the reactor volume, residual reactor red dye concentration, and the flow rate. We added a volume of red dye #40 stock until the maximum concentration of the tracer was about 30 mg/L near the influent of the reactor. We calculated data until the majority of the tracer has exited the reactor. Once we terminated the experiment, we poured the contents of the the reactor into a container and weighted it to determine the exact volume of the reactor. We used this information to obtain the average concentration in the reactor and to further perform a mass balance on the red dye.

Day 2: Baffles
The ideal CMFR model assumes that the fluid in the reactor is perfectly mixed and that there are no concentration gradients inside the reactor. However, in a real-world stirred tank reactor, there most likely will not be perfect mixing and will be concentration gradients present. Baffles contribute additional disturbance to the flow created by the mixer, and provide more effective mixing. We used the set up from the prior week to continue with this part of the lab. For this part if the experiment, we included baffles in order to bring our reactor closer to the ideal of perfect mixing in each of the baffle zones. We also experimented with baffles with different sized pores to achieve mixing within zones. Our objective was to determine the diameter and spacing of the pores required to achieve adequate mixing by measuring the Peclet number. An additional constraint regarding pore design that we took into consideration is that the head loss through the pores does not get too excessive. We tested 3 different baffle designs:
1.     No holes
2.     Small holes on the first baffle but no holes on the second baffle
3.     Small holes on both baffles
We dropped red dye into the first section of the reactor and calculated the concentration of the red dye at the effluent using ProCoDA software.  

Day 3: Coiling
We used full coil tubing connected on one end to a pump and a Jerrican filled with tap water and on the other end an effluent tube. In order to determine concentration of the red dye, we first needed to measure the volume of the tubes. We measured the tube absent of anything as 1240g and then filled with water as 2015g. These values were used to calculate the mass of the water inside the tubing, 775g. One our system was set up, we added a pulse of .05 mL (20mg/L) of 100g/L red dye into the coiled tube (pump running at 380 rev/min pump).



#####1) *Use multivariable nonlinear regression to obtain the best fit between the experimental data and the two models by minimizing the sum of the squared errors. Use EPA.Solver_AD_Pe and EPA.Solver_CMFR_N. These functions will minimize the error by varying the values of average residence time, (mass of tracer/reactor volume), and either the number of CMFR in series or the Peclet number.*

```python
from aide_design.play import *
import Environmental_Processes_Analysis as EPA
import importlib
importlib.reload(EPA)

data_file_path = 'Lab5Part2(CMFR_Final).xls'
print(EPA.notes(data_file_path))

#I eliminate the beginning of the data file because this is a CMFR and the first data was taken before the dye reached the sensor.
firstrow = 37
time_data = EPA.ftime(data_file_path,firstrow,-1)
concentration_data = EPA.Column_of_data(data_file_path,firstrow,-1,1,'mg/L')
V_CMFR = 4*u.L
Q_CMFR = 380 * u.mL/u.min
theta_guess = (V_CMFR/Q_CMFR).to(u.s)
C_bar_guess = np.max(concentration_data)
C_bar_guess
#The Solver_CMFR_N will return the initial tracer concentration, residence time, and number of reactors in series.
#This experiment was for a single reactor and so we expect N to be 1!

CMFR = EPA.Solver_CMFR_N(time_data, concentration_data, theta_guess, C_bar_guess)
#use dot notation to get the 3 elements of the tuple that are in CMFR
CMFR.C_bar
CMFR.N
CMFR.theta
#create a model curve given the curve fit parameters.
CMFR_model = CMFR.C_bar * EPA.E_CMFR_N(t_data/CMFR.theta,CMFR.N)
plt.plot(t_data.to(u.min), concentration_data.to(u.mg/u.L),'r')
plt.plot(t_data.to(u.min), CMFR_model,'b')
plt.xlabel(r'$time (min)$')
plt.ylabel(r'Concentration $\left ( \frac{mg}{L} \right )$')

plt.legend(['Measured dye','CMFR Model'])
#plt.savefig('images/reactorplot.png')

plt.show()
```
#Load a data file for a reactor with baffles. This was from a test that used acid as the tracer.
#The concentration units are moles/L

#####2) *Generate a plot showing the experimental data as points and the model results as thin lines for each of your experiments. Explain which model fits best and discuss those results based on your expectations.*
```python
data_file_path1 = 'Baffle1.txt'
#time initiates at pulse addition
time_data = EPA.Column_of_data(data_file_path1,367,920,0,'s')
time_data = time_data*86400
concentration_data = EPA.Column_of_data(data_file_path1,367,920,1,'mole/L')
V_CMFR = 4*u.L
Q_CMFR = 380 * u.mL/u.min
theta_guess = (V_CMFR/Q_CMFR).to(u.s)
theta_guess
C_bar_guess = np.max(concentration_data)
CMFR = EPA.Solver_CMFR_N(time_data, concentration_data, theta_guess, C_bar_guess)
CMFR.C_bar
CMFR.N
CMFR.theta.to(u.min)
CMFR_model = (CMFR.C_bar*EPA.E_CMFR_N(time_data/CMFR.theta, CMFR.N)).to(u.mole/u.L)
#use solver to get the advection dispersion parameters
AD = EPA.Solver_AD_Pe(time_data, concentration_data, theta_guess, C_bar_guess)
AD.C_bar
AD.Pe
AD.theta.to(u.min)
#Created the advection dispersion model curve based on the solver parameters
AD_model = (AD.C_bar*EPA.E_Advective_Dispersion((time_data/AD.theta).to_base_units(), AD.Pe)).to(u.mole/u.L)
plt.plot(time_data.to(u.min), concentration_data.to(u.mole/u.L),'-')
plt.plot(time_data.to(u.min), CMFR_model,'b')
plt.plot(time_data.to(u.min), AD_model,'g')
plt.xlabel(r'$time (min)$')
plt.ylabel(r'Concentration $\left ( \frac{mg}{L} \right )$')
plt.legend(['Measured dye','CMFR Model', 'AD Model'])
#plt.savefig('images/reactorplot.png')
plt.show()

data_file_path2 = 'Baffle2.txt'
#time initiates at pulse addition
time_data = EPA.Column_of_data(data_file_path2,367,920,0,'s')
time_data = time_data*86400
concentration_data = EPA.Column_of_data(data_file_path2,367,920,1,'mole/L')
V_CMFR = 4*u.L
Q_CMFR = 380 * u.mL/u.min
theta_guess = (V_CMFR/Q_CMFR).to(u.s)
theta_guess
C_bar_guess = np.max(concentration_data)
CMFR = EPA.Solver_CMFR_N(time_data, concentration_data, theta_guess, C_bar_guess)

CMFR.C_bar

CMFR.N
CMFR.theta.to(u.min)
CMFR_model = (CMFR.C_bar*EPA.E_CMFR_N(time_data/CMFR.theta, CMFR.N)).to(u.mole/u.L)
#use solver to get the advection dispersion parameters


AD = EPA.Solver_AD_Pe(time_data, concentration_data, theta_guess, C_bar_guess)
AD.C_bar
AD.Pe
AD.theta.to(u.min)
#Created the advection dispersion model curve based on the solver parameters
AD_model = (AD.C_bar*EPA.E_Advective_Dispersion((time_data/AD.theta).to_base_units(), AD.Pe)).to(u.mole/u.L)
plt.plot(time_data.to(u.min), concentration_data.to(u.mole/u.L),'-')
plt.plot(time_data.to(u.min), CMFR_model,'b')
plt.plot(time_data.to(u.min), AD_model,'g')
plt.xlabel(r'$time (min)$')
plt.ylabel(r'Concentration $\left ( \frac{mg}{L} \right )$')
plt.legend(['Measured dye','CMFR Model', 'AD Model'])
#plt.savefig('images/reactorplot.png')
plt.show()

data_file_path3 = 'Baffle3.txt'
#time initiates at pulse addition
time_data = EPA.Column_of_data(data_file_path3,34,-1,0,'s')
time_data = time_data*86400
concentration_data = EPA.Column_of_data(data_file_path3,34,-1,1,'mole/L')
V_CMFR = 4*u.L
Q_CMFR = 380 * u.mL/u.min
theta_guess = (V_CMFR/Q_CMFR).to(u.s)
theta_guess
C_bar_guess = np.max(concentration_data)
CMFR = EPA.Solver_CMFR_N(time_data, concentration_data, theta_guess, C_bar_guess)

CMFR.C_bar

CMFR.N
CMFR.theta.to(u.min)
CMFR_model = (CMFR.C_bar*EPA.E_CMFR_N(time_data/CMFR.theta, CMFR.N)).to(u.mole/u.L)
#use solver to get the advection dispersion parameters


AD = EPA.Solver_AD_Pe(time_data, concentration_data, theta_guess, C_bar_guess)
AD.C_bar
AD.Pe
AD.theta.to(u.min)
#Created the advection dispersion model curve based on the solver parameters
AD_model = (AD.C_bar*EPA.E_Advective_Dispersion((time_data/AD.theta).to_base_units(), AD.Pe)).to(u.mole/u.L)
plt.plot(time_data.to(u.min), concentration_data.to(u.mole/u.L),'-')
plt.plot(time_data.to(u.min), CMFR_model,'b')
plt.plot(time_data.to(u.min), AD_model,'g')
plt.xlabel(r'$time (min)$')
plt.ylabel(r'Concentration $\left ( \frac{mg}{L} \right )$')
plt.legend(['Measured dye','CMFR Model', 'AD Model'])
#plt.savefig('images/reactorplot.png')
plt.show()
```

#####2) *Generate a plot showing the experimental data as points and the model results as thin lines for each of your experiments. Explain which model fits best and discuss those results based on your expectations.*

done above ^
#####3) *Compare the trends in the estimated values of N and Pe across your set of experiments. How did your chosen reactor modifications effect dispersion?*

#####4) *Report the values of $t^\star$ at F = 0.1 for each of your experiments. Do they meet your expectations?*

#####5) *Evaluate whether there is any evidence of “dead volumes” or “short circuiting” in your reactor.*

#####6) *Make a recommendation for the design of a full scale chlorine contact tank. As part of your recommendation discuss the parameter you chose to vary as part of your experimentation and what the optimal value was determined to be.*

``` python
def CMFR_Analysis(time,concentration,Q,V,plotnumber):
  guessedtheta = (V/Q).to(u.min)
  Cbarguess = np.max(concentration)
  CMFR= EPA.Solver_CMFR_N(time, concentration, guessedtheta, Cbarguess)
  CMFR_model = CMFR.C_bar * EPA.E_CMFR_N((time/CMFR.theta).to_base_units(),CMFR.N)
  CMFRgraph = 'Reactors/images/CMFRplot'
  CMFRgraph+= plotnumber
  CMFRgraph+='.png'

  plt.plot(time.to(u.min), concentration.to(u.mg/u.L))
  plt.plot(time.to(u.min), CMFR_model,'b')
  plt.xlabel(r'$time (min)$')
  plt.ylabel(r'Concentration $\left ( \frac{mg}{L} \right )$')
  plt.legend(['Measured dye','CMFR Model'])

  plt.savefig(CMFRgraph)
  plt.show()
  print(CMFR.N)

def Baffles_Analysis(timeB,concentrationB,Q_B,V_B,plotnumber_B):

  theta_guessB = (V_B/Q_B).to(u.min)
  C_bar_guess_B = np.max(concentrationB)
  CMFR_B = EPA.Solver_CMFR_N(timeB,concentrationB,theta_guessB,C_bar_guess_B)
  CMFR_Model_B = CMFR_B.C_bar* EPA.E_CMFR_N((timeB/CMFR_B.theta).to_base_units(),CMFR_B.N)

  AD = EPA.Solver_AD_Pe(timeB, concentrationB, theta_guessB, C_bar_guess_B)
  AD_model = (AD.C_bar*EPA.E_Advective_Dispersion((timeB/AD.theta).to_base_units(), AD.Pe))

  saved = 'Reactors/images/reactorplot'
  saved+= plotnumber_B
  saved+='.png'
  plt.scatter(timeB.to(u.min), concentrationB.to(u.mg/u.L))
  plt.plot(timeB.to(u.min), CMFR_Model_B.to(u.mg/u.L),'b')
  plt.plot(timeB.to(u.min), AD_model.to(u.mg/u.L),'g')
  plt.xlabel(r'$time (min)$')
  plt.ylabel(r'Concentration $\left ( \frac{mg}{L} \right )$')
  plt.legend(['CMFR Model', 'AD Model','Measured dye'])

  plt.savefig(saved)
  plt.show()
  print(CMFR_B.N,AD.Pe)
  ```

  ```python
    #TO CHECK
  #analysis

  def CMFR_Analysis(time,concentration,Q,V,plotnumber):
    guessedtheta = (V/Q).to(u.min)
    Cbarguess = np.max(concentration)
    CMFR= EPA.Solver_CMFR_N(time, concentration, guessedtheta, Cbarguess)
    CMFR_model = CMFR.C_bar * EPA.E_CMFR_N((time/CMFR.theta).to_base_units(),CMFR.N)
    CMFRgraph = 'Reactors/CMFRplot'
    CMFRgraph+= plotnumber
    CMFRgraph+='.png'

    plt.plot(time.to(u.min), concentration.to(u.mg/u.L))
    plt.plot(time.to(u.min), CMFR_model,'b')
    plt.xlabel(r'$time (min)$')
    plt.ylabel(r'Concentration $\left ( \frac{mg}{L} \right )$')
    plt.legend(['Measured dye','CMFR Model'])

    plt.savefig(CMFRgraph)
    plt.show()
    print(CMFR.N)

  def Baffles_Analysis(timeB,concentrationB,Q_B,V_B,plotnumber_B):

    theta_guessB = (V_B/Q_B).to(u.min)
    C_bar_guess_B = np.max(concentrationB)
    CMFR_B = EPA.Solver_CMFR_N(timeB,concentrationB,theta_guessB,C_bar_guess_B)
    CMFR_Model_B = CMFR_B.C_bar* EPA.E_CMFR_N((timeB/CMFR_B.theta).to_base_units(),CMFR_B.N)

    AD = EPA.Solver_AD_Pe(timeB, concentrationB, theta_guessB, C_bar_guess_B)
    AD_model = (AD.C_bar*EPA.E_Advective_Dispersion((timeB/AD.theta).to_base_units(), AD.Pe))

    saved = 'Reactors/reactorplot'
    saved+= plotnumber_B
    saved+='.png'
    plt.scatter(timeB.to(u.min), concentrationB.to(u.mg/u.L))
    plt.plot(timeB.to(u.min), CMFR_Model_B.to(u.mg/u.L),'b')
    plt.plot(timeB.to(u.min), AD_model.to(u.mg/u.L),'g')
    plt.xlabel(r'$time (min)$')
    plt.ylabel(r'Concentration $\left ( \frac{mg}{L} \right )$')
    plt.legend(['CMFR Model', 'AD Model','Measured dye'])

    plt.savefig(saved)
    plt.show()
    print(CMFR_B.N,AD.Pe)




  Week1file = 'Reactors/CMFRJonathansGroup.xls'
  Week2file = 'Reactors/Reactor28.xls'
  Week3file = 'Reactors/Reactor37.xls'

  data_file_pathCMFR = 'Reactors/CMFRJonathansGroup.xls'


  #I eliminate the beginning of the data file because this is a CMFR and the first data was taken before the dye reached the sensor.
  firstrowCMFR = 5
  timeCMFR = EPA.ftime(data_file_pathCMFR,firstrowCMFR,-1)
  CMFR_data = EPA.Column_of_data(data_file_pathCMFR,firstrowCMFR,-1,1,'mg/L')
  V_CMFR = 1.5*u.L
  Q_CMFR = 380 * u.mL/u.min
  CMFRplotnumber = 'CMFRplot'
  CMFR_Analysis(timeCMFR,CMFR_data,Q_CMFR,V_CMFR,CMFRplotnumber)
  CMFR_N = 1
  timeCMFR


  #Baffles
  #--------------------------------------------------

  V_Baffles = 2*u.L
  Q_Baffles = 380 * u.mL/u.min

  #Week 2


  w2e1time = EPA.ftime(Week2file,276,459)
  w2e1dye = EPA.Column_of_data(Week2file,276,459,1,'mg/L')
  w2e1plot='w2e1'
  Baffles_Analysis(w2e1time,w2e1dye,Q_Baffles,V_Baffles,'w2e1')
  # N = 2.8595
  # Pe = 3.569

  w2e2time = EPA.ftime(Week2file,631,710)
  w2e2dye = EPA.Column_of_data(Week2file,631,710,1,'mg/L')
  Baffles_Analysis(w2e2time,w2e2dye,Q_Baffles,V_Baffles,'w2e1')
  # N = 1.436
  # Pe = 0.5494
  w2e3time = EPA.ftime(Week2file,1193,-1)
  w2e3dye = EPA.Column_of_data(Week2file,1193,-1,1,'mg/L')
  Baffles_Analysis(w2e3time,w2e3dye,Q_Baffles,V_Baffles,'w2e3')
  # N = 1.3767
  # Pe = 0.289

  #Week 3

  w3e1time=EPA.ftime(Week3file,453,589)
  w3e1dye=EPA.Column_of_data(Week3file,453,589,1,'mg/L')
  Baffles_Analysis(w3e1time,w3e1dye,Q_Baffles,V_Baffles,'w3e1')
  # N = 1
  # Pe = 8.865

  w3e2time=EPA.ftime(Week3file,903,1060)
  w3e2dye=EPA.Column_of_data(Week3file,903,1060,1,'mg/L')
  Baffles_Analysis(w3e2time,w3e2dye,Q_Baffles,V_Baffles,'w3e2')
  # N = 1
  # Pe = 6.9845


  plt.plot(w2e1time.to(u.min),w2e1dye.to(u.mg/u.L), label ="First Experiment")
  plt.plot(w2e2time.to(u.min),w2e2dye.to(u.mg/u.L), label="Second Experiment")
  plt.plot(w2e3time.to(u.min),w2e3dye.to(u.mg/u.L), label="Third Experiment")
  plt.plot(w3e1time.to(u.min),w3e1dye.to(u.mg/u.L), label="Fourth Experiment")
  plt.plot(w3e2time.to(u.min),w3e2dye.to(u.mg/u.L), label="Fifth Experiment")
  plt.xlabel('Time (min)')
  plt.ylabel('Concentration (mg/L)')
  plt.legend()
  #plt.savefig('Experimentsplots.png')
  plt.show()
  ```
