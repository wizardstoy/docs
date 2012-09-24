Software Dependencies
*********************

MetaRelate requires a variety of software packages to be installed and configured in order to operate correctly.

.. toctree::
   :maxdepth: 1


Python
======

Currently supported versions of Python are 2.4.x - 2.7.x.
Python 3.x is not currently supported.
Python can be built from source but most systems have it available via
a system package manager.


Java
====

Currently supported versions of Java are 1.6.x.
Only the JRE is actually required but we recommend
that the full JDK be installed.

Once installed, the environment variable JAVAHOME must be set to the path to 
the java execution engine, 'java'

Jena
====

Available from `Jena <http://www.apache.org/dist/jena/binaries/apache-jena-2.7.3.tar.gz>`_.
Once unpacked into an installation directory, the environment variable JENAROOT
must be set to the location of said directory.

Fuseki
======

Available from `Fuseki <http://www.apache.org/dist/jena/binaries/jena-fuseki-0.2.4-distribution.tar.gz>`_.
Once unpacked into an installation directory, the environment variable FUSEKI_HOME
must be set to the location of said directory.

Django
======

Available from `Django <https://www.djangoproject.com/download/1.3.3/tarball/>`_.
Currently supported versions of Django are 1.3.x.
New versions should work fine but are not supported at this time.

