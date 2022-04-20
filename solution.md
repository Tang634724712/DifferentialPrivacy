## Task 1
**Suppose the size of the Excel data is public information, gender and heighet are what we can change, and the weight is private sensitive information**
Linear regression is a way to model a relationship between two sets of variables. 

The equation has the form Y= a + bX, where Y is the dependent variable (that’s the variable that goes on the Y axis), 
X is the independent variable (i.e. it is plotted on the X axis), b is the slope of the line and a is the y-intercept.

The first step in finding a linear regression equation is to determine if there is a relationship between the two variables. 
The implementation code is shown in the ipynb file.

## Task2
1. Since the information we need to protect is the sensitive information - Weight, we don't need to make noises to the height and the size.
2. When 𝑓(𝑇) = ∑𝑦𝑖 = ∑𝑤𝑒𝑖𝑔ℎ𝑡𝑖, we can assume that the height distribution is 60-80, and the weight distribution is 150-250.
Weight sum changed by 20, so 𝐺𝑆(𝑓) = 20 / 10000 = 0.002
3. When 𝑔(𝑇) = ∑(𝑥𝑖*𝑦𝑖) = ∑(ℎ𝑒𝑖𝑔ℎ𝑡*𝑖𝑤𝑒𝑖𝑔ℎ), we can assume that the height distribution is 60-80, and the weight distribution is 150-250.
weight*height's sum change by  20 * 100 = 2000
𝐺𝑆(𝑔) = 2000 / 10000 = 0.2
4. The noise parameters for both can be 0.1.
For ∑𝑦𝑖, 𝐺𝑆(𝑓) / 𝜖  = 0.002 / 0.1 = 0.0002
For ∑𝑥𝑖𝑦i, 𝑔(𝑇) / 𝜖 = 0.2 / 0.1 = 0.02

## Task3
No. As we get a different line for each choice of random ϵ, we are interested in what happens on average.
The result can be worse but no significance if we did reasonable assumption on the height and weight.

## Task4
1. The data scientist can use stratified sampling to determine the smaller data size.
For example, get 7000 records where male 3500 and female 3500 respectively.
2. We can divide the dataset into 10 intervals according to the weight, and then transfer the weight information into interval information, then calculate the population of each interval.
In each interval, use $\delta$ to select the possibly smallest dataset to make the people's information in the interval similar.
In the end, return the data sum of the 10 intervals.
3. When t = 100, it means the utility(obtained from exponential mechanism) > the utility(obtained from the correct report) - the difference in utilities.
It shows that exponential mechanism can make the result be close as much as possible when using two adjancent data.
4.  SmallDB algorithm will give us a good result because it filters some useless data by sampling.

## Task5
SmallDB algorithm will give a a good result.
Reason: 
The Laplacian mechanism simply adds noise to the logarithm, and how the noise is generated will have a great impact on the linear regression results.
Through sampling, smallDB filters the influence of some datasets on the whole, so it can get better results.
