.. meta::
   :description: Troubleshooting guidance for issues related to building and publishing documentation using the Sphinx Stack at Read the Docs.

.. _build_errors_troubleshooting:

Build errors
============

In this guide, you will find information on how to troubleshoot local or GitHub PR build errors that may occur when building the documentation set.

'Module not found' error
------------------------

The build fails unexpectedly with a ``ModuleNotFoundError: No module named ...`` error message. 

Probable cause
~~~~~~~~~~~~~~

The error message may indicate that the build system is unable to find a module that is required for building the documentation even though the module is installed in the local development environment. This can happen due to ``myst-parser`` version mismatch.

Resolution
~~~~~~~~~~

Use the latest version of ``myst-parser`` in your local development environment and ensure that the same version is specified in the ``requirements.txt`` file. 

'Pip resolution too deep' error
--------------------------------

Sphinx based documentation builds fail with a ``pip resolution too deep`` error message. This can happen with local builds, on GitHub PR builds or at Read the Docs.

Probable cause
~~~~~~~~~~~~~~

This error typically occurs when the ``requirements.txt`` file has conflicting dependencies or a dependency tree too complex for ``pip`` to resolve efficiently.

Documentation repositories initialized from Canonical's Sphinx Stack project often hit this error due to an **unpinned** or incompatible version of ``myst-parser``.

Resolution
~~~~~~~~~~

Review the dependencies listed in the ``requirements.txt`` file and resolve any conflicts. You may need to update or pin specific versions of packages to ensure compatibility. 

This error showed up for several Sphinx Stack based documentation sets on a specific day when a new version of ``myst-parser`` was released. The issue could be resolved by pinning the ``myst-parser`` version in the ``requirements.txt`` file.

