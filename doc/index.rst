.. sphinxcontrib-autoprogram documentation master file, created by
   sphinx-quickstart on Sun Mar  2 02:39:38 2014.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

.. module:: sphinxcontrib.autoprogram

:mod:`sphinxcontrib.autoprogram` --- Documenting CLI programs
=============================================================

.. image:: https://badge.fury.io/py/sphinxcontrib-autoprogram.svg
   :target: https://pypi.org/project/sphinxcontrib-autoprogram/
   :alt: Latest PyPI version

.. image:: https://readthedocs.org/projects/sphinxcontrib-autoprogram/badge/
   :target: https://sphinxcontrib-autoprogram.readthedocs.io/
   :alt: Documentation Status

.. image:: https://travis-ci.org/sphinx-contrib/autoprogram.svg?branch=master
   :alt: Build Status
   :target: https://travis-ci.org/sphinx-contrib/autoprogram

This contrib extension, :mod:`sphinxcontrib.autoprogram`, provides an automated
way to document CLI programs.  It scans :class:`argparse.ArgumentParser`
object, and then expands it into a set of :rst:dir:`.. program::` and
:rst:dir:`.. option::` directives.

In order to use it, add :mod:`sphinxcontrib.autoprogram` into
:data:`extensions` list of your Sphinx configuration file (:file:`conf.py`)::

    extensions = ['sphinxcontrib.autoprogram']

.. seealso::

   Module :mod:`argparse`
      This extension assumes a program to document is made using
      :mod:`argparse` module which is a part of the Python standard library.


:rst:dir:`.. autoprogram::` directive
-------------------------------------

Its only and simple way to use is :rst:dir:`.. autoprogram::` directive.
It's similar to :mod:`sphinx.ext.autodoc` extension's
:rst:dir:`.. automodule::` and other directives.

For example, given the following Python CLI program (say it's :file:`cli.py`):

.. include:: cli.py
   :code:

In order to document the above program:

.. code-block:: rst

   .. autoprogram:: cli:parser
      :prog: cli.py

That's it.  It will be rendered as:

    .. autoprogram:: cli:parser
       :prog: cli.py

If there are subcommands (subparsers), they are rendered to subsections.
For example, givem the following Python CLI program (say it's
:file:`subcmds.py`):

.. include:: subcmds.py
   :code:

.. code-block:: rst

   .. autoprogram:: subcmds:parser
      :prog: subcmds.py

The above reStructuredText will render:

    .. autoprogram:: subcmds:parser
       :prog: subcmds.py

.. rst:directive:: .. autoprogram:: module:parser

   It takes an import name of the parser object.  For example, if ``xyz``
   variable in ``abcd.efgh`` module refers an :class:`argparse.ArgumentParser`
   object:

   .. code-block:: rst

      .. autoprogram:: abcd.efgh:xyz

   The import name also can evaluate other any Python expressions.
   For example, if ``get_parser()`` function in ``abcd.efgh`` module creates
   an :class:`argparse.ArgumentParser` and returns it:

   .. code-block:: rst

      .. autoprogram:: abcd.efgh:get_parser()

   It also optionally takes an option named ``prog``.  If it's not present
   ``prog`` option uses :class:`~argparse.ArgumentParser` object's
   prog_ value.

.. _prog: http://docs.python.org/library/argparse.html#prog


.. _autoprogram-options:

Additional Options for :rst:dir:`.. autoprogram::`
--------------------------------------------------

.. versionadded:: 0.1.3

``:maxdepth: ##``
    Only show subcommands to a depth of ``##``.

``:no_usage_codeblock:``
    Don't put the usage text in a :rst:dir:`.. codeblock:: console` directive.

``:start_command: subcommand``
    Render document for the given subcommand. ``subcommand`` can be a space
    separated list to render a sub-sub-...-command. 
    
``:strip_usage:``
    Removes all but the last word in the usage string before the first option,
    replaces it with '...', and removes an amount of whitespace to realign
    subsequent lines.


Author and license
------------------

The :mod:`sphinxcontrib.autoprogram` is written by `Hong Minhee`__ and
distributed under BSD license.

The source code is maintained under the `GitHub repository`__:

.. sourcecode:: console

   $ git clone git://github.com/sphinx-contrib/autoprogram.git

__ https://hongminhee.org/
__ https://github.com/sphinx-contrib/autoprogram

.. include:: changelog.rst
