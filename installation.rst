.. DalmatinerDB installation manual
   Heinz N. Gies on Sat Jul  5 16:49:03 2014.

Installation
============

Binaries
--------

Binary packages for SmartOS are are in the project-fifo repository they can be installed via pkgin:

.. code-block:: bash

   VERSION='dev' # use 'rel' for release packages
   echo "http://release.project-fifo.net/pkg/${VERSION}/" >>/opt/local/etc/pkgin/repositories.conf
   pkgin -fy up
   pkgin install dalmatinerdb # To install the backend package
   pkgin install dalmatinerfe # To install the frontend package


From Source
-----------

Dependencies:

* Erlang > R16B3
* Make
* GCC

Installing the datastore
````````````````````````
.. code-block:: bash

   git clone https://github.com/dalmatinerdb/dalmatinerdb.git
   cd dalmatinerdb
   make deps all rel
   cp -r rel/dalmatinerdb $TARGET_DIRECTORY
   cd $TARGET_DIRECTORY
   cp etc/dalmatinerdb.conf.example etc/dalmatinerdb.conf
   vi etc/dalmatinerdb.conf # check the settings and adjust if needed
   ./bin/ddb start

.. note::
    DalmatinerDB by default expects to run as the user ``dalmatiner``, this can be changed or disabled by editing the ``bin/ddb`` file's entry ``RUNNER_USER``

Installing the frontend
```````````````````````

.. code-block:: bash

   git clone https://github.com/dalmatinerdb/dalmatiner-frontend.git
   cd dalmatiner-frontend
   make deps all rel
   cp -r rel/dalmatinerfe $TARGET_DIRECTORY
   cd $TARGET_DIRECTORY
   cp etc/dalmatinerfe.conf.example etc/dalmatinerfe.conf
   vi etc/dalmatinerfe.conf # check the settings and adjust if needed
   ./bin/dalmatinerfe start

.. note::
    DalmatinerFrontend by default expects to run as the user ``dalmatiner``, this can be changed or disabled by editing the ``bin/dalmatinerfe`` file's entry ``RUNNER_USER``

.. warning::
    At the moment automatic handling of disconnected upstream servers isn't handled well and might require a restart of the frontend.
