# Ans1

### ***Algorithm:***
- Let $i = 0$ 
- Let an empty list be $B = [\ ]$ to store the positions of the base stations.
**While there exists an uncovered house:**
- Let $s = h_i$ be the position of the left most house that is not yet covered.
- Place a base station at position $b = s + 5$ (This base station coves all houses from $s$ up to $s + 10$)
- Append $b$ to $B$
- Advance $i$ until you find a house with $h_i > b + 5$ (That is, skip all houses covered by the base station)
Return $B$ as the set of base station positions.

**Pseudo-code**:
```python
def place_base_stations(house):
	# housese: list of unsorted house positions
	houses.sort()
	base_stations = []
	i = 0
	n = len(houses)

	while i < n:
		# Let s be the position of the left most uncovered house
		s = house[i]
		# Place a base station 5 miles to the right of s.
		b = s + 5
		base_stations.append(b)
		# Skip all houses covered by this base station.
		while i < n and houses[i] <= b + 5:
			i += 1

	return base_stations
```

***TimeComplexity***
- Sorting the houses or any sorting generally takes $O(n\log{n})$ time
- The while loop scans $n$ times as at worst it needs to go over all $n$ houses with none of them skipped.
- **Overall Time Complexity:** $O(n\log{n})$

# Ans2
