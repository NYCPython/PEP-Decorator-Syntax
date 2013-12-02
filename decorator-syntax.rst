PEP:
Title: Change to decorator syntax
Version: $Revision$
Last-Modified: $Date$
Author: James Powell <james@nycpython.com>,
        Andy Dirnberger <andy@nycpython.com>
Status:
Type:
Content-Type: text/x-rst
Created:
Post-History:
Resolution: http://bugs.python.org/issue19660


Abstract
========

This PEP provides a relaxed syntax for decorators. Currently, a
decorator statement is limited in what it can accept, and arbitrary
expressions will not work. The @ sign may be followed only by a dotted
name with an optional, single set of parentheses, itself optionally
containing an argument list. This restriction was introduced
deliberately, and this PEP argues for its relaxation.

Motivation
==========

Currently there is little documentation about the syntax that can be
used for decorators. `PEP-318`_ documents the syntax, but the `Python
documentation`_ only specifies the syntax using Extended Backus-Naur
Form (EBNF). There is also little explanation available for why the
syntax was used.

Upon investigation of the EBNF, these restrictions seem to stand out
in the grammar. The only other part of the grammar that enforces the
use of a dotted name is the ``import`` statement.

Relaxing the restrictions imposed on decorators, new, arguably useful
forms can be introduced. It would be possible to use decorators
consisting of syntaxes available elsewhere in the grammar. Examples
include chained callables and a decorator registry. While such
techniques can be used today, they must be wrapped inside another
callable or another similar approach.

- some of these restrictions may appear arbitrary a.b() but not a().b

- the wrapper approach makes all of these possible, but unsightly
  _ = lambda x: x
  @_( a().b )
  def foo(): pass

- the restriction serves better as a style guide issue

.. _PEP-318: http://www.python.org/dev/peps/pep-0318/
.. _Python documentation: http://docs.python.org/3/reference/compound_stmts.html#function-definitions

Rationale
=========

The change described here requires only a lifting of a deliberate
restriction, which requires very minimal changes to the Grammar and
interpreter. Most work will be focused on modifying documentation and
adding unit tests. Beyond the designs discussed in PEP-318, there were
no alternative designs considered.

Specification
=============

This relaxed syntax supports any callable expression for use as a
decorator::

    # indexed callables
    @registry[name]
    def foo():
        return 42

    # chained callables or other expressions
    @spam().eggs
    def foo():
        return 42

    @spam()()
    def foo():
        return 42

    # callables determined by a conditional
    @(spam if exp else eggs)
    def foo():
        return 42

    # lambda expressions
    @(lambda f: f)
    def foo():
        return 42

Copyright
=========

This document has been placed in the public domain.




..
   Local Variables:
   mode: indented-text
   indent-tabs-mode: nil
   sentence-end-double-space: f
   fill-column: 70
   coding: utf-8
