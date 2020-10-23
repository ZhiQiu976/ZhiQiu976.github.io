---
layout: post
title:  API Requesting and Json Formatting
subtitle: Who is the oldest in the world of Star Wars?
gh-repo: ZhiQiu976/source-codes-tech-posts
gh-badge: [star, fork, follow]
cover-img: /assets/img/yoda.jpeg
thumbnail-img: /assets/img/starwars.png
tags: [api request, json]
comments: true
---

This post is about doing **api requesting** and **json formatting** with the [SWAPI](https://swapi.dev/documentation) (`The Star Wars API`) to find the oldest person (or robot or alien) in the Star Wars, and all the films they appeared in.

**Detailed source codes about this post are included in this [notebook](https://github.com/ZhiQiu976/source-codes-tech-posts/blob/master/Star%20Wars/star_wars_api.ipynb).**

<br />

# SWAPI

Firstly we need to explore the [source API website](https://swapi.dev/documentation) a little bit so as to find the correct way of using this API:

![image1](/assets/img/baseurl.png){: .mx-auto.d-block :}

![image2](/assets/img/searchurl.png){: .mx-auto.d-block :}

As we are trying to find information about **characters** (`people`), our first base url would according be `https://swapi.dev/api/people/`, we could use the following codes to get information about characters that appear in Star Wars:

```javascript
base = 'https://swapi.dev/api/people/'
people = requests.get(base).json()
```
    
<br /> 
 
# JSON

The results we have in `people` now is quite nested. We could easily notice that there ought to be `82` people in total but our dictionary only have 10 records. That is because of the `next` key: the currrent result is just one **page**, we would need to do some more requests to get results from the **next pages**:

```javascript
results = people['results'] # a list of dictionary

while people['next']:
    people = requests.get(people['next']).json()
    results = results + people['results']
```

<br /> 

As the `results` variable is actually a list of dictionaries, we can easily transform it into a dataframe:


```javascript
people_df = pd.DataFrame(results)
```

<br /> 

![image3](/assets/img/df1.png){: .mx-auto.d-block :}

As we can see, this dataframe is not cleaned yet and has some nested lists in its columns. We could transform it in some particular ways to suit our needs and we would mainly focus on `name`, `birth_year` and `films`.

<br /> 

# Analysis

By doing some simple explorations we could find that the `birth_year` column basically has two types of entries: the **unknowns** who we don't know their age and the **BBYs** who were born **Before Battle of Yavin**.

Therefore, we onld only look at the ones we have age information about: the BBYs.

```javascript
BBY = people_df[people_df.birth_year.str.endswith('BBY')] # filter out the BBYs

# remove the redundant words 'BBY'
BBY = BBY.assign(birth_year = BBY['birth_year'].map(lambda x: float(x.rstrip('BBY'))))
```

After filtering out the BBYs and remove the redundant string, we could easily find the oldest one by `sorting`:

```javascript
oldest = BBY.sort_values('birth_year', ascending=False).head(1)
```

<br /> 

![image4](/assets/img/starwars_df2.png){: .mx-auto.d-block :}

😃 It turns out that [Yoda](https://starwars.fandom.com/wiki/Yoda) is the one we want to find!

Now the only thing left is to handle the nested `film` column and doing one more round of **API requesting** to get the film names:

```javascript
oldest_films = [requests.get(y).json() for x in oldest.films for y in x]
```

<br /> 

![image5](/assets/img/results.png){: .mx-auto.d-block :}

Therefore, `The Empire Strikes Back`, `Return of the Jedi`, `The Phantom Menace`, `Attack of the Clones`, `Revenge of the Sith` are the five films that our oldest friend Yoda appears! 🌠




