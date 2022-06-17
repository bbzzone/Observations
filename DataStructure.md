# Data Structures

1. [Basics of algorithms](#Basics-of-algorithms)
   1. [Insertion Sort](#INSERTION-SORT)
   2. [Loop Invariant](#Loop-Invariant)
   3. [Analyzing Algorithm](#Analyzing-Algorithm)
   4. [Linear Search](#Linear-Search)
   5. [Selection Sort](#Selection-Sort)
   6. [Designing Algorithms](#Designing-Algorithms)



## Basics of algorithms

#### INSERTION SORT

We start with insertion sort, which is an efficient algorithm for sorting a small number of elements. Insertion sort works the way many people sort a hand of playing cards. We start with an empty left hand and the cards face down on the table. We then remove one card at a time from the table and insert it into the correct position in the left hand. To find the correct position for a card, we compare it with each of the cards already in the hand, from right to left. At all times, the cards held in the left hand are sorted, and these cards were originally the top cards of the pile on the table.

```c
int insertion(int array[], int size){
    for (int i = 1; i < size; i++){
        int key = array[i];
        int index = i - 1;
        while (key < array[index] && index >= 0){
            array[index + 1] = array[index];
            index--;
        }
        array[index + 1] = key;
    }
    return 0;
}
```

#### Loop Invariant

To make things simple with any algorithm using loops, one should use loop invariant. Loop invariant is the simple condition:-

1. **INITIALIZATION**: which is true prior to any iteration of loop
2. **MAINTAINANCE**: which is true before any iteration of the loop and will also be true before next iteration of the loop
3. **TERMINATION**: when the loop ends it gives us a useful property that proves the algorithm to be correct. (one can say that it gives the **primary goal** ).

This is very similar to Mathematical induction where to prove a property, we use a base case and an inductive step. *Here invariant holds true before any interation is base case and invariant holds true from iteration to iteration corresponds to inductive step*. 

In insertionsort algorithm, the loop invariant is the fact that array[i] is always sorted.

1.  **INITIALIZATION** : Here at the initialization of for loop when value of i = 1, array[i] (array[1]) is sorted (although trivially).
2. **MAINTAINANCE** : Even when loop iterates, for every iteration, array[i] is always sorted.
3. **TERMINATION** : When loop terminates, the value for i will be size and sorted array will be `array[size]`. we have our array fully sorted. So our algorithm is correct.

**To create an array of elements in descending order rather than ascending order.** Just change the condition in while loop to `while (key > array[index] && index >= 0)`

#### Analyzing Algorithm

Ananlysis of any algorithm is a mean to predict resources computer requires to run the program. Occasionally, sources such as memory, cpu and most importantly computational time.

Analyzing Algorithms needs some mathematical tools like combinatrics, probability theory and algebra

##### Analyzing Insertion Sort Algorithm

In general case runnig time of a program is directly proportional to the input size it is given. While considering input size as a measure for time complexity, one should know that size for different problems is calculated differently. 

- For mutiplication size considered is the size of the binary representation of the number.
- For an array size will be the number of elements in the array.
- For a graph size will be determined by number of vertices and edges in the graph

for any code, the running time will be the sum of times taken by all of the instructions.

```c
for (int i = 1; i < size; i++){						c1		size
        int key = array[i];							c2		size-1						
        int index = i - 1;							c3		size-1
        while (key < array[index] && index >= 0){	c4		1+2+3...size-1
            array[index + 1] = array[index];		c5		1+2+3...size-2
            index--;								c6		1+2+3...size-2
        }
        array[index + 1] = key;						c7		size-1
    }
```

The total running time for this algorithm an be computed as sum of time taken by each instruction. 

In above code block after the code $c_i$ represents the time a single instruction in that line will take and in the very next column there is another value which will tell how much time each instruction will take. So the total time program take will be given as follow:
$$
c_1(size) + c_2(size-1) + c_3(size-1) + c_4 \sum_{i=1}^{size-1} t_i + c_5 (\sum_{i=1}^{size-2} t_i) + c_6 (\sum_{i=1}^{size-2} t_i) + c_7 (size-1)
$$
There are some possible situation where this algorithm is tested.

1. The Best case scenario (when whole array is already sorted)
2. Worst case scenario (when array is reverse sorted)

**In Best case scenario while loop will never run because key element will always be greater than it's previous element so time complexity will reduce down as:**
$$
c_1(size) + c_2(size-1) + c_3(size-1) + c_4 (size_1) + c_5 (0) + c_6(0) + c_7(size-1) \\ 
= size (c_1 + c_2 + c_3 + c_4 + c_7) - (c_2 + c_3 + c_4 + c_7) \\
= an - b
$$ {best case}
which can be represented as $an-b$. So the time complexity of insertion sort for best case scenario can be said as $O(n)$. 

**But for the worst case scenario (when array is reverse sorted)**.  On solving values with $c_4, c_5, c_6$ 
$$
c_4 (\frac{n-2}{2})(n-1+1) = c_4(\frac{n^2-2}{2})
$$
So on solving the whole equation it will be in the form of a quadratic equation like 
$$
T(x) = ax^2 + bx + c
$$

##### Order of Growth/ Rate of Growth

In reality **Order of growth** is something we are intersted in when talking about time complexity of any algorithm. To get order of growth we only taking leading term of the formula. Here for the equation $ax^2+bx+c$, order of growth will be given as $\theta(x^2)$. 

**For now consider Big O as upper bound and Big theta as tight bound (upper bound and lower bound)** 

Big O usually represents that the given algorithm can't get worst than this. So for a algorithm with `O(n)` upper bound can be anything above `O(n)`. As insertionsort runs at worst case with $O(n^2)$, It won't be wrong to say that it has a time complexity of $O(n^3)$ or anything more than $O(n^2)$, because there is no restriction on upper bound for Big O notation. 

- To say equation $T(x)=ax^2 + bx+c$ is asymptotically equal to $x^2$ in mathematical way, one can use $T(x)\sim{x^2}$.

#### Linear Search

Linear search is the algorithm to find an element in a given array by iterating over all the elements

```c
int linear_search(int array[], int size ,int node){
    for (int i = 0; i < size; i++){
        if (array[i] == node) return i;
    }
    return -1;
}
```

This maintains a loop variant which says **array[i] doesn't contains the node in it**

Time complexity of this algorithm is $O(n)$ as we have to iterate over the array to find the value in worst case. 

#### Selection Sort

This is the sorting algorithm very similar to that of Insertion Sort. In this algorithm, array is iterated once to find the minimum of all the numbers and than it is placed at very 1st place.

```c
int selection_sort(int array[], int size){
    // invariant: array[i] is always sorted
    for (int i = 0; i < size-1; i++){
        int min = i;
        int index = i+1;
        while (index < size){
            if (array[index] < array[min]) min = index;
            index++;
        }
        int tmp = array[min];
        array[min] = array[i];
        array[i] = tmp;
    }
    return 0;
}
```

Unlike insertion sort, selection sort algorithm always runs with a time complexity of $O(n^2)$. This is due to the fact that while loop will always runs to find the minimum value.

**Here Loop Invariant says that array[i] will always be sorted**. This is true before any iteration of the loop and is always true during all iterations and is true when loop ends.

#### Designing Algorithms

There are many ways one can design algorithms. In insertionsort or selection sort we simply used **incremental approach**, but now we can try do the same with **divide and conqure approach.** The advantage of **divide and conquer approach** is that it's time complexity is less than the **incremental approach**. 

##### Divide and Conquer Approach

Many useful algorithms are recursive in nature, what they do is divide the problem into subprolems which are similar than deal with them by recursively calling them. These type of algorithms works in 3 steps:

- **Divide** the problem into subproblems which are smaller instances of the same problem
- **Conquer** the subproblems by solving them recursively.
- **Combine** the solutions of subprolems to get the solution of the problem.

**Merge Sort** follows the same approach to sort values. 

1. **Divide** the array of size n into $\frac{n}{2}$ 
2. **Sort** the 2 subsequences recursively using mergesort
3. **Combine** the 2 sorted subsequences to get the answer.

**Stopping condition or base condition** for mergesort will be when length of the sorted sequence will be 1 as it will be already sorted. The key operation in mergesort is to combine the 2 sorted arrays which will be done by another function **merge.** 



