=========================
Specification RST example
=========================

.. role:: json(code)
   :language: json

.. role:: optimade-filter(code)
   :language: optimade-filter


.. sectnum::

.. contents::

Example markup
==============

Lists
-----
This is an itemized list

- One
- Two

  - Sub element 1
  - Sub element 2
  - Sub element 3
  
- Three
- Four  

This is an auto-enumerated list

#. Item one

#. Item two

#. Item three

#. Item four

Images
------
Vector image can be inserted from an image folder.

.. image:: images/flowchart.svg
   :width: 15%

Inline Code
-----------
Regular inline literals `inline literal without format specifier` 
inline literal marked as json :json:`{'hello':'data', 'cucumber':42}` and
inline literal marked as optimade filter :optimade-filter:`a > b AND C:D HAS ANY 5:"x", 7:"y", 3:"z"`

Comments
--------

We can have comments in the source file which are not rendered. 

.. This text will not be shown

Notes
-----

We can use indented blocks for, e.g., implementors notes.

  **Note**: all databases should implement OPTiMaDe.
  Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do 
  eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut 
  enim ad minim veniam, quis nostrud exercitation ullamco laboris 
  nisi ut aliquip ex ea commodo consequat. 
  
  Embeded itemized list
  
  * Item 1
  * Item 2
  * Item 3
  
  Duis aute irure dolor 
  in reprehenderit in voluptate velit esse cillum dolore eu fugiat 
  nulla pariatur. Excepteur sint occaecat cupidatat non proident, 
  sunt in culpa qui officia deserunt mollit anim id est laborum.

Tables
------
Tables are about as simple/difficult as in markdown.

+------------+------------+-----------+
| Header 1   | Header 2   | Header 3  |
+============+============+===========+
| body row 1 | column 2   | column 3  |
+------------+------------+-----------+
| body row 2 | Cells may span columns.|
+------------+------------+-----------+
| body row 3 | Cells may  | - Cells   |
+------------+ span rows. | - contain |
| body row 4 |            | - blocks. |
+------------+------------+-----------+

=====  =====  ======
   Inputs     Output
------------  ------
  A      B    A or B
=====  =====  ======
False  False  False
True   False  True
False  True   True
True   True   True
=====  =====  ======

Footnotes and citations
-----------------------

We can use auto-numbered footnotes that render further down. [#one]_.
Here is another one [#two]_. And we then refer to [#one]_ again.

.. [#one] Footnote 1.
.. [#two] Footnote 2.

We can use citation references, like [CIT1]_.
And another one [CIT2]_. One can also
do an in-text citation like CIT1_.

.. [CIT1] A citation
.. [CIT2] Another citation

Term Definition
===============
There is a specific format for doing term definitions.

cucumber
  This is the definition of a cucumber

banana
  A banana is a yellow fruit.

Includes
--------
Includes of other files exist in RST, but are disabled for github rendering, so we probably shouldn't use them.

.. include:: includes/include_demo.rst


Example section from real OPTiMaDe spec
---------------------------------------
"Entry listing" endpoint response dictionaries MUST have a `data`
key. The value of this key MUST be a list containing dictionaries that
represent individual entries. In the JSON API format every dictionary
`resource object <http://jsonapi.org/format/1.0/#document-resource-objects>`_
MUST have the following fields:

* **type**: field containing the Entry type as defined in section `Responses`_
* **id**: field containing the ID of entry as defined in section `Responses`_.
  This can be the local database ID.
* **attributes**: a dictionary, containing key-value pairs representing the
  entry's properties and the following fields:
  
  * **local\_id**: the entry's local database ID (having no OPTiMaDe requirements/conventions)
  * **last\_modified**: an `ISO 8601 <https://www.iso.org/standard/40874.html>`_
    representing the entry's last modification time
  * **immutable\_id**: an OPTIONAL field containing the entry's immutable ID (e.g., an UUID).
  This is important for databases having preferred IDs that point to "the latest version" of a
  record, but still offer access to older variants. This ID maps to the version-specific record,
  in case it changes in the future.

  Database-provider-specific properties need to include the database-provider-specific prefix
  (see `Appendix 1: Database-Provider-Specific Namespace Prefixes`_).

OPTIONALLY it can also contains the following fields:

* **links**: a `JSON API links object <http://jsonapi.org/format/1.0/#document-links>`_ can OPTIONALLY
  contain the field
  
  * **self**: the entry's URL
  
* **meta**: a `JSON API meta object <https://jsonapi.org/format/1.0/#document-meta>`_ that contains
  non-standard meta-information about the object
  
* **relationships**: a dictionary containing references to other resource objects as defined in
  `Responses`_

Example:

.. code:: jsonc

  {
    "data": [
      {
        "type": "structure",
        "id": "example.db:structs:0001",
        "attributes": {
          "chemical_formula_descriptive": "Es2 O3",
          "local_id": "example.db:structs:0001",
          "url": "http://example.db/structs/0001",
          "immutable_id": "http://example.db/structs/0001@123",
          "last_modified": "2007-04-05T14:30Z"
        }
      },
      {
        "type": "structure",
        "id": "example.db:structs:1234",
        "attributes": {
          "chemical_formula_descriptive": "Es2",
          "local_id": "example.db:structs:1234",
          "url": "http://example.db/structs/1234",
          "immutable_id": "http://example.db/structs/1234@123",
          "last_modified": "2007-04-07T12:02Z"
        },
      },
      // ...
    ]
    // ...
  }

Responses
---------
Bla bla

Response Format
...............
Bla bla
  
Database-Provider-Specific Namespace Prefixes
=============================================

The Filter Language EBNF Grammar
================================

The Regular Expressions to Check OPTiMaDe Number Syntax
=======================================================

Appendicies
===========

Appendix 1: Database-Provider-Specific Namespace Prefixes
---------------------------------------------------------

Appendix 2: The Filter Language EBNF Grammar
--------------------------------------------

Appendix 3: The Regular Expressions to Check OPTiMaDe Number Syntax
-------------------------------------------------------------------

