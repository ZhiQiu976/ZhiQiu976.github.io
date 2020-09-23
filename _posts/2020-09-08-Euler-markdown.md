---
layout: post
title:  Interesting Programming Problems - the Project Euler
subtitle: Example Q&As
gh-repo: ZhiQiu976/source-codes-tech-posts
gh-badge: [star, fork, follow]
cover-img: /assets/img/banner-wood.jpg
thumbnail-img: /assets/img/photo-Euler.jpg
tags: [algorithm, string, dynamic programming, itertools]
comments: true
---

This post will talk about some interesting programming problems in the famous [Project Euler](https://projecteuler.net), which is a series of challenging mathematical 🧮 / computer programming ⌨️ problems that will require more than just mathematical insights to solve. As stated on the website, 'although **mathematics** will help you arrive at elegant and efficient methods, the use of a computer and **programming** skills will be required to solve most problems'. In the next few minutes, I'll walk you through some useful algorithms and codes that could solve `three typical mathe puzzles` 🧩 in Project Euler elegantly.

**In the discussion below I would talk about the generalized version of the original problems. The exact answers to the original problems are shown [here](https://github.com/ZhiQiu976/source-codes-tech-posts/blob/master/Euler%20Project/Euler-problem-output.ipynb).**

**You can check the `Euler Project` folder in my `Github Repo` [ZhiQiu976/source-codes-tech-posts](https://github.com/ZhiQiu976/source-codes-tech-posts) for detailed scorce codes and outputs.**

You can simply change the inputs in these .py files and get new outputs by re-running the scripts in your terminal. ✨

<br />

## [Euler Problem 8](https://projecteuler.net/problem=8)

❓ Given a 1000-digit number, what are the thirteen adjacent digits in this number that could give the greatest elementwise product? What is the value of this product?

- `Solution`: 
    - The solution logic of this problem is quite transparent: firstly get the collection of all possible **thirteen adjacent digits** in the 1000-digit number. Then calculate the **product** of each 13-digit-set. Lastly find the maximum.
    
    - This logic is quite simple to accomplish in coding. `List comprehension` could be very helpful here.
    
    - Remember to take care of data types.
     
<br />
**Codes Glimpse** 👀

```javascript
def compute(s, n):
    '''
    Function for solving Project Euler Problem 8.
    Parameters
    ----------
    s : str
        The original input string of the 1000-digit number, 
        with a line break every 50 digits.
    n : int
        Number of adjacent digits that wants to find greatest product with.
    Returns
    -------
    digits : list of int
        The n adjacent digits in the input 1000-digit number that 
        have the greatest product.
    result : int
        The value of this greatest product.
        
    '''
    
    # rearrange the original string
    xs = ''.join(s.split())
    # get the adjacent digits
    ss = [list(xs[i : i+n]) for i in range(1000 - (n-1))]
    # turn into floating number
    ss = [list(map(int, s)) for s in ss]
    # calculate productes
    products = [np.prod(s) for s in ss]
    # find the maximum
    idx = np.argmax(products)
    
    result = products[idx]
    digits = ss[idx]
    
    return digits, result
```

Clike [here](https://github.com/ZhiQiu976/source-codes-tech-posts/blob/master/Euler%20Project/Euler-problem-8.py) to check the source .py file.

<br />


## [Euler Problem 31](https://projecteuler.net/problem=31)

❓ Given a set of different denominations of coins, and a target amount of money, how many different ways can this amount of money be made using any number of coins?

- `Solution`:
    - This problem can be done itertively but this method is computationally complex.
    
    - We would use the idea of `dynamic programming` to improve programming efficiency.
    
    - The main idea is: 
        - Firstly we try only using the first denomination to achieve the amount of **[1, 2, ... , total]** and record the **number of ways**,
        
        - then add another denomination, we record the **number of ways** of using only these two denominations to achieve **[1, 2, ... , total]**,
        
            - ![Crepe](/assets/img/Screenshot-1.png)
            
            - The idea behind the above equation is that if you already have **n** ways to achieve amount **j**, the after including a new denomination **i**, you have exactly **n** ways to achieve amount **j + i**.
            
        - next repeat this process until all the denominations get included, and the very last cell would be our answer.
        
    - Note that the order of including different denominations doesn't matter here.

<br />
**Codes Glimpse** 👀

```javascript
def compute(inputs, total):
    '''
    Function for solving Project Euler Problem 31. Dynamic programming.
    Parameters
    ----------
    inputs : list of int
        The original input value set.
    total : int
        The target total sum.
    Returns
    -------
    total_ways : int
        The number of combinations of the inputs that 
        could sum up to the target total.
        
    '''
    
    # At the beginning of each loop iteration,
    # ways[j] is the number of combinations of using the coin values before i
    # to form a sum of j
    
    # the list is updated within each loop
    # then get the final total number of ways to sum up to the target total
    # in the ways[total] cell
    
    # using Dynamic Programming algorithm
    
    ways = [1] + [0] * total
    for i in inputs:
        for j in range(1, total+1):
            if i <= j:
                ways[j] += ways[j-i]
    total_ways = ways[total]
    
    return total_ways
```

Clike [here](https://github.com/ZhiQiu976/source-codes-tech-posts/blob/master/Euler%20Project/Euler-problem-31.py) to check the source .py file.

<br />


## [Euler Problem 77](https://projecteuler.net/problem=77)

❓ What is the first value which can be written as the sum of primes in over a certain number (call it **threshold**) of different ways?

- `Solution`:
    - This problem is an upgraded version of `Problem 31`, so we can use exactly the **same** `dynamic programming` structure/function to compute the **total number of ways** of achieving a sum with a **list of different numbers**.
    
    - Using `next`, `filter` and `itertools` to find this **list of different numbers**.

<br />
**Codes Glimpse** 👀

```javascript
def prime_ways(n):
    '''
    Function to calculate how many different ways can an integer n 
    be written as the sum of primes.
    Parameters
    ----------
    n : int
        The number to be calculated with.
    Returns
    -------
    num_ways : int
        The total number of ways of different combinations.
    '''
    
    # get the primes before n (includes n)
    primes_set = primes(n)
    
    # dynamic programming
    ways = [1] + [0] * n
    for p in primes_set:
        for j in range(1, n+1):
            if p <= j:
                ways[j] += ways[j-p]
            
    num_ways = ways[n]
    
    return num_ways
```

<br />

```javascript
def compute(threshold):
    '''
    The main function for finding the target number for Euler problem 77.
    Get the first value which can be written as the sum of primes in over
    the threshold number of different ways.
    Parameters
    ----------
    threshold : int
        The threshold number of ways.
    Returns
    -------
    sum_value : int
        The target sum of primes.
    '''
    
    # get the first item from an iterable that matches a condition
    sum_value = next(filter(lambda n: prime_ways(n) > threshold,
                            itertools.count(2)))
    # starts from 2, step = 1
    
    return sum_value
```

Clike [here](https://github.com/ZhiQiu976/source-codes-tech-posts/blob/master/Euler%20Project/Euler-problem-77.py) to check the source .py file.


![Crepe](/assets/img/math.jpg){: .mx-auto.d-block :}








