:mod:`uos` -- basic "operating system" services
===============================================

.. module:: uos
   :synopsis: basic "operating system" services

The ``os`` module contains functions for filesystem access and ``urandom``
function.

Port specifics
--------------

The filesystem has ``/`` as the root directory and the
available physical drives are accessible from here.  They are currently:

    ``/flash``      -- the internal flash filesystem

    ``/sd``         -- the SD card (if it exists)

.. only:: port_pyboard

    On boot up, the current directory is ``/flash`` if no SD card is inserted,
    otherwise it is ``/sd``.

.. only:: port_wipy

    On boot up, the current directory is ``/flash``.

Functions
---------

.. function:: uname()

    Return information about the system, firmware release version, and
    micropython interpreter version.

.. function:: chdir(path)

   Change current directory.

.. function:: getcwd()

   Get the current directory.

.. function:: listdir([dir])

   With no argument, list the current directory.  Otherwise list the given directory.

.. function:: mkdir(path)

   Create a new directory.

.. function:: remove(path)

   Remove a file.

.. function:: rmdir(path)

   Remove a directory.

.. function:: rename(old_path, new_path)

   Rename a file.

.. function:: stat(path)

   Get the status of a file or directory.

.. function:: sync()

   Sync all filesystems.

.. only:: not port_pycom_esp32

    .. function:: urandom(n)

        Return a bytes object with n random bytes, generated by the hardware
        random number generator.

.. only:: port_pycom_esp32

    .. function:: urandom(n)

        Return a bytes object with n random bytes. 

.. only:: port_wipy or port_pycom_esp32

    .. function:: unlink(path)

        Alias for the :func:`~uos.remove` method.

    .. function:: mount(block_device, mount_point, \*, readonly=False)

       Mounts a block device (like an ``SD`` object) in the specified mount
       point. Example::

          os.mount(sd, '/sd')

    .. function:: unmount(path)

       Unmounts a previously mounted block device from the given path.

    .. function:: mkfs(block_device or path)

       Formats the specified path, must be either ``/flash`` or ``/sd``.
       A block device can also be passed like an ``SD`` object before
       being mounted.

    .. function:: dupterm(stream_object)

       Duplicate the terminal (the REPL) on the passed stream-like object.
       The given object must at least implement the ``.read()`` and ``.write()`` methods.

Constants
---------

.. data:: sep

   separation character used in paths

.. only:: port_pycom_esp32

    .. note::
        As of firmware version 0.9.5.b1, SD card drivers are a work in progress, so operations using it are still not supported.