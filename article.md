# Variance and Standard Deviation Variance and standard deviation are measures of spread in a dataset.

::::::::::::::::::::::::::::::::### Variance and Standard Deviation 

#### Variance and standard deviation are measures of spread in a dataset.
Imagine you're working in a business setting, and your manager
confidently asserts that 12% of customers leave the company each month.
Or perhaps you're running a call center, and your boss believes that
agents spend an average of 12 minutes on each call. These assumptions
form the foundation for decisions and policies, but how do you determine
if they're accurate? The answer lies in conducting statistical tests,
specifically T-tests, and leveraging standard deviation to evaluate
confidence intervals.

We'll explore:

- How to test your manager's claims using customer churn or call center
  data.
- The role of confidence intervals in validating or rejecting
  hypotheses.
- A step-by-step guide to interpreting the results.


### Scenario 1: Testing Customer Churn
#### The Problem
Your manager claims that the customer churn rate is **12%**. To validate
this, you:

1.  [Gather a sample dataset of churn rates.]
2.  [Calculate the sample mean and standard deviation.]
3.  [Conduct a **T-test** to determine if the sample data supports the
    manager's claim.]

#### Steps to Solve
**Define Hypotheses**:

- Null Hypothesis (H_0​): The churn rate is 12%.
- Alternative Hypothesis (H_1): The churn rate is not 12%. (in this
  case it could be higher or lower than 12%, we don't define which way
  in this version of the test.

**Collect and Analyze Data**: Assume the following sample data (churn
rates in percentage):

Sample Data: \[10,13,11,14,15,12,9,16\]

- Mean: 12.5%
- Standard Deviation: 2%

**Conduct T-Test**: Use the formula for the T-statistic:

1.  [Compute the T-value and compare it to the critical T-value for a
    95% confidence level.]

**Interpret Results**:

- If the T-value exceeds the critical value, reject H_0H and conclude
  the churn rate is not 12%.
- Otherwise, we fail to reject H_0​ and conclude there is not sufficient
  evidence to refute the manager's claim.
::::### Scenario 2: Call Center Analysis 

#### The Problem
Your boss believes that call agents spend an average of **12 minutes**
on calls. After conducting a survey, you find:

- Sample Mean: 17 minutes
- Standard Deviation: 2 minutes
- Sample Size: 30 calls

#### Steps to Solve
**Set Up Hypotheses**:

- H_0​: Average call time = 12 minutes.
- H_1: Average call time ≠ 12 minutes.

**Understand the Standard Deviation**:

- **1 Standard Deviation**: 12+2=1412 + 2 = 1412+2=14 (68% of data
  within this range).
- **2 Standard Deviations**: 12+4=1612 + 4 = 1612+4=16 (95% of data
  within this range).

**Interpret the Survey Results**: The observed mean (17 minutes) is more
than 2 standard deviations away from the hypothesized mean (12 minutes).
Using a 95% confidence level:

- The critical threshold is ±1.96 standard deviations.
- Since 17 minutes exceeds this threshold, reject H_0​.
::::### Visualizing the Results 

Let's visualize the concept using a **normal distribution curve**. The
hypothesized mean is **12 minutes**, and the standard deviation is **2
minutes**.


```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import norm

# Define parameters
mean = 12
std_dev = 2
x = np.linspace(mean - 4 * std_dev, mean + 4 * std_dev, 100)
y = norm.pdf(x, mean, std_dev)

# Plot the normal distribution
plt.plot(x, y, label="Normal Distribution", color="blue")

# Add critical values (±1.96 standard deviations)
plt.axvline(mean + 1.96 * std_dev, color="red", linestyle="--", label="Critical Value (Upper)")
plt.axvline(mean - 1.96 * std_dev, color="red", linestyle="--", label="Critical Value (Lower)")

# Add observed value (17 minutes)
plt.axvline(17, color="green", linestyle="-", label="Observed Value (17 min)")

plt.title("Call Time Distribution: Hypothesized vs. Observed")
plt.xlabel("Call Time (minutes)")
plt.ylabel("Probability Density")
plt.legend()
plt.savefig("call_time_dist.png")
plt.show()
```

### Confidence Intervals: Upper and Lower Bounds
Confidence intervals are another way to validate assumptions.

Using the call center example:

- Mean (x_bar): 17 minutes
- Standard Deviation (sd): 2 minutes
- Sample Size (n): 30

```python
import scipy.stats as stats
# Calculate confidence interval
n = 30
sample_mean = 17
sample_std = 2
confidence_level = 0.95
alpha = 1 - confidence_level
t_critical = stats.t.ppf(1 - alpha / 2, df=n - 1)
margin_of_error = t_critical * (sample_std / np.sqrt(n))
lower_bound = sample_mean - margin_of_error
upper_bound = sample_mean + margin_of_error
print(f"Confidence Interval: ({lower_bound:.2f}, {upper_bound:.2f})")
```

Output:

Confidence Interval: (16.28, 17.72)
::::### Key Takeaways 

**Standard Deviation and Confidence Intervals**:

- Standard deviation defines the range of expected values around a
  mean.
- Confidence intervals provide upper and lower bounds for the true
  mean.

**T-Tests**:

- T-tests compare the observed mean to a hypothesized mean.
- Reject or fail to reject the null hypothesis based on the
  T-value.

**Practical Applications**:

- Use these techniques to validate business claims, such as customer
  churn rates or agent call times.
- Visualize data to support decision-making.
::::Statistical tests, confidence intervals, and visualizations help us
answer practical questions about things like customer churn, call center
performance, or policy adherence.

**Variance** measures the average squared deviation from the mean.

**Standard Deviation** is the square root of variance, providing a
measure of spread in the same units as the data.

#### Formula:
For a sample:

1.  [**Variance**:]
2.  [**Standard Deviation**:]

Where:

- x_i​ = each data point
- x_bar = sample mean
- n = number of data points
::::#### Ingredients: 

- A dataset (list of numbers).
- Python libraries: `statistics`,
  `math`, or basic Python
  calculations.
::::#### Instructions in Python: 

**Import necessary libraries**:

```python
import statistics as stats 
import math
```

**Step 1: Define your dataset:**
`data = [3, 21, 98, 203, 17, 9]`

**Step 2: Calculate the mean**:

``` 
mean = sum(data) / len(data) 
print(f"Mean: {mean}")
```

**Step 3: Calculate variance manually**:

``` 
squared_deviations = [(x - mean) ** 2 for x in data] 
variance = sum(squared_deviations) / (len(data) - 1) 
print(f"Variance: {variance}")
```

**Step 4: Calculate the standard deviation**:

``` 
std_dev = math.sqrt(variance) 
print(f"Standard Deviation: {std_dev}")
```

**Step 5: Use Python's** **`statistics`**
**module for faster calculation**:

``` 
variance = stats.variance(data) 
std_dev = stats.stdev(data)  
print(f"Variance (using stats): {variance}") 
print(f"Standard Deviation (using stats): {std_dev}")
```
::::#### Full Code: 

```python
import statistics as stats
import math
```

``` 
data = [3, 21, 98, 203, 17, 9]
```

``` 
# Manual calculation
mean = sum(data) / len(data)
squared_deviations = [(x - mean) ** 2 for x in data]
variance = sum(squared_deviations) / (len(data) - 1)
std_dev = math.sqrt(variance)
print(f"Mean: {mean}")
print(f"Variance: {variance}")
print(f"Standard Deviation: {std_dev}")
# Using statistics library
print(f"Variance (using stats): {stats.variance(data)}")
print(f"Standard Deviation (using stats): {stats.stdev(data)}")
```
::::#### Output Example: 

For the dataset `3, 21, 98, 203, 17, 9`:

- **Mean**: 58.5
- **Variance**: 4760.3
- **Standard Deviation**: 69.0
::::::::::::::::::::::::::::::::::::::::By [Kyle Jones](https://medium.com/@kyle-t-jones) on
[December 31, 2024](https://medium.com/p/dfd1c8fce115).

[Canonical
link](https://medium.com/@kyle-t-jones/variance-and-standard-deviation-dfd1c8fce115)

Exported from [Medium](https://medium.com) on November 10, 2025.
