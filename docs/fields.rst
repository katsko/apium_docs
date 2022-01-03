======
Fields
======

Python JSON-RPC Framework

BaseField
---------

Description
~~~~~~~~~~~

If you want create API-field without any base attributes and methods you can inherit your class from this base field.

Framework search API-fields in API-method by type *BaseField*.

.. warning::
   In most cases you should use the class *Field* for inheritance

Example
~~~~~~~

.. code-block:: python

    from apium import af

    class MyVeryCustomField(BaseField):
        pass


Field
-----

Description
~~~~~~~~~~~

Main API-field class. Other API-field classes inherit by this one, e. g.: *Int*, *Bool*, *Str*, etc.

If you want create custom API-field type in most cases you should inherit by *Field*.

Class *Field* contains base attributes and method.

Attributes
~~~~~~~~~~

validators
