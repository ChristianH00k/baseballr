---
layout: page
title: Data Aquisition Functions
subtitle: 
---

`baseballr` comes with a number of functions that help with acquiring data from various sources.

### Standings

You  can acquire the standings for any given date in MLB history from [Baseball-Reference.com](http://www.baseball-reference.com) using the `standings_on_date_bref()` function. Just pass the year, month, day, and division you want:

```r
> standings_on_date_bref(date = "2015-08-01", division = "NL East", from = FALSE)
$`NL East`
   Tm  W  L  W-L%   GB  RS  RA pythW-L%
1 WSN 54 48 0.529   -- 422 391    0.535
2 NYM 54 50 0.519  1.0 368 373    0.494
3 ATL 46 58 0.442  9.0 379 449    0.423
4 MIA 42 62 0.404 13.0 370 408    0.455
5 PHI 41 64 0.390 14.5 386 511    0.374
```

If you want to see the standings from a particular date forward you can set the `from` parameter to `TRUE`:

```r
> standings_on_date_bref(date = "2015-08-01", division = "NL East", from = TRUE)
$`NL East`
   Tm  W  L  W-L%   GB  RS  RA pythW-L%
1 NYM 36 22 0.621   -- 315 240    0.622
2 MIA 29 29 0.500  7.0 243 270    0.452
3 WSN 29 31 0.483  8.0 281 244    0.564
4 PHI 22 35 0.386 13.5 240 298    0.402
5 ATL 21 37 0.362 15.0 194 311    0.297
```

The function can also generate standings across an entire league (AL or NL) by including "Overall" in the division paramater:

```r
> standings_on_date_bref(date = "2015-08-01", division = "NL Overall", from = TRUE)
$`NL Overall`
    Tm  W  L  W-L%   GB  RS  RA pythW-L%
1  CHC 41 18 0.695   -- 293 218    0.632
2  PIT 38 21 0.644  3.0 271 219    0.596
3  NYM 36 22 0.621  4.5 315 240    0.622
4  STL 34 24 0.586  6.5 232 219    0.526
5  LAD 33 25 0.569  7.5 236 229    0.514
6  MIA 29 29 0.500 11.5 243 270    0.452
7  ARI 29 31 0.483 12.5 270 269    0.502
8  WSN 29 31 0.483 12.5 281 244    0.564
9  SFG 27 32 0.458 14.0 247 231    0.531
10 MIL 24 33 0.421 16.0 247 275    0.451
11 COL 24 36 0.400 17.5 270 317    0.427
12 SDP 23 35 0.397 17.5 244 279    0.439
13 PHI 22 35 0.386 18.0 240 298    0.402
14 ATL 21 37 0.362 19.5 194 311    0.297
15 CIN 17 43 0.283 24.5 227 302    0.372
```

### Daily Player Performance

You can also pull data for all hitters or pitchers over a specific date range from [Baseball-Reference.com](http://www.baseball-reference.com) using the `daily` functions. There are two parameters: t1 is the start date and t2 is the end date.

Here are the results for all hitters from August 1st through October 3rd during the 2015 season:

```r
> head(daily_batter_bref(t1 = "2015-08-01", t2 = "2015-10-03"))
  season             Name Age  Level          Team  G  PA  AB  R  H X1B X2B X3B
1   2015    Manny Machado  22 MLB-AL     Baltimore 59 266 237 36 66  43  10   0
2   2015       Matt Duffy  24 MLB-NL San Francisco 59 264 248 33 71  54  12   2
3   2015      Jose Altuve  25 MLB-AL       Houston 57 262 244 30 81  53  19   3
4   2015       Adam Eaton  26 MLB-AL       Chicago 58 262 230 37 74  56  12   1
5   2015    Shin-Soo Choo  32 MLB-AL         Texas 58 260 211 48 71  47  14   1
6   2015 Francisco Lindor  21 MLB-AL     Cleveland 58 259 224 35 79  51  17   4
  HR RBI BB IBB uBB SO HBP SH SF GDP SB CS    BA   OBP   SLG   OPS
1 13  32 26   1  25 42   2  0  1   5  6  4 0.278 0.353 0.485 0.839
2  3  30 15   0  15 35   0  0  1   9  8  0 0.286 0.326 0.387 0.713
3  6  18 10   1   9 28   4  1  3   6 11  4 0.332 0.364 0.508 0.872
4  5  31 23   1  22 55   5  2  2   1  9  4 0.322 0.392 0.448 0.840
5  9  34 39   1  38 51   8  1  1   1  2  0 0.336 0.456 0.540 0.996
6  7  32 18   0  18 38   1 11  5   4 10  2 0.353 0.395 0.558 0.953
```

The function works the same for pitchers:

```r
> head(daily_pitcher_bref(t1 = "2015-08-01", t2 = "2015-10-03"))
  season              Name Age  Level          Team  G GS  W  L SV   IP  H  R ER uBB
1   2015   Clayton Kershaw  27 MLB-NL   Los Angeles 12 12  8  1 NA 89.0 56 17 16  15
2   2015      Jake Arrieta  29 MLB-NL       Chicago 12 12 11 NA NA 88.1 41  7  4  14
3   2015  Justin Verlander  32 MLB-AL       Detroit 12 12  4  5 NA 83.1 63 28 23  19
4   2015   Hisashi Iwakuma  34 MLB-AL       Seattle 12 12  7  3 NA 82.0 65 25 24  12
5   2015    Dallas Keuchel  27 MLB-AL       Houston 12 12  8  3 NA 81.0 69 28 25  17
6   2015 Madison Bumgarner  25 MLB-NL San Francisco 11 11  7  3 NA 80.1 54 21 19  12
  BB  SO HR HBP  ERA  AB X1B X2B X3B IBB GDP SF SB CS PO  BF  Pit  Str  StL  StS GB.FB
1 15 109  4   1 1.62 314  43   9   0   0   3  0  1  3  2 331 1278 0.69 0.17 0.16  0.47
2 14  89  1   3 0.41 302  33   6   1   0   7  0 11  0  0 320 1280 0.65 0.17 0.13  0.65
3 20  78  4   1 2.48 302  43  14   2   1   3  3  2  3  0 327 1330 0.65 0.16 0.10  0.37
4 13  74  7   1 2.63 301  45  13   0   1   5  1  0  1  0 319 1154 0.69 0.18 0.11  0.52
5 17  84  9   2 2.78 304  50   9   1   0   7  2  3  0  0 325 1293 0.63 0.19 0.12  0.58
6 13  95  5   1 2.13 289  40   7   2   1   2  3  4  1  0 308 1208 0.66 0.16 0.13  0.46
    LD   PU  WHIP BAbip  SO9 SO.W SO_perc uBB_perc SO_uBB
1 0.28 0.07 0.798 0.259 11.0 7.27   0.329    0.045      0
2 0.21 0.04 0.623 0.189  9.1 6.36   0.278    0.044      0
3 0.21 0.16 0.996 0.265  8.4 3.90   0.239    0.058      0
4 0.27 0.05 0.951 0.262  8.1 5.69   0.232    0.038      0
5 0.22 0.07 1.062 0.282  9.3 4.94   0.258    0.052      0
6 0.28 0.07 0.834 0.255 10.6 7.31   0.308    0.039      0
```

Game logs are also available via FanGraphs and these two functions:

- `batter_game_logs_fg`
- `pitcher_game_logs_fg`  

Both functions has two arguments:  `player_id` and `year`. Both will return detailed game logs from FanGraphs for the selected season.

```r
> batter_game_logs_fg(playerid = 10155, year = 2018)
        Date Team  Opp BO Pos PA H X2B X3B HR R RBI SB CS BB_perc K_perc  ISO
1 2018-04-04  LAA  CLE  2  CF  5 0   0   0  0 0   0  0  0    0.40  0.200 .000
2 2018-04-03  LAA  CLE  2  CF  5 1   0   0  1 1   1  0  0    0.20  0.000 .750
3 2018-04-02  LAA  CLE  2  CF  4 0   0   0  0 0   0  0  0    0.25  0.250 .000
4 2018-04-01  LAA @OAK  2  CF  5 2   1   0  0 1   1  0  0    0.00  0.000 .200
5 2018-03-31  LAA @OAK  2  CF  5 3   2   0  0 2   2  1  0    0.00  0.200 .400
6 2018-03-30  LAA @OAK  2  CF  4 1   0   0  1 2   1  0  0    0.00  0.000 .750
7 2018-03-29  LAA @OAK  2  CF  6 0   0   0  0 0   0  0  0    0.00  0.167 .000
  BABIP  AVG  OBP   SLG wOBA wRC_plus
1  .000 .000 .400  .000 .276       78
2  .000 .250 .400 1.000 .559      280
3  .000 .000 .250  .000 .172        5
4  .400 .400 .400  .600 .432      190
5  .750 .600 .600 1.000 .686      371
6  .000 .250 .250 1.000 .526      257
7  .000 .000 .000  .000 .000     -100
```

### FanGraphs Guts and Park Factors 

__Guts__

[FanGraphs](http://fangraphs.com) provides visitors with a table of many of the components and constants they use for calculating some metrics on the site, such as wOBA and FIP. 

The `fg_guts()` function will pull this table and format it as a data frame when called (there are no paramters needed):

```r
> head(fg_guts())
  season lg_woba woba_scale   wBB  wHBP   w1B   w2B   w3B   wHR runSB  runCS lg_r_pa
1   2016   0.318      1.212 0.691 0.721 0.878 1.242 1.569 2.015   0.2 -0.410   0.118
2   2015   0.313      1.251 0.687 0.718 0.881 1.256 1.594 2.065   0.2 -0.392   0.113
3   2014   0.310      1.304 0.689 0.722 0.892 1.283 1.635 2.135   0.2 -0.377   0.108
4   2013   0.314      1.277 0.690 0.722 0.888 1.271 1.616 2.101   0.2 -0.384   0.110
5   2012   0.315      1.245 0.691 0.722 0.884 1.257 1.593 2.058   0.2 -0.398   0.114
6   2011   0.316      1.264 0.694 0.726 0.890 1.270 1.611 2.086   0.2 -0.394   0.112
  lg_r_w  cFIP
1  9.778 3.147
2  9.421 3.134
3  9.117 3.132
4  9.264 3.048
5  9.544 3.095
6  9.454 3.025
```

__Park Factors__

You can also obtain park factors from FanGraphs for every team and every season.

For overall park factors, use the `fg_park()` function, supplying the year you are interested in:

```r
> head(fg_park(1986))
  season home_team basic_5yr 3yr 1yr single double triple  hr  so UIBB GB FB LD IFFB FIP
1   1986    Angels        98  98  95     99     92     81 105 100   99 NA NA NA   NA 101
2   1986   Orioles        98  99  99     99     97     75 103 102  102 NA NA NA   NA 101
3   1986   Red Sox       103 100  99    102    112    105  98 101   99 NA NA NA   NA  98
4   1986 White Sox       103 103 101    100    102    122  97 100  106 NA NA NA   NA 100
5   1986   Indians       101 100  99    104     98     95  99  97   99 NA NA NA   NA 100
6   1986    Tigers        97  98  95     97     91     90 105 100   98 NA NA NA   NA 101
```
For park factors by batter handedness, use the `fg_park_hand()` function. Note that handedness park factors are only available going back to the 2002 season:

```r
> head(fg_park_hand(2012))
  season home_team single_as_LHH single_as_RHH double_as_LHH double_as_RHH
1   2012    Angels            99           100            95            96
2   2012   Orioles           101           101           102            98
3   2012   Red Sox           102           104           117           113
4   2012 White Sox            98            99           101            97
5   2012   Indians           101            98           101           102
6   2012    Tigers           103           101            93           102
  triple_as_LHH triple_as_RHH hr_as_LHH hr_as_RHH
1            91            85        91        93
2            88            85       114       104
3           112            88        90       102
4            94            87       106       114
5            82            85       109        93
6           122           126       100       100
```

### Leaderboards

[FanGraphs](http://fangraphs.com) has a great inteface for generating leaderboards. Currently, `baseballr` includes a function for acquiring leaderboards for batters (pitchers coming soon) using the `fg_bat_leaders()` function.

There are a few parameters you need to input:

`x`: first year of statistics to be included.
`y`: last year of statistics to be included. If you want a single year, just set `y` the same as `x`.
`league`: you can get records for all of MLB (`all`), the National Leagye (`nl`), or the American League (`al`).
`qual`: whether to include only batters that were qualified. Defaults to `y`. Alternatively, you can pass a minimum number of plate appearances to restrict the data to.
`ind`: whether to split the data by batter and individual season, or to simply aggregate by batter across the seasons selected. Defaults to aggregating (`ind = 0`). To spliy by season, use `ind = 1`.

The leaderboards will include all available metrics that FanGraph's produces.

Here's a truncated example for 2015 through 2016:

```r
> head(fg_bat_leaders(x = 2015, y = 2016, league = "all", qual = "y", ind = 0)) %>%
+     select(Seasons:AVG)
    Seasons #             Name         Team Age   G   AB   PA   H  1B 2B 3B HR   R RBI  BB IBB
1 2015-2016 1       Joey Votto         Reds  32 316 1101 1372 352 223 67  4 58 196 177 251  30
2 2015-2016 2       Mike Trout       Angels  24 318 1124 1363 345 200 64 11 70 227 190 208  26
3 2015-2016 3   Miguel Cabrera       Tigers  32 277 1024 1190 333 216 59  2 56 156 184 152  30
4 2015-2016 4     Bryce Harper    Nationals  22 300 1027 1281 295 164 62  3 66 202 185 232  35
5 2015-2016 5   Josh Donaldson    Blue Jays  30 313 1197 1411 348 190 73  7 78 244 222 182   6
6 2015-2016 6 Paul Goldschmidt Diamondbacks  28 317 1146 1400 354 221 71  5 57 209 205 228  44
   SO HBP SF SH GDP SB CS   AVG
1 255  10 10  0  27 19  4 0.320
2 295  21 10  0  16 41 14 0.307
3 198   7  7  0  45  1  1 0.325
4 248   8 14  0  26 27 14 0.287
5 252  15 13  4  32 13  1 0.291
6 301   9 15  0  30 53 10 0.309
```

And here's the same query, but this time splitting the seasons individually:

```r
> head(fg_bat_leaders(x = 2015, y = 2016, league = "all", qual = "y", ind = 1)) %>%
+     select(Season:AVG)
  Season             Name         Team Age   G  AB  PA   H  1B 2B 3B HR   R RBI  BB IBB  SO
1   2015     Bryce Harper    Nationals  22 153 521 654 172  91 38  1 42 118  99 124  15 131
2   2015       Joey Votto         Reds  31 158 545 695 171 107 33  2 29  95  80 143  15 135
3   2016      David Ortiz      Red Sox  40 151 537 626 169  82 48  1 38  79 127  80  15  86
4   2016       Mike Trout       Angels  24 159 549 681 173 107 32  5 29 123 100 116  12 137
5   2015 Paul Goldschmidt Diamondbacks  27 159 567 695 182 109 38  2 33 103 110 118  29 151
6   2015       Mike Trout       Angels  23 159 575 682 172  93 32  6 41 104  90  92  14 158
  HBP SF SH GDP SB CS   AVG
1   5  4  0  15  6  4 0.330
2   5  2  0  11 11  3 0.314
3   2  7  0  22  2  0 0.315
4  11  5  0   5 30  7 0.315
5   2  7  0  16 21  5 0.321
6  10  5  0  11 11  7 0.299
```

We can also take our original query and limit it only to batters with at least 1200 plate appearances (`qual = 1200`):

```r
> head(fg_bat_leaders(x = 2015, y = 2016, league = "all", qual = 1200, ind = 0)) %>%
+     select(Seasons:AVG)
    Seasons #             Name         Team Age   G   AB   PA   H  1B 2B 3B HR   R RBI  BB IBB
1 2015-2016 1       Joey Votto         Reds  32 316 1101 1372 352 223 67  4 58 196 177 251  30
2 2015-2016 2       Mike Trout       Angels  24 318 1124 1363 345 200 64 11 70 227 190 208  26
3 2015-2016 3     Bryce Harper    Nationals  22 300 1027 1281 295 164 62  3 66 202 185 232  35
4 2015-2016 4   Josh Donaldson    Blue Jays  30 313 1197 1411 348 190 73  7 78 244 222 182   6
5 2015-2016 5 Paul Goldschmidt Diamondbacks  28 317 1146 1400 354 221 71  5 57 209 205 228  44
6 2015-2016 6      David Ortiz      Red Sox  40 297 1065 1240 313 152 85  1 75 152 235 157  31
   SO HBP SF SH GDP SB CS   AVG
1 255  10 10  0  27 19  4 0.320
2 295  21 10  0  16 41 14 0.307
3 248   8 14  0  26 27 14 0.287
4 252  15 13  4  32 13  1 0.291
5 301   9 15  0  30 53 10 0.309
6 181   2 16  0  38  2  1 0.294
```

### NCAA Statistics

baseballr can acquire statistics for NCAA baseball teams across the three major divisions going back to 2013.

The function, `ncaa_scrape`, requires the user to pass values for three parameters for the function to work:

`school_id`: numerical code used by the NCAA for each school
`year`: a four-digit year
`type`: whether to pull data for batters or pitchers

If you want to pull batting statistics for Vanderbilt for the 2013 season, you would use the following:

```r
> baseballr::ncaa_scrape(736, 2013, "batting") %>%
+     select(year:OBPct)
   year     school   conference division Jersey            Player Yr Pos GP GS    BA OBPct
1  2013 Vanderbilt Southeastern        1     18 Yastrzemski, Mike Sr  OF 66 66 0.312 0.411
2  2013 Vanderbilt Southeastern        1     20   Harrell, Connor Sr  OF 66 66 0.312 0.418
3  2013 Vanderbilt Southeastern        1      3      Conde, Vince So INF 66 65 0.307 0.380
4  2013 Vanderbilt Southeastern        1      6        Kemp, Tony Jr  OF 66 66 0.391 0.471
5  2013 Vanderbilt Southeastern        1     55    Gregor, Conrad Jr  OF 65 65 0.308 0.440
6  2013 Vanderbilt Southeastern        1      9    Turner, Xavier Fr INF 59 51 0.324 0.387
7  2013 Vanderbilt Southeastern        1      5    Navin, Spencer Jr   C 57 56 0.302 0.430
8  2013 Vanderbilt Southeastern        1     51        Lupo, Jack Sr  OF 57 51 0.297 0.352
9  2013 Vanderbilt Southeastern        1      8    Wiseman, Rhett Fr  OF 54 11 0.289 0.360
10 2013 Vanderbilt Southeastern        1     10     Norwood, John So  OF 33  9 0.328 0.388
11 2013 Vanderbilt Southeastern        1     43      Wiel, Zander So INF 33 15 0.305 0.406
12 2013 Vanderbilt Southeastern        1     44     Harvey, Chris So   C 29 13 0.250 0.328
13 2013 Vanderbilt Southeastern        1     42   McKeithan, Joel Jr INF 25 12 0.220 0.267
14 2013 Vanderbilt Southeastern        1     39       Smith, Kyle Fr INF 23  7 0.250 0.455
15 2013 Vanderbilt Southeastern        1     17    Harris, Andrew Sr INF 21  0 0.125 0.222
16 2013 Vanderbilt Southeastern        1      2   Campbell, Tyler Fr INF 12  2 0.312 0.389
17 2013 Vanderbilt Southeastern        1      7   Swanson, Dansby Fr INF 11  4 0.188 0.435
18 2013 Vanderbilt Southeastern        1     25        Luna, D.J. Jr INF  8  0 0.000 0.333
19 2013 Vanderbilt Southeastern        1     23      Cooper, Will So  OF  4  0 1.000 1.000
20 2013 Vanderbilt Southeastern        1      -            Totals  -   -  -  - 0.313 0.407
21 2013 Vanderbilt Southeastern        1      -   Opponent Totals  -   -  -  - 0.220 0.320
```

The same can be done for pitching, just by changing the `type` parameter:

```r
> baseballr::ncaa_scrape(736, 2013, "pitching") %>%
+     select(year:ERA)
   year     school   conference division Jersey           Player Yr Pos GP App GS  ERA
1  2013 Vanderbilt Southeastern        1     11     Beede, Tyler So   P 37  17 17 2.32
2  2013 Vanderbilt Southeastern        1     33    Miller, Brian So   P 32  32 NA 1.58
3  2013 Vanderbilt Southeastern        1     35    Ziomek, Kevin Jr   P 32  17 17 2.12
4  2013 Vanderbilt Southeastern        1     15   Fulmer, Carson Fr   P 26  26 NA 2.39
5  2013 Vanderbilt Southeastern        1     39      Smith, Kyle Fr INF 23   1 NA 0.00
6  2013 Vanderbilt Southeastern        1     28    Miller, Jared So   P 22  22 NA 2.31
7  2013 Vanderbilt Southeastern        1     19     Rice, Steven Jr   P 21  21 NA 2.57
8  2013 Vanderbilt Southeastern        1     13  Buehler, Walker Fr   P 16  16  9 3.14
9  2013 Vanderbilt Southeastern        1     22  Pfeifer, Philip So   P 15  15 12 3.68
10 2013 Vanderbilt Southeastern        1     12  Ravenelle, Adam So   P 11  11 NA 3.18
11 2013 Vanderbilt Southeastern        1     40   Pecoraro, T.J. Jr   P 10  10  7 5.97
12 2013 Vanderbilt Southeastern        1     45  Ferguson, Tyler Fr   P  8   8  4 4.21
13 2013 Vanderbilt Southeastern        1     27 Kolinsky, Keenan Jr   P  2   2 NA 0.00
14 2013 Vanderbilt Southeastern        1     24    Wilson, Nevin So   P  1   1 NA 0.00
15 2013 Vanderbilt Southeastern        1      -           Totals  -   -  -  NA NA 2.76
16 2013 Vanderbilt Southeastern        1      -  Opponent Totals  -   -  -  NA NA 6.19
```

Now, the function is dependent on the user knowing the `school_id` used by the NCAA website. Given that, I've included a `school_id_lu` function so that users can find the `school_id` they need.

Just pass a string to the function and it will return possible matches based on the school's name:

```r
> school_id_lu("Vand")
# A tibble: 4 × 6
      school   conference school_id  year division conference_id
       <chr>        <chr>     <dbl> <dbl>    <dbl>         <dbl>
1 Vanderbilt Southeastern       736  2013        1           911
2 Vanderbilt Southeastern       736  2014        1           911
3 Vanderbilt Southeastern       736  2015        1           911
4 Vanderbilt Southeastern       736  2016        1           911
```









=======
>>>>>>> Stashed changes

```R
> head(fg_bat_leaders(x = 2015, y = 2016, league = "all", qual = "y", ind = 1)) %>%
+     select(Season:AVG)
  Season             Name         Team Age   G  AB  PA   H  1B 2B 3B HR   R RBI  BB IBB  SO
1   2015     Bryce Harper    Nationals  22 153 521 654 172  91 38  1 42 118  99 124  15 131
2   2015       Joey Votto         Reds  31 158 545 695 171 107 33  2 29  95  80 143  15 135
3   2016      David Ortiz      Red Sox  40 151 537 626 169  82 48  1 38  79 127  80  15  86
4   2016       Mike Trout       Angels  24 159 549 681 173 107 32  5 29 123 100 116  12 137
5   2015 Paul Goldschmidt Diamondbacks  27 159 567 695 182 109 38  2 33 103 110 118  29 151
6   2015       Mike Trout       Angels  23 159 575 682 172  93 32  6 41 104  90  92  14 158
  HBP SF SH GDP SB CS   AVG
1   5  4  0  15  6  4 0.330
2   5  2  0  11 11  3 0.314
3   2  7  0  22  2  0 0.315
4  11  5  0   5 30  7 0.315
5   2  7  0  16 21  5 0.321
6  10  5  0  11 11  7 0.299
```

We can also take our original query and limit it only to batters with at least 1200 plate appearances (`qual = 1200`):

```R
> head(fg_bat_leaders(x = 2015, y = 2016, league = "all", qual = 1200, ind = 0)) %>%
+     select(Seasons:AVG)
    Seasons #             Name         Team Age   G   AB   PA   H  1B 2B 3B HR   R RBI  BB IBB
1 2015-2016 1       Joey Votto         Reds  32 316 1101 1372 352 223 67  4 58 196 177 251  30
2 2015-2016 2       Mike Trout       Angels  24 318 1124 1363 345 200 64 11 70 227 190 208  26
3 2015-2016 3     Bryce Harper    Nationals  22 300 1027 1281 295 164 62  3 66 202 185 232  35
4 2015-2016 4   Josh Donaldson    Blue Jays  30 313 1197 1411 348 190 73  7 78 244 222 182   6
5 2015-2016 5 Paul Goldschmidt Diamondbacks  28 317 1146 1400 354 221 71  5 57 209 205 228  44
6 2015-2016 6      David Ortiz      Red Sox  40 297 1065 1240 313 152 85  1 75 152 235 157  31
   SO HBP SF SH GDP SB CS   AVG
1 255  10 10  0  27 19  4 0.320
2 295  21 10  0  16 41 14 0.307
3 248   8 14  0  26 27 14 0.287
4 252  15 13  4  32 13  1 0.291
5 301   9 15  0  30 53 10 0.309
6 181   2 16  0  38  2  1 0.294
```


### Statcast and PITCHf/x

Daren Wilman and the rest of the MLBAM crew make pitch-by-pitch and Statcast data available on the [Baseball Savant](https://baseballsavant.mlb.com) site.

`baseballr` contains five functions for acquiring this data directly into `R`:

`scrape_statcast_savant`<br>
`scrape_statcast_savant_batter`<br>
`scrape_statcast_savant_batter_all`<br>
`scrape_statcast_savant_pitcher`<br>
`scrape_statcast_savant_pitcher_all`<br>

*Note: the last four will likely be deprecated, as the first function allows users to query data in just about every way you'd want to in terms of single player, multiple players, pitchers, batters, etc.*

The pitcher/batter `savant` functions allow a user to retrieve PITCHf/x and Statcast data for either a specific batter or pitcher from [Baseball Savants' Statcast Search](https://baseballsavant.mlb.com/statcast_search). The user needs to provide a `start_date`, `end_date`, and the batter or pitcher's MLBAMID.

In this example, we are pulling data for Carlos Correa from 4/6 through 4/15/2016:

```r
> scrape_statcast_savant_batter(start_date = "2016-04-06", end_date = "2016-04-15", batterid = 621043) %>% 
     filter(type == "X") %>%
     select(3,7,54:56) %>%
     tail()
[1] "Be patient, this may take a few seconds..."
[1] "Data courtesy of Baseball Savant and MLBAM  (baseballsavant.mlb.com)"     
    game_date   player_name hit_distance_sc hit_speed hit_angle
26 2016-04-07 Carlos Correa             385    103.33     31.10
27 2016-04-07 Carlos Correa             288     87.25     27.77
28 2016-04-06 Carlos Correa             392    103.97     29.62
29 2016-04-06 Carlos Correa             189    105.20      0.11
30 2016-04-06 Carlos Correa             462    113.55     23.76
31 2016-04-06 Carlos Correa             228    113.39     -2.18
```

With the `scrape_statcast_savant` function you can query however you'd like:

```r
>head(scrape_statcast_savant(start_date = "2016-04-06", end_date = "2016-04-15", playerid = 592789, player_type='pitcher'))
 pitch_type  game_date release_speed release_pos_x release_pos_z
1         FF 2016-04-12          97.3       -0.6733        6.4372
2         FF 2016-04-12          97.8       -0.6366        6.4466
3         FF 2016-04-12          97.6       -0.4936        6.4440
4         FF 2016-04-12          97.0       -0.6884        6.5753
5         SL 2016-04-12          91.6       -0.7873        6.4002
6         CH 2016-04-12          88.9       -1.0913        6.2130
       player_name batter pitcher    events          description spin_dir
1 Noah Syndergaard 400085  592789    single        hit_into_play       NA
2 Noah Syndergaard 400085  592789      <NA>        called_strike       NA
3 Noah Syndergaard 425772  592789 field_out        hit_into_play       NA
4 Noah Syndergaard 425772  592789      <NA>        called_strike       NA
5 Noah Syndergaard 588751  592789 field_out        hit_into_play       NA
6 Noah Syndergaard 518618  592789    double hit_into_play_no_out       NA 
```
```r
>head(scrape_statcast_savant(start_date = "2016-04-06", end_date = "2016-04-06"))
  pitch_type  game_date release_speed release_pos_x release_pos_z     player_name batter pitcher
1         FT 2016-04-06          91.2       -1.9089        6.4077  Jake Marisnick 545350  467100
2         CU 2016-04-06          77.7       -1.7753        6.7376   Carlos Correa 621043  467100
3         CU 2016-04-06          80.3       -1.5339        6.6463   Carlos Correa 621043  467100
4         SL 2016-04-06          84.7       -1.7689        6.4903   Carlos Correa 621043  467100
5         FT 2016-04-06          90.8       -1.8843        6.4235   Carlos Correa 621043  467100
6         FT 2016-04-06          90.2       -1.7467        6.5141 George Springer 543807  467100
     events             description spin_dir spin_rate_deprecated break_angle_deprecated
1 field_out           hit_into_play       NA                   NA                     NA
2 strikeout swinging_strike_blocked       NA                   NA                     NA
3      <NA>                    ball       NA                   NA                     NA
4      <NA>           called_strike       NA                   NA                     NA
5      <NA>           called_strike       NA                   NA                     NA
6      walk                    ball       NA                   NA                     NA
```

Since the savant functions require users to pass a valid MLBAMID, a lookup function is included that leverages the [Chadwich Bureau Register](https://github.com/chadwickbureau/register). Users provide a text string and only those players with that string present in their last name will be returned.

Here is an example where the user is looking for players with the last name "Seager":

```r
> playerid_lookup("Seager")
[1] "Be patient, this may take a few seconds..."
[1] "Data courtesy of the Chadwick Bureau Register (https://github.com/chadwickbureau/register)"
  first_name last_name  given_name name_suffix nick_name birth_year mlb_played_first mlbam_id retrosheet_id  bbref_id fangraphs_id
1        Ben    Seager         Ben                               NA               NA       NA                                   NA
2      Corey    Seager  Corey Drew                             1994             2015   608369      seagc001 seageco01        13624
3     Justin    Seager Justin Ryan                             1992               NA   643529                                   NA
4       Kyle    Seager  Kyle Duerr                             1987             2011   572122      seagk001 seageky01         9785
```

As you can see, the table is extremely helpful as it also provides a crosswalk between a player's IDs from Retrosheet, Baseball-Reference, and FanGraphs along with MLBAM.

The file is quite large and so can take a while to return a result. So, after the first time you run the function the entire table will be added to your Global environment. This will cut down on the time of subsequent queries considerably.

The `edge_scrape()` function allows the user to scrape PITCHf/x data from the GameDay application using Carson Sievert's [pitchRx](https://github.com/cpsievert/pitchRx) package and to calculate metrics associated with [Edge%](https://billpetti.shinyapps.io/edge_shiny/). The function returns a dataframe grouped by either pitchers or batters and the percentge of pitches in each of the various Edge zones.

Example (pitchers):

```r
> edge_scrape("2015-04-06", "2015-04-07", "pitcher") %>% .[, c(1:3,7:12)] %>% head(10)
     pitcher_name pitcher All_pitches Upper_Edge Lower_Edge Inside_Edge Outside_Edge Heart Out_of_Zone
            (chr)   (dbl)       (int)      (dbl)      (dbl)       (dbl)        (dbl) (dbl)       (dbl)
1   Bartolo Colon  112526          86      0.035      0.081       0.058        0.151 0.209       0.465
2  LaTroy Hawkins  115629          12      0.000      0.333       0.000        0.000 0.083       0.583
3      Joe Nathan  150274           4      0.000      0.000       0.000        0.000 0.000       1.000
4   Buddy Carlyle  234194           9      0.000      0.222       0.000        0.000 0.333       0.444
5    Jason Grilli  276351          14      0.000      0.000       0.214        0.000 0.286       0.500
6     Kevin Gregg  276514          17      0.000      0.000       0.118        0.176 0.235       0.471
7  Joaquin Benoit  276542          19      0.053      0.053       0.105        0.000 0.158       0.632
8  Ryan Vogelsong  285064          99      0.010      0.051       0.141        0.061 0.182       0.556
9  Jeremy Affeldt  346793           5      0.000      0.000       0.200        0.000 0.000       0.800
10  Grant Balfour  346797          21      0.095      0.000       0.000        0.048 0.333       0.524
```

Example (batters):

```r
> edge_scrape("2015-04-06", "2015-04-07", "batter") %>% .[, c(1:3,7:12)] %>% head(10)
       batter_name batter All_pitches Upper_Edge Lower_Edge Inside_Edge Outside_Edge Heart Out_of_Zone
             (chr)  (dbl)       (int)      (dbl)      (dbl)       (dbl)        (dbl) (dbl)       (dbl)
1    Bartolo Colon 112526           7      0.000      0.000       0.429        0.000 0.143       0.429
2     Torii Hunter 116338          19      0.000      0.105       0.105        0.105 0.000       0.684
3      David Ortiz 120074          18      0.056      0.000       0.111        0.056 0.222       0.556
4   Alex Rodriguez 121347          17      0.000      0.000       0.353        0.000 0.118       0.529
5   Aramis Ramirez 133380          23      0.000      0.087       0.261        0.000 0.261       0.391
6    Adrian Beltre 134181          26      0.000      0.038       0.154        0.115 0.231       0.462
7   Carlos Beltran 136860          22      0.136      0.045       0.136        0.000 0.136       0.545
8  Michael Cuddyer 150212          14      0.000      0.214       0.214        0.000 0.214       0.357
9    Jimmy Rollins 276519          41      0.024      0.122       0.049        0.049 0.220       0.537
10  Ryan Vogelsong 285064          10      0.000      0.200       0.300        0.000 0.200       0.300
```

### Team Schedule and Results

Sometimes it is helpful to have the game-to-game schedule and results for a given team. This can easily be acquired using the `team_results_bref()` function. You need to supply the team acronym used at [Baseball-Reference.com](http://www.baseball-reference.com) and the season you are interested in.

Here's an example looking at the 1927 Yankees (yes, their third game of the season ended in a tie--odd, I know):

```r
> head(team_results_bref("NYY", 1927))
  Year Rk Gm#              Date  Tm H_A Opp Result  R RA Inn Record Rank     GB
1 1927  1   1   Tuesday, Apr 12 NYY   H PHA      W  8  3  NA    1-0    1   Tied
2 1927  2   2 Wednesday, Apr 13 NYY   H PHA      W 10  4  NA    2-0    1 up 0.5
3 1927  3   3  Thursday, Apr 14 NYY   H PHA      T  9  9  10    2-0    1   Tied
4 1927  4   4    Friday, Apr 15 NYY   H PHA      W  6  3  NA    3-0    1   Tied
5 1927  5   5  Saturday, Apr 16 NYY   H BOS      W  5  2  NA    4-0    1 up 1.0
6 1927  6   6    Sunday, Apr 17 NYY   H BOS      W 14  2  NA    5-0    1 up 2.0
      Win    Loss Save Time D/N Attendance Streak
1    Hoyt   Grove      2:05   D      72000      1
2 Ruether    Gray      2:15   D       8000      2
3                      2:50   D       9000      2
4 Pennock   Ehmke      2:27   D      16000      3
5 Shocker Ruffing      2:05   D      25000      4
6    Hoyt Russell      2:01   D      35000      5
```
