---
layout: post
title:  Constructing Python Dashboard/Small App with Streamlit
subtitle: Analysis for 2017 Doctorate Recipients Dataset
gh-repo: ZhiQiu976/Streamlit-Dashboard
gh-badge: [star, fork, follow]
cover-img: /assets/img/yoda.jpeg
thumbnail-img: /assets/img/starwars.png
tags: [api request, json]
comments: true
---

This post is about doing data analysis and visualization for the [2017 Doctorate Recipients Dataset](https://ncses.nsf.gov/pubs/nsf19301/data) and constructing a dashboard with [Streamlit](https://www.streamlit.io) for results demonstration. Note that dashboard built with `Streamlit` originally can only be accessed locally, but we can use [Heroku](https://signup.heroku.com/t/platform?c=70130000000NZToAAO&gclid=Cj0KCQiAhZT9BRDmARIsAN2E-J0neOTuMFKjU_5XcTFj0g_50syoK-pGXQ6p9fTLCs9nfrJ6aJiafhYaAtFBEALw_wcB) to built a small app and make this dashboard online and public!

My final dashboard can be accessed via this [link](https://tranquil-shelf-65765.herokuapp.com) and the source codes could be find on my [Streamlit-Dashboard](https://github.com/ZhiQiu976/Streamlit-Dashboard) branch at GitHub.

<br />

# Data

The [2017 Doctorate Recipients Dataset](https://ncses.nsf.gov/pubs/nsf19301/data) is quite a rich dateset and contains a lot of information. My analysis mainly focus on information about recipents and institutions. The tables I used are `Table 1, Table 3, Table 5 and Table 6`.

Firstly I did some pre-processing for the excel data to make them more suitable for plotting and visualization (details included in the [pre-processing notebook](https://github.com/ZhiQiu976/Streamlit-Dashboard/blob/main/pre-processing%20for%20tables.ipynb)).

For the first three tables oprations are quite simple, mainly about formatting. As for the last Table, it is kind of a nested shape, so I transformed its structure a little bit.

**Before**

![image3](/assets/img/g1.png){: .mx-auto.d-block :}

**After**

![image3](/assets/img/g1.png){: .mx-auto.d-block :}
    
<br /> 
 
# Visual

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

It turns out that [Yoda](https://starwars.fandom.com/wiki/Yoda) is the one we want to find!

Now the only thing left is to handle the nested `film` column and doing one more round of **API requesting** to get the film names:

```javascript
oldest_films = [requests.get(y).json() for x in oldest.films for y in x]
```

<br /> 

![image5](/assets/img/results.png){: .mx-auto.d-block :}

Below are the links/APIs I find very useful for dashboard construction and deployment ⭐:

- [How to Build a Streamlit App in Python](https://pythonforundergradengineers.com/streamlit-app-with-bokeh.html)

- [Altair: Declarative Visualization in Python](https://altair-viz.github.io)






