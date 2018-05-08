# Group 6 Research Report
# A New Approach to Aerator Design
## Chris Galantino, Ben Gassaway, Anna Lawrence

### Abstract

### Introduction

The problem which the team will seek to solve is the aeration situation of the Ocotal plant in Nicaragua. The facility that currently stands in Ocotal will be replaced by an AguaClara plant and is assumed to contain an aerator in the treatment train. However, available head is not sufficient to power a traditional cascade style aerator. Therefore, more investigation is needed in order design a performing aerator that may be catered to the plant's constraints.

Monroe has recommended that the plant operators count the LFOM as an aeration system and that they enhance the performance of the LFOM as an aerator by extending the LFOM tube to the bottom of the flocculator so that it carries the entrained bubbles deeper. The core idea is that we want to maximize the residence time of the bubbles in the water because it was learned from the aeration lab that 97% of the oxygen was still in the bubbles when they escaped from the reactor.

Initially, a venturi system was proposed for the introduction of oxygen without the need for active air pumping. A venturi works by providing a constriction in a flowing fluid, increasing velocity and decreasing pressure at the point in which the channel narrows. This decreased pressure promotes the inflow of oxygen from the atmosphere as a result of the produced vacuum effect.

![venturi](https://github.com/Galantino/crg_4530/blob/master/Photos/venturi4.gif?raw=true)

**need to center this photo**

While a venturi may replace the free fall cascade effect of the LFOM, it may prove difficult to keep the bubbles in suspension for a long time throughout the length of the reactor. Thus, the team experimented with various air injection systems such as an air stone and eventually a high pressure jet.

In order to align with the mission of AguaClara, it would be invaluable to invent a hydraulically driven aerator in which the gravitational potential energy is utilized to power the system, and does so with great efficiency.

###Objectives

The driving hypothesis behind this research proposal is that a hydraulically-driven aeration system can perform at comparable efficiencies to that of an electrical powered plant. By modeling various scenarios of oxygen introduction and bubble sequestration, the team hopes to achieve an acceptable aeration rate.

###Experimental Plan

Experiments to test the efficiency of the aerator will be tested on a benchtop scale tentatively using a PVC tube reactor. In order to test the efficacy of aeration, DO probes will be placed at the influent and effluent stream of the water flow in order to gauge the performance of the system.

The team intends to fine tune the experimental setup based on what is learned from experimental trials. Below are questions that the team seeks to answer:

  1. What determines the required residence time?
  2. What is important about the geometry of this proposed reactor?
  3. Should flow be horizontal or vertical up or vertical down?
  4. What determines the optimal velocity of the water?
  5. Is there a way to make a reactor more compact?
  6. Is there a way to break up large bubbles into smaller bubbles?

####Key design parameters

1. System flow rate
2. Reactor length
3. Reactor diameter
4. Headloss (orifices, peizometric, etc.)

####Timeline of tasks/experiments
- 4/16: Develop a working benchtop system to begin flow and constriction tests
- 4/23: Present a robust model of the benchtop model regarding flow aeration
- 4/30: Manipulate the model in order to maximize bubble retention and overall aeration performance
- Final presentations of the experiments and results

####Possible hurdles/challenges
- Access to data to compare the efficiency of a hydraulic system to the already-implemented aerator in Ocotal
- Developing a consistent testing system for the reactor's performance
- Providing an appropriate amount of water for the experiments

####Resources needed to conduct experiments
1. Electric drill
2. Peristaltic pumps (600 RPM)
3. PVC piping (from AguaClara lab)
4. 2 DO probes (if time permits DO testing)
5. Plastic sheets
6. sulfite and cobalt items to deoxygenate water (if time permits DO testing)
7. push-to-connects (adapters as well)

####Expectations/Anticipated results

The team expects that a working model for aeration system will perform relatively well; however, it is unlikely that the team will be able to reach the point of development to produce an elegant prototype given the time constraints for the project. It is expected that the team will find valuable data to give insight into the value of pursuing this type of research.

###Procedures

The team moved through a series of preliminary steps before beginning the fabrication. To begin, there were several calculations to perform to understand the effects of specific constraints and how these parameters influence expected performance

####Calculations

The team began with a simple experiment through an aeration stone similar to the aeration lab done earlier in the semester. The purpose of this was to observe how large the average bubble was. By determining the diameter of a bubble, one could then find the resulting upflow velocity in a fluid (in this case water). With this upflow velocity known, the team then knows the minimum downward velocity needed within the apparatus to retain bubbles in the system.


[picture of aeration stone in action]


After a short trial of the aeration stone with a airflow of 200uM/s, the diameter of the average bubble was about 4 mm.

so from this known value, we must determine (in order) the: volume of a bubble, resulting upflow velocity of a bubble (which in turn is the minimum downward velocity needed to retain the bubbles in the system), the resulting flow rate needed (with 1 inch diam tube).

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

d_bubble = 4*u.mm
rho_air = 1.225*u.kg/u.m**3
rho_water = 997*u.kg/u.m**3
Cd = .6  #since bubble experiences turbulence
Nu = 9.554*(10**-7)*u.m**2/u.sec  #at 22 C
Vt = -np.sqrt((4*pc.gravity*d_bubble*(rho_water-rho_air)/(3*Cd*rho_water)))
Re = (Vt.to(u.m/u.s)*d_bubble.to(u.m))/Nu
>> Re = 1235 #this is a good Re to correlate with the drag coeff of 0.6
>> Vt = 0.295 m/s

d_tube = 0.5*u.inch
A_tube = pc.area_circle(d_tube)
Q = -1*Vt*A_tube
Q.to(u.mL/u.s)
>>Q_needed = 37.378 mL/s
```
```python
#headloss Calculations through a different push-to-connects
pi_orifice = .62
d_orifice_1 = .17*u.inch
headloss_1 = pc.head_orifice(d_orifice_1, pi_orifice,Q )
headloss_1
d_orifice_2 = .25*u.inch
headloss_2 = pc.head_orifice(d_orifice_2, pi_orifice,Q )
headloss_2
l = 1*u.m

headloss_major = pc.headloss_fric(Q,d_orifice_2,l,Nu,.01*u.mm)
headloss_major
headloss_fric(FlowRate, Diam, Length, Nu, PipeRough)

```
