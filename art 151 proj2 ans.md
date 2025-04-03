## Interval Partitioning Problem

### Problem Statement
We are given a set of intervals (each representing a lecture with a start time and a finish time). The goal is to assign each lecture to a classroom such that no two lectures in the same classroom overlap. We want to use the minimum number of classrooms possible.

### Greedy Algorithm Intuition
A greedy algorithm makes the best local decision at each step, hoping these choices lead to an overall optimal solution. In the interval partitioning problem, the key observation is that the minimum number of classrooms needed equals the maximum number of lectures that overlap at any point in time (this is called the "depth").

### How the Greedy Algorithm Works
1. **Sort the lectures by start time.**  
   This ensures we process lectures in the order they begin.

2. **Process each lecture in order:**
   - For each lecture, check if it can be assigned to an existing classroom. A classroom is available if the lecture's start time is greater than or equal to the finish time of the last lecture scheduled in that room.
   - If a classroom is available, assign the lecture there.
   - If no classroom is free, open a new classroom and assign the lecture to it.

### Pseudocode

```python
def interval_partitioning(lectures):
    # lectures: list of tuples (start, finish)
    lectures.sort(key=lambda lecture: lecture[0])  # Sort by start time
    classrooms = []  # Each classroom is represented as a list of lectures
    
    for lecture in lectures:
        assigned = False
        for room in classrooms:
            # Check if the current lecture can be scheduled in this room.
            # The room is available if the lecture's start time is at least 
            # as large as the finish time of the last lecture in that room.
            if lecture[0] >= room[-1][1]:
                room.append(lecture)
                assigned = True
                break
        # If no room was found, open a new classroom.
        if not assigned:
            classrooms.append([lecture])
    
    return classrooms
```


## Optimizing Interval Partitioning

**Problem Statement:**  
Given a set of lectures (intervals) with start and finish times, assign each lecture to a classroom so that no two lectures in the same classroom overlap, using the minimum number of classrooms.

**Observation:**  
The minimum number of classrooms required is equal to the maximum number of lectures overlapping at any moment (this is called the "depth" of the intervals).

**Optimal Greedy Algorithm:**  
1. **Sort the lectures by start time.**  
2. **Use a min-heap** to keep track of finish times of the currently assigned classrooms.
3. **For each lecture:**
   - If the earliest finishing lecture (top of the heap) ends on or before the start of the current lecture, then that classroom is free. Remove its finish time from the heap.
   - Add the current lecture’s finish time to the heap.
4. **The number of classrooms required** is the size of the heap after processing all lectures.

**Pseudocode:**

```python
import heapq

def interval_partitioning(lectures):
    # lectures: list of tuples (start, finish)
    lectures.sort(key=lambda lecture: lecture[0])
    heap = []  # min-heap to store finish times

    for start, finish in lectures:
        if heap and heap[0] <= start:
            heapq.heappop(heap)  # Reuse an available classroom
        heapq.heappush(heap, finish)
    
    return len(heap)
