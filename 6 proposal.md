# Research Proposal
## Chris Galantino, Ben Gassaway, Anna Lawrence

<span style="color:blue">Great start. I'd really like to guide you down a slightly different path. See below.</span>

###Introduction

The problem which the team will seek to solve is the aeration problem for Ocotal, Nicaragua plant. The facility that currently stands in Ocotal will be replaced by an AguaClara plant, and is assumed to contain an aerator in the treatment train. In order to align with the mission of AguaClara, it would be invaluable to invent a hydraulically driven aerator in which the gravitational potential energy is utilized to power the system, and does so with great efficiency.


![venturi](https://github.com/Galantino/crg_4530/blob/master/Photos/venturi4.gif?raw=true)

<span style="color:blue">Update from Ocotal. The available head isn't sufficient to power a traditional cascade style aerator. I am recommending that they count the LFOM as an aeration system and that they enhance the performance of the LFOM as an aerator by extending the LFOM tube to the bottom of the flocculator so that it carries the entrained bubbles deeper. The core idea is that we want to maximize the residence time of the bubbles in the water because we learned from the aeration lab that 97% of the oxygen was still in the bubbles when they escaped from the reactor! The venturi that you discuss below is your proposal for entraining air into the water. This will replace the free fall cascade effect of the LFOM. The interesting part of the research is designing a reactor that keeps those bubbles in suspension for a longer time. Thus you could use any air injection system including the little air stone as your bubble source. </span>

###Objectives

The driving hypothesis behind this research proposal is that a hydraulically-driven aeration system can perform at comparable efficiencies to that of an electrical powered plant. The fluid system that the team will be modeling is the Venturi effect in which the reduction in fluid pressure results from a constricted section in a pipe. This constriction will be utilized in pulling in air into the system driven by the flow of through the system.

###Experimental Plan

Experiments to test the efficiency of a Venturi-based aerator will be tested on a benchtop scale tentatively using a PVC tube reactor. There will be a number of holes drills on the sides of the reactor at various constrictions <span style="color:blue">I'd start with one!</span> throughout the flow of the reactor. In order to test the efficacy of aeration, DO probes will be placed at the influent and effluent stream of the water flow in order to gauge the performance of the system.

<span style="color:blue">You will need have a source of deoxygenated water that you can run through your reactor and then measure the aeration. You could also begin to get an idea of the required residence time based on the aeration lab results. What is important about the geometry of this proposed reactor? Should flow be horizontal or vertical up or vertical down? What determines the optimal velocity of the water? What determines the required residence time? Is there a way to make a reactor more compact? Is there a way to break up large bubbles into smaller bubbles?  </span>

###Key design parameters

1. System flow rate
2. Reactor length
3. Reactor diameter
4. Number of holes
5. Number of constrictions

###Timeline of tasks/experiments
- 4/16: Develop a working benchtop system to begin flow and constriction tests
- 4/23: Present a robust model of the benchtop model regarding flow aeration
- 4/30: Establish scalable parameters for the system to be implemented on the scale of an AguaClara plant
- Final presentations of the experiments and results

###Possible hurdles/challenges
- Access to data to compare the efficiency of a hydraulic system to the already-implemented aerator in Ocotal
- Developing a consistent testing system for the reactor's performance

###Resources needed to conduct experiments
1. Electric drill
2. Peristaltic pumps
3. PVC piping (from Aguaclara lab)
4. 3 DO probes
5. Plastic sheets
6. sulfite and cobalt items to deoxygenate water

###Expectations/Anticipated results

The team expects that a working model for the Venturi system to perform relatively well, however, it is unlikely that the team will be able to reach the point of development to produce an elegant prototype given the time constraints for the project. It is expected that the team will find valuable data to give insight into the value of pursuing this type of research.

Things to calculate:
we know that the diameter of a bubble was 4 mm

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
Q = Vt*A_tube
Q.to(u.mL/u.s)
>>Q_needed = 37.378 mL/s
```
