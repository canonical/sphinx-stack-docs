.. _set-up-a-new-project:


Set up a new project
====================

This page contains a short guide on how to set up and use the Sphinx Stack.

.. _initial-setup:

Copy the Sphinx Stack
---------------------

If you're starting a new project, `copy the Sphinx Stack as a template repository
<https://github.com/new?template_name=sphinx-stack&template_owner=canonical>`__.

If you're creating documentation for a Canonical project, set the owner to
**canonical**.

If you're adding documentation to an existing software project, copy the following files
from the Sphinx Stack repository into your project:

* the entire ``docs`` directory
* ``.readthedocs.yaml`` (configuration for the building on Read the Docs)
* the entire ``.github/workflows`` directory


.. _remove-unneeded-files:

Remove the unneeded files
-------------------------

Next, review the Sphinx Stack files and remove those that could interfere with your
project.

Remove the files that can't be reused:

- ``CONTRIBUTING.md``
- ``.github/CODEOWNERS``
- ``.github/workflows/test-sphinx-stack.yml``

Review and remove the GitHub workflows in ``.github/workflows/`` that your project might
not need:

- ``cla-check.yml`` verifies whether contributors have signed the `Canonical License
  Agreement <https://canonical.com/legal/contributors>`_. All Canonical projects require
  this check, so if you're adding docs to an existing Canonical project that already has
  it, remove this workflow.
- ``sphinx-python-dependency-build-checks.yml`` verifies Python dependencies for the
  documentation system. If your project has its own dependency checks, remove this
  workflow.
- ``markdown-style-checks.yml`` runs the built-in Markdown linter. If your project
  already validates its Markdown files, remove this workflow.


Build and run the local server
------------------------------

Building the documentation requires ``make``, ``python3``, ``python3-venv``,
``python3-pip``.

In the ``docs`` directory, run:

.. code-block:: bash

    make run

This creates and activates a virtual environment in ``docs/.venv``, builds the project,
and serves it at :literalref:`http://127.0.0.1:8000/`.

The server watches the source files, including the ``docs/conf.py`` file, and rebuilds
automatically on changes.


Edit content
------------

The home page is ``docs/index.rst``. Other pages are under one of the sub-directories
under ``docs/``.

The navigation menu structure is set by ``.. toctree::`` directives. These directives
define the hierarchy of included content throughout the documentation. The
``index.rst`` page's ``toctree`` block contains the top level navigation, which by
default is the `Diátaxis`_ documentation structure.

To add a new page to the documentation:    

1. Create a new file in the ``docs/`` directory. For example, to create a new
   **Reference** page, create a document under the ``docs/reference/`` directory called
   ``settings.rst``, insert the following heading, and save the file:

   .. code-block:: rest
      :caption: reStructuredText title example

      Settings
      ========

   If you prefer to use Markdown (MyST) syntax instead of |RST|, you can create a
   Markdown file. To create the equivalent ``settings.md`` file, add the following
   Markdown-formatted heading at the beginning:

   .. code-block:: markdown
      :caption: Markdown title example
         
      # Settings

2. Add the new page to the Navigation Menu: open the ``docs/reference/index.rst``
   file or another file where you want to nest the new page; at the bottom of the file,
   add the following ``toctree`` directive:

   .. code-block::
         
      .. toctree::
        :hidden:
        :maxdepth: 2

        settings

The documentation will now show the new page added to the navigation when rebuilt.

By default, the page's title (the first heading in the file) is shown in the global
navigation. You can overwrite a name of a menu element by specifying it explicitly in
the ``toctree`` block (e.g., ``Reference </reference/index>``).


Configure Sphinx
----------------

Work through the settings in the build configuration file, ``docs/conf.py``. Most
parameters can be left with the default values as they can be changed later.
:ref:`configure-your-project` contains further guidance.


Configure pre-commit (optional)
-------------------------------

Use `pre-commit <https://pre-commit.com/>`_ hooks with the Sphinx Stack to automate
checks like spelling and inclusive language.

The Sphinx Stack includes a ready-to-use ``.pre-commit-config.yaml`` file under
``docs/.sphinx/``:

.. literalinclude:: /.sphinx/.pre-commit-config.yaml
   :language: yaml

For a new project, copy this file to your project's root directory. For an existing
project using pre-commit, add these hooks to your configuration.

To apply the configuration, install the Sphinx Stack hooks, for instance:

.. code-block:: bash

    pre-commit install --config docs/.sphinx/.pre-commit-config.yaml


After that, you should see the checks running with every commit:

.. terminal::

    git commit -m 'add spelling errors'

    Run make spelling.......................................................Failed
    Run make linkcheck......................................................Passed
    Run make woke...........................................................Passed
