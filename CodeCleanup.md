# Files that are no longer used #

(but we might want to keep around to use in the future)

  * write state (this will be replaced by Rggobi2 functionality)
    * I think the purpose is to write out the current file names and displays so ggobi can start up where it left off; I agree with replacing it. (dfs)
  * dbms related stuff (should be a plugin)
  * noop-checkbutton.c (not currently built - not currently needed but should be kept around)

These could be moved into an old directory so they are out of the way, but still easily accessible.

Deleted
  * write svg (plugin, should we have rendering plugins?)
    * doubtless obsolete, and never completed in the first place; deleted (dfs)
  * record\_id.c (not currently built?)
    * obsolete; deleted (dfs)
  * rotate\_ui.c (not currently built - apparently replaced by tour2d3)
    * obsolete; deleted (dfs)
  * scale\_click.c (not currently built?)
    * obsolete; deleted (dfs)
  * ascii (and binary, see read\_array.c) read and write code
    * deleted. (dfs)
  * s\_erf.c (error function stuff, required by C99 standard, so we don't need this anymore)

# Code that is no longer used: #

(Found by grepping for #ifdef)

## Things I'm pretty sure could be removed ##

  * DISALLOW\_PARADOX\_QUOTE\_ERRORS - This will be rewritten eventually using GScanner
  * BEFORE      barchart.c:555
  * WRITEASCII      io.c:106
    * deleted (dfs)
  * XXX      read\_xml.c:304
  * FORMERLY      vartable\_ui.c:376
  * GGOBI\_MAIN      GGStructSizes.c:32
  * G\_ENABLE\_DEBUG      marshal.c:5
  * G\_LIKELY      ggobi-data.c:15
  * HAVE\_UNDERSCORE\_SYMBOL\_PREFIX      plugin.c:186
  * OBSOLETE\_EDGE\_CODE      ggobi-API.c:794
    * deleted (dfs)
  * OVER      tourcorr.c:663
  * PREV      barchart.c:1233
  * PREV      barchart.c:1341
  * PREV      barchartClass.c:537
  * SPECTRUM7      color.c:126
    * keep for debugging purposes (dfs)
  * UNUSED      read\_array.c:463
  * USE\_DEPRECATED      read\_array.c:487
  * TEST\_DESTROY      ggobiClass.c:231
  * TEST\_DESTROY      ggobiClass.c:247
  * TEST\_GGOBI\_APPP      ggobi.c:444
  * TEST\_GGOBI\_EVENTS      main\_ui.c:1070
  * TEST\_GGOBI\_EVENTS      main\_ui.c:35
  * TEST\_KEYS      ggobi.c:304
  * TEST\_KEYS      ggobi.c:422
  * FORCE\_ADD\_DISPLAY      ggobi-API.c:431
  * FORCE\_ADD\_DISPLAY      ggobi-API.c:446
  * FORCE\_ADD\_DISPLAY      ggobi-API.c:459
  * FORCE\_ADD\_DISPLAY      ggobi-API.c:473


## Past experiments that never got finished? ##

  * SMOOTH\_IMPLEMENTED      main\_ui.c:783
  * SMOOTH\_IMPLEMENTED      main\_ui.c:889
  * SMOOTH\_IMPLEMENTED      main\_ui.c:949
  * INFERENCE\_IMPLEMENTED      main\_ui.c:879
  * INFERENCE\_IMPLEMENTED      main\_ui.c:931
  * TS\_EXTENSIONS\_IMPLEMENTED      time\_ui.c:102
  * TS\_EXTENSIONS\_IMPLEMENTED      time\_ui.c:29
  * TS\_EXTENSIONS\_IMPLEMENTED      time\_ui.c:47
  * TS\_EXTENSIONS\_IMPLEMENTED      time\_ui.c:76
  * EXPLICIT\_IDENTIFY\_HANDLER      ggobi-API.c:1074
  * EXPLICIT\_IDENTIFY\_HANDLER      identify\_ui.c:203
  * FREEZE\_IMPLEMENTED      varcircles.c:246
  * FREEZE\_IMPLEMENTED      varcircles.c:279
  * FREEZE\_IMPLEMENTED      varcircles.c:443
  * STORE\_SESSION\_ENABLED      main\_ui.c:858

## Tour related ##

  * TESTING\_TOUR\_STEP      tour1d.c:381
  * TESTING\_TOUR\_STEP      tour1d.c:58
  * TESTING\_TOUR\_STEP      tour1d.c:824
  * TOUR\_ADV\_IMPLEMENTED   tour1d\_ui.c:155
  * TOUR\_ADV\_IMPLEMENTED   tour1d\_ui.c:303
  * TOUR\_ADV\_IMPLEMENTED   tour1d\_ui.c:330
  * TOUR\_ADV\_IMPLEMENTED   tour1d\_ui.c:362
  * TOUR\_ADV\_IMPLEMENTED   tour1d\_ui.c:372
  * TOUR\_ADV\_IMPLEMENTED   tour1d\_ui.c:381
  * TOUR\_ADV\_IMPLEMENTED   tour1d\_ui.c:388
  * TOUR\_ADV\_IMPLEMENTED   tour1d\_ui.c:402
  * TOUR\_ADV\_IMPLEMENTED   tour1d\_ui.c:409
  * TOUR\_ADV\_IMPLEMENTED   tour1d\_ui.c:426
  * TOUR\_ADV\_IMPLEMENTED   tour2d\_ui.c:134
  * TOUR\_ADV\_IMPLEMENTED   tour2d\_ui.c:293
  * TOUR\_ADV\_IMPLEMENTED   tour2d\_ui.c:324
  * TOUR\_ADV\_IMPLEMENTED   tour2d\_ui.c:380
  * TOUR\_ADV\_IMPLEMENTED   tourcorr\_ui.c:128
  * TOUR\_PP\_IMPLEMENTED    tourcorr\_ui.c:123
  * TOUR\_PP\_IMPLEMENTED    tourcorr\_ui.c:336
  * TOUR\_PP\_IMPLEMENTED    tourcorr\_ui.c:75
  * EXCEPTION\_HANDLING     tour.c:408
  * EXCEPTION\_HANDLING     tour.c:430
  * EXCEPTION\_HANDLING     tour.c:440
  * EXCEPTION\_HANDLING     tour.c:450
  * EXCEPTION\_HANDLING     tour.c:493
  * EXCEPTION\_HANDLING     tour.c:598
  * EXCEPTION\_HANDLING     tour.c:812
  * EXCEPTION\_HANDLING     tour2d.c:1292
  * EXCEPTION\_HANDLING     tour2d.c:1299
  * EXCEPTION\_HANDLING     tour2d.c:1306
  * EXCEPTION\_HANDLING     tour2d.c:1366
  * EXCEPTION\_HANDLING     tour2d.c:950
  * EXCEPTION\_HANDLING     tour2d3.c:1011
  * EXCEPTION\_HANDLING     tour2d3.c:1018
  * EXCEPTION\_HANDLING     tour2d3.c:1025
  * EXCEPTION\_HANDLING     tour2d3.c:1085
  * EXCEPTION\_HANDLING     tour2d3.c:663

## Database related ##

  * USE\_DBMS      GGStructSizes.c:11
  * USE\_DBMS      GGStructSizes.c:24
  * USE\_MYSQL      ggobi.c:158
  * USE\_MYSQL      make\_ggobi.c:39
  * USE\_PROPERTIES      dbms.c:231
  * USE\_PROPERTIES      dbms\_ui.c:19


## Don't know why we have these ones ##

I don't know for sure, either, but I know that some compilers on some architectures require include files that others don't. (dfs)

  * USE\_STRINGS\_H      brush\_ui.c:22
  * USE\_STRINGS\_H      color.c:19
  * USE\_STRINGS\_H      display.c:18
  * USE\_STRINGS\_H      identify\_ui.c:19
  * USE\_STRINGS\_H      io.c:21
  * USE\_STRINGS\_H      lineedit\_ui.c:18
  * USE\_STRINGS\_H      main\_ui.c:19
  * USE\_STRINGS\_H      movepts\_ui.c:18
  * USE\_STRINGS\_H      p1d\_ui.c:17
  * USE\_STRINGS\_H      rotate\_ui.c:18
  * USE\_STRINGS\_H      scale\_ui.c:19
  * USE\_STRINGS\_H      scatmat.c:17
  * USE\_STRINGS\_H      scatmat\_ui.c:17
  * USE\_STRINGS\_H      tour.c:20
  * USE\_STRINGS\_H      tour1d.c:18
  * USE\_STRINGS\_H      tour1d\_pp.c:23
  * USE\_STRINGS\_H      tour1d\_ui.c:19
  * USE\_STRINGS\_H      tour2d.c:18
  * USE\_STRINGS\_H      tour2d3.c:18
  * USE\_STRINGS\_H      tour2d3\_ui.c:19
  * USE\_STRINGS\_H      tour2d\_pp.c:23
  * USE\_STRINGS\_H      tour2d\_ui.c:19
  * USE\_STRINGS\_H      tourcorr.c:18
  * USE\_STRINGS\_H      tourcorr\_ui.c:19
  * USE\_STRINGS\_H      tour\_pp.c:23
  * USE\_STRINGS\_H      varpanel\_ui.c:18
  * USE\_STRINGS\_H      xyplot\_ui.c:17

## Windows related ##

(should be reduced as much as possible, use more
cross-platform gtk stuff?)

  * WIN32      splot.c:402
  * WIN32      splot.c:526
  * WIN32      sp\_plot.c:182
  * WIN32      sp\_plot.c:214
  * WIN32      sp\_plot.c:348
  * WIN32      sp\_plot.c:387 - Need to test speed without Win32 drawing code.
  * WIN32      win32\_draw.c:35
  * G\_OS\_WIN32      plugin.c:26
  * G\_OS\_WIN32      plugin.c:562
  * G\_OS\_WIN32      plugin.c:718 - The plugin stuff should be moved to libltdl for cross-platform compatibility.

## Compiler ##

  * STRICT\_ANSI      fileio.c:27
  * STRICT\_ANSI      plugin.c:61

## Files with #if 0 ##

  * barchartClass.c:577
  * barchart\_ui.c:368
  * barchart\_ui.c:97 - This is now BARCHART\_SCALE
  * edges.c:261
    * added comment (dfs)
  * tour2d\_pp.c:693

## Cairo experiementation ##

  * ENABLE\_CAIRO      scatterplotClass.c:260
  * ENABLE\_CAIRO      scatterplotClass.c:275
  * ENABLE\_CAIRO      scatterplotClass.c:28
  * ENABLE\_CAIRO      scatterplotClass.c:303
  * ENABLE\_CAIRO      scatterplotClass.c:327
  * ENABLE\_CAIRO      scatterplotClass.c:355
  * ENABLE\_CAIRO      scatterplotClass.c:367
  * ENABLE\_CAIRO      scatterplotClass.c:412
  * ENABLE\_CAIRO      sp\_plot\_axes.c:100
  * ENABLE\_CAIRO      sp\_plot\_axes.c:131
  * ENABLE\_CAIRO      sp\_plot\_axes.c:151
  * ENABLE\_CAIRO      sp\_plot\_axes.c:157
  * ENABLE\_CAIRO      sp\_plot\_axes.c:162
  * ENABLE\_CAIRO      sp\_plot\_axes.c:225
  * ENABLE\_CAIRO      sp\_plot\_axes.c:246
  * ENABLE\_CAIRO      sp\_plot\_axes.c:252
  * ENABLE\_CAIRO      sp\_plot\_axes.c:257
  * ENABLE\_CAIRO      sp\_plot\_axes.c:373
  * ENABLE\_CAIRO      sp\_plot\_axes.c:379
  * ENABLE\_CAIRO      sp\_plot\_axes.c:384
  * ENABLE\_CAIRO      sp\_plot\_axes.c:407
  * ENABLE\_CAIRO      sp\_plot\_axes.c:413
  * ENABLE\_CAIRO      sp\_plot\_axes.c:418
  * ENABLE\_CAIRO      sp\_plot\_axes.c:437
  * ENABLE\_CAIRO      sp\_plot\_axes.c:49
  * ENABLE\_CAIRO      sp\_plot\_axes.c:56
  * ENABLE\_CAIRO      sp\_plot\_axes.c:89
  * ENABLE\_CAIRO      sp\_plot\_axes.c:95
  * ENABLE\_CAIRO      utils\_gdk.c:23
  * ENABLE\_CAIRO      utils\_gdk.c:296
  * ENABLE\_CAIRO      varcircles.c:23
  * ENABLE\_CAIRO      varcircles.c:259
  * ENABLE\_CAIRO      varcircles.c:284
  * ENABLE\_CAIRO      varcircles.c:641
  * ENABLE\_CAIRO      varcircles.c:671
  * ENABLE\_CAIRO      varcircles.c:695
  * ENABLE\_CAIRO      varcircles.c:719
  * ENABLE\_CAIRO      varcircles.c:726
  * ENABLE\_CAIRO      varcircles.c:734

There'll be a lot less of these once we get a modular rendering system.