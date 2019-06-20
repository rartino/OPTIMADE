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

.. figure:: images/flowchart.svg
   :width: 15%
   :align: center
   :name: flowchart
   
   This is the caption of the figure.
   
This is a link to the figure named flowchart_. The link text `can be customized <flowchart_>`_.

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
.. code:: EBNF

  (* BEGIN EBNF GRAMMAR Filter *)
  (* The top-level 'filter' rule: *)

  Filter = [Spaces], Expression ;

  (* Values *)

  Constant = String | Number ;

  Value = String | Number | Property ;
  (* Note: support for Property in Value is OPTIONAL *)

  ValueList = [ Operator ], Value, { Comma, [ Operator ], Value } ;
  (* Support for Operator in ValueList is OPTIONAL *)

  ValueZip = [ Operator ], Value, Colon, [ Operator ], Value, {Colon, [ Operator ], Value} ;
  (* Support for Operator in ValueZip is OPTIONAL *)

  ValueZipList = ValueZip, { Comma, ValueZip } ;

  (* Expressions *)

  Expression = ExpressionClause, [ OR, Expression ] ;

  ExpressionClause = ExpressionPhrase, [ AND, ExpressionClause ] ;

  ExpressionPhrase = [ NOT ], ( Comparison | PredicateComparison | OpeningBrace, Expression, ClosingBrace );

  Comparison = ConstantFirstComparison |
             PropertyFirstComparison ;
  (* Note: support for ConstantFirstComparison is OPTIONAL *)

  PropertyFirstComparison = Property, ( 
                ValueOpRhs |
                KnownOpRhs |
                FuzzyStringOpRhs |
                SetOpRhs | 
                SetZipOpRhs );
  (* Note: support for SetZipOpRhs in Comparison is OPTIONAL *)

  ConstantFirstComparison = Constant, ValueOpRhs ;
				
  PredicateComparison = LengthComparison ;

  ValueOpRhs = Operator, Value ;

  KnownOpRhs = IS, ( KNOWN | UNKNOWN ) ; 

  FuzzyStringOpRhs = CONTAINS, String | STARTS, [ WITH ], String | ENDS, [ WITH ], String ;

  SetOpRhs = HAS, ( [ Operator ], Value | ALL, ValueList | EXACTLY, ValueList | ANY, ValueList | ONLY, ValueList ) ;
  (* Note: support for ONLY in SetOpRhs is OPTIONAL *)
  (* Note: support for [ Operator ] in SetOpRhs is OPTIONAL *)

  SetZipOpRhs = PropertyZipAddon, HAS, ( ValueZip | ONLY, ValueZipList | ALL, ValueZipList | EXACTLY, ValueZipList | ANY, ValueZipList ) ;

  LengthComparison = LENGTH, Property, Operator, Value ;

  PropertyZipAddon = Colon, Property, {Colon, Property} ;

  (* Property *)

  Property = Identifier, { Dot, Identifier } ;

  (* TOKENS *)

  (* Separators: *)

  OpeningBrace = '(', [Spaces] ;
  ClosingBrace = ')', [Spaces] ;

  Dot = '.', [Spaces] ;
  Comma = ',', [Spaces] ;
  Colon = ':', [Spaces] ;

  (* Boolean relations: *)

  AND = 'A', 'N', 'D', [Spaces] ;
  NOT = 'N', 'O', 'T', [Spaces] ;
  OR = 'O', 'R', [Spaces] ;

  IS = 'I', 'S', [Spaces] ;
  KNOWN = 'K', 'N', 'O', 'W', 'N', [Spaces] ;
  UNKNOWN = 'U', 'N', 'K', 'N', 'O', 'W', 'N', [Spaces] ;

  CONTAINS = 'C', 'O', 'N', 'T', 'A', 'I', 'N', 'S', [Spaces] ;
  STARTS = 'S', 'T', 'A', 'R', 'T', 'S', [Spaces] ;
  ENDS = 'E', 'N', 'D', 'S', [Spaces] ;
  WITH = 'W', 'I', 'T', 'H', [Spaces] ;

  LENGTH = 'L', 'E', 'N', 'G', 'T', 'H', [Spaces] ;
  HAS = 'H', 'A', 'S', [Spaces] ;
  ALL = 'A', 'L', 'L', [Spaces] ;
  ONLY = 'O', 'N', 'L', 'Y', [Spaces] ;
  EXACTLY = 'E', 'X', 'A', 'C', 'T', 'L', 'Y', [Spaces] ;
  ANY = 'A', 'N', 'Y', [Spaces] ;

  (* OperatorComparison operator tokens: *)

  Operator = ( '<', [ '=' ] | '>', [ '=' ] | '=' | '!', '=' ), [Spaces] ;

  (* Property syntax *)

  Identifier = LowercaseLetter, { LowercaseLetter | Digit }, [Spaces] ;

  Letter = UppercaseLetter | LowercaseLetter ;

  UppercaseLetter =
      'A' | 'B' | 'C' | 'D' | 'E' | 'F' | 'G' | 'H' | 'I' | 'J' | 'K' | 'L' |
      'M' | 'N' | 'O' | 'P' | 'Q' | 'R' | 'S' | 'T' | 'U' | 'V' | 'W' | 'X' |
      'Y' | 'Z'
  ;

  LowercaseLetter =
      'a' | 'b' | 'c' | 'd' | 'e' | 'f' | 'g' | 'h' | 'i' | 'j' | 'k' | 'l' | 
      'm' | 'n' | 'o' | 'p' | 'q' | 'r' | 's' | 't' | 'u' | 'v' | 'w' | 'x' |
      'y' | 'z' | '_'
  ;

  (* Strings: *)

  String = '"', { EscapedChar }, '"', [Spaces] ;

  EscapedChar = UnescapedChar | '\', '"' | '\', '\' ;

  UnescapedChar = Letter | Digit | Space | Punctuator | UnicodeHighChar ;

  Punctuator =
      '!' | '#' | '$' | '%' | '&' | "'" | '(' | ')' | '*' | '+' | ',' |
      '-' | '.' | '/' | ':' | ';' | '<' | '=' | '>' | '?' | '@' | '[' |
      ']' | '^' | '`' | '{' | '|' | '}' | '~'
  ;

  (* BEGIN EBNF GRAMMAR Number *)
  (* Number token syntax: *)

  Number = [ Sign ] ,
           ( Digits, [ '.', [ Digits ] ] | '.' , Digits ),
           [ Exponent ], [Spaces] ;

  Exponent =  ( 'e' | 'E' ) , [ Sign ] , Digits ;

  Sign = '+' | '-' ;

  Digits =  Digit, { Digit } ;

  Digit = '0' | '1' | '2' | '3' | '4' | '5' | '6' | '7' | '8' | '9' ;

  (* White-space: *)

  (* Special character tokens: *)

  tab = ? \t ?;
  nl  = ? \n ?;
  cr  = ? \r ?;
  vt  = ? \v ?;
  ff  = ? \f ?;

  Space = ' ' | tab | nl | cr | vt | ff ;

  Spaces = Space, { Space } ;

  (* The 'UnicodeHighChar' specifies all Unicode characters above 0x7F;
     the syntax used is the one compatible with Grammatica: *)

  UnicodeHighChar = ? [^\x00-\x7F] ? ;
 
  (* END EBNF GRAMMAR Number *)
  (* END EBNF GRAMMAR Filter *)

Appendix 3: The Regular Expressions to Check OPTiMaDe Number Syntax
-------------------------------------------------------------------

