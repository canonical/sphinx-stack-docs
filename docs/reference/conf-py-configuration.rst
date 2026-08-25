.. meta::
   :description: Configuration parameters in the conf.py file.

.. _conf-py-configuration:

Common configuration settings in conf.py
=========================================


The ``conf.py`` file contains required project settings and optional features, with details about their purpose and when to use them. 


.. _conf-py-required-configuration:

Required configuration
----------------------

Mandatory configuration values are marked with ``TODO``. Review and adjust these configuration values to align with your project requirements, and ensure you comment out any settings that are not relevant to your environment.


.. _conf-py-project-information:

Project, repository, and site metadata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The ``Project Information`` section contains settings for your project's official name, Open Graph Protocol (OGP) metadata, and global variables that are passed into the Sphinx context across your entire site.

.. list-table::
   :widths: 30 70
   :header-rows: 1

   * - Configuration setting
     - Description
   * - ``project``
     - Specifies the official name of your project.
   * - ``ogp_site_name``, ``ogp_image``
     - Defines the preview website name and preview image. When you post a link to your documentation somewhere (for example, on Mattermost or Discourse), it can be shown with a preview. This preview is configured through the OGP configuration.
   * - ``html_favicon``
     - Defines the small icon shown in the browser tab, bookmarks, and sometimes the browser history for your documentation.
   * - ``html_context``
     - Specifies a dictionary of custom values that Sphinx passes into the HTML template rendering context, including:
     
       * Product website links (``product_page``)
       * Community or contact links (``discourse``, ``mattermost``, ``matrix``)
       * Documentation source and issue integration (``github_url``, ``repo_default_branch``, ``repo_folder``, ``github_issues``)
       * UI behavior (``sequential_nav``, ``display_contributors``)
       * Footer and license metadata (``author``, ``license``)
   * - ``html_theme_options``
     - Sets options that the HTML theme reads when rendering pages. Use the ``source_edit_link`` option to tell the theme where to send users when they click the edit button on all pages.


.. _conf-py-sitemap:

Sitemap
~~~~~~~~~~~~~~~~~~~

Sphinx, via the `sphinx_sitemap <https://sphinx-sitemap.readthedocs.io/en/latest/>`__ extension configured in the ``conf.py`` file, generates a ``sitemap.xml`` file that lists the public pages in your docs site. Search engines use that file to discover pages, understand your URLs, and sometimes pick up metadata like last modification time. 

To understand how the Sphinx Stack generates sitemaps, see :ref:`Sitemaps <sitemaps>`.
For instructions on validating sitemaps and supporting versioned documentation, see
:ref:`Manage sitemaps for versioned documentation <manage-sitemaps>`.

.. list-table::
   :widths: 30 70
   :header-rows: 1

   * - Configuration setting
     - Description
   * - ``html_baseurl``
     - Specifies the base URL of your documentation website. 
     
       By default, it is set to ``html_baseurl = os.environ.get("READTHEDOCS_CANONICAL_URL", "/")``. 
     
       When building on Read the Docs, this sets ``html_baseurl`` dynamically to the value of the ``READTHEDOCS_CANONICAL_URL`` environment variable, which resolves to the full URL of the documentation including the version and language (if applicable). In local builds and builds on other hosts, ``html_baseurl`` defaults to ``/``.
   * - ``sitemap_url_scheme``
     - Determines how page URLs are formed.
      
       It is set to ``'{link}'`` by default. This uses the value of ``html_baseurl`` to generate the full URL for each page for the sitemap.
   * - ``sitemap_show_lastmod``
     - Specifies whether to include the last modification time in the sitemap.
   * - ``sitemap_excludes``
     - Lists the non-public pages to be excluded from the sitemap. 
      
       Wildcards are supported. For example, ``_modules/*`` excludes the path ``_modules/`` and all paths such as ``_modules/foo/bar/``. For details, see `Excluding Pages <https://sphinx-sitemap.readthedocs.io/en/latest/advanced-configuration.html#excluding-pages>`_.

.. note::

    If you are implementing a sitemap on an RTD instance that is not a subproject, and
    it uses ``{link}`` for the ``sitemap_url_scheme``, RTD will replace your sitemap
    with their own.

    This is a known bug. The only current workaround is to use a different `sitemap name
    <https://sphinx-sitemap.readthedocs.io/en/latest/advanced-configuration.html#changing-the-filename>`_
    and a custom ``robots.txt`` pointing to it.


.. _conf-py-llm-context:

LLM context
~~~~~~~~~~~~~

The ``llms_txt_description`` configuration setting is for LLM-oriented documentation metadata. Sphinx uses the sphinx_llm.txt extension to generate ``llms.txt``, which is a machine-readable summary intended to give language models a short, reliable description of what the documentation set is about. Provide a concise description using this configuration setting so that an LLM consuming your documentation site can understand the subject before reading individual pages.


.. _conf-py-link-checker:

Sphinx link checker
~~~~~~~~~~~~~~~~~~~~~~

The link checker is the part of Sphinx that validates hyperlinks in your documentation when you run ``make linkcheck``. It tries each URL in the docs, reports broken links, and can also check whether anchors/fragments on a page exist. Use configuration settings in the Link checker exceptions section to tell Sphinx which URLs to skip, which anchor checks to relax, and how persistent to be when a request is slow or fails. 

.. list-table::
   :widths: 30 70
   :header-rows: 1

   * - Configuration setting
     - Description
   * - ``linkcheck_ignore``
     - Lists the URLs to ignore entirely. Use this configuration setting when the whole link is unreliable or intentionally excluded.
   * - ``linkcheck_anchors_ignore_for_url``
     - Lists anchor fragments to ignore for matching URLs. Use this configuration setting when the page is valid, but its section anchors are not worth verifying.
   * - ``linkcheck_timeout``
     - Specifies how long in seconds to wait for a response before timing out
   * - ``linkcheck_retries``
     - Specifies how many times to retry failures


.. _conf-py-feedback-button:

Feedback button
~~~~~~~~~~~~~~~~~~~~~

By default, the Sphinx Stack includes a feedback button at the top of each page. This button redirects users to your GitHub issues page and populates an issue for them with details of the page they were on when they clicked the button.

To use this feedback feature, set the ``github_url`` setting in ``html_context`` to the URL of your GitHub repository, and set the ``github_issues`` setting to be enabled.

To disable the feedback button, at the top level of the ``conf.py`` file, set the ``disable_feedback_button`` setting to ``True``.


.. _conf-py-optional-configuration:

Optional configuration
----------------------

The Sphinx Stack contains several features that you can configure or turn off if they
aren't suitable for your documentation.


.. _conf-py-html-templates:

HTML templates
~~~~~~~~~~~~~~~~~~~

The Sphinx Stack provides default header and footer templates. The ``templates_path`` setting specifies the directories that Sphinx searches for project-specific templates. To use your own templates, uncomment the ``templates_path = ["_templates"]`` line, and then create the ``docs/_templates`` directory to save your local templates. See :ref:`custom-html-templates` for more information on how to create your own templates.


.. _conf-py-redirects:

Redirects
~~~~~~~~~~~

The ``rediraffe_redirects`` setting specifies the file that contains redirect mappings. This file is a ``.txt`` file created in the same directory as the ``conf.py`` file. 

The ``rediraffe_dir_only`` setting controls whether redirect destination URLs omit ``/index.html`` when Sphinx builds documentation. When set to ``True``, destination URLs use directory-style paths and the trailing ``/index.html`` is removed.

For instructions on adding redirect mappings, see :ref:`how-to-redirect-pages`.


.. _conf-py-extensions:

Extensions
~~~~~~~~~~~~~

The Sphinx Stack includes a set of extensions that are useful for all documentation sets. Some extensions are :doc:`enabled by default </reference/default-extensions>` within the Sphinx Stack, but you can customize the selection in the ``conf.py`` file.

The canonical_sphinx extension is required for the Sphinx Stack and provides the Furo-based theme and custom templates. The following extensions are needed by canonical_sphinx:

- notfound.extension
- sphinx_design
- sphinx_reredirects
- sphinx_tabs.tabs
- sphinxcontrib.jquery
- sphinxext.opengraph

To add new extensions needed for your documentation set, add them to the ``extensions`` setting in the ``conf.py`` file. If any additional extensions need specific Python packages, ensure they are installed alongside the other requirements by adding them to the ``docs/requirements.txt`` file.
   
.. admonition:: Extension support
    :class: note

    The only extensions formally supported by the Sphinx Stack are those included in its
    `default requirements.txt file
    <https://github.com/canonical/sphinx-stack/blob/main/docs/requirements.txt>`__. If
    you add any extensions to this list, it's your responsibility to ensure that they're
    compatible with the rest of the Sphinx Stack.

.. _conf-py-ui-behavior:

.. _ui-behavior:

UI behavior
~~~~~~~~~~~

You can configure whether to display Previous/Next buttons at the bottom of pages by configuring the ``sequential_nav`` setting in ``html_context``. Valid options are:

.. list-table::
   :widths: 20 80
   :header-rows: 1

   * - Value
     - Description
   * - ``both``
     - Both the Previous and Next buttons are shown at the bottom.
   * - ``none``
     - No Previous or Next button is shown at the bottom.
   * - ``prev``
     - Only the Previous button is shown at the bottom.
   * - ``next``
     - Only the Next button is shown at the bottom.

You can then override this global setting for a specific page (for example, to turn off the Previous/Next buttons by default, but display them in a multi-page tutorial). See :ref:`how-to-add-page-specific-configuration`.


.. _conf-py-custom-configuration-settings:

Custom configuration settings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can add custom configuration settings for your project to extend or override the common configuration that is defined by the ``conf.py`` file.
The following links can help you with additional configuration:

- `Sphinx configuration <https://www.sphinx-doc.org/en/master/usage/configuration.html>`__
- `Sphinx extensions <https://www.sphinx-doc.org/en/master/usage/extensions/index.html>`__
- `Furo documentation <https://pradyunsg.me/furo/quickstart/>`__

If you need additional Python packages for any custom processing you do in your documentation, add them to the ``docs/requirements.txt`` file.

