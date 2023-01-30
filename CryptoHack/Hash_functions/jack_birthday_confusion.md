# Jack's Birthday Confusion

Category: Cryptography, 30 points.

This is a continuation of the problem **Jack's Birthday Hash**, so I recommended starting from that writeup before coming here. 

### Description
Given no other data of the ``JACK11`` hash algorithm, how many unique secrets would you expect to hash to have (on average) a **75% chance** of a collision between **two distinct secrets**?


# Solution
### Pre-Solve
We have to calculate the total number of hashes needed to have a 75% chance of collison between exactly two distinct hashes in the set of total hashes. 


> The problem can be viewed from a **birthday problem** perspective whereby you are calculating the odds of **any** two people sharing a birthday. 

**N** is the total hash space.
After one unique hash generation, the possible hash space reduces to ****.

Therefore,

$$\frac{(N - 1)}{N}$$

Is the probability of randomly generating two unique hashes.
And your hash space reduces again to **(N - 2)**.

Following that pattern, we get the product of finite terms:


$$\frac{(N - 1)}{N} \times \frac{(N - 2)}{N} ... \frac{(N - (k-2))}{N} \times \frac{(N - (k-1))}{N}$$

$$\prod_{a = 1}^{N} \frac{(N - (k-a))}{N}$$

**k** is the number of hashes needed.
Solving this becomes difficult, but the above equation can be approximated as:

$$ e^{\frac{(-k(k-1))}{2N}} $$

Since the equation above is the probability for unique hashes, we can subtract by one to get the probability of gettting same hashes. (a.k.a. hash collision).

### Solve:
**P** = probability of a hash collision

$$ P = 1 - e^{\frac{(-k(k-1))}{2N}} $$



Since P is the probability we can set and the probability we are solving for is 75%:

$$ 0.75 = 1 - e^{\frac{(-k(k-1))}{2N}} $$

> N = hash space = $2^n$ ; n = 11(bit array length)

The only unknown variable becomes **k**, which we can now solve for.

$$ 0.75 = 1 - e^{\frac{(-k(k-1))}{2(2^{11})}} $$

k can be solved with Mathematica by running this function:

**Solve[1 - (e^(((-k)*(k - 1))/(2*(2^11)))) == 0.75, k]**

Answer:

`76`






 