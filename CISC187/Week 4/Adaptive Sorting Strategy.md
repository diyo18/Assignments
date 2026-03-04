## Objective
The objective of this assignment is to analyze how input order affects sorting algorithm performance and to apply that analysis to make an adaptive algorithmic decision. 

---

The following are the O(N) notations of the following sorting algorithms.

|                | Best case | Average case | Worst case |
| -------------- | --------- | ------------ | ---------- |
| Selection sort | $N^2$       | $N^2$          | $N^2$        |
| Insertion sort | N           | $N^2$          | $N^2$        |

## Part A: Adaptive Sorting Selection

1. Create an array of **50 integers**.
2. Implement both sorting algorithms:
   - **Selection Sort**
   - **Insertion Sort**

3. Your program must analyze the initial ordering of the array and determine which scenario it represents (best, average, or worst) based on a **clearly defined threshold** that you assume.

4. Based on your analysis, your program should automatically choose the more appropriate sorting algorithm.

CODE : 

```
#include <iostream> 
using namespace std;

const int SIZE = 50; // sets variable Size as 50 so we can use it to create array

// function for choosing which sort is best
double analyzeArray(int arr[], int size) {
    int numberofBadPairs = 0; // create a counter to see how many pairs of numbers are unordered

    
    for (int i = 0; i < size - 1; i++) { // loop to check all numbers except final
        if (arr[i] > arr[i + 1]) { // checking whether current number is bigger than the one in front of it
            numberofBadPairs++; // if the number is bigger, add one to the count
        }
    }

    int notInOrderPercentage = ((double)numberofBadPairs / (size - 1)) * 100; // find % that are unordered

    if (notInOrderPercentage < 30) { // based on percent, the sort method is used 
        cout << "Using Insertion Sort (mismatched numbers was under 30 percent)" << endl;
    } else {
        cout << "Using Selection Sort (mismached numbers was over 30 percent)" << endl;
    }

    return notInOrderPercentage;
}

// selection sort algorithm
void selectionSort(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        int minIndex = i;
        for (int j = i + 1; j < size; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        int temp = arr[i];
        arr[i] = arr[minIndex];
        arr[minIndex] = temp;
    }
}

// insertion sort algorithm
void insertionSort(int arr[], int size) {
    for (int i = 1; i < size; i++) {
        int current = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > current) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = current;
    }
}

int main() {
    // creating the array
    int arr[SIZE] = { 
        45, 12, 78, 3, 56, 89, 23, 67, 34, 90,
        11, 55, 42, 77, 8, 19, 63, 29, 84, 51,
        6, 38, 72, 15, 48, 93, 27, 61, 5, 80,
        33, 70, 17, 44, 88, 22, 59, 9, 76, 40,
        14, 68, 31, 95, 50, 25, 83, 37, 64, 2
    };

    double percentage = analyzeArray(arr, SIZE); // analyze the array and store the percentage

    // decides which sort to use
    if (percentage < 30) {
        insertionSort(arr, SIZE);
    } else {
        selectionSort(arr, SIZE);
    }

    // prints out sorted array
    for (int i = 0; i < SIZE; i++) {
        cout << arr[i] << " ";
    }

    return 0; // kills code
}
```

Result : 

<img width="1297" height="53" alt="image" src="https://github.com/user-attachments/assets/110e5de9-0d16-4f01-a9b5-e0f8d084e20e" />


---

## Part B: Case Classification Without Sorting

Using the same threshold defined in Part A:

1. The user will input 50 integers.
2. Without actually sorting the array, your program must analyze the order of elements.
3. The program should classify the input as:
   - **Average Case**
   - **Worst Case**

The program must then display the classification result.

> No sorting should be performed in this part; only classification is required.

CODE : 

```
#include <iostream>
using namespace std;

const int SIZE = 50;

// same analyzing code from part a
void analyzeArray(int arr[], int size) {
    int numberofBadPairs = 0; // create a counter to see how many pairs of numbers are unordered

    
    for (int i = 0; i < size - 1; i++) { // loop to check all numbers except final
        if (arr[i] > arr[i + 1]) { // checking whether current number is bigger than the one in front of it
            numberofBadPairs++; // if the number is bigger, add one to the count
        }
    }

    int notInOrderPercentage = ((double)numberofBadPairs / (size - 1)) * 100; // find % that are unordered

 
    
    cout << "Out-of-order percentage: " << notInOrderPercentage << "%" << endl;

    if (notInOrderPercentage < 30) {
        cout << "Classification: Best Case" << endl;
    } else if (notInOrderPercentage <= 70) {
        cout << "Classification: Average Case" << endl;
    } else {
        cout << "Classification: Worst Case" << endl;
    }
}
int main() {
    int arr[SIZE];

  // get input for array
    cout << "Enter 50 integers: " << endl;
    for (int i = 0; i < SIZE; i++) {
        cin >> arr[i];
    }

analyzeArray(arr, SIZE);

    return 0;
}

```

Result for 50 - 1 : 

<img width="609" height="890" alt="image" src="https://github.com/user-attachments/assets/d5db2a8e-74df-46a4-bddc-9688e3f785e8" />

Result for 1 - 50 (messed up a couple of entries) : 

<img width="510" height="901" alt="image" src="https://github.com/user-attachments/assets/78821d22-b336-4b37-81b1-55ab18d58156" />


Result for 25 - 1 then 26 - 50 : 

<img width="319" height="885" alt="image" src="https://github.com/user-attachments/assets/cfbc4afe-a012-4c04-bb03-d32ac293702b" />


---


## Part C: Documentation

Provide a written explanation that includes:

- The **threshold definition** you used to differentiate between best, average, and worst cases.
- The reasoning behind your assumption.
- Why your program selects one sorting algorithm over the other in specific scenarios.
- A brief discussion of how input order affects the time complexity of Selection Sort and Insertion Sort.

Your explanation should demonstrate a clear understanding of algorithmic behavior and time complexity analysis.

Threshold Definition : 
In my process, I counted how many pairos of numbers were next to each other and speicficially the ones that were in the wrong order. If less than 30% were out of order, I called it best case, between 30 - 70% I called average case, and over 70% is worst case.

Reasoning : 
I picked 30% and 70% as it felt more fair to split the area into some what thirds for best, average, and worst case. It makes it so that everything in order is almost always in best case, opposite for worst case, and a good mix for average case.

Algorithm Selection :
The code picks insertion sort when the array is already mostly sorted due to the time compleixty for insertion sort's best case scenario. It is much faster than selection sort when the array is already or close to being fully sorted. Selection sort behaves the same no matter what so that can be reserved for average and worst case.

How Input Order Affects Time Complexity : 
Input order matters a lot for Insertion Sort but not at all for Selection Sort. If the array is already sorted, Insertion Sort runs with a time complexity of O(N) which is faster than selection sort's best case but if its completely backwards it slows down to O(N^2) because it has to move every element. Selection Sort is always O(N^2) no matter what the input looks like, so it never gets faster or slower based on the order of the array.


---




