## Central GGobi Issue ##

The API to the GGobi core does not and should not explicitly interact with
the GUI. However, the GUI must be made aware of the core's state in order
to preserve consistency. This will necessitate encapsulation of core
functionality into objects with signals that will inform agents like the GUI
and Rggobi of changes to the core. For example, currently if one changes the
brush mode programmatically, the GUI will not be implictly updated,
yielding an invalid state.

This work seems to be partially completed by Duncan.

## Minor GGobi API issues ##

  * It would be nice if display widgets could be created without a parent window, in order to simplify embedding
  * Instead of associating a filename with a dataset, there should be a more abstract 'source' string, because data doesn't always come from files.