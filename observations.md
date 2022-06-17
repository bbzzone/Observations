# Index
1. [gcd/factors/lcm](#gcd)
2. [Bitwise](#Bitwise-Operators)
3. [](#)


## gcd

gcd can be calculated with Euclidean's algorithm

1. gcd(a, b):
   factors of abs(a-b)
   [this question](https://www.codechef.com/problems/DISTGCD)
2. gcd(N-a, a) -> a:
   moreover minimum value of gcd(N-a, a)+lcm(N-a, a) will be N.
   every value of a or N-a which will be a factor of N is able to get the value N as answer.
   [editorial](https://discuss.codechef.com/t/optpairs-editorial/101602)
   [question](https://www.codechef.com/problems/OPTPAIRS)

3. Calculating factors of a Number
   - **Trial Division**: try dividing all the numbers with N. if reminder is 0 than it is a factor.
      - A number is divisible by 1 and itself. Greatest factor other than itself can be N/2. So we don't have to look any value greater than N/2.
   - **Factors of a number always exist in pairs also known as co-factors** If n is divisible by `A`, than their will be a factor of n `B`. So that `A*B == n`
   - Algorithm below will compute all the factors of `a` which is 625 in this case with a running time complexity of O(sqrt(n))
   ```python
   a = 625
   factors = [625]
   for i in range(1,math.sqrt(a)+1):
      if (a%i == 0):
         factors.append(i)
         # To avoid adding a value twice. In this case 25.
         if (i != int(math.sqrt(a))):
            factors.append(n/i)
   ```

4. LCM of 2 numbers `a, b`  will be `LCM(a, b) = (a*b)/GCD(a, b)`

## Bitwise Operators

1. For a problem where we have to equate the given number of values, We can equate bits at each position to achieve that. example [problem](https://www.codechef.com/submit/MAKEQUAL)

2. xor of any four numbers starting from any even number will be 0, because all the 4 bits are going to cancel themselves to make 0 as final bit.

3. For the [problem](https://www.codechef.com/problems/PERMAND), to create 2 permutations `A, B`  where $A_{i}$ & $B_{i}$ will be equal for the whole permutation (i is the index of the array)
   
   - As permutation will contain 1 as an element and as `&` of 1 (for any value) can yield 0 or 1 only, the constant value we can achieve by doing $A_{i}$ & $B_{i}$ is 0 or 1.
   
   - As permutations with size 2 or above will also have even elements and `&` of even element can never be 1, So the only constant value we can achieve is 0.
   
   - So to turn an odd element to 0 we need an even element. So for `k` odd elements we need `k` even elements
   
   - To turn `0b1001` to 0 we need `0b0110` adding which will produce `0b1111`. So for `0b1001`(9), one need `0b1111 - 0b1001` (15-9) which is `0b0110`(6). So for a value `a` having `n` bits, it's counter element we need will be ($2^{n}-1$)-a.









