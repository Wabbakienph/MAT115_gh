Pipe Exercises with baby names dataset
================
Kien Pham
2024-03-13

1.  Find the number of names per year per gender, and arrange your
    output from the most recent to oldest.

``` r
names_by_year |>
  group_by(Year, Gender) |>
  summarize(n()) |>
  arrange(desc(Year))
```

    ## `summarise()` has grouped output by 'Year'. You can override using the
    ## `.groups` argument.

    ## # A tibble: 286 × 3
    ## # Groups:   Year [143]
    ##     Year Gender `n()`
    ##    <dbl> <chr>  <int>
    ##  1  2022 F      17660
    ##  2  2022 M      14255
    ##  3  2021 F      17628
    ##  4  2021 M      14057
    ##  5  2020 F      17485
    ##  6  2020 M      14032
    ##  7  2019 F      17997
    ##  8  2019 M      14112
    ##  9  2018 F      18126
    ## 10  2018 M      14095
    ## # ℹ 276 more rows

> 2.  Find the top five most popular boy and girl names in 2022, 2021,
>     and 2020.

``` r
names_by_year |>
  filter(Year >= 2020) |>
  group_by(Gender, Year) |> # if dont group by year, will only pick the 1 most popular name/gender
  slice_max(Count, n = 5) |>
  print(n = 30) # display all 30 rows
```

    ## # A tibble: 30 × 4
    ## # Groups:   Gender, Year [6]
    ##     Year Name      Gender Count
    ##    <dbl> <chr>     <chr>  <dbl>
    ##  1  2020 Olivia    F      17664
    ##  2  2020 Emma      F      15680
    ##  3  2020 Ava       F      13179
    ##  4  2020 Charlotte F      13083
    ##  5  2020 Sophia    F      13070
    ##  6  2021 Olivia    F      17798
    ##  7  2021 Emma      F      15510
    ##  8  2021 Charlotte F      13336
    ##  9  2021 Amelia    F      13007
    ## 10  2021 Ava       F      12830
    ## 11  2022 Olivia    F      16573
    ## 12  2022 Emma      F      14435
    ## 13  2022 Charlotte F      12891
    ## 14  2022 Amelia    F      12333
    ## 15  2022 Sophia    F      12310
    ## 16  2020 Liam      M      19828
    ## 17  2020 Noah      M      18407
    ## 18  2020 Oliver    M      14261
    ## 19  2020 Elijah    M      13172
    ## 20  2020 William   M      12643
    ## 21  2021 Liam      M      20365
    ## 22  2021 Noah      M      18849
    ## 23  2021 Oliver    M      14683
    ## 24  2021 Elijah    M      12774
    ## 25  2021 James     M      12429
    ## 26  2022 Liam      M      20456
    ## 27  2022 Noah      M      18621
    ## 28  2022 Oliver    M      15076
    ## 29  2022 James     M      12028
    ## 30  2022 Elijah    M      11979

> 3.  How popular is `Christopher` as a baby boy name in 2022, 2021, and
>     2020? Is it in the top 50? top 100?

``` r
names_by_year |>
  filter(Year >= 2020) |>
  filter(Gender == 'M') |>
  group_by(Year) |>
  mutate(Rank = rank(-Count)) |> # reverse it so Largest count = smallest rank
  filter(Name == "Ben") |>
  arrange(Year)
```

    ## # A tibble: 3 × 5
    ## # Groups:   Year [3]
    ##    Year Name  Gender Count  Rank
    ##   <dbl> <chr> <chr>  <dbl> <dbl>
    ## 1  2020 Ben   M        313  768 
    ## 2  2021 Ben   M        327  762.
    ## 3  2022 Ben   M        325  772.

> 4.  How popular is `Catherine` or `Katherine` as a baby girl name in
>     2022, 2021, and 2020? Is either in the top 50? top 100? Which
>     spelling `C` or `K` is more popular?

``` r
names_by_year |>
  filter(Year >= 2020) |>
  filter(Gender == 'F') |>
  group_by(Year) |>
  mutate(Rank = rank(-Count)) |> # reverse it so Largest count = smallest rank
  filter(Name %in% c('Catherine','Katherine')) |>
  arrange(Year)
```

    ## # A tibble: 6 × 5
    ## # Groups:   Year [3]
    ##    Year Name      Gender Count  Rank
    ##   <dbl> <chr>     <chr>  <dbl> <dbl>
    ## 1  2020 Katherine F       1989   135
    ## 2  2020 Catherine F       1155   267
    ## 3  2021 Katherine F       1816   157
    ## 4  2021 Catherine F       1003   323
    ## 5  2022 Katherine F       1727   166
    ## 6  2022 Catherine F        976   328
