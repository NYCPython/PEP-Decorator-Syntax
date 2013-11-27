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

This PEP provides a relaxed syntax for decorators. Currently, a decorator statement is limited in what it can accept, and arbitrary expressions will not work. The @ sign may be followed only by a dotted name with an optional, single set of parentheses, itself optionally containing an argument list. This restriction was introduced deliberately, and this PEP argues for its relaxation.

Motivation
==========

- there is almost no documentation of this restriction. PEP-318 documents it, but the standard documentation only specifies it in terms of the EBNF. Almost no discussions of the language mention this restriction, and it is not widely known.
- the restriction is a special case to the grammar without an immediately visible reason why; the only other place where a dotted name is used is in the import statement
- the restriction prevents some arguably useful forms, such as a decorator registry or the chained callable, which current require a wrapping function or some repetition to achieve
- some of these restrictions may appear arbitrary a.b() but not a().b
- the wrapper approach makes all of these possible, but unsightly
  _ = lambda x: x
  @_( a().b )
  def foo(): pass
- the restriction serves better as a style guide issue

Rationale
=========


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
