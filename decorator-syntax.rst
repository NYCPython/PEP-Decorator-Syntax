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

This PEP provides a relaxed syntax for decorators.


Motivation
==========


Rationale
=========


Specification
=============

This relaxed syntax supports any callable expression for use as a
decorator::

    # lambda expressions
    @(lambda f: f)
    def foo():
        return bar

    # callables determined by a conditional
    @(spam if exp else eggs)
    def foo():
        return bar

    # chained callables
    @spam().eggs
    def foo():
        return bar


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
