**This is a research based course of Differential Privacy with the Prof. Vorapong from the The University of Tokyo With 5 main topics**

Topic 1: Anonymity, Privacy-Preciseness trade-offs

Topic 2: Differential Privacy, Laplacian Mechanism

Topic 3: Exponential Mechanism

Topic 4: SmallDB algorithm

Topic 5: Private PAC learning

## Linking attack
A linkage attack is an attempt to re-identify individuals in an anonymized dataset by combining that data with background information.
Data like age, location, gender, and so on are generally used.

## K-ANONYMITY
1. Put data into groups of ≥ 𝑘
2. Make quasi-identifier in the same group looks indistinguishable by generalizations
In practice, 𝑘 ≥ 20. 
Larger 𝑘 → More privacy but reveal less information
𝑘-anonymity became a standard for data publication.

## HOW TO FIND A GOOD GROUP?
𝑘′-mean when 𝑘′ = |𝑇|/𝑘? 
Actually, 𝑘′-center should be more appropriated.
No standard grouping algorithm. 
There is 𝑂(𝑘)-approximation algorithm.

## L-DIVERSITY
It is is a form of group based anonymization that is used to preserve privacy in data sets by reducing the granularity of a data representation.
ℓ-diversity: #same sensitive information in group 𝐺𝑖 is no larger than |𝑮𝒊|/ℓ .

## PROBLEMS OF L-DIVERSITY
If the elements of a group have a same characteristic, then the private information can be leaked. (Information Leakage)
For example, the salary between the group ranges from 3M to 5M, the l=3, then we can know that this group is a low salary group. -> Alice (inside this group) also earns a low salary.

## INFORMATION GAIN
Take Alice's salary as an example, we can easily find that her salary is between 3~5M and gain a lot of information according to the Quasi-Identifiers of age before publication.
To protect her privacy, we can put into another publication where Alice Salary ∈ {5𝑀, 8𝑀, 11𝑀}
Question: How to quantify the information gain?

## EARTH MOVING DISTANCE (EMD)
The Earth Mover's Distance (EMD) between two distributions is proportional to the minimum amount of work required to change one distribution into the other. Here one unit
of work is defined as the amount of work necessary to move one unit of weight by one unit of distance.

Choosing {5,8,11} has less information leakage than {3,4,5}.
The EMD of {5,8,11} is 1 while the other is 3.

## T-CLOSENESS
Each group must have EMD ≤ 𝑡 - When 𝑡 = 0, sensitive information of all groups are identical. - Machine learning algorithm cannot learn anything from the published information
- When 𝑡 → ∞, each group can be anything.
- No privacy for users
There is no standard value for 𝑡

## DIFFERENTIAL PRIVACY
Problem: 
Charles does not want to publish his weight,
but Alice, Bob, and Doe do publish the information
Average Weight = (𝑤𝐴𝑙𝑖𝑐𝑒+𝑤𝐵𝑜𝑏+𝑤𝐶ℎ𝑎𝑟𝑙𝑒𝑠+𝑤𝐷𝑜𝑒)/4
60 = (40+60+𝑤𝐶ℎ𝑎𝑟𝑙𝑒𝑠+60)/4
𝑤𝐶ℎ𝑎𝑟𝑙𝑒𝑠 = 80 Information Leakage!!!

Idea: Add noise to public information
Average weight = 55 ---> Average Weight + Noise = 55
By the noise, it is very hard to predict Charles’weight.

## ATTACKERS’ VIEWPOINT
Average weight = 55 ---> Average Weight + Noise = 55
The noise difference is +-5, and the Average weight of 60 or 50 can be used to calculate Thomas's weight, where P1 ≈ P2.

## DIFFERENTIAL PRIVACY
Two tables are neighbors if the sensitive information is different just by one 
records.
We have: 𝑓(𝑇1) + Noise and 𝑓(𝑇2) + Noise
Published information = 𝑌 
Pr 𝑓 𝑇1 + Noise = 𝑌 ≈ Pr[ 𝑓 𝑇2 + Noise = 𝑌]

## Noise?
Lap(𝑏) has distribution 𝑝(𝑥; 𝑏) = (1/(2b))*exp(-|x|/b)
（where x from Lap(b)）

Example:Lap(1):𝑝(𝑥;𝑏) = 0.5 ⋅ exp(−|x|)
Expected value = 0
Variance = 2*𝑏^2
Larger 𝑏 = wider probability distribution

## LAPLACIAN MECHANISM
𝑓(𝑇)= statistical conclusion from Table 𝑇
Ex 𝑓(𝑇) = average weight of persons in Table 𝑇
𝐺𝑆(𝑓) =               max                  * |𝑓(𝑇1) − 𝑓(𝑇2)|   ----->Maximum difference in statistical conclusion pbtained from two neighboring tables.   
          𝑇1,𝑇2:neighboring tables

Example: Let assume that weights are always between 30 and 150.
When we have four persons 𝑓(𝑇) = (𝑤1+𝑤2+𝑤3+𝑤4) / 4
Can change from 30 to 150
Sum changed by 120
Average changed by 120/4 = 30
𝐺𝑆(𝑓) = 30

Published Information = 𝑓(𝑇) + 𝐿𝑎𝑝(𝐺𝑆(f) / 𝜖 ) 𝜖 𝑓
when 𝜖 > 0 is a parameter. 
Larger 𝐺𝑆(𝑓) → fatter probability distribution
Larger 𝜖 → thinner probability

