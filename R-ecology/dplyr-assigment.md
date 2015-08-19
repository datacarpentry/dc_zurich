# dplyr assignment

Obtain the gapminder dataset by installing a package with the same name. 

```
install.packages("gapminder")
```

The load with `library(gapminder)`


**Exercises.**

1. Take the gapminder dataset as input
select only continent, country and life expectancy
arrange by life expectancy
get first five rows


2. Break the gapminder dataset by continent
calculate mean life expectancy for each country
pick country with highest life expectancy
then arrange by continent from highest to lowest mean life expectancy

hint: use `top_n()` to select n number of rows from each subset. `top_n(1)` will grab the first row. 