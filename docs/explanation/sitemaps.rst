.. meta::
    :description: How the Sphinx Stack generates sitemaps with Read the Docs and sphinx-sitemap.

.. _sitemaps:

Sitemaps
========

Sitemaps help search engines discover and index documentation pages. The Sphinx Stack generates a sitemap with the `sphinx-sitemap <https://sphinx-sitemap.readthedocs.io/en/latest/index.html>`__ extension.


Read the Docs-generated sitemaps
---------------------------------

RTD generates a basic sitemap pointing to the index page, and relies on crawlers to
index the site. This is sufficient for some projects, but RTD does not generate sitemaps
for subprojects.

This means any project under the Ubuntu documentation library project must generate its
own sitemap.


``sphinx-sitemap``-generated sitemaps
--------------------------------------

The standard Sphinx Stack uses the ``dirhtml`` builder for Sphinx recipes in the
project's Makefile. The ``dirhtml`` builder is required because sitemap links use
directory-style URLs. Projects using an older version of the Sphinx Stack or a different
builder generate malformed sitemap links.

The Sphinx Stack includes the ``sphinx-sitemap`` extension and its default
configuration. For the available sitemap settings and their default values, see
:ref:`Sitemap configuration <conf-py-sitemap>`.

For instructions on validating sitemaps and supporting versioned documentation, see
:ref:`Manage sitemaps for versioned documentation <manage-sitemaps>`.

