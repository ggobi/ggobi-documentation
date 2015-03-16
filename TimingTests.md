Here are some sample timing results obtained using the trunk version of ggobi on 17 April, 2006; red hat linux.  `(ggobi -t foo)`

```
data/laser.xml
TIME(init) 0.12 msec
TIME(brushing) 52.43 msec
TIME(tour_default_variables) 15.88 msec
TIME(tour_all_variables) 29.02 msec

data/olive.xml
TIME(init) 0.10 msec
TIME(brushing) 41.73 msec
TIME(tour_default_variables) 26.44 msec
TIME(tour_all_variables) 25.57 msec

data/places.xml
TIME(init) 0.11 msec
TIME(brushing) 37.58 msec
TIME(tour_default_variables) 25.40 msec
TIME(tour_all_variables) 25.75 msec

data/prim7.xml
TIME(init) 0.10 msec
TIME(brushing) 45.68 msec
TIME(tour_default_variables) 29.76 msec
TIME(tour_all_variables) 29.97 msec
```

There's some variability, of course.  Here are four sequential tests for big100x10.xml.gz

|TIME(init)|TIME(brushing)|TIME(tour\_default\_variables)|TIME(tour\_all\_variables)|
|:---------|:-------------|:-----------------------------|:-------------------------|
|0.14 msec|52.94 msec|40.89 msec|56.17 msec|
|0.11 msec|50.19 msec|41.05 msec|53.64 msec|
|0.17 msec|50.79 msec|42.51 msec|55.60 msec|
|0.11 msec|50.12 msec|41.76 msec|55.55 msec|

