
======================
    python-nitrate
======================

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    Python API for the Nitrate test case management system
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:Manual section: 1
:Manual group: User Commands
:Date: February 2012


DESCRIPTION
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
python-nitrate is a Python interface to the Nitrate test case
management system. The package consists of a high-level Python
module (provides natural object interface), a low-level driver
(allows to directly access Nitrate's xmlrpc API) and a command
line interpreter (useful for fast debugging and experimenting).


FEATURES
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Among the most essential python-nitrate features are:

    * Natural and concise Python interface
    * Custom level of caching & logging
    * Automated status coloring
    * Integrated test suite
    * Utility functions

The main motivation was to hide unnecessary implementation details
wherever possible so that using the API is as concise as possible.

Scripts importing python-nitrate can make use of several useful
helper functions including info() for logging to stderr, listed()
which converts list into nice human readable form, color() for
coloring and of course log.{debug,info,warn,error} for logging.


EXAMPLES
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Initialize or create an object::

    testcase = TestCase(1234)
    testrun = TestRun(testplan=<plan>, summary=<summary>)

Default iterators provided for all container objects::

    for case in TestRun(1234):
        if case.automated:
            case.status = Status("RUNNING")
            case.update()

Linking case to a plan is as simple as adding an item to a set::

    testplan.testcases.add(testcase)
    testplan.update()

However, it's still possible to use the low-level driver when a
specific features is not implemented yet or not efficient enough::

    inject = Nitrate()._server.TestCase.get(46490)

For a quick start you can get some inspiration in the examples
directory. The 'matrix.py' script demonstrates how to easily
display a matrix view of the test run results for a specific test
plan. The 'create.py' script gives a broader overview covering
object creation, attribute setting, adjusting logs and caching.


INSTALLATION
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Install directly from Fedora/Copr repository using yum or dnf::

    yum install python-nitrate

or use PIP (sudo required if not in a virtualenv)::

    pip install nitrate

Note that for successful pip installation several extra
dependencies are necessary::

    yum install gcc python-devel krb5-devel postgresql-devel

Here's the list of required packages for Debian systems::

    apt install gcc python-dev libkrb5-dev libpq-dev


CONFIGURATION
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
To be able to contact the Nitrate server a minimal user config
file ~/.nitrate has to be provided in the user home directory::

    [nitrate]
    url = https://nitrate.server/xmlrpc/


TEST SUITE
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The high-level interface has an integrated test suite, which can
be easily run against a stage server instance. For this a couple
of objects needs to be prepared and already existing on the server
so that we can check valid results. For detailed information about
what data has to be prepared see the module documentation.


LINKS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Project page:
https://github.com/psss/python-nitrate

Download:
https://github.com/psss/python-nitrate/releases

Copr repo:
http://copr.fedoraproject.org/coprs/psss/python-nitrate/

PyPI:
https://pypi.python.org/pypi/nitrate

File bugs:
https://bugzilla.redhat.com/enter_bug.cgi?product=Fedora&component=python-nitrate

Nitrate:
https://fedorahosted.org/nitrate/


SEE ALSO
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Manual pages covering command line interpreter and release notes::

    nitrate
    nitrate-notes

For more detailed and most up-to-date description of all available
nitrate module features see the Python online documentation::

    pydoc nitrate

For area-specific details see respective module documentation::

    nitrate.base ......... Nitrate class, search support
    nitrate.cache ........ Persistent cache, multicall support
    nitrate.config ....... Configuration, logging, coloring, caching
    nitrate.containers ... Container classes implementation
    nitrate.immutable .... Immutable Nitrate objects
    nitrate.mutable ...... Mutable Nitrate objects
    nitrate.teiid ........ Teiid support
    nitrate.tests ........ Test suite
    nitrate.utils ........ Utilities
    nitrate.xmlrpc ....... XMLRPC driver


AUTHORS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
High-level Python module:
Petr Šplíchal, Zbyšek Mráz, Martin Kyral, Lukáš Zachar, Filip
Holec, Aleš Zelinka, Miroslav Vadkerti, Leoš Pol, Iveta
Wiedermann, Martin Frodl, Alexander Todorov, Robbie Harwood,
Martin Zelený and Lumír Balhar.

Low-level XMLRPC driver:
Airald Hapairai, David Malcolm, Will Woods, Bill Peck, Chenxiong
Qi, Tang Chaobin, Yuguang Wang and Xuqing Kuang.

Hope, the library will save you time and bring some joy when
writing scripts interacting with the Nitrate server. Looking
forward to your feedback, comments, suggestions and patches ;-)

Petr Šplíchal <psplicha@redhat.com>


COPYRIGHT
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Copyright (c) 2012 Red Hat, Inc. All rights reserved.

This library is free software; you can redistribute it and/or
modify it under the terms of the GNU Lesser General Public
License as published by the Free Software Foundation; either
version 2.1 of the License, or (at your option) any later version.
