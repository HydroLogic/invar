================
invar |release|
================

About
=====

.. include:: ../README

Installation
============

invar only works with Mapnik2. Instructions for installing Mapnik2 can be found `here <https://github.com/mapnik/mapnik/wiki/Mapnik-Installation>`_. Once you have Mapnik2 installed you can install invar using pip::

    pip install invar

It can be quite tricky to get Mapnik2 working within virtualenv, so it may be simpler/better to install invar in the global site-packages.

Usage
=====

ivtile
------

ivtile renders continous tiles of the map, such as those used by Google Maps, Open Street Map, or any other "slippy" map provider.

invar tiler sample usage::

    ivtile examples/bus_stops.xml tiles 32.6 -95.6 32.00 -95.0 8 10 --process-count 2

Details of each parameter are available via::

    ivtile -h

ivframe
-------

ivframe renders discontinous frames of the map centered on locations, such as an individual map for the area around each of a hundred bus stops.

ivframe rendering a single large frame to the current directory::

    ivframe examples/bus_stops.xml . 32.35 -95.3 -z 11 -w 512 -t 512

ivframe supports rendering a series frames from latitude/longitude pairs in a CSV file::

    ivframe map.xml output_directory --csv data.csv --name name_column  --process_count 2

Details of each parameter are available via::

    ivframe -h

ivs3
----

ivs3 pushes a collection of tiles (or anything, really) into an Amazon S3 bucket using concurrent connections (so its super-fast).

Sample usage pushing a tiles directory into a bucket called "test_bucket"::

    ivs3 tiles_directory test_bucket -P

You must have your Amazon Web Services access credentials defined in the AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY environment variables. The -P flag makes the uploaded files public. For a complete list of flags run::

    ivs3 -h

Using with TileMill
-------------------

In order to use invar with `TileMill <http://tilemill.com/>`_ you need to convert TileMill's .mml configuration and .mss styles into a Mapnik .xml file. Here is an example of how to do this::

    $TILEMILL_PATH/node_modules/carto/bin/carto map.mml > map.xml

Note: some versions of TileMill (0.10.1) print debug statements to STDOUT which can mess up the output of this conversion. If you see a line at the top of your output XML file like ``[millstone] finished processing '/path/to/my/file'`` then prefix your compile command with ``NODE_ENV=foo`` which will disable these statements.

Credits
=======

Open Street Map
---------------

Much of this application is derived from selections of the Open Street Map project--notably `generate_tiles.py <http://svn.openstreetmap.org/applications/rendering/mapnik/generate_tiles.py>`_.

Projects
--------

invar was developed to address the needs of both `@tribapps <http://twitter.com/tribapps>`_ and the `#hacktyler <http://hacktyler.com>`_ project.

Authors
=======

.. include:: ../AUTHORS

License
=======

.. include:: ../COPYING

Release process
===============

#. Ensure these files all have the correct version number:
    * CHANGELOG
    * setup.py
    * docs/conf.py
#. Tag the release: ``git tag -a x.y.z; git push --tags``
#. Roll out to PyPI: ``python setup.py sdist upload``
#. Iterate the version number in all files where it is specified. (see list above)
#. Flag the new version for building on `Read the Docs <https://readthedocs.org/dashboard/invar/versions/>`_.
#. Wait for the documentation build to finish.
#. Flag the new release as the default documentation version.
#. Announce the release on Twitter, etc.

Changelog
=========

.. include:: ../CHANGELOG

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
