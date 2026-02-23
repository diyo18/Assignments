# Sorting Assignment


1. Use Big O Notation to describe the time complexity of an algorithm that takes 4N + 16 steps.

Using Big O notation, we drop the constants which include 4 in 4N and 16 in +16. With that dropped, we are left with just N so that is our time complexity = O(N).

##


2. Use Big O Notation to describe the time complexity of an algorithm that takes 2N^2.

For 2n^2, we remove the constant from the N but keep the exponent as it is not a constant. Once done, we are left with N^2 which would be our time complexity = O(N^2)

##


3. Use Big O Notation to describe the time complexity of the following function, which returns the sum of all numbers of an array after the numbers have been doubled:
   
```
def double_then_sum(array) 
	doubled_array = []

	array.each do |number| 
		doubled_array << number *= 2
	end

	sum = 0

	doubled_array.each do |number| 
		sum += number
	end
	return sum 
end

```

The code features two seperate loops. The first loop goes through every element in the array and doubles each number, which takes N steps. The second loop also goes through every element in the new array to add them together, which takes also N steps. So altogether, since the loops are seperate, the work done is 2N which in Big O notation would be just O(N).

##


4. Use Big O Notation to describe the time complexity of the following function, which accepts an array of strings and prints each string in multiple cases:
   
```
def multiple_cases(array) 
	array.each do |string|
		puts string.upcase 
		puts string.downcase 
		puts string.capitalize
	end 
end
```

The code has one loop and inside the loop it has three different print statements. One prints uppercase, another prints lowercase, and the final one prints capatilized. So for each element, there is a total of 3N work being done. With that calculauted, we can use Big-O notation and drop the constants. With that, we get O(N) as the result for the time complexity.

##



5. The next function iterates over an array of numbers, and for each number whose index is even, it prints the sum of that number plus every number in the array. What is this function’s efficiency in terms of Big O Notation?


```
def every_other(array) 
	array.each_with_index do |number, index|
		if index.even?
			array.each do |other_number|
            	puts number + other_number
			end 
		end
	end 
end
```

The following code has one loop that runs N times based on the element the code is using. Within that loop, is another loop that runs only when the index is even so N/2 times. So in all, the total number of operations is (N/2) x N which would be N^2/2. Using Big O, we ignore the constant so the time complexity becomes O(N^2).


##
Video : 

https://github.com/user-attachments/assets/eb62152a-1788-4d2b-bc36-d3721f021347


