========
Usage
========

To use oceansdb in a project:

.. code-block:: python

    import oceansdb

Now create a World Ocean Atlas database object by:

.. code-block:: python

    db = oceansdb.WOA()

On the first time you run this, it might take sometime since it needs to download the actual database files. You don't need to do anything other than wait.

The propriety extract() of the database object is who takes care of sub-sample, and if necessary interpolate, to give you the variable(s) on the requested coordinates. The returned output is always a dictionary, even if you requested only one variable from the database.

To get temperature at one point:

.. code-block:: python

    >>> t = db['TEMP'].extract(var='t_mn', doy=136.875, depth=0, lat=17.5, lon=-37.5)

The WOA climatologic temperature will be available as t['t_mn'].

.. code-block:: python

    >>> t.keys()
    ['t_mn']

    >>> t['t_mn'].shape
    (1,)

    >>> t['t_mn']
    masked_array(data = [ 24.60449791],
                 mask = False,
           fill_value = 1e+20)

If you prefer you can obtain all available variables by not defining var, like:

.. code-block:: python

    >>> t = db['PSAL'].extract(doy=136.875, depth=[0, 10, 15, 18], lat=17.5, lon=-37.5)

    >>> t.keys()
    ['s_dd', 's_sd', 's_se', 's_mn']

To get one profile of salinity:

.. code-block:: python

    >>> t = db['PSAL'].extract(var='t_mn', doy=136.875, depth=[0, 10, 15, 18], lat=17.5, lon=-37.5)

To get one section of temperature:

.. code-block:: python

    >>> t = db['TEMP'].extract(var='t_mn', doy=136.875, lat=17.5, lon=[-39, -37.5, -35])

To get a regular 3D grid:

.. code-block:: python

    >>> t = db['TEMP'].extract(var='t_mn', depth=[0, 10.23], doy=136.875, lat=[15, 17.5, 23], lon=[-39, -37.5, -35, -32.73])

    >>> t['t_mn'].shape
    (2, 3, 4)
