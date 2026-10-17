.. meta::
    :description: A list of extensions included in the Sphinx Stack by default.

.. _reference-default-sphinx-extensions:

Default Sphinx extensions
=========================

These extensions are enabled in the Sphinx Stack by default.

``ulwazi``
   Sphinx theme for Canonical documentation, based on the `Vanilla framework
   <https://vanillaframework.io/>`__.

``myst_parser``
   Adds support for the MyST markdown flavor.

``sphinx_design``
   Provides UI components like responsive grids, cards, and badges.

``sphinxcontrib.jquery``
   Ensures jQuery is loaded to maintain compatibility with older extensions and themes.

``sphinxext.opengraph``
   Generates OpenGraph metadata to create rich preview cards when links are shared on social media.

``sphinx_rerediraffe``
   Handles URL redirects for moved or deleted pages. Redirects can be defined as a
   dictionary in the ``conf.py`` file or in a separate file.

``sphinx.ext.intersphinx``
   Generates automatic links to the documentation objects of other Sphinx projects.

``sphinx_config_options``
   Provides customized directives to easily document system or project configuration options.

``sphinx_llm.txt``
   Generates Markdown artifacts that improve readability for LLMs.

``sphinx_related_links``
   Generates and injects a list of related links into documentation pages.

``sphinx_roles``
   Provides custom inline text roles for standardized formatting or linking across the project.

``sphinx_sitemap``
   Automatically generates a standard sitemap.xml file to improve indexing for search engine optimization (SEO).

``sphinx_terminal``
   Renders styled terminal sessions and command-line output within the documentation.

``sphinx_youtube_links``
   Provides a directive to embed YouTube videos into a page.

``sphinxcontrib.cairosvgconverter``
   Converts SVG images into PDF.

``canonical_sphinx``
   Required for the Sphinx Stack. Provides the Furo-based theme and custom templates.

   .. versionremoved:: 3.0

      Replaced by the Ulwazi theme.

``notfound.extension``
   Allows creating custom 404 pages.

   .. versionremoved:: 3.0

      Now set up automatically by the Ulwazi theme.

``sphinx_contributor_listing``
   Automatically generates a list of contributors to the project repository.

   .. versionremoved:: 3.0

      No longer aligns with Canonical design practices.

``sphinx_filtered_toctree``
   Filters Table of Contents (``toctree``) entries based on specific tags or conditions.

   .. versionremoved:: 3.0

      Was a holdover from a previously removed feature.

``sphinx_last_updated_by_git``
   Fetches and displays the accurate 'last updated' date for pages by reading Git commit
   metadata.

   .. versionremoved:: 3.0

      Now set up automatically by the sphinx-sitemap extension.

``sphinx_reredirects``
   Handles URL redirects for moved or deleted pages.

   .. versionremoved:: 3.0

      Replaced by the sphinx-rerediraffe extension.

``sphinx_tabs.tabs``
   Provides tabs.

   .. versionremoved:: 3.0

      Replaced by the sphinx-design extension.

``sphinx_ubuntu_images``
   Generates lists of official Ubuntu disk images for specific release ranges and architectures.

   .. versionremoved:: 3.0

      Removed due to its low adoption rate, but can be reinstalled in downstream projects
      that use its directive.
