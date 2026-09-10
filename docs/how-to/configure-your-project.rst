.. meta::
   :description: How to configure project-specific parameters.

.. _configure-your-project:

Configure your project
=======================

Sphinx Stack documentation projects are configured in the ``docs/conf.py`` file. The default configuration will work for most projects, but you still need to set some project-specific values, such as your product's name and documentation URL.

.. important::

    The Sphinx Stack is updated periodically. After you set up your documentation repository with the Sphinx Stack, you need to track the changes made to the Sphinx Stack and manually maintain your repository.

    Use the Sphinx Stack `release notes <https://documentation.ubuntu.com/sphinx-stack/latest/release-notes>`__ or `changelog <https://github.com/canonical/sphinx-stack/blob/main/CHANGELOG.md>`__ to track changes to the Sphinx Stack. Subscribe to the repository releases to get notified whenever there is a new release. For the recommended way of manually updating your Sphinx Stack, see :ref:`update-sphinx-stacks`.

Mandatory configuration values are marked with ``TODO`` in the ``conf.py`` file. Set these to align with your project and ensure you comment out any settings that aren't relevant to your environment. 

Steps 1 – 5 cover the required configuration. Each step links to the relevant configuration guidance. For all available common settings, see :ref:`conf-py-configuration`.

1. Set :ref:`project identity, branding, and repository metadata <conf-py-project-information>`.
2. Set the :ref:`documentation site URL <conf-py-sitemap>`.
3. Configure :ref:`feedback and page navigation behavior <conf-py-ui-behavior>`.
4. Define :ref:`LLM metadata <conf-py-llm-context>`.
5. Configure :ref:`how Sphinx should validate links <conf-py-link-checker>`.
6. Add :ref:`optional configuration <conf-py-optional-configuration>` as needed. The following links can help you with additional configuration:

   - `Sphinx configuration <https://www.sphinx-doc.org/en/master/usage/configuration.html>`__
   - `Sphinx extensions <https://www.sphinx-doc.org/en/master/usage/extensions/index.html>`__
   - `Furo documentation <https://pradyunsg.me/furo/quickstart/>`__
