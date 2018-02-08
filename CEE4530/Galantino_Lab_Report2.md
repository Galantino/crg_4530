```python
from aide_design.play import*
```
# Christopher Galantino

##Objectives

The goal of this lab is to gain a broad understanding on laboratory techniques for the firm as well as determine the concentration of an unknown sample of methylene blue thought to be the "perfect ratio." Such a discovery will have desirable consequences on the company's value and move the firm in a new direction of research. In order to tackle this challenge, the laboratory team must first learn how to calibrate and use electronic balances, familiarize themselves with the data acquisition software in the lab (ProCoDA), learn proper pipetting techniques and dilution preparation, and understand how to measure concentrations using a US Vis spectrophotometer. Only then will the unknown concentration be found successfully.


##Datasheet for Week 2 Lab: Laboratory Measurements

| Temperature Measurement     | value |
| --------------------------- | ----- |
| Distilled water temperature |   22.47 C   |

| Pipette Technique (use DI-100 or Ohaus 160 balance) | value |
| --------------------------------------------------- | ----- |
| Density of water at that temperature                |  997.7 kg/m^3    |
| Actual mass of 990 µL of pure water                 | 0.9877 g      |
| Mass of 990 µL of water (rep 1)                     |  0.9878 g     |
| Mass of 990 µL of water (rep 2)                     |  0.9731 g     |
| Mass of 990 µL of water (rep 3)                     |  0.9800 g     |
| Mass of 990 µL of water (rep 4)                     |  0.9361 g     |
| Mass of 990 µL of water (rep 5)                     | 0.8997 g      |
| Average of the 5 measurements                       |  0.9553 g     |
| Standard deviation of the 5 measurements            |  0.0368     |

| Precision                                              | value |
| ------------------------------------------------------ | ----- |
| Percent coefficient of variation of the 5 measurements |   0.0385    |

| Accuracy                            | value |
| ----------------------------------- | ----- |
| average percent error for pipetting |   3.27%    |

Percent error for pipetting is calculated as follows:
$100*\frac{\left | mass_{density} - mass_{balance} \right |}{mass_{density}}$

| Measure Density (use DI-800 or Ohaus 400D or Prec. Std) | value |
| ------------------------------------------------------- | ----- |
| Molecular weight of NaCl                                |   58.4 g/mol    |
| Mass of NaCl in 100 mL of a 1-M solution                |   5.84 g    |
| Measured mass of NaCl used                              |  5.841 g     |
| Measured mass of empty 100 mL flask                     |  22.955 g     |
| Measured mass of flask + 1M solution                    |  126.433 g     |
| Mass of 100 mL of 1 M NaCl solution                     |  103.478 g     |
| Density of 1 M NaCl solution                      |   1034.78 g/L    |
| Literature value for density of 1 M NaCl solution       |   1041 g/L    |
| percent error for density measurment                    |  0.60 %     |

| Prepare methylene blue standards of several concentrations | value |
| ---------------------------------------------------------- | ----- |
| Volume of 1 g/L MB diluted to 100 mL to obtain:            |       |
| 1 mg/L MB                                                  |  1 mL     |
| 2 mg/L MB                                                  |  2 mL     |
| 3 mg/L MB                                                  |  3 mL     |
| 4 mg/L MB                                                  |   4 mL    |
| 5 mg/L MB                                                  |  5 mL     |
| Absorbance of unknown at 660 nm                            |    0.6988   |


| Measure absorbance at 660 nm using a spectrophotometer | value |
| ------------------------------------------------------ | ----- |
| Absorbance of distilled water                          |   -0.0021		   |
| Absorbance of 1 mg/L methylene blue                    |   0.1993	    |
| Absorbance of 2 mg/L methylene blue                    |   0.3448	    |
| Absorbance of 3 mg/L methylene blue                    |  0.5167	     |
| Absorbance of 4 mg/L methylene blue                    |   0.7134    |
| Absorbance of 5 mg/L methylene blue                    |    0.7379    |
| Slope at 660 nm (m)                                    |   0.5386    |
| Intercept at 660 nm (b)                                |   -1.0991    |
| Correlation coefficient at 660 nm (r)                  |   0.988    |
| Calculated concentration of unknown                    |  3.34 mg/L     |                                       


2. Create a graph of absorbance at 660 nm vs. concentration of methylene blue in Atom using the exported data file. Does absorbance at 660 nm increase linearly with concentration of methylene blue?

```python
# import your file
file = pd.read_csv('Lab2_absorbancies.csv')
array = np.array(file)

concentration = [0,1,2,3,4,5]
absorbance660 = array[235,1:7]
## plotting


plt.figure('ax',(10,8))


plt.plot(concentration,absorbance660)
# put in your x and y variables
plt.xlabel('Methylene Blue concentration', fontsize=15)
plt.ylabel('Absorbance', fontsize=15)
plt.show()
```
**Answer:** Absorbance seems to increase linearly with concentration of methylene blue at 660 nm.

3. Plot $\epsilon$ as a function of wavelength for each of the standards on a single graph. Note that the path length is 1 cm. Make sure you include units and axis labels on your graph. If Beer’s law is obeyed what should the graph look like?
```python
b = 1 * u.cm

wavelength = array[0:316,0]

#e = A/(b*c) where A is absorbance and c is concentrations

absorbance_1 = array[0:316,2]
epsilon_1 = absorbance_1/(b*concentration[1])
plt.figure('ax',(10,8))
plt.plot(wavelength,epsilon_1)


absorbance_2 = array[0:316,3]

epsilon_2 = absorbance_2/(b*concentration[2])

plt.plot(wavelength,epsilon_2)

absorbance_3 = array[0:316,4]
epsilon_3 = absorbance_3/(b*concentration[3])


plt.plot(wavelength,epsilon_3)

absorbance_4 = array[0:316,5]
epsilon_4 = absorbance_4/(b*concentration[4])

plt.plot(wavelength,epsilon_4)


absorbance_5 = array[0:316,6]
epsilon_5 = absorbance_4/(b*concentration[5])

plt.plot(wavelength,epsilon_5)


plt.xlabel('Wavelength (nm)', fontsize=15)
plt.ylabel('Extinction coefficients', fontsize=15)
plt.show()
```

**Answer:** If Beer's law is obeyed, the graph should be directly proportional to concentration. That is, as concentration increases, the overall graph of extinction coefficient vs wavelength will be of lower in magnitude for its data points as seen in the graph above.

4. Did you use interpolation or extrapolation to get the concentration of the unknown?

**Answer:** I used interpolation to get the concentration of the unknown, finding the slope and y-intercept that relates absorbance to concentration at 660 nm and relating this to the absorbance of the unknown at 660 nm.

5. What colors of light are most strongly absorbed by methylene blue?

**Answer:** Reddish colors of light are most strongly absorbed by methylene blue. The other type of light that is strongly absorbed is ultraviolet light, but this is not a color.

6. What measurement controls the accuracy of the density measurement for the NaCl solution? What density did you expect (see prelab 2)? Approximately what should the accuracy be?

**Answer:** The measurement that controls the accuracy of the density measurement for the NaCl solution is the mass of the empty 100 mL flask and the mass of the flask filled with 100 mL of the 1 M solution. This is due to the change in volume that occurs when water is added to such a large amount of salt, causing one to make sure water is added until the meniscus. This adds another factor for error. The density I expected was 1039 g/L. We calculated a value of 1034.78 g/L, which is a very close approximation. The accuracy should be under 2% error, which we achieved with an error of .41 %.

##Conclusions

This lab helped provide insight not only on how to properly prepare a standard, but also how to measure the concentration of an unknown sample through spectrophotometry. By measuring and graphing a relationship between concentration and absorbance at a given wavelength, one can use interpolation (or potentially extrapolation) to locate where on a known graph that an unknown solution's absorbance lays and in turn find the respective concentration. This is because concentration is linearly proportional to absorbance at a given wavelength. For this lab, the team found that concentration of the unknown to be 3.34 mg/L methylene blue from a best fit line whose slope was 0.5386 and y-intercept was -1.0991. We know this calculation to be fairly accurate since the correlation coefficient is 0.988. Another finding of this lab was the observation that as concentration increases, the extinction coefficient, $\epsilon$, decreases for all points along a wavelength spectrum. This finding agrees with Beer's law which establishes the relationship $\epsilon$ = A/(bc) where A is absorbance, b is path length, and A is absorbance.

##Suggestions/comments

I do not have much to suggest for this lab. It was very straight forward and, being a canned lab, had a linear series of steps that had to be taken to arrive at the appropriate conclusion. The only issue that arose was the disorganization of scale usage and spectrophotometer analysis. However, due to the high volume in which these were needed and it being the first day in the lab, it is understandable that there wasn't much cohesiveness or fluidity among the various teams. The TAs are doing a great job and have been very helpful!
