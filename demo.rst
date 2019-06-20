=========================
Specification RST example
=========================

.. sectnum::

.. contents::

Introduction
============
Bla bla.

Term Definition
===============
Bla bla.

General API Requirements and Conventions
========================================
Bla bla

Base URL
--------
This is an unordered list

- One
- Two

  - Sub element 1
  - Sub element 2
  - Sub element 3
  
- Three
- Four  

Example section from OPTiMaDe spec
----------------------------------
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

