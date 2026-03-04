# Sorting Assignment

---

## 1. Proof that, under the average-case scenario, the insertion sort has a time complexity of O(N^2)

### Answer
For average case scenario, we can assume that it compares half of the available elements. So we can visualize it by thinking of

1/2 (1+2+3+...+(N-1))

This is just showing the increasing amount of comparisons that the sort makes once the element count starts increasing until it reaches

N-1

In this case, there are about N passes, and each pass can involve up to N comparisons. So overall we can visualize this like

N × N

which gives

N^2

Since this is an average case scenario, we divide it by 2 so it would be

N^2/2

but for Big O we ignore the constant and get a time complexity of

O(N^2)

---

## 2. Insertion sort normally begins with i = 1 (0-based indexing)

Let N = 5 and assume the array is in descending order (worst case).

Count operations where:
- a comparison is A[j] > key  
- a shift is A[j+1] = A[j]

a) Start the algorithm at i = 1. Verify the total operations = 20.  
b) Start the algorithm at i = 2, then i = 3. Count operations again.  
c) For (b), does the algorithm still sort the entire array? Explain.

### a)
i = 1  
Compare 4 with 5 → 1 comparison  
Shift once → 1 shift  
Moves : 2  
i = 2  
3 is compared across 2 numbers → 2 comparisons  
Shifted twice → 2 shifts  
Moves : 4  
i = 3  
2 is checked across 3 numbers → 3 comparisons  
Shifted 3 times → 3 shifts  
Moves : 6  
i = 4  
1 is checked across 4 numbers → 4 comparisons  
Shifted 4 times → 4 shifts  
Moves : 8  
Adding everything up:  
2 + 4 + 6 + 8 = 20  
We can say that 20 is correct.

### b)
Starting from I = 2  
i = 2  
3 is compared across 2 numbers → 2 comparisons  
Shifted twice → 2 shifts  
Moves : 4  
i = 3  
2 is checked across 3 numbers → 3 comparisons  
Shifted 3 times → 3 shifts  
Moves : 6  
i = 4  
1 is checked across 4 numbers → 4 comparisons  
Shifted 4 times → 4 shifts  
Moves : 8  
In total 18 steps  
Starting from I = 3  
i = 3  
2 is checked across 3 numbers → 3 comparisons  
Shifted 3 times → 3 shifts  
Moves : 6  
i = 4  
1 is checked across 4 numbers → 4 comparisons  
Shifted 4 times → 4 shifts  
Moves : 8  
In total 14 steps

### c)
No, the insertion sort must start at the utmost left position. It does no retrace or go backwards once elements are skipped so you are eseentially only sorting half of your array and forgetting the rest. If you program it to start from that position, the code assumes that the ignored part is already sorted unless told otherwise.

---

## 3. The following function returns whether or not a capital “X” is present within a string. **4 pt**

```
function containsX(string) {
	foundX = false;
	for(let i = 0; i < string.length; i++) { 
		if (string[i] === "X") {
			foundX = true; 
		}
	}
	return foundX; 
}
```

### (a) What is this function’s time complexity regarding Big O Notation?

In this case, there is only one loop within the function and it operates without a break from i = 0 to the length of the string which is N. So regardless of whether the X is found earlier, the loop will still run through all the N characters so the time complexity would be O(N)


### (b) Then, modify the code to improve the algorithm’s efficiency for best- and average-case scenarios.

```
function containsX(string) {
	foundX = false;
	for(let i = 0; i < string.length; i++) { 
		if (string[i] === "X") {
			foundX = true;
      break;
		}
	}
	return foundX; 
}
```

Video : 


https://github.com/user-attachments/assets/0d564363-71df-46b0-8032-784625c5d442


