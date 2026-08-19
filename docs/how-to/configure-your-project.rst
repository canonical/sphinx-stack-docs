.. meta::
   :description: How to configure project-specific parameters.

.. _configure-your-project:

Configure your project
======================

Configuration for a Sphinx Stack based documentation is set in the ``docs/conf.py`` configuration file. The default configuration in the Sphinx Stack is prepared in a way that makes sense for most projects. However, you must set some critical project-specific configuration values, like the project's name, to ensure the documentation reflects your project accurately.

.. important::

    The Sphinx Stack is updated periodically. After you set up your documentation repository with the Sphinx Stack, you need to track the changes made to the Sphinx Stack and manually maintain your repository.

    Use the Sphinx Stack `release notes <https://documentation.ubuntu.com/sphinx-stack/latest/release-notes>`__ or `changelog <https://github.com/canonical/sphinx-stack/blob/main/CHANGELOG.md>`__ to track changes to the Sphinx Stack. Subscribe to the repository releases to get notified whenever there is a new release. For the recommended way of manually updating your Sphinx Stack, see :ref:`update-sphinx-stacks`.


Required configuration
----------------------

The ``conf.py`` file marks mandatory configuration values with ``TODO``. Reviewing these configuration values is enough if you do not require custom or advanced features.


Project information
~~~~~~~~~~~~~~~~~~~~

The ``conf.py`` file's ``Project Information`` section contains settings for your project's official name, preview of your documentation, and global variables that are passed into the Sphinx context across your entire site.

Adjust these configuration values to align with your project requirements, and ensure you comment out any settings that are not relevant to your environment.

.. list-table::
   :widths: 30 70
   :header-rows: 1

   * - Configuration setting
     - Description
   * - ``project``
     - Specifies the official name of your project.
   * - ``ogp_site_name``, ``ogp_image``
     - Defines the preview website name and preview image. When you post a link to your documentation somewhere (for example, on Mattermost or Discourse), it can be shown with a preview. This preview is configured through the Open Graph Protocol (OGP) configuration.
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


Sitemap
~~~~~~~

Sphinx, via the `sphinx_sitemap <https://sphinx-sitemap.readthedocs.io/en/latest/>`__ extension configured in the ``conf.py`` file, generates a ``sitemap.xml`` file that lists the public pages in your docs site. Search engines use that file to discover pages, understand your URLs, and sometimes pick up metadata like last modification time.

.. list-table::
   :widths: 30 70
   :header-rows: 1

   * - Configuration setting
     - Description
   * - ``html_baseurl``
     - Specifies the base URL of your documentation website.
   * - ``sitemap_url_scheme``
     - Determines how page URLs are formed.
   * - ``sitemap_show_lastmod``
     - Specifies whether to include the last modification time in the sitemap.
   * - ``sitemap_excludes``
     - Lists the non-public pages to be excluded from the sitemap.


LLM context
~~~~~~~~~~~~~

The ``llms_txt_description`` configuration setting is for LLM-oriented documentation metadata. Sphinx uses the sphinx_llm.txt extension to generate ``llms.txt``, which is a machine-readable summary intended to give language models a short, reliable description of what the documentation set is about. Provide a concise description using this configuration setting so that an LLM consuming your documentation site can understand the subject before reading individual pages.


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


Feedback button
~~~~~~~~~~~~~~~~~~~~~

By default, the Sphinx Stack includes a feedback button at the top of each page. This button redirects users to your GitHub issues page and populates an issue for them with details of the page they were on when they clicked the button.

To use this feedback feature, set the ``github_url`` setting in ``html_context`` to the URL of your GitHub repository, and set the ``github_issues`` setting to be enabled.

To disable the feedback button, set the ``disable_feedback_button`` setting to ``True``.


Optional configuration
----------------------

The Sphinx Stack contains several features that you can configure or turn off if they
aren't suitable for your documentation.


HTML templates
~~~~~~~~~~~~~~~~~~~

The default Sphinx Stack templates provide an initial configuration for your documentation set and are sufficient for most cases, including:

- Header template - The top section of the page that contains your product's tag image and name, a link to your product's page (if available), and a drop-down menu for "More resources".
- Footer template - The bottom section of the page that contains sequential navigation
  controls, copyright information, licensing details, and other relevant links.

If you want to use your own templates, uncomment the ``templates_path = ["_templates"]`` line in the ``docs/conf.py`` file, and then create the ``docs/_templates`` directory to save your local templates. See :ref:`custom-html-templates` for more information on how to create your own templates.


Redirects
~~~~~~~~~~~

When files in your documentation set are renamed, deleted, or relocated, they become inaccessible at their previous paths. Consequently, users attempting to access those original links will encounter a 404 Not Found error. To provide a better user experience, set up redirects to point to the new file name, new path, or an alternative path where the information can be found.

In the ``conf.py`` file, use the ``rediraffe_redirects`` configuration setting to specify the name of the file that hosts all of your redirects. This file is a ``.txt`` file created in the same directory as the ``conf.py`` file. Use the ``rediraffe_dir_only`` configuration setting to tell the `sphinx_rerediraffe <https://github.com/sphinx-doc/sphinxext-rediraffe>`_ extension how to format redirect destination URLs when Sphinx builds documentation. When set to ``True``, the trailing ``/index.html`` will be stripped from the redirect targets. See :ref:`how-to-redirect-pages`.


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


Custom configuration settings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can add custom configuration settings for your project to extend or override the common configuration that is defined by the ``conf.py`` file.
The following links can help you with additional configuration:

- `Sphinx configuration <https://www.sphinx-doc.org/en/master/usage/configuration.html>`__
- `Sphinx extensions <https://www.sphinx-doc.org/en/master/usage/extensions/index.html>`__
- `Furo documentation <https://pradyunsg.me/furo/quickstart/>`__

If you need additional Python packages for any custom processing you do in your documentation, add them to the ``docs/requirements.txt`` file.

