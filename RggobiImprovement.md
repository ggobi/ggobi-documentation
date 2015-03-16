
```
Basic objects
==============

 * ggobi instance(s)
 * display
 * plot
 * data set
 * interaction modes
 * projection modes
 * widgets
 * plugins
 
 These objects will be maintained as references to the C structures.
 They can be (de)serialized (from) to R code.
 
Example session
======================

    g <- ggobi()
    
    g$data
    g$data["mtcars"] <- data(mtcars)
    g$data

    g$data["mtcars"]$test <- rnorm(32)

    g$displays
    g$displays["first"] <- scatterplot_matrix("mtcars")
    g$displays["second"] <- scatterplot"("mtcars")
    g$displays
        
    f <- g$displays["first"]
    variables(f) <- names(mtcars)
    interaction(f) <- "brushing"
    
    brush_position(f) <- c(45,34)
    brush_size(f) <- c(10,30)

    s <- g$displays["second"]
    projection(s) <- "2D tour"
    variables(s) <- c("am","gear","carb")
    
    tour_start(s)
    tour_speed(s) <- 15
    tour_pause(s)
    

---
Datasets
---

 (x) get: records, varnames, rownames, ids, colors, glyphs, sampled, excluded, shadowed, selected, 
 (x) set: records, varnames, rownames, ids, colors, glyphs, sampled, excluded, shadowed
 (x) add: variables
 (x) clear dataset
 (x) create empty datasets, and from data frames and files
 (x) rename dataset
 (x) get the 'source' of the dataset (ie, filename)
 (x) get the dataset dimensions
 (x) get/set point colour 
 (x) get/set point glyph (includes size)
 ( ) get dataset name
	
---
Displays
---

 (x) Create/close graph display (with specified data set)
 (x) Create displays with arrays of plots
 (x) Get list of graph displays
 (x) Get display dataset
 (x) Get available display types
 (.) Get/set projection mode (only operates on current display)
 (.) Get/set interaction mode (this and the above are same operation, need to be split)
 (.) Get/set active display (cannot set)
 (x) Raise/Lower displays
 (x) Update display
 (x) Get/set display size
 (x) Get/set display location (RGtk)
 (x) Get plots within display
 (x) Get/set display options (show points, axes, tour axes, axes labels, edges, etc)
 
 *** The following modules need to become objects in GGobi (and rggobi) ***

---
Plots
---

 (x) Create plots
 (.) Get/set variables (different displays will need error checking) (cannot get)
 (.) Get/set range (cannot get)
 ( ) Get/set viewport position

---
Projection modes
---

These functions should operate on a pmode object.

Touring:

 (.) get/set projection (tentative support for getting vectors)
 ( ) get projected data
 ( ) get/set target projection
 ( ) signals for target changes and user manipulations

---
Interaction modes
---

2x1D tour:
2D tour:
Rotation:
1D tour:

 ( ) UI: get/set speed
 ( ) UI: pause/start
 ( ) UI: reinit
 ( ) UI: scramble
 ( ) UI: snap
 ( ) UI: toggle video
 ( ) UI: set manip mode (off, oblique, vert, horiz, radial, angular)

1D tour:

 ( ) UI: get/set ASH smoothing
 ( ) UI: get/set display ASH lines

1D plot:

 ( ) UI: get/set spreading method (ASH/textured)
 ( ) UI: get/set ASH smoothing
 ( ) UI: get/set display ASH lines

Parallel coordinates:

 ( ) UI: get/set row or column arrangement
 ( ) UI: get/set spreading method (dotplot, texturing, ash)
 ( ) UI: get/set ASH +smoothness

Brushing:

 (x) UI: get/set brush position
 ( ) UI: get/set transient/persistent
 ( ) UI: get/set point brushing (color & glyph, color, glyph, shadow)
 ( ) UI: get/set edge brushing (off, color & line, color only, line only, shadow)
 (x) UI: get/set brush size
 (x) UI: get/set brush location
 ( ) UI: get/set link variable
 ( ) UI: include!/exclude! shadows
 ( ) UI: brush on/off
 (x) get/set current color + glyph
 ( ) get points with certain color/glyph/size
 (.) get points under brush (see selected indices in dataset)

Scaling:

 ( ) UI: get/set position
 ( ) UI: get/set zoom
 ( ) relative changes (eg. move left 30, zoom 110%)

Identify:

 ( ) UI: get/set identify variable
 ( ) UI: get/set record label/record number/variable label/record id
 ( ) UI: remove labels!
 ( ) UI: get/set persistent/transient
 ( ) UI: get/set labelling points or edges
 ( ) get/set identified points

---
Projection pursuit
---

 ( ) UI: start/stop optimisation
 ( ) UI: get/set index (holes, central mass, LDA, gini-C, entropy-C)
 ( ) UI: get/set cooling & start temperature
 ( ) supply R call-back to calculate index from projected data

Coordinate systems
==================

Want to be able to easily convert between various coordinate systems:

 * pixel 
 * percentage
 * data (how would this work for projections?)

Serialization
=============

Need to be able to easily save/retrieve the above R objects to reconstruct a plot.  
Preferably serialisation should be in form of R code so it's possible to modify it by hand.  
Will need to ensure get and set calls are totally symmetrical.  

    serialize <- function(object, functions) {
        objectname <- deparse(substitute(object))
        paste(lapply(functions, function (f) {
            paste(f,"(", objectname, ") <- ", deparse(get(f)(object)))
        }), collapse ="\n")
    }

For each plot, write a function that does so appropriately.

A serialized dataset should include:
 * the data... as GGobi XML? (includes more info than writing out an R data frame)
 * sampled, excluded, hidden indices
 * case colors, glyphs, ids

R-Ggobi call backs
==================

 * on a timer? (for making movies)
 * on number key press
 * in general we can listen to the signals of the GGobi objects with RGtk
```