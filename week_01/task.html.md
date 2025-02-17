---
title: "Testing"
execute:
  keep-md: true
  df-print: paged
  warning: false
format:
  html:
    code-fold: true
    code-line-numbers: true
editor_options: 
  chunk_output_type: console
---





# Section Header

Explanation text...



::: {.cell}

```{.r .cell-code}
library(nycflights13)
library(tidyverse)
```
:::

::: {.cell}

```{.r .cell-code}
top_dest <- flights %>%
  group_by(dest) %>%
  summarise(total_flights = n()) %>%
  arrange(desc(total_flights)) %>%
  slice(1:10)

# Plot
ggplot(top_dest, aes(x = reorder(dest, -total_flights), y = total_flights)) +
  geom_bar(stat = "identity", fill = "purple") +
  labs(
    title = "Top 10 Destinations by Number of Flights",
    x = "Destination",
    y = "Total Flights"
  ) +
  theme_minimal()
```

::: {.cell-output-display}
![](task_files/figure-html/unnamed-chunk-2-1.png){width=672}
:::
:::

::: {.cell}

```{.r .cell-code}
flights_count <- flights %>%
  group_by(carrier) %>%
  summarise(total_flights = n()) %>%
  left_join(airlines, by = "carrier")

# Plot
ggplot(flights_count, aes(x = reorder(name, -total_flights), y = total_flights)) +
  geom_bar(stat = "identity", fill = "steelblue") +
  coord_flip() +
  labs(
    title = "Number of Flights by Airline",
    x = "Airline",
    y = "Total Flights"
  ) +
  theme_minimal()
```

::: {.cell-output-display}
![](task_files/figure-html/unnamed-chunk-3-1.png){width=672}
:::
:::



From these graphs I can conclude that Chicago O'Hare is the most popular destination for passengers. The most airline used by passengers is united. What I think is interesting about these graphs is that jetBlue and express jet is a airline that passengers use more than delta and american. I would think that delta american and united would be top 3 but the top 3 are united jetblue and expressjet. I have never heard of express jet so I wonder why that airline is so popular. With the top 10 destination there was no surprise that Chicago, Atlanta, and Los angles were the top 3 destinations.
