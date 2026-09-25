.. _sphinx-stack:

Sphinx Stack documentation
==========================

The **Sphinx Stack** is a well-crafted template repository for Sphinx projects, and is the standard documentation setup at Canonical.

The repository contains a setup for Sphinx and its required extensions, plus basic scaffolding for standard document types. A CLI is provided for building the documents and checking their quality.

The Sphinx Stack contains everything you need to bootstrap and host new documentation. You can copy it as a standalone documentation repository, or incorporate into a project's codebase.

The Sphinx Stack is for all employees at Canonical, and is available to writers and developers looking to begin a robust and capable Sphinx project.


In this documentation
---------------------

Getting started
~~~~~~~~~~~~~~~

Create, configure, build and publish your documentation.

..  domain::

    ..  slice:: First project

        :doc:`Set up a new project <set-up-a-new-project>`
        :doc:`Configure your project <how-to/configure-your-project>`

    ..  slice:: Build and publish

        :doc:`Build and preview <how-to/build-and-preview>`
        :doc:`Publishing on Read the Docs <how-to/publish-on-rtd>`


Document elements
~~~~~~~~~~~~~~~~~

Write your pages in either supported markup language, enrich them with diagrams and
generated reference material, and control how they are rendered and found.

..  domain::

    ..  slice:: Syntax guides

        :doc:`MyST for Markdown <reference/myst-syntax>`
        :doc:`reStructuredText <reference/rst-syntax>`

    ..  slice:: Diagrams and tables

        :doc:`Mermaid diagrams <how-to/optional-customisation/mermaid-diagrams>`
        :doc:`Interactive tables <how-to/optional-customisation/interactive-tables>`

    ..  slice:: API documentation

        :doc:`API docs from Python docstrings <how-to/optional-customisation/python-docstrings>`
        :doc:`OpenAPI specifications <how-to/optional-customisation/openapi-specifications>`

    ..  slice:: Customizing output

        :doc:`Custom HTML templates <how-to/optional-customisation/custom-html-templates>`
        :doc:`PDF output <how-to/optional-customisation/customise-pdf>`
        :doc:`Page-specific configuration <how-to/optional-customisation/add-page-specific-configuration>`

    ..  slice:: Stable and outbound links

        :doc:`Redirects for moved pages <how-to/optional-customisation/redirect-pages>`
        :doc:`Intersphinx links to other doc sets <how-to/optional-customisation/external-referencing-intersphinx>`

    ..  slice:: Discoverability

        :doc:`Manage sitemaps <how-to/optional-customisation/manage-sitemaps>`
        :doc:`Enable Google Analytics <how-to/optional-customisation/enable-google-analytics>`


Content quality
~~~~~~~~~~~~~~~

Check your prose, links, and documented commands, run those checks automatically on
every change, and diagnose failures when they occur.

..  domain::

    ..  slice:: Quality checks

        :doc:`Documentation checks <how-to/run-documentation-checks>`
        :doc:`Testing documented commands with Spread <how-to/optional-customisation/add-documentation-testing>`

    ..  slice:: Continuous integration

        :doc:`GitHub workflows <reference/github-workflows>`
        :doc:`Bridging project and docs builds <how-to/optional-customisation/bridge-project-and-docs-builds>`


Lifecycle management
~~~~~~~~~~~~~~~~~~~~~

Upgrade an existing documentation set onto a current version of the Sphinx Stack.

..  domain::

    ..  slice:: Upgrade paths

        :doc:`Upgrade from a new version <how-to/update-sphinx-stack/new-sphinx-stack>`
        :doc:`Upgrade from the legacy version <how-to/update-sphinx-stack/legacy-sphinx-stack>`

    ..  slice:: Troubleshooting

        :doc:`Build errors <how-to/troubleshooting/build-errors>`
        :doc:`Local deployment issues <how-to/troubleshooting/local-deployment-issues>`
        :doc:`Runtime errors <how-to/troubleshooting/runtime-errors>`
        :doc:`Read the Docs failures <how-to/troubleshooting/rtd-issues>`


How the stack works
~~~~~~~~~~~~~~~~~~~~

Understand what the stack ships with and how it assembles your source files into a
finished site.

..  domain::

    ..  slice:: Core components

        :doc:`Sphinx Stack structure <explanation/components>`
        :doc:`The build process <explanation/build>`

    ..  slice:: Default settings

        :doc:`Default Sphinx extensions <reference/default-extensions>`
        :doc:`Default Sphinx configuration <reference/conf-py-configuration>`
        :doc:`Sitemaps <explanation/sitemaps>`


How this documentation is organized
-------------------------------------

This documentation uses the `Diátaxis documentation structure <https://diataxis.fr/>`_.

* The :ref:`tutorial <set-up-a-new-project>` walks through copying the Sphinx
  Stack template, removing unneeded files, and performing the required initial
  configuration before the first build.
* :ref:`How-to guides <how-to-guides>` cover specific tasks: building locally, running
  documentation checks, publishing on Read the Docs, updating the stack, and enabling
  optional extensions.
* :ref:`Reference <reference>` provides the list of default Sphinx extensions, GitHub
  workflow definitions, and the reST and MyST syntax guides.
* :ref:`Explanation <explanation>` describes the architecture of the Sphinx Stack,
  covering its core components (Sphinx, Python, extensions), the Make-based build
  system, and sitemap generation.


Project and community
-----------------------

The Sphinx Stack is a Canonical open source project that forms part of the tooling
supporting documentation across Ubuntu and other Canonical offerings.


Get involved
~~~~~~~~~~~~

* `Sphinx Stack repository <https://github.com/canonical/sphinx-stack>`__
* `Issue tracker <https://github.com/canonical/sphinx-stack/issues>`__
* :ref:`Contribute to documentation <contribute-documentation>`
* :ref:`Contribute to development <contribute-development>`

Releases
~~~~~~~~

* :ref:`Release notes <release-notes>`


Governance and policies
~~~~~~~~~~~~~~~~~~~~~~~~

* `Code of conduct <https://ubuntu.com/community/ethos/code-of-conduct>`__


.. toctree::
    :hidden:
    :maxdepth: 2

    set-up-a-new-project
    how-to/index
    reference/index
    explanation/index

.. toctree::
    :hidden:

    release-notes/index
    contribute/index
