---
layout: what-ive-learned
title: Exponential majorticks and linear minorticks
tags: ggplot R
is_wil_snippet: true
---
**tl;dr** DO THE MATH

```{r}
df <- data.frame(x = 1:1000, y = 1:1000)
major.breaks=10^(seq(floor(log10(min(y))), ceiling(log10(max(y)))))
minor.breaks=unlist(lapply(major.breaks, function(x) x * 1:f))

ggplot(df) + geom_line(aes(x = x, y = y)) +
  scale_x_continuous(trans = 'log10',
                     breaks = major.breaks,
                     minor_breaks = minor.breaks)
```
