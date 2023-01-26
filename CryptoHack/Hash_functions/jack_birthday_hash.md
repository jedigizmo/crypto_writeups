# Jack's Birthday Hash

Category: Cryptography, 20 points.

## Jack's Birthday Hash
### Description

Given any input data, `JACK11` has been designed to produce a deterministic **bit array of length 11**, which is sensitive to small changes using the avalanche effect.

Using `JACK11`, his secret has the hash value: `JACK(secret) = 01011001101`.

Given no other data of the `JACK11` hash algorithm, how many **unique secrets** would you expect to hash to have (on average) a **50%** chance of a collision with **Jack's secret**?

This is a very Ad Hoc problem purely involving math.

# Solution

We are given an initial hash value. Thus, we have to calculate the total number of hashes needed to have at least one hash collide with the hash of Jack's secret.


> The problem can be viewed from a **birthday problem** perspective whereby you are calculating the odds of a person sharing the same birthday as you.

```math
P(B) = (H-1/H)^N
```
Probability that N people do not have the same birthday as you.

```math
P(N) = 1-(H-1/H)^N
```
Therefore, this is the probability that N people share the same birthday.

```math
P(N;H) = 1-((H-1)/H)^N
```
So, to convert the birthday problem to a hash collision problem we can think of **H** as the total number of hashes **2^n** (n = # of bits) and N being the number of strings until collision. 

> To Summarize:
```math
H = 2^n 
```
> P(N;H) = probability that a hash collision will happen
> 
> n = \# of bits


Since P(N;H) is the probability we can set:

```math
P(N;H) = 0.5 
H = 2^n = 2^11; 
```

0.5 is the probability of collision with Jack's secret that we are looking for.
(n = bit array size)

The only unknown variable becomes N, which we can now solve for.
N can be solved with Mathematica by running this function:

> Solve[1 - ((2^11 - 1)/2\^11)^x) == 0.5, x]

Answer:

`1420`






 
