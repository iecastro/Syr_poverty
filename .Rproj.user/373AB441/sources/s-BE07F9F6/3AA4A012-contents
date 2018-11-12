Syracuse Poverty
================

Poverty in Syracuse
===================

Percent of people in poverty in Syracuse since 2011 (ACS 1-yr)
--------------------------------------------------------------

![](post_figs/census_poverty-poverty%20history-1.png)

Poverty by city in 2017
-----------------------

![](post_figs/census_poverty-poverty%20compared-1.png)

Public Transportation History
-----------------------------

![](post_figs/census_poverty-public%20transportation%20poverty%20history-1.png)

Public transportation by city
-----------------------------

![](post_figs/census_poverty-public%20transport%20city-1.png)

Map of public transportation ridership
--------------------------------------

    ## Reading layer `City_Streets_2011' from data source `\\hd.ad.syr.edu\02\c3964a\Documents\Desktop\DataProjects\Syr_poverty\shapefile\City_Streets_2011.shp' using driver `ESRI Shapefile'
    ## Simple feature collection with 5650 features and 50 fields
    ## geometry type:  LINESTRING
    ## dimension:      XY
    ## bbox:           xmin: -76.20455 ymin: 42.98442 xmax: -76.07427 ymax: 43.08618
    ## epsg (SRID):    4326
    ## proj4string:    +proj=longlat +datum=WGS84 +no_defs

![](post_figs/census_poverty-public%20transportation%20map-1.png)

Percent public transportation overall
-------------------------------------

![](post_figs/census_poverty-unnamed-chunk-2-1.png)

Percent of people with computer science or math degrees
-------------------------------------------------------

![](post_figs/census_poverty-compsci-1.png)

No schooling by census tract
----------------------------

    ## Reading layer `highway_SYR' from data source `\\hd.ad.syr.edu\02\c3964a\Documents\Desktop\DataProjects\Syr_poverty\shapefile\highway_SYR.shp' using driver `ESRI Shapefile'
    ## Simple feature collection with 313 features and 69 fields
    ## geometry type:  LINESTRING
    ## dimension:      XY
    ## bbox:           xmin: 402638.1 ymin: 4760100 xmax: 411745.1 ymax: 4770180
    ## epsg (SRID):    26918
    ## proj4string:    +proj=utm +zone=18 +datum=NAD83 +units=m +no_defs

    ## Reading layer `Syracuse_TNT_Areas' from data source `\\hd.ad.syr.edu\02\c3964a\Documents\Desktop\DataProjects\Syr_poverty\shapefile\Syracuse_TNT_Areas.shp' using driver `ESRI Shapefile'
    ## Simple feature collection with 8 features and 3 fields
    ## geometry type:  POLYGON
    ## dimension:      XY
    ## bbox:           xmin: 401858.6 ymin: 4759706 xmax: 412459.8 ymax: 4771030
    ## epsg (SRID):    26918
    ## proj4string:    +proj=utm +zone=18 +datum=NAD83 +units=m +no_defs

Less than high school education
-------------------------------

![](post_figs/census_poverty-unnamed-chunk-3-1.png)

Percentage of people with computers and internet connectivity
-------------------------------------------------------------

![](post_figs/census_poverty-connectivity-1.png)

Lived in the same house 1 year ago
----------------------------------

### Quantiles

![](post_figs/census_poverty-same%20house%20-1.png)

### Percentages

``` r
SouthCampus <- same_house %>% filter(GEOID == "36067005602") %>%
  st_centroid()

MainCampus <-same_house %>% filter(GEOID == "36067004302") %>%
  st_centroid()


ggplot() +
  geom_sf(data = same_house, aes(fill = percentage, color = percentage)) + 
  geom_sf(data=MainCampus) +
  geom_sf(data = SouthCampus) +
  theme_minimal() + theme(axis.text = element_blank()) +
  scale_fill_viridis_c(option = "cividis",labels = scales::percent, direction = -1) +
  scale_color_viridis_c(option = "cividis",labels = scales::percent, direction = -1) +
  labs(fill ="", color="", caption = "*Census-tracts of Syracuse University's Main and South Campus") 
```

![](post_figs/census_poverty-unnamed-chunk-4-1.png)

### Unfit properties

``` r
Unfit_prop.Dec2017 <-st_read("https://opendata.arcgis.com/datasets/9ec2872366974b949bbee2e43047b730_0.geojson")
```

    ## Reading layer `9ec2872366974b949bbee2e43047b730_0' from data source `https://opendata.arcgis.com/datasets/9ec2872366974b949bbee2e43047b730_0.geojson' using driver `GeoJSON'
    ## Simple feature collection with 233 features and 14 fields
    ## geometry type:  POINT
    ## dimension:      XY
    ## bbox:           xmin: -76.19794 ymin: 42.99771 xmax: -76.09212 ymax: 43.07647
    ## epsg (SRID):    4326
    ## proj4string:    +proj=longlat +datum=WGS84 +no_defs

``` r
ggplot() +
  geom_sf(data = same_house, aes(fill = percentage, color = percentage)) + 
  geom_sf(data = Unfit_prop.Dec2017, colour = "red", size = .90)+
  theme_minimal() + theme(axis.text = element_blank()) +
  scale_fill_viridis_c(option = "cividis",labels = scales::percent, direction = -1) +
  scale_color_viridis_c(option = "cividis",labels = scales::percent, direction = -1) +
  labs(fill ="", color="") 
```

![](post_figs/census_poverty-unnamed-chunk-5-1.png)

Moved into current residence in the past year
---------------------------------------------

``` r
Moved <- c(TotalM = "B07001_001",M1to4 = "B07001_002",M5to17 = "B07001_003",
           M18to19 = "B07001_004", M20to24 = "B07001_005", M25to29 = "B07001_006",
           M30to34 = "B07001_007", M35to39 = "B07001_008", M40to44 = "B07001_009",
           M45to49 = "B07001_010", M50to54 = "B07001_011",M55to59 = "B07001_012",
           M60to64 = "B07001_013", M65to69 = "B07001_014", M70to74 = "B07001_015",
           M75over = "B07001_016")

mobility <- get_acs(geography = "tract", state = "NY", county = "Onondaga",
                    variables = Moved, 
                    output = "wide", geometry = TRUE, year = 2016,
                    survey = "acs5")
```

``` r
mobility %>%  
  filter(as.numeric(GEOID) < 36067006104) %>% 
  ggplot() + geom_sf(aes(fill = TotalME, color = TotalME)) + 
  scale_fill_viridis_c(labels = scales::comma) +
  scale_color_viridis_c(labels = scales::comma) +
  geom_sf(data=MainCampus) +
  geom_sf(data = SouthCampus) +theme_minimal() + 
  theme(axis.text = element_blank()) +
  labs(fill ="", color="" , caption = "*Census-tracts of Syracuse University's Main and South Campus")
```

![](post_figs/census_poverty-unnamed-chunk-7-1.png)
