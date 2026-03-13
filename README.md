# Fitting Poisson  distribution
# Aim : 

To fit poisson distribution for the arrival of objects per minute from the feeder

# Software required :  

Python and Visual component tool

# Theory:

The Poisson distribution is the discrete probability distribution of the number of events occurring in a given time period, given the average number of times the event occurs over that time period.

![image](https://user-images.githubusercontent.com/104613195/166248326-fd042076-8b0b-40c4-8b11-1d8e8fcb74db.png)

 Conditions for Poisson Distribution:

1. An event can occur any number of times during a time period.
2. Events occur independently. I
3. The rate of occurrence is constant.
4. The probability of an event occurring is proportional to the length of the time period. 
 
# Procedure :

![image](https://user-images.githubusercontent.com/104613195/166251988-d0c53205-6080-4f7b-ae4c-398178586637.png)

# Experiment :

![image](https://user-images.githubusercontent.com/103921593/230282876-f4a5afbf-cac1-4648-a1b0-c78840638a8e.png)

# Program :
````
import math
from scipy.stats import chi2
data = list(map(int, input("Enter values separated by space: ").split()))
x = sorted(set(data))
obs = [data.count(i) for i in x]
n = sum(obs)
mean = sum(i*f for i,f in zip(x,obs))/n
print("\nMean =", round(mean,4))
chi = 0
print("\nX   P(X=x)   Obs   Exp   Xi^2")
for i,o in zip(x,obs):
    p = (math.exp(-mean)*(mean**i))/math.factorial(i)
    e = p*n
    xi = ((o-e)**2)/e if e>0 else 0
    chi += xi
    print(i, round(p,4), o, round(e,4), round(xi,4))
print("\nCalculated Chi-square =", round(chi,4))
df = len(x)-1
table = chi2.ppf(0.99,df)
print("Table value =", round(table,4))
if chi < table:
    print("Data fits Poisson distribution")
else:
    print("Data does NOT fit Poisson distribution")
 
````
 

# Output : 

````
Enter values separated by space:   1 2 3 4 5 6 7 8 

Mean = 4.5

X   P(X=x)   Obs   Exp   Xi^2
1 0.05 1 0.3999 0.9004
2 0.1125 1 0.8998 0.0112
3 0.1687 1 1.3497 0.0906
4 0.1898 1 1.5185 0.177
5 0.1708 1 1.3666 0.0983
6 0.1281 1 1.025 0.0006
7 0.0824 1 0.6589 0.1766
8 0.0463 1 0.3706 1.0687

Calculated Chi-square = 2.5235
Table value = 18.4753
Data fits Poisson distribution

````

# Results

The Poisson distribution is fitted for the objects arrived from feeder per minute and the data is tested using Chi-square test. 
 
