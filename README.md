# Scheduling_CPM_PERT

This Python project provides tools for project scheduling and analysis using the Critical Path Method (CPM), Program Evaluation and Review Technique (PERT), and Monte Carlo Simulation. It allows you to estimate project durations, identify critical paths, and assess project completion probabilities.

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
  - [Input](#input)
  - [The Critical Path Method (CPM)](#the-critical-path-method-cpm)
  - [The Program Evaluation and Review Technique (PERT)](#the-program-evaluation-and-review-technique-pert)
  - [Monte Carlo Simulation](#monte-carlo-simulation)

## Installation <a name="installation"></a>

To use this project, you'll need to install the required Python packages. You can do this using pip:

```bash
pip install pertdist pandas numpy matplotlib
```

## Usage <a name="usage"></a>

### Input <a name="input"></a>

Before using the project, provide the following input:

- `activities`: A list of activity names.
- `optimistic`: A list of optimistic durations for each activity.
- `likely`: A list of likely durations for each activity.
- `pessimistic`: A list of pessimistic durations for each activity.
- `predecessor`: A list of predecessors for each activity, separated by commas. Use '-' for activities with no predecessors.

Here's an example input:

```python
activities = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j']
optimistic = [135, 160, 15, 105, 100, 40, 30, 140, 110, 85]
likely = [150, 180, 30, 120, 120, 60, 60, 150, 120, 90]
pessimistic = [180, 220, 45, 140, 135, 70, 75, 185, 145, 125]
predecessor = ['-', '-', 'b', 'c', 'a,c', 'd', 'e,f', 'd', 'h', 'i']
```

### The Critical Path Method (CPM) <a name="the-critical-path-method-cpm"></a>

The Critical Path Method (CPM) calculates project duration based on the provided input and identifies the critical path. It provides the following functionality:

#### Create a DataFrame of Input

```python
data = {'Activity': activities, 
        'Optimistic_a': optimistic,
        'Most_likely_m': likely,
        'Pessimistic_b': pessimistic,
        'Predecessor': predecessor}
df_pm = pd.DataFrame(data)
```

#### Calculate Project Duration

```python
def pro_dur_cpm(df):
    # ... (calculations)
    return max(pro_end)

project_duration = pro_dur_cpm(df_pm)
print('The project duration as calculated by CPM is: ' + str(project_duration))
```
[aoa3.drawio.pdf](https://github.com/arora-amit37/project_management_cpm_pert/files/12501609/aoa3.drawio.pdf)

### The Program Evaluation and Review Technique (PERT) <a name="the-program-evaluation-and-review-technique-pert"></a>

The Program Evaluation and Review Technique (PERT) calculates project duration using a probabilistic approach. It provides the following functionality:

#### Create a DataFrame of Input (Similar to CPM)

```python
data = {'Activity': activities, 
        'Optimistic_a': optimistic,
        'Most_likely_m': likely,
        'Pessimistic_b': pessimistic,
        'Predecessor': predecessor}
df_pm = pd.DataFrame(data)
```

#### Calculate Project Duration using PERT Distribution

```python
def pro_dur_pert(df):
    # ... (calculations)
    return max(pro_end)

project_duration = pro_dur_pert(df_pm)
```

### Monte Carlo Simulation <a name="monte-carlo-simulation"></a>

Monte Carlo Simulation is used to assess project completion probabilities based on the PERT distribution. It includes the following steps:

1. Define the number of simulations and a random seed.
2. Simulate project durations and store them in a list.
3. Plot a histogram of project durations.
4. Calculate the probability of finishing the project by a specified deadline.

Here's an example of how to perform Monte Carlo Simulation:

```python
seed = 869080
simulations = 1000

np.random.seed(seed)
durations = []
for i in range(simulations):
    # ... (simulations)
```

#### Histogram of Project Durations

```python
plt.hist(durations, bins=30, edgecolor='black')
plt.xlabel('Project Duration')
plt.ylabel('Frequency')
plt.title('Histogram of Project Durations based on the PERT distribution')
plt.show()
```
![histogram](https://github.com/arora-amit37/pm_cpm_pert/assets/50020662/242e8326-a6d4-4030-93f9-788544d19da6)

#### Calculate the Probability of Meeting a Deadline

```python
deadline = 708

ecdf = np.cumsum(np.sort(durations)) / len(durations)
probability = np.searchsorted(np.sort(durations), deadline, side='right') / len(durations)

print('There is ' + f"{probability*100:.2f}" + '% probability that the project will be finished in ' + str(deadline) + ' days.')
```
