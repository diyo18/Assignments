## Tasks
The following exercises provide you with the opportunity to practice with space constraints.

1. Following is the 'Word Builder' algorithm. Describe its space complexity in terms of Big O.

```
function wordBuilder(array) { 
		let collection = [];
		for(let i = 0; i < array.length; i++) { 
				for(let j = 0; j < array.length; j++) {
						if (i !== j) {
								collection.push(array[i] + array[j]);
						}
				}
		}
		return collection; 
}
```
Answer : For this algorithm, the space complexity would be O(n^2). This is because the function stores every pair between i and j, but with n input elements, that means i is checked across every j which gives n^2 total pairs. Some pairs are skipped but that equals just N which is small in comparison to N^2 so it is not included.

2. Following is a function that reverses an array. Describe its *space* complexity in terms of Big O:

```
function reverse(array) { 
		let newArray = [];
		for (let i = array.length - 1; i >= 0; i--) { 
				newArray.push(array[i]);
		}
		return newArray;
}
```
Answer : For this function, we have a loop grabbing values from an input array and moving them into a new array. No other modifications are done, so we end up pulling N elements from initial array into the new one. No other things being interacted with. So, in the end, we get N elements stored which means the space complexity is O(n).

3. Create a new function to reverse an array that takes up just $O(1)$ extra space.

```
#include <vector>
#include <algorithm>
using namespace std;

void reverseFunction(vector<int>& array) {
  
  int left = 0;
  int right = array.size() - 1;
  while (left < right) {
    swap(array[left], array[right]);
    left++;
    right--;
  }
}

```
Answer : This algorithm takes an array. Creates a counter for the beginning of the array and then end. With that, it runs a while loop which swaps the two ends and then increases/decreases their count to capture the next ones. And because this is swapping the elements within the original array, its space complexity is only O(1)

4. Following are three different implementations of a function that accepts an array of numbers and returns an array containing those numbers multiplied by 2. For example, if the input is [5, 4, 3, 2, 1], the output will be [10, 8, 6, 4, 2].

````
function doubleArray1(array) { 
	let newArray = [];

	for(let i = 0; i < array.length; i++) { 
		newArray.push(array[i] * 2);
	}
	return newArray; 
}


function doubleArray2(array) {
	for(let i = 0; i < array.length; i++) {
  	array[i] *= 2;
  }
	return array; 
}


function doubleArray3(array, index=0) { 
	if (index >= array.length) {
  return;
}
  array[index] *= 2;
  doubleArray3(array, index + 1);
	return array; 
}
````

Fill in the table that follows to describe the efficiency of these three versions in terms of both time and space:

| Version    | Time complexity | Space complexity |
| ---------- | --------------- | ---------------- |
| Version #1 | O(N)               | O(N)               |
| Version #2 | O(N)               | O(1)                |
| Version #3 | O(N)              | O(N)              |

Version 1 creates a new array and pushes the values onto it. That means the Time and Space Complexities are only N because it is running/storing through all elements once. Version 2 directly changes the elements within the array. So time complexity still has to check all N elements so it would be O(N) but space complexity does not change since it is directly changing the input. Version 3 takes an array and an index and doubles the values based on index through recursion. So the change are happening in the original array but since its done through recursion, we get frames added to the call stack which is counted as N memory. So time and space complexity would be O(N)
