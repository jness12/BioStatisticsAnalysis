---
title: "Palmer Penguins Initial Analysis"
author: "Jennessa Brunette"
format: html
editor: visual
execute: 
  keep-md: true
---



## Palmer Penguin Analysis

This is an analysis of the Palmer Penguin data set.

## Loading Packages and data sets

Here we will load the tidyverse packages and penguins data.


::: {.cell}

```{.r .cell-code}
#Load the tidyverse
library(tidyverse)
```

::: {.cell-output .cell-output-stderr}
```
── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
✔ ggplot2 3.4.0      ✔ purrr   1.0.0 
✔ tibble  3.1.8      ✔ dplyr   1.0.10
✔ tidyr   1.2.1      ✔ stringr 1.5.0 
✔ readr   2.1.3      ✔ forcats 0.5.2 
── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
✖ dplyr::filter() masks stats::filter()
✖ dplyr::lag()    masks stats::lag()
```
:::

```{.r .cell-code}
library(kableExtra)
```

::: {.cell-output .cell-output-stderr}
```

Attaching package: 'kableExtra'

The following object is masked from 'package:dplyr':

    group_rows
```
:::

```{.r .cell-code}
#Read the penguins_samp1 data file from github
penguins <- read_csv("https://raw.githubusercontent.com/mcduryea/Intro-to-Bioinformatics/main/data/penguins_samp1.csv")
```

::: {.cell-output .cell-output-stderr}
```
Rows: 44 Columns: 8
── Column specification ────────────────────────────────────────────────────────
Delimiter: ","
chr (3): species, island, sex
dbl (5): bill_length_mm, bill_depth_mm, flipper_length_mm, body_mass_g, year

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```
:::

```{.r .cell-code}
#See the first six rows of the data we've read in to our notebook
penguins %>% 
  head() %>%
  kable() %>%
  kable_styling(c("striped", "hover"))
```

::: {.cell-output-display}

`````{=html}
<table class="table table-striped table-hover" style="margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> species </th>
   <th style="text-align:left;"> island </th>
   <th style="text-align:right;"> bill_length_mm </th>
   <th style="text-align:right;"> bill_depth_mm </th>
   <th style="text-align:right;"> flipper_length_mm </th>
   <th style="text-align:right;"> body_mass_g </th>
   <th style="text-align:left;"> sex </th>
   <th style="text-align:right;"> year </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Gentoo </td>
   <td style="text-align:left;"> Biscoe </td>
   <td style="text-align:right;"> 59.6 </td>
   <td style="text-align:right;"> 17.0 </td>
   <td style="text-align:right;"> 230 </td>
   <td style="text-align:right;"> 6050 </td>
   <td style="text-align:left;"> male </td>
   <td style="text-align:right;"> 2007 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Gentoo </td>
   <td style="text-align:left;"> Biscoe </td>
   <td style="text-align:right;"> 48.6 </td>
   <td style="text-align:right;"> 16.0 </td>
   <td style="text-align:right;"> 230 </td>
   <td style="text-align:right;"> 5800 </td>
   <td style="text-align:left;"> male </td>
   <td style="text-align:right;"> 2008 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Gentoo </td>
   <td style="text-align:left;"> Biscoe </td>
   <td style="text-align:right;"> 52.1 </td>
   <td style="text-align:right;"> 17.0 </td>
   <td style="text-align:right;"> 230 </td>
   <td style="text-align:right;"> 5550 </td>
   <td style="text-align:left;"> male </td>
   <td style="text-align:right;"> 2009 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Gentoo </td>
   <td style="text-align:left;"> Biscoe </td>
   <td style="text-align:right;"> 51.5 </td>
   <td style="text-align:right;"> 16.3 </td>
   <td style="text-align:right;"> 230 </td>
   <td style="text-align:right;"> 5500 </td>
   <td style="text-align:left;"> male </td>
   <td style="text-align:right;"> 2009 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Gentoo </td>
   <td style="text-align:left;"> Biscoe </td>
   <td style="text-align:right;"> 55.1 </td>
   <td style="text-align:right;"> 16.0 </td>
   <td style="text-align:right;"> 230 </td>
   <td style="text-align:right;"> 5850 </td>
   <td style="text-align:left;"> male </td>
   <td style="text-align:right;"> 2009 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Gentoo </td>
   <td style="text-align:left;"> Biscoe </td>
   <td style="text-align:right;"> 49.8 </td>
   <td style="text-align:right;"> 15.9 </td>
   <td style="text-align:right;"> 229 </td>
   <td style="text-align:right;"> 5950 </td>
   <td style="text-align:left;"> male </td>
   <td style="text-align:right;"> 2009 </td>
  </tr>
</tbody>
</table>

`````

:::
:::


You can add options to executable code like this


::: {.cell}
::: {.cell-output .cell-output-stdout}
```
[1] 4
```
:::
:::


The `echo: false` option disables the printing of code (only output is displayed).

# About our data

The dats includes 8 features measured on 44 penguins. The features included are physiological features like bill length, bill depth, flipper length, body mass, etc. as well as other features like the year the penguin was observed, sex of the penguin, the island the penguin was observed on, and the species of the penguin.

# Interesting Questions to Ask

-   What is the average flipper length? What about for each species?

-   Are there more male or female penguins? per island? per species?

-   What is the average body mass? By species? By sex?

-   What is the ratio of bill length to bill depth for a penguin? What is the overall average of this metric? Does it change by species, sex, or island?

-   Does average body mass change by year?

    # Data manipulation tools & strategies

    We can look at individual columns in a data set or subsets of columns in a data set. For ex, we are only interested in flipper length and species we can select those columns.


    ::: {.cell}
    
    ```{.r .cell-code}
    penguins %>%
      select (species, body_mass_g)
    ```
    
    ::: {.cell-output .cell-output-stdout}
    ```
    # A tibble: 44 × 2
       species body_mass_g
       <chr>         <dbl>
     1 Gentoo         6050
     2 Gentoo         5800
     3 Gentoo         5550
     4 Gentoo         5500
     5 Gentoo         5850
     6 Gentoo         5950
     7 Gentoo         5700
     8 Gentoo         5350
     9 Gentoo         5550
    10 Gentoo         6300
    # … with 34 more rows
    ```
    :::
    :::


If we want to filter and only show certain rows, we can do that too.


::: {.cell}

```{.r .cell-code}
penguins %>%
  filter (species == "chinstrap")
```

::: {.cell-output .cell-output-stdout}
```
# A tibble: 0 × 8
# … with 8 variables: species <chr>, island <chr>, bill_length_mm <dbl>,
#   bill_depth_mm <dbl>, flipper_length_mm <dbl>, body_mass_g <dbl>, sex <chr>,
#   year <dbl>
```
:::
:::


# Answering our questions

Most of our questions involve summarizing data, and perhaps summarizing over groups. We can summarize data using summarize() function, and group data using group_by().

Lets find average flipper length


::: {.cell}

```{.r .cell-code}
#overall average flipper length
penguins %>%
  summarize(avg_flipper_length = mean(flipper_length_mm)) 
```

::: {.cell-output .cell-output-stdout}
```
# A tibble: 1 × 1
  avg_flipper_length
               <dbl>
1               212.
```
:::

```{.r .cell-code}
# Grouped Average
penguins %>%
  group_by(species) %>%
  summarize(avg_flipper_length = mean(flipper_length_mm)) 
```

::: {.cell-output .cell-output-stdout}
```
# A tibble: 3 × 2
  species   avg_flipper_length
  <chr>                  <dbl>
1 Adelie                  189.
2 Chinstrap               200 
3 Gentoo                  218.
```
:::
:::


How many of each species do we have?


::: {.cell}

```{.r .cell-code}
penguins %>%
  group_by(species) %>%
  summarize (sex)
```

::: {.cell-output .cell-output-stderr}
```
`summarise()` has grouped output by 'species'. You can override using the
`.groups` argument.
```
:::

::: {.cell-output .cell-output-stdout}
```
# A tibble: 44 × 2
# Groups:   species [3]
   species   sex   
   <chr>     <chr> 
 1 Adelie    male  
 2 Adelie    female
 3 Adelie    female
 4 Adelie    male  
 5 Adelie    male  
 6 Adelie    female
 7 Adelie    female
 8 Adelie    female
 9 Adelie    female
10 Chinstrap male  
# … with 34 more rows
```
:::

```{.r .cell-code}
penguins %>%
  group_by(island) %>%
  summarize(sex)
```

::: {.cell-output .cell-output-stderr}
```
`summarise()` has grouped output by 'island'. You can override using the
`.groups` argument.
```
:::

::: {.cell-output .cell-output-stdout}
```
# A tibble: 44 × 2
# Groups:   island [3]
   island sex  
   <chr>  <chr>
 1 Biscoe male 
 2 Biscoe male 
 3 Biscoe male 
 4 Biscoe male 
 5 Biscoe male 
 6 Biscoe male 
 7 Biscoe male 
 8 Biscoe male 
 9 Biscoe male 
10 Biscoe male 
# … with 34 more rows
```
:::

```{.r .cell-code}
penguins %>%
  count(sex)
```

::: {.cell-output .cell-output-stdout}
```
# A tibble: 2 × 2
  sex        n
  <chr>  <int>
1 female    20
2 male      24
```
:::
:::


we can use mutate() to add new columns to our data set.


::: {.cell}

```{.r .cell-code}
penguins %>%
  mutate(bill_ltd_ratio = bill_length_mm / bill_depth_mm) %>%
  summarize (mean_bill_ltd_ratio = mean(bill_ltd_ratio),
             median_bill_ltd_ratio =median(bill_ltd_ratio))
```

::: {.cell-output .cell-output-stdout}
```
# A tibble: 1 × 2
  mean_bill_ltd_ratio median_bill_ltd_ratio
                <dbl>                 <dbl>
1                2.95                  3.06
```
:::
:::

::: {.cell}

```{.r .cell-code}
penguins %>%
  mutate(bill_ltd_ratio = bill_length_mm / bill_depth_mm) %>%
  summarize(mean_bill_ltd_ratio = mean(bill_ltd_ratio),
             median_bill_ltd_ratio =median(bill_ltd_ratio))
```

::: {.cell-output .cell-output-stdout}
```
# A tibble: 1 × 2
  mean_bill_ltd_ratio median_bill_ltd_ratio
                <dbl>                 <dbl>
1                2.95                  3.06
```
:::
:::

::: {.cell}

```{.r .cell-code}
penguins %>%
  group_by(year)%>%
  summarize(mean_body_mass = mean(body_mass_g))
```

::: {.cell-output .cell-output-stdout}
```
# A tibble: 3 × 2
   year mean_body_mass
  <dbl>          <dbl>
1  2007          5079.
2  2008          4929.
3  2009          4518.
```
:::
:::

::: {.cell}

```{.r .cell-code}
penguins %>%
  mutate(bill_ltd_ratio = bill_length_mm / bill_depth_mm) %>%
  summarize(mean_bill_ltd_ratio = mean(bill_ltd_ratio),
             median_bill_ltd_ratio =median(bill_ltd_ratio))
```

::: {.cell-output .cell-output-stdout}
```
# A tibble: 1 × 2
  mean_bill_ltd_ratio median_bill_ltd_ratio
                <dbl>                 <dbl>
1                2.95                  3.06
```
:::
:::


# Data Visualization
