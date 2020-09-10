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

This post will talk about some interesting programming problems in the famous [Project Euler](https://projecteuler.net), which is a series of challenging mathematical/computer programming problems that will require more than just mathematical insights to solve. As stated on the website, 'although **mathematics** will help you arrive at elegant and efficient methods, the use of a computer and **programming** skills will be required to solve most problems'. In the next few minutes, I'll walk you through some useful algorithms and codes that could solve `three typical mathe puzzles` in Project Euler elegantly.

**You can check the `Euler Project` folder in my `Github Repo` [ZhiQiu976/source-codes-tech-posts](https://github.com/ZhiQiu976/source-codes-tech-posts) for detailed scorce codes and outputs.**

<br />

## [Euler Problem 8](https://projecteuler.net/problem=8)

- `Problem`: Given a 1000-digit number, what are the thirteen adjacent digits in this number that could give the greatest elementwise product? What is the value of this product?

- `Solution`: 
    - The solution logic of this problem is quite transparent: firstly get the collection of all possible **thirteen adjacent digits** in the 1000-digit number. Then calculate the **product** of each 13-digit-set. Lastly find the maximum.
    - This logic is quite simple to accomplish in coding. `List comprehension` could be very helpful here.
    - Remember to take care of data types.
     
<br />
**Codes Glimpse**:

```javascript
ss = [list(xs[i : i+n]) for i in range(1000 - (n-1))]
ss = [list(map(int, s)) for s in ss] # turn into floating number

products = [np.prod(s) for s in ss]
idx = np.argmax(products) # get the index of the maximum

result = products[idx]
digits = ss[idx]
```

Clike [here](https://github.com/ZhiQiu976/source-codes-tech-posts/blob/master/Euler%20Project/Euler-problem-8.py) to check the source .py file.

<br />


## [Euler Problem 31](https://projecteuler.net/problem=31)

- `Problem`: Given a set of different denominations of coins, and a target amount of money, how many different ways can this amount of money be made using any number of coins?

- `Solution`:
    - This problem can be done itertively but this method is computationally complex.
    - We would use the idea of `dynamic programming` to improve programming efficiency.
    - The main idea is: 
        - firstly we try only using the first denomination to achieve the amount of `[1, 2, ... , total]`

<br />
**Codes Glimpse**:

```javascript
ways = [1] + [0] * total
for i in inputs:
    for j in range(1, total+1):
        if i <= j:
            ways[j] += ways[j-i]
            
total_ways = ways[total]
```

Clike [here](https://github.com/ZhiQiu976/source-codes-tech-posts/blob/master/Euler%20Project/Euler-problem-31.py) to check the source .py file.

<br />


## [Euler Problem 77](https://projecteuler.net/problem=77)

- Problem: Given a 1000-digit number, what are the thirteen adjacent digits in this number that could give the greatest elementwise product? What is the value of this product?

- Solution:

- Codes Glimpse:

```javascript
sum_value = next(filter(lambda n: prime_ways(n) > threshold, itertools.count(2)))
```

Clike [here](https://github.com/ZhiQiu976/source-codes-tech-posts/blob/master/Euler%20Project/Euler-problem-77.py) to check the source .py file.


![Crepe](/assets/img/math.jpg){: .mx-auto.d-block :}








