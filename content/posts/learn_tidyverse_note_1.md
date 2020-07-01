+++
title = "tidyverse notes I"
description = ""
featured_image = "/img/tidyverse-package-workflow.png"
date = 2020-07-01T15:26:59+08:00
categories = ["coding"]
tags = ["R", "tidyverse", "ggplot"]
+++

> What does `+ geom_*()` mean?

```R
ggplot(iris, mapping=aes(x=Sepal.Length, y=Sepal.Width)) +
  geom_point()
  layer(geom="point", stat="identity", position="identity")
```

is a shortcut to

```R
ggplot(iris, mapping=aes(x=Sepal.Length, y=Sepal.Width)) +
  layer(geom="point", stat="identity", position="identity")
```

- Usage of `layer()`

  ```R
  layer(
    geom = NULL,
    stat = NULL,
    data = NULL,
    mapping = NULL,
    position = NULL,
    params = list(),
    inherit.aes = TRUE,
    check.aes = TRUE,
    check.param = TRUE,
    show.legend = NA,
    key_glyph = NULL,
    layer_class = Layer
  )
  ```

- Component and Defaults in 'layer'

  - Besides data and aesthetic mapping, there are 3 basic components, `geom`, `stat` and `position`.
  - The default settings[^1]:

  | geom       | Useful stats (default in bold) | Default position adjustment | Parameters (when used with given stat)                                                                                                            |
  | ---------- | ------------------------------ | --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
  | blank      | **identity**                   | identity                    | no parameters                                                                                                                                     |
  | abline     | **abline**                     | identity                    | slope, intercept, size, linetype, colour, alpha                                                                                                   |
  |            | identity                       | identity                    | slope, intercept, size, linetype, colour, alpha                                                                                                   |
  | hline      | **hline**                      | identity                    | yintercept, size, linetype, colour, alpha                                                                                                         |
  |            | identity                       | identity                    | y, yend, size, linetype, colour, alpha                                                                                                            |
  | vline      | **vline**                      | identity                    | xintercept, size, linetype, colour, alpha                                                                                                         |
  |            | identity                       | identity                    | x, xend, size, linetype, colour, alpha                                                                                                            |
  | text       | **identity**                   | identity                    | x, y, label, size, colour, alpha, hjust, vjust, parse                                                                                             |
  | point      | **identity**                   | identity                    | x, y, size, shape, colour, fill, alpha, na.rm                                                                                                     |
  | jitter     | **identity**                   | jitter                      | x, y, size, shape, colour, fill, alpha, na.rm                                                                                                     |
  | segment    | **identity**                   | identity                    | x, xend, y, yend, size, linetype, colour, alpha, arrow                                                                                            |
  | line       | **identity**                   | identity                    | group, x, y, size, linetype, colour, alpha, arrow                                                                                                 |
  | bar        | identity                       | stack                       | x, y, size, linetype, colour, fill, alpha, weight(?) ???                                                                                          |
  |            | **bin**                        | stack                       | x, y, size, linetype, colour, fill, alpha, weight(?) ???                                                                                          |
  | histogram  | _alias for geom_bar_           |                             |                                                                                                                                                   |
  | area       | **identity**                   | stack                       | group, x, y, size, linetype, colour, fill, alpha, na.rm                                                                                           |
  | ribbon     | **identity**                   | identity                    | group, x, ymin, ymax, size, linetype, colour, fill, alpha, na.rm                                                                                  |
  | linerange  | **identity**                   | identity                    | x, ymin, ymax, size, linetype, colour, alpha                                                                                                      |
  | pointrange | **identity**                   | identity                    | x, y, ymin, ymax, size, shape, linetype, colour, fill, alpha                                                                                      |
  | errorbar   | **identity**                   | identity                    | x, ymin, ymax, size, linetype, colour, alpha, width                                                                                               |
  | errorbarh  | **identity**                   | identity                    | x, xmin, xmax, y, size, linetype, colour, alpha, height                                                                                           |
  | crossbar   | **identity**                   | identity                    | x, y, ymin, ymax, size, linetype, colour, fill, alpha, width, fatten                                                                              |
  | boxplot    | identity                       | dodge                       | x, ymin, lower, middle, upper, ymax, size, colour, fill, alpha, weight(?), width(?), outliers(?), outlier.size, outlier.shape, outlier.colour ??? |
  |            | **boxplot**                    | dodge                       | x, ymin, lower, middle, upper, ymax, size, colour, fill, alpha, weight(?), width(?), outliers(?), outlier.size, outlier.shape, outlier.colour ??? |
  | path       | **identity**                   | identity                    | group, x, y, size, linetype, colour, alpha, na.rm, arrow, linemitre, linejoin, lineend                                                            |
  | polygon    | **identity**                   | identity                    | group, x, y, size, linetype, colour, fill, alpha                                                                                                  |
  | rect       | **identity**                   | identity                    | xmin, xmax, ymin, ymax, size, linetype, colour, fill, alpha                                                                                       |
  | rug        | **identity**                   | identity                    | x, y, size, linetype, colour, alpha                                                                                                               |
  | step       | **identity**                   | identity                    | group, x, y, size, linetype, colour, alpha, direction                                                                                             |
  | bin2d      | identity                       | identity                    | xmin, xmax, ymin, ymax, size, linetype, colour, fill, alpha, weight(?) ???                                                                        |
  |            | **bin2d**                      | identity                    | xmin, xmax, ymin, ymax, size, linetype, colour, fill, alpha, weight(?) ???                                                                        |
  | tile       | identity                       | identity                    | x, y, size, linetype, colour, fill, alpha                                                                                                         |
  | hex        | **identity**                   | identity                    | x, y, size, colour, fill, alpha                                                                                                                   |
  |            | binhex                         | identity                    | x, y, size, colour, fill, alpha                                                                                                                   |
  | density    | identity                       | identity                    | group, x, y, size, linetype, colour, fill, alpha, weight(?) ???                                                                                   |
  |            | **density**                    | identity                    | group, x, y, size, linetype, colour, fill, alpha, weight(?) ???                                                                                   |
  | density2d  | identity                       | identity                    | group, x, y, size, linetype, colour, alpha, weight(?), na.rm, arrow, linemitre, linejoin, lineend ???                                             |
  |            | **density2d**                  | identity                    | group, x, y, size, linetype, colour, alpha, weight(?), na.rm, arrow, linemitre, linejoin, lineend ???                                             |
  | contour    | identity                       | identity                    | group, x, y, size, linetype, colour, alpha, weight(?), na.rm, arrow, linemitre, linejoin, lineend ???                                             |
  |            | **contour**                    | identity                    | group, x, y, size, linetype, colour, alpha, weight(?), na.rm, arrow, linemitre, linejoin, lineend ???                                             |
  | freqpoly   | identity                       | identity                    | group, x, y, size, linetype, colour, alpha, weight(?) ???                                                                                         |
  |            | **bin**                        | identity                    | group, x, y, size, linetype, colour, alpha, weight(?) ???                                                                                         |
  | quantile   | identity                       | identity                    | group, x, y, size, linetype, colour, alpha, na.rm, arrow, linemitre, linejoin, lineend                                                            |
  |            | **quantile**                   | identity                    | group, x, y, size, linetype, colour, alpha, weight, quantiles, formula, xseq, method, na.rm, arrow, linemitre, linejoin, lineend                  |
  | smooth     | identity                       | identity                    | group, x, y, ymin, ymax, size, linetype, colour, fill, alpha                                                                                      |
  |            | **smooth**                     | identity                    | group, x, y, size, linetype, colour, fill, alpha, weight                                                                                          |

- Annotations (a special type of layer)

  Annotations don’t inherit global settings from the plot.
  They are used to add fixed reference data to plots.

[^1]: http://sape.inf.usi.ch/quick-reference/ggplot2/geom
