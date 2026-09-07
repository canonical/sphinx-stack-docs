.. meta::
   :description: Troubleshooting guidance for issues related to building and publishing documentation using the Sphinx Stack with Read the Docs.

.. _build_errors_troubleshooting:

Build errors
============

In this guide, you will find information on how to troubleshoot local or GitHub PR build errors that may occur when building a documentation set.

'Module not found' error
------------------------

The build fails unexpectedly with a ``ModuleNotFoundError: No module named ...`` error message. 

Probable cause
~~~~~~~~~~~~~~

The error message may indicate that the build system is unable to find a module that is required for building the documentation even though the module is installed in the local development environment. This can be because the wrong version is installed and something is being called that doesn't exist - as with your myst-parser case - or the system path hasn't been extended to find the package - as happens with local extensions (you may need a ``sys.path.insert(0, os.path.abspath('<path>'))`` to include the path to the module).

It has been observed that this failure can also happen due to ``myst-parser`` version mismatch.

Resolution
~~~~~~~~~~

Use the latest version of ``myst-parser`` in your local development environment and ensure that the same version is specified in the ``requirements.txt`` file. 

'Pip resolution too deep' error
--------------------------------

Sphinx based documentation builds fail with a ``pip resolution too deep`` error message. This can happen with local builds, on GitHub PR builds or at Read the Docs.

Probable cause
~~~~~~~~~~~~~~

This error typically occurs when the ``requirements.txt`` file has conflicting dependencies or a dependency tree too complex for ``pip`` to resolve efficiently.

Documentation repositories initialized from Canonical's Sphinx Stack project often hit this error due to an **unpinned** or incompatible version of a package like ``myst-parser``.

Resolution
~~~~~~~~~~

Review the dependencies listed in the ``requirements.txt`` file and resolve any conflicts caused by incompatible or unpinned package versions or newly released versions. To fix this, try:

* Restricting problem packages to recent versions (using package>=version)
* Using a constraints file

As an example, the error showed up recently while building several Sphinx Stack based documentation sets independently on different machines on a specific day when a new version of ``myst-parser`` was released. The issue could be resolved by pinning the ``myst-parser`` version in the ``requirements.txt`` file.
