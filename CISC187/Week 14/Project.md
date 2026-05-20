# Project 

## Task 1

You’re working on software that analyzes sports players. Following are two arrays of players of different sports:

```
basketball_players = [
      {first_name: "Jill", last_name: "Huang", team: "Gators"},
      {first_name: "Janko", last_name: "Barton", team: "Sharks"},
      {first_name: "Wanda", last_name: "Vakulskas", team: "Sharks"},
      {first_name: "Jill", last_name: "Moloney", team: "Gators"},
      {first_name: "Luuk", last_name: "Watkins", team: "Gators"}
]

football_players = [
      {first_name: "Hanzla", last_name: "Radosti", team: "32ers"},
      {first_name: "Tina", last_name: "Watkins", team: "Barleycorns"},
      {first_name: "Alex", last_name: "Patel", team: "32ers"},
      {first_name: "Jill", last_name: "Huang", team: "Barleycorns"},
      {first_name: "Wanda", last_name: "Vakulskas", team: "Barleycorns"}
]
```

If you look carefully, you’ll see that some players participate in more than one sport. Jill Huang and Wanda Vakulskas play both basketball *and* football.

You are to write a function that accepts two arrays of players and returns an array of the players who play in *both* sports. In this case, that would be:

`["Jill Huang", "Wanda Vakulskas"]`

While there are players who share first names and players who share last names, we can assume there’s only one person who has a particular *full* name (meaning first *and* last name).

We can use a nested-loops approach, comparing each player from one array against each player from the other array, but this would have a runtime of $O(N * M)$. 

**Your job is to optimize the function so that it can run just $O(N + M)$.**

ANSWER : 

```
#include <iostream>
#include <vector>
#include <string>
#include <unordered_set>

// For this code, I created a struct to receive the data of the players.
// From there, I run a loop that combines the first array of first and last names and store that in a hash set. This takes O(N).
// With that saved, I then run another loop that looks at the second array. This takes O(M)
// There is an if statement within that loop to check if names match and if they do, that first and last name gets deposited in the result variable.
// With that, I was able to get a time complexity of O(N+M).

struct Playerinfo {

    std::string first_name;
    std::string last_name;
    std::string team;
};
// function created here with the two arrays as parameters
std::vector<std::string> findSamePlayers(std::vector<Playerinfo> basketball_players, std::vector<Playerinfo> football_players ){

    std::unordered_set<std::string> tempMemory; // hashset to use as reference when comparing names
    std::vector<std::string> result;

    // loop to insert first array of specifically player names into hashset
    for (Playerinfo& player : basketball_players) {
        std::string fullName = player.first_name + " " + player.last_name;
        tempMemory.insert(fullName);
    }
    // loop that compares the second array across the first one which is in the hash set
    for (Playerinfo& player : football_players) {
        std::string fullName = player.first_name + " " + player.last_name;

        // if statement to see if name is in set, if it is then we save it
        if (tempMemory.find(fullName) != tempMemory.end()){
        result.push_back(fullName);
        }
        
    }

    return result;
}
```

## Task 2

You’re writing a function that accepts an array of distinct integers from 0, 1, 2, 3...up to N. However, the array will be missing one integer, and your function is to *return the missing one.*

For example, this array has all the integers from 0 to 6, but is missing the 4:

```
[2, 3, 0, 6, 1, 5]
```

Therefore, the function should return 4.

The next example has all the integers from 0 to 9, but is missing the 1:

```
[8, 2, 3, 9, 4, 7, 5, 0, 6]
```

In this case, the function should return the 1.

Using a nested-loops approach would take up to $O(N^2)$. 

**Your job is to optimize the code so that it has a runtime of $O(N)$.**

ANSWER :

```
#include <vector>

// For this algorithm, I found a formula that I used for expected sum since there is only one missing integer and there are no duplicates.
// From there, I created a for loop that added up all the values within the array.
// After that, it subtracts the actual value from the expected one which gives us our missing integer
// Since it only passes through the array once, my time complexity ends up being O(N).

// creating function with array of numbers as parameter
int FindMissingNumber (std::vector<int>& numberlist){

    int N = numberlist.size(); // counter to use in for loop
    int expectedsum = N * (N+1) / 2; // equation that calculates sum of 0 to N, 
    int actualsum = 0; 

    for (int i = 0; i < N; i++){
        actualsum = actualsum + numberlist[i]; // loops through and adds up all numbers
    }

    int missingNumber = expectedsum - actualsum; // subtract against expected sum to get the missing integer

    return missingNumber;
}
```

## Task 3

You’re working on some more stock-prediction software. The function you’re writing accepts an array of predicted prices for a particular stock over the course of time.

For example, this array of seven prices:

```
[10, 7, 5, 8, 11, 2, 6]
```

predicts that a given stock will have these prices over the next seven days. (On Day 1, the stock will close at \$10; on Day 2, the stock will close at $7; and so on.)

Your function should calculate the greatest profit that could be made from a single “buy” transaction followed by a single “sell” transaction.

In the previous example, the most money could be made if we bought the stock when it was worth \$5 and sold it when it was worth \$11. This yields a profit of $6 per share.

Note that we could make even more money if we buy and sell multiple times, but for now, this function focuses on the most profit that could be made from just *one* purchase followed by *one* sale.

Now, we could use nested loops to find the profit of every possible buy and sell combination. However, this would be $O(N^2)$ and too slow for our hotshot trading platform. 

**Your job is to optimize the code so that the function clocks in at just $O(N)$.**

ANSWER : 

```
#include <vector>

// This function only passes through the array once and checks the values during that pass which makes the time complexity O(N)

// function with array of stock prices as parameter
int FindBestProfit (std::vector<int>& stockPriceList){

    int mostProfit = 0; // variable to store the highest profit
    int N = stockPriceList.size(); // counter for array size
    int cheapestDay = stockPriceList[0]; // setting the cheapest day to the first day

    // for each day, check if it's a new cheapest or a chance to update profit
    for (int i = 1; i < N; i++){
        if (stockPriceList[i] < cheapestDay) {
            cheapestDay = stockPriceList[i]; // if it is cheaper, then it gets set as the cheapest and we move on
        }
        // if it is not cheaper, then we subtract it from the cheapest day to get profit and we store it
        else {
            int profit = stockPriceList[i] - cheapestDay;
                if (profit > mostProfit) // as we get more profits calculated, we can compare it with the highest profit to see if it needs to be swapped
                    mostProfit = profit;
        }
    }

    return mostProfit;
}
```

## Task 4

You’re writing a function that accepts an array of numbers and computes the highest product of any two numbers in the array. At first glance, this is easy, as we can just find the two greatest numbers and multiply them. However, our array can contain negative numbers and look like this:

```
[5, -10, -6, 9, 4]
```
We could use nested loops to multiply every possible pair of numbers, but this would take $O(N^2)$ time. **Your job is to optimize the function so that it’s a speedy $O(N)$.**

ANSWER : 

```
#include <vector>

// For this function, the easiest way that I thought we could do this was by finding the top 2 greatest values and bottom 2 values.
// That way I am accounting for every number when finding the product in case the negatives have a higher product than positives.
// Because this function only passes through the array once, it has a time complexity of O(N).

// function with our list of positive and negative numbers as the parameter
int FindHighestProduct (std::vector<int>& numberList){

    int N = numberList.size(); // array size for loop
    int top1; // creating variables to store top values
    int top2;

    // if statement to set the first two values within array to top. 
    if (numberList[0] >= numberList[1]){ // check for which one is greater then it assigns values top1 or 2.
            top1 = numberList[0];
            top2 = numberList[1];
     }

    else{
            top1 = numberList[1];
            top2 = numberList[0];
     }
        
    int bottom1 = top2; // setting values for bottom variables which may or may not get swapped out.
    int bottom2 = top1;

    // for loop starts at the 3rd values since first two are already used
    for (int i = 2; i < N; i++) {
        int n = numberList[i]; // creating n variable to assign current number and check

        // if and else statement to see if it is greater than the current top value then assigns accordingly
        if (n > top1){
            top2 = top1;
            top1 = n;
        }
        else if (n > top2)
            top2 = n;

        // another if statement to check if n is smaller than bottom1 or bottom 2.
        if (n < bottom1){
            bottom2 = bottom1;
            bottom1 = n;
        }

        else if (n < bottom2){
            bottom2 = n;
        }
    }   

    
    // final check by finding product of top and bottom values
    int topProduct = top1 * top2;
    int bottomProduct = bottom1 * bottom2;

    // whichever product is greater is the one that is returned
    if (topProduct > bottomProduct){
        return topProduct;
    }

    else {
        return bottomProduct;
    }
}
```

## Task 5

You’re creating software that analyzes the data of body temperature readings taken from hundreds of human patients. These readings are taken from healthy people and range from 97.0 degrees Fahrenheit to 99.0 degrees Fahrenheit. An important point: within this application, *the decimal point never goes beyond the tenth place.*

Here’s a sample array of temperature readings:

```
[98.6, 98.0, 97.1, 99.0, 98.9, 97.8, 98.5, 98.2, 98.0, 97.1]
```

You are to write a function that sorts these readings from lowest to highest.

Using a classic sorting algorithm such as Quicksort would take $O(N log N)$. However, in this case, writing a faster sorting algorithm is possible.

Yes, that’s right. Even though you’ve learned that the fastest sorts are $O(N log N)$, this case is different. Why? In this case, there are limited possibilities for the readings. In such a case, we can sort these values in $O(N)$. It may be $N$ multiplied by a constant, but that’s still considered $O(N)$.

ANSWER : 

```
#include <vector>

// For this function, I used a counting sort since there are only 21 possible values of temperature so that allows us to pass through the array once.
// Only one push happens per temperature so the time complexity is O(N)

// function using double values for decimal points with array of temps as parameter
std::vector<double> temperatureSorter(std::vector<double> tempList){

    // creating 21 slots for each value of temperature
    std::vector<int> counts(21,0);

    // for each temperature in the list, we find its place within the slot index by subtracting 97 and then multiplying by 10
    // for example, 97.1 gets turned into 97.1 - 97 = 0.1 * 10 = 1 so its slot index is 1 
    for (double temps : tempList){
        int slot = (temps - 97) * 10;
        counts[slot]++; // once we find its index, we then increase its count by 1
    }

    
    std::vector<double> result;

    // go through each slot that was created
    for(int i = 0; i <= 20; i++){
        // for every single time the slot was tallied, we push that slot through an equation to get the original temperature
        for(int j = 0; j < counts[i]; j++){
            double temp = i / 10.0 + 97.0; // original temp is found
            result.push_back(temp); // then pushed to the result variable which is later returned in order
        }
        }

    return result;
}
```

## Task 6

You’re writing a function that accepts an array of unsorted integers and returns the length of the *longest consecutive sequence* among them. The sequence is formed by integers that increase by 1. For example, in the array:

```
[10, 5, 12, 3, 55, 30, 4, 11, 2]
```

the longest consecutive sequence is 2-3-4-5. These four integers form an increasing sequence because each integer is one greater than the previous one. While there’s also a sequence of 10-11-12, it’s only a sequence of three integers. In this case, the function should return 4, since that’s the length of the *longest* consecutive sequence that can be formed from this array.

One more example:

```
[19, 13, 15, 12, 18, 14, 17, 11]
```

This array’s longest sequence is 11-12-13-14-15, so the function would return 5.

**Your job is to optimize the function so that it takes $O(N)$ time.**

ANSWER : 

```
#include <vector>
#include <unordered_set>

// For this function, I used a hash set to avoid checking every single number.
// Once I had the array of numbers in the hashset, I began by cycling through the array and subtracting from the current value.
// This was done to see whether the value was inside of a sequence or was a unique number / start of a sequence.
// For and while loops ran counters to see the length of sequence which was saved and returned at the end.
// In total, we only inserted the array once (hash set) and the rest was looking up and checking values.

int sequenceFinder(std::vector<int>& seqList){

    // creating hashset that will be used to find sequences
    std::unordered_set<int> currentSeq;
    int bestLength = 0;

    // using for loop to insert list of numbers into hash set
    for (int numbers : seqList){
        currentSeq.insert(numbers);
    }

    int N = seqList.size(); 

    
    for (int i = 0; i < N; i++){
        int currentNumber = seqList[i];
            // checks if currentNumber - 1 is not in the set. If it is not found, then it is the start of a sequence.
            if (currentSeq.find(currentNumber - 1) == currentSeq.end()){
                int seqCounter = 1; // start counter if it is the start of a sequence
                int currentValue = currentNumber;

                // this loop keeps running as long as we find currentValue + 1. If it does not, then we stop
                while (currentSeq.find(currentValue + 1) != currentSeq.end()){
                    currentValue++;
                    seqCounter++;
                }
            // when while loop ends, we check if the counter is greater than current length
            if (seqCounter > bestLength) {
                bestLength = seqCounter;
            }
        }
    }
    return bestLength;
}
```

