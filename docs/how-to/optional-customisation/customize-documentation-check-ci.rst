:relatedlinks: https://docs.github.com/en/actions/reference/workflows-and-actions

.. meta::
   :description: How to modify the Sphinx Stack's default GitHub workflow for documentation checks.

.. _modify-documentation-check-workflow:

Customize the documentation check CI
====================================

The Sphinx Stack provides a GitHub Actions workflow,
``.github/workflows/documentation-checks.yaml``, to automate spelling, link, and
inclusive language checks. This guide describes how to configure the working
directory and Python version, and how to add or remove documentation checks.

You can also :ref:`run these checks locally <run-documentation-checks>`.

Change the working directory
----------------------------

By default, the workflow uses ``docs`` as the documentation directory. If
your documentation is located in a different directory, you must modify
``documentation-checks.yaml`` in two places:

* The workflow is configured to run on pull requests that modify files in the
  ``docs`` directory. Find the ``"docs/**"`` string under
  ``on.pull_request.paths``, and replace ``docs`` with the path to your
  documentation. For example, you can change the documentation directory from
  ``docs`` to ``doc``:

  .. code-block:: diff

      on:
        push:
          branches:
            - main
        pull_request:
          paths:
     -     - "docs/**"
     +     - "doc/**"

* In the remainder of ``documentation-checks.yaml``, the working directory is
  configured with the ``DOCS_DIR`` environment variable set under ``env``.
  Change the value of ``DOCS_DIR`` from ``"docs"`` to the path to your
  documentation.

  .. code-block:: diff

      env:
     -  DOCS_DIR: "docs"
     +  DOCS_DIR: "doc"
        PYTHON_VERSION: "3.10"

  .. note::

     Do not include a trailing slash character when changing the value of
     the ``DOCS_DIR`` variable.

Modify the Python version
-------------------------

The Python version is configured with the ``PYTHON_VERSION`` environment
variable set under ``env``. Change this value to use a different version:

.. code-block:: diff

    env:
      DOCS_DIR: "docs"
      DOCS_DIR: "doc"
   -  PYTHON_VERSION: "3.10"
   +  PYTHON_VERSION: "3.12"

.. note::

   Place the Python version number in quotation marks. Version numbers without
   quotation marks will be parsed as floating-point numbers, and the GitHub
   Action will fail.

Add or remove a Makefile target
-------------------------------

The ``documentation-checks.yaml`` workflow uses a matrix strategy to run three
jobs in parallel: the spelling, links, and inclusive language checks.  Each
check in the matrix defines a ``name`` and a ``target``. The ``name`` is how the
check is listed when it runs on GitHub, and the ``target`` corresponds to a Make
target defined in the Sphinx Stack ``Makefile``. The job itself consists of a
single command: ``make <target>``.

To add a new ``Makefile`` target to the matrix, add a ``name`` and ``target``
pair to the array under ``jobs.checks.strategy.matrix.check``.  To remove a
check, simply remove the lines containing the check's ``name`` and ``target``.
For example, you can remove the spelling check and add a style guide check:

.. code-block:: diff

    jobs:
      checks:
        name: ${{ matrix.check.name }}
        runs-on: ubuntu-24.04
        strategy:
          fail-fast: false
          matrix:
            check:
   -          - name: Spelling check
   -            target: spelling
   +          - name: Style guide check
   +            target: vale
              - name: Link check
                target: linkcheck
              - name: Inclusive language check
                target: woke

