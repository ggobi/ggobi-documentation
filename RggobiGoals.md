# Basic objects #

  * ggobi instance(s)
  * display
  * plot
  * data set
  * interaction modes
  * projection modes
  * widgets
  * plugins

> These objects will be maintained as references to the C structures.
> They can be (de)serialized (from) to R code.

# Example session #

> g <- ggobi()

> g$data
> g$data["mtcars"] <- data(mtcars)
> g$data

> g$data["mtcars"]$test <- rnorm(32)

> g$displays
> g$displays["first"] <- scatterplot\_matrix("mtcars")
> g$displays["second"] <- scatterplot"("mtcars")
> g$displays

> f <- g$displays["first"]
> variables(f) <- names(mtcars)
> interaction(f) <- "brushing"

> brush\_position(f) <- c(45,34)
> brush\_size(f) <- c(10,30)

> s <- g$displays["second"]
> projection(s) <- "2D tour"
> variables(s) <- c("am","gear","carb")

> tour\_start(s)
> tour\_speed(s) <- 15
> tour\_pause(s)

Status codes:
> [ ] not implemented
> [x](x.md) implemented in old api
> [u](u.md) updated to new api
> [t](t.md) tests written

# Datasets #

> [x](x.md) get: records, varnames, rownames, ids, selected, colors, glyphs, rows-in-plot, sampled, excluded, hidden
> [x](x.md) set: records, varnames, rownames, ids, colors, glyphs, sampled, excluded, hidden
> [x](x.md) add: variables
> [x](x.md) clear dataset
> [x](x.md) create empty datasets, and from data frames and files
> [x](x.md) rename dataset
> [x](x.md) get the 'source' of the dataset (ie, filename)
> [x](x.md) get the dataset dimensions
> [x](x.md) get/set point colour
> [x](x.md) get/set point glyph (includes size)
> [ ] get dataset name

# Displays #

> [x](x.md) Create/close graph display (with specified data set)
> [x](x.md) Create displays with arrays of plots
> [x](x.md) Get list of graph displays
> [x](x.md) Get display dataset
> [x](x.md) Get available display types
> [.] Get/set projection mode (only operates on current display)
> [.] Get/set interaction mode (this and the above are same operation, need to be split)
> [.] Get/set active display (cannot set)
> [x](x.md) Raise/Lower displays
> [x](x.md) Update display
> [x](x.md) Get/set display size
> [x](x.md) Get/set display location (RGtk)
> [x](x.md) Get plots within display
> [x](x.md) Get/set display options (show points, axes, tour axes, axes labels, edges, etc)

  * **The following modules need to become objects in GGobi (and rggobi)**

# Plots #

> [x](x.md) Create plots
> [.] Get/set variables (different displays will need error checking) (cannot get)
> [.] Get/set range (cannot get)
> [ ] Get/set viewport position

# Projection modes #

These functions should operate on a display object.

## 1D plot ##

> [ ] UI: get/set spreading method (ASH/textured)
> [ ] UI: get/set ASH smoothing
> [ ] UI: get/set display ASH lines

## 1D tour ##

> [ ] UI: get/set ASH smoothing
> [ ] UI: get/set display ASH lines
> [ ] touring

## 2D tour ##

> [ ] rotation

## 2x1D tour ##

> [ ] rotation
> [ ] UI: get/set manip variable (one for each of x and y axes).
> [ ] UI: get/set manip mode (off, comb, vert, horz, equalcomb)

## Parallel coordinates ##

> [ ] UI: get/set row or column arrangement
> [ ] UI: get/set spreading method (dotplot, texturing, ash)
> [ ] UI: get/set ASH +smoothness

## Rotation/Touring/Manual ##

> [ ] UI: get/set speed
> [ ] UI: pause/start
> [ ] UI: reinit
> [ ] UI: scramble
> [ ] UI: set manip variable
> [ ] UI: set manip mode (off, oblique, vert, horiz, radial, angular)
> [.] get/set projection (tentative support for getting vectors)
> [ ] get projected data
> [ ] get/set target projection
> [ ] signals for target changes and user manipulations

## Projection pursuit ##

> [ ] UI: start/stop optimisation
> [ ] UI: get/set index (holes, central mass, LDA, gini-C, entropy-C)
> [ ] UI: get/set cooling & start temperature
> [ ] supply R call-back to calculate index from projected data

# Interaction modes #

## Brushing ##

> [x](x.md) UI: get/set brush position
> [ ] UI: get/set transient/persistent
> [ ] UI: get/set point brushing (color & glyph, color, glyph, shadow)
> [ ] UI: get/set edge brushing (off, color & line, color only, line only, shadow)
> [x](x.md) UI: get/set brush size
> [x](x.md) UI: get/set brush location
> [ ] UI: get/set link variable
> [ ] UI: include!/exclude! shadows
> [ ] UI: brush on/off
> [x](x.md) get/set current color + glyph
> [ ] get points with certain color/glyph/size
> [.] get points under brush (see selected indices in dataset)

## Scaling ##

> [ ] UI: get/set position
> [ ] UI: get/set zoom
> [ ] relative changes (eg. move left 30, zoom 110%)

## Identify ##

> [ ] UI: get/set identify variable
> [ ] UI: get/set record label/record number/variable label/record id
> [ ] UI: remove labels!
> [ ] UI: get/set persistent/transient
> [ ] UI: get/set labelling points or edges

> [ ] get/set identified points

# Coordinate systems #

Want to be able to easily convert between various coordinate systems:

  * pixel
  * percentage
  * data (how would this work for projections?)

# Serialization #

Need to be able to easily save/retrieve the above R objects to reconstruct a plot.
Preferably serialisation should be in form of R code so it's possible to modify it by hand.
Will need to ensure get and set calls are totally symmetrical.

```
    serialize <- function(object, functions) {
       objectname <- deparse(substitute(object))
       paste(lapply(functions, function (f) {
           paste(f,"(", objectname, ") <- ", deparse(get(f)(object)))
       }), collapse ="\n")
    }
```
For each plot, write a function that does so appropriately.

A serialized dataset should include:

  * the data... as GGobi XML? (includes more info than writing out an R data frame)
  * sampled, excluded, hidden indices
  * case colors, glyphs, ids

# R-GGobi call backs #

  * on a timer? (for making movies)
  * on number key press
  * in general we can listen to the signals of the GGobi objects with RGt

# Testing #

We need a comprehensive suite of tests that is run every time that the rggobi2 package is built (regularly!).  These should start off with basic tests of rggobi functions (eg. set a value and then retrieve it), but will eventually provide a set of regression and integration tests for ggobi that ensure that everything is working ok.