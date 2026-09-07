.. meta::
   :description: Troubleshooting guidance for issues related to building and publishing documentation with the Sphinx Stack and Read the Docs.

.. _build_errors_troubleshooting:

Build errors
============

In this guide, you will find information on how to troubleshoot local or GitHub PR build errors that may occur when building a documentation set.

'Module not found' error
------------------------

The build fails with a ``ModuleNotFoundError: No module named '<module>'`` error message when you run it locally (or in a GitHub PR check).

Probable cause
~~~~~~~~~~~~~~

A ``ModuleNotFoundError`` means the Python interpreter running the build cannot locate the named module at all. The most common causes for a local build are:

* **The dependencies were never installed, or the wrong environment is active.** The build is running against a Python interpreter that does not have the documentation dependencies installed, for example because the virtual environment was not activated or ``requirements.txt`` was not installed into it.
* **The package is missing from** ``requirements.txt``. The module is not installed because it is not declared as a dependency. If it works for you but fails for a colleague or in CI, it is likely installed in your environment but absent from ``requirements.txt``.
* **A local module or extension is not on** ``sys.path``. Custom extensions or ``conf.py`` helpers that live inside the repository are not importable unless their directory is added to the path in ``conf.py``, for example ``sys.path.insert(0, os.path.abspath('_ext'))``.

Resolution
~~~~~~~~~~

#. Read the full traceback and note the exact module name reported after ``No module named`` error message.
#. Confirm you are building inside the correct environment with the dependencies installed::

.. code-block:: bash
   
     source .venv/bin/activate    # or your environment's activation command
     pip install -r requirements.txt

#. If it is a third-party package (for example ``myst-parser``), check whether it is listed in ``requirements.txt``. If it is missing, add it and reinstall. If it is present, confirm it is actually installed in the active environment with ``pip show <package>``. If a newer version is available, consider updating it and adjusting the version constraints in 

#. Rebuild to confirm the fix::

.. code-block:: bash

   sphinx-build -W -b html . _build/html

.. tip::

   If the build works for you but fails for a colleague or in a GitHub PR check, the module is almost always installed in your local environment but missing from ``requirements.txt``. Add it there so every environment installs it.

'Pip resolution too deep' error
--------------------------------


Probable cause
~~~~~~~~~~~~~~

This error typically occurs when the ``requirements.txt`` file has conflicting dependencies or a dependency tree too complex for ``pip`` to resolve efficiently.

Documentation based on the Sphinx Stack often hit this error due to an unpinned or incompatible version of a package.

Resolution
~~~~~~~~~~

Review the dependencies listed in the ``requirements.txt`` file and resolve any conflicts caused by incompatible or unpinned package versions or newly released versions. To fix this, try:

* Restricting problem packages to recent versions (using ``package~=version``)
* Using a constraints file

As an example, the error showed up recently while building several Sphinx Stack based documentation sets independently on different machines on a specific day when a new version of ``myst-parser`` was released. The issue could be resolved by pinning the ``myst-parser`` version in the ``requirements.txt`` file.
