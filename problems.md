## Problem 1: Activity Selection

**Problem Statement**  
You are given `n` activities with their start and end times.  
Select the maximum number of non-overlapping activities that can be performed by a single person.

Example Input:  
Start = [1, 3, 0, 5, 8, 5]  
End   = [2, 4, 6, 7, 9, 9]  

Output: 4  
(Activities at index 0, 1, 3, and 4 can be selected.)

### 🔹 Hints
1. Try to sort the activities based on something.
2. Once you choose an activity, skip all that overlap with it.

### 🔹 Brute Force Idea  
Try all possible subsets of non-overlapping activities and find the one with the maximum count.  

### 🔹 Optimized Idea  
Sort activities by end time. Always pick the earliest finishing activity that starts after the last selected one. This is a greedy strategy that guarantees an optimal solution.

### 🔹 Code Fragment
```python
activities = list(zip(start, end))
activities.sort(key=lambda x: x[1])  # Sort by end time

count = 0
last_end = 0

for s, e in activities:
    if s >= last_end:
        count += 1
        last_end = e
```

## Problem 2: Fractional Knapsack

**Problem Statement**  
Given weights and values of n items and a knapsack of capacity W, select items to maximize total value. You can take fractions of items.

Input:  
Values = [60, 100, 120], Weights = [10, 20, 30], W = 50  

Output: 240.0

### 🔹 Hints
1. What happens if you sort items by value-to-weight ratio?
2. Can you take part of an item?

### 🔹 Brute Force Idea  
Try all possible combinations and fractions of items.  

### 🔹 Optimized Idea  
Greedy strategy:
1. Calculate value/weight ratio.
2. Sort items by ratio.
3. Take as much of the highest-ratio items as possible.

### 🔹 Code Fragment
```python
items = sorted(zip(values, weights), key=lambda x: x[0]/x[1], reverse=True)

total_value = 0
for v, w in items:
    if W >= w:
        total_value += v
        W -= w
    else:
        total_value += v * (W / w)
        break
```


## Problem 3: Set Cover for Radio Broadcast

**Problem Statement**  
You want your radio program to be heard in all 50 U.S. states. You have a list of radio stations, each covering certain states. Your goal is to choose the minimum number of stations such that every state is covered at least once.

Example Input:
stations = {
    'Kone':   {'Id', 'Nv', 'Ut'},
    'Ktwo':   {'Va', 'Id', 'Nt'},
    'Kthree': {'Or', 'Nv', 'Ca'},
    'Kfour':  {'Nv', 'Ut'},
    'Kfive':  {'Ca', 'Nz'}
}

Output: A subset of stations that covers all states.
One possible answer: {'Ktwo', 'Kthree', 'Kfive'}

###🔹 Hints
A greedy approach can give a good approximation.
At each step, pick the station that covers the most uncovered states.

###🔹 Brute Force Idea
Try every possible combination of stations and select the one with the smallest number that covers all states.


###🔹 Optimized Idea
Use a greedy algorithm:
While there are uncovered states:
Choose the station that covers the largest number of remaining uncovered states.
Add that station to the final set.
Remove those states from the uncovered list.


###🔹 Code Fragment
states_needed = {'Id', 'Nv', 'Ut', 'Va', 'Nt', 'Or', 'Ca', 'Nz'}
stations = {
    'Kone':   {'Id', 'Nv', 'Ut'},
    'Ktwo':   {'Va', 'Id', 'Nt'},
    'Kthree': {'Or', 'Nv', 'Ca'},
    'Kfour':  {'Nv', 'Ut'},
    'Kfive':  {'Ca', 'Nz'}}

final_stations = set()
while states_needed:
    best_station = None
    states_covered = set()
    for station, states in stations.items():
        covered = states_needed & states
        if len(covered) > len(states_covered):
            best_station = station
            states_covered = covered
    if best_station:
        final_stations.add(best_station)
        states_needed -= states_covered

print(final_stations) 



## Problem 4: Job Sequencing for Maximum Profit

**Problem Statement**  
You are given n jobs where each job has a deadline and a profit, if it is completed before or on its deadline. Each job takes exactly 1 unit of time. Your task is to schedule jobs to maximize total profit.

Input:  
Jobs = [(id=A, deadline=2, profit=100),  
        (id=B, deadline=1, profit=19),  
        (id=C, deadline=2, profit=27),  
        (id=D, deadline=1, profit=25),  
        (id=E, deadline=3, profit=15)]  

Output: Total Profit = 142 
(Jobs A, C, E)

### 🔹 Hints
1. Schedule high-profit jobs first.
2. Always place each job in the latest available time slot before its deadline.

### 🔹 Brute Force Idea  
Try all possible job orderings and time slots to find the one with the highest profit.  

### 🔹 Optimized Idea  
1. Sort jobs by profit descending.
2. For each job, find the latest free time slot ≤ deadline.
3. Use a boolean array to track occupied time slots.

### 🔹 Code Fragment
```python
jobs = [('A', 2, 100), ('B', 1, 19), ('C', 2, 27), ('D', 1, 25), ('E', 3, 15)]
jobs.sort(key=lambda x: x[2], reverse=True)  # Sort by profit

n = max(job[1] for job in jobs)  # Max deadline
slots = [False] * n
total_profit = 0
for job in jobs:
    for t in range(min(n, job[1]) - 1, -1, -1):  # Find latest free slot
        if not slots[t]:
            slots[t] = True
            total_profit += job[2]
            break
print(total_profit)




