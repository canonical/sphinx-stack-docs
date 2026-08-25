.. meta::
   :description: How to configure project-specific parameters.

.. _configure-your-project:

Configure your project
=======================

Configuration for a Sphinx Stack based documentation is set in the ``docs/conf.py`` configuration file. The default configuration in the Sphinx Stack is prepared in a way that makes sense for most projects. However, you must set some critical project-specific configuration values, like the project's name, to ensure the documentation reflects your project accurately.

.. important::

    The Sphinx Stack is updated periodically. After you set up your documentation repository with the Sphinx Stack, you need to track the changes made to the Sphinx Stack and manually maintain your repository.

    Use the Sphinx Stack `release notes <https://documentation.ubuntu.com/sphinx-stack/latest/release-notes>`__ or `changelog <https://github.com/canonical/sphinx-stack/blob/main/CHANGELOG.md>`__ to track changes to the Sphinx Stack. Subscribe to the repository releases to get notified whenever there is a new release. For the recommended way of manually updating your Sphinx Stack, see :ref:`update-sphinx-stacks`.

Configure the following project settings in the ``conf.py`` file. Steps 1 – 5 cover the required configuration. Each step links to the relevant configuration guidance. For all available common settings, see :ref:`conf-py-configuration`.

1. Set :ref:`project identity, branding, and repository metadata <conf-py-project-information>`.
2. Set the :ref:`documentation site URL <conf-py-sitemap>`.
3. Configure :ref:`feedback and page navigation behavior <conf-py-ui-behavior>`.
4. Define :ref:`LLM metadata <conf-py-llm-context>`.
5. Configure :ref:`how Sphinx should validate links <conf-py-link-checker>`.
6. Add :ref:`optional configuration <conf-py-optional-configuration>` as needed.