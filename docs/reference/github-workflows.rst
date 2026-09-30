.. meta::
    :description: Reference for the built-in GitHub workflows that check your documentation's spelling, links, and language.


.. _github-workflows:

GitHub workflows
================

The Sphinx Stack provides several GitHub Actions workflows to run checks on
documentation projects.

Spelling, link, and inclusive language checks
---------------------------------------------

The ``documentation-checks.yaml`` workflow runs several checks that correspond
to targets in the Sphinx Stack ``Makefile``:

* Spelling check (``spelling``)
* Link check (``linkcheck``)
* Inclusive language check (``woke``)

Refer to the how-to guides for details about how to :ref:`modify this workflow
<modify-documentation-check-workflow>` or :ref:`run documentation checks locally
<run-documentation-checks>`.

Default configuration
~~~~~~~~~~~~~~~~~~~~~

The documentation workflow is configured as follows:

.. list-table::
   :header-rows: 1

   * - Key
     - Description
     - Default
   * - ``working-directory``
     - The root of the documentation project.
     - ``docs``
   * - ``python-version``
     - The Python interpreter to use for the workflow's jobs.
     - ``3.10``
   * - ``fetch-depth``
     - The number of commits to fetch from your repository.
     - ``0`` (the full history is fetched)
   * - ``runs-on``
     - The host system for the workflow's runners.
     - ``ubuntu-24.04``

Check for removed URLs
----------------------

.. versionadded:: 1.2.0

The Sphinx Stack includes a GitHub Actions workflow to identify when pages have
been removed. This includes moving pages to another path, or removing them
completely.

This does not cover higher-level changes to URL paths, such as changes to the
project name or URL slug pattern on RTD.

This check ensures that redirects are implemented when pages are moved, or
appropriate information is provided when anything is removed. It only runs on
pull request builds.

