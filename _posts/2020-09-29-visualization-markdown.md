---
layout: post
title: Investigation into Global Malaria Situation
subtitle: 3 visualizations worth attention
gh-repo: ZhiQiu976/source-codes-tech-posts
gh-badge: [star, fork, follow]
cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
tags: [website, jekyll]
comments: true
---

Note: This post is a step-by-step investigation into the [Malaria Dataset](https://github.com/ZhiQiu976/source-codes-tech-posts/tree/master/Malaria%20Dataset%20Visualisation/data) from the `different-income-entities` perspective. You can check the `Malaria Dataset Visualisation` folder in my `Github Repo` [ZhiQiu976/source-codes-tech-posts](https://github.com/ZhiQiu976/source-codes-tech-posts) for detailed data processing and visualization making.

**Main codes and outputs are included in this [notebook](https://github.com/ZhiQiu976/source-codes-tech-posts/blob/master/Malaria%20Dataset%20Visualisation/visuals_malaria_data.ipynb).**

<br />

## Incidence of Malaria for Different Income Entities

Firstly we take a look at Malaria situation over the last two decades in countries categorized into four different income entities (`Low income, Lower middle income, Middle income and Upper middle income`). Note that Malaria is actually very rare in High income countries, so we don't have data and thus didn't plot for these countries.

![plot1](https://raw.githubusercontent.com/ZhiQiu976/source-codes-tech-posts/master/Malaria%20Dataset%20Visualisation/plot1.png){: .mx-auto.d-block :}

From this plot we can see that Malaria is much more **severe in lower income entities** and the overall situation for this disease is actually **improving over years**. In upper middle income countries, there's nearly no incidence of Malaria per 1,000 population at risk. However, in low income countries the incidence number is still quite high though already reduced by half from 2000 to 2015.

<br />

## Deaths of Malaria in Four Example Countries

Next we will take a further look into the seriousness of Malaria in different income entites. We would pick **four representative countries** from each of these four income categories and take a glimpse at the `exact deaths` of Malaria among the whole population in these example countries.

![plot2](https://raw.githubusercontent.com/ZhiQiu976/source-codes-tech-posts/master/Malaria%20Dataset%20Visualisation/plot2.png){: .mx-auto.d-block :}

From this plot we can conclude that Malaria is actually not a severe problem in all income entities except the **low income** (represented by **Central African Republic**). In lower middle (Nepal), middle (Bangladesh) and upper middle (China) income countries, Malaria is a highly curable disease and thus we may not need to worry a lot. However, in Central African Republic, the deaths number remains at a quite significant level from 2000 to 2010 and it still unneglectable in 2015.

<br />

## Deaths of Malaria for Different Age Groups

Lastly, continuing from above, we would now focus only on the **low income entity** - Central African Republic and investigate **deaths of Malaria** among `different age groups`.

![plot3](https://raw.githubusercontent.com/ZhiQiu976/source-codes-tech-posts/master/Malaria%20Dataset%20Visualisation/plot3.png){: .mx-auto.d-block :}

From this plot we can see that **children under 5 years old** are most susceptible for Malaria and elders over 70 is actually a relatively safe population. The other three age groups are also not very susceptible and are all at a similar risk level.

<br />

### Conclusion

In summary, Malaria is not a very severe global disease anymore but is still worth attention in `low income entities`. It is most susceptible for `children under 5 years old` in these countries and thus we should **invest more in health care for young child in poor countries** so as to prevent them from suffering Malaria.













