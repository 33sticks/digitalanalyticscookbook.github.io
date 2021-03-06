---

layout: responsive
title: Visualizing State Level Data With R and Statebins

---
## Visualizing State Level Data With R and Statebins

Author: Jowanza Joseph

__Problem__: For an organization that is geographically distributed, understanding how interactions are distributed across the geography becomes important. Presenting that information in a simple and effective manner is best.

__Actions__: We'll walk through a simple example of how to visualize your state data from Google Analytics (any other analytics solution would be similar).


### Example

Within the Google Analytics interface, you can find a visualization that looks like this:

![googleanalytics](http://i.imgur.com/HjHXZhX.png)

It's handy for understanding traffic and other engagement patterns from a geographical perspective. We can simplify it a bit an add some depth using some statebins.

The Statebin comes from the Washington Post:

![washingtonpost](http://i.imgur.com/ymtccWx.png)


We'll take the same data from this graph and make it a statebin!

Step one is preparing the data. All you need is a state column and another column (in this case percentage new visitors). Data should look like this:
<br>

| Region        | newsessions           | Other Data  |
| ------------- |:-------------:| -----:|
| New York     | .23 | 1 |
| California      | .77      |   2 |
| Florida | .65      |    3 |

<br>

From here we'll use R. First thing we need to do is translate the state data into state abbreviations. For example, "New York" would become "NY" and so on. R already has a handy function for this:

```R
library(openintro)
data = read.csv("mydat.csv", header=TRUE)
data$states = as.character(state2abbr(data$Region))
```

From here, we just need to adjust our options and make a plot:

{% highlight r%}
library(statebins)

gg <- statebins_continuous(data, "states", "newsessions",legend_position="bottom",
                           legend_title="%", font_size=5,
                           brewer_pal="Blues", text_color="black", breaks = 4,
                           plot_title="% New Visitors Feb 2014 - Feb 2015", title_position="top")
{% endhighlight %}

![statebin](http://i.imgur.com/d43Gr0f.png)



#### References:

[Statebins](https://github.com/hrbrmstr/statebins)

[Washington Post](http://www.washingtonpost.com/wp-srv/special/business/states-most-threatened-by-trade/)

[Dataset](http://1drv.ms/1RyAqMC)
