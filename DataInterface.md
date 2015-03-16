# Data interface #

(methods that have been implemented will in data.gob)

```
public guint copy_col(self, guint j)
// returns index of new col
```

For compatibility with existing code, but will eventually be unnecessary because of pipeline changes:

  * methods to get and set vartable values (from `vartable.c`)

Should the signals be primarly column or row based?  I think column based signals will probably be sufficient most of the time, given that most operations occur on columns.

## Attribute API ##

```
_install_[row|col|data]_attribute(GParamSpec *)
_remove_[row|col|data]_attribute(name)

_set_data_attribute(name, value)
_set_col_attribute(name, j, value)
_set_row_attribute(name, i, value)

_set_col_attributev(name, value)
_set_row_attributev(name, value)

gboolean _get_data_attribute(name, &value)
gboolean _get_col_attribute(name, j, &value)
gboolean _get_row_attribute(name, i, &value)

gboolean _get_col_attributev(name, &value)
gboolean _get_row_attributev(name, &value)

gboolean _has_[row|col|data]_attribute(name)

GSList* (of GParamSpecs) _get_[row|col|data]_attributes()
```

The boolean values indicate whether the attribute was actually retrieved, since it is not possible to return `NULL` given that we may retrieve primitive types.