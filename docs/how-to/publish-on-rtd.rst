.. meta::
   :description: How to publish your documentation on Read the Docs.

.. _publish-on-rtd:


Publish on Read the Docs
========================

Publishing your documentation on Read the Docs makes it available to a wider audience with automatic builds triggered by repository updates. This guide walks you through the process of setting up your Sphinx Stack project on Read the Docs. 


Prepare your project and account
---------------------------------

- Ensure your documentation :ref:`builds without errors or warnings <build-clean>`.
- Ensure you have the permission to manage webhooks for the documentation repository, or get in touch with someone who does. A webhook is needed if you want Read the Docs to automatically build your documentation whenever a change occurs. 
- Create a `Read the Docs account <https://docs.readthedocs.com/platform/stable/tutorial/index.html#creating-a-read-the-docs-account>`__. If your documentation is hosted on a supported Git provider (such as GitHub, GitLab, or Bitbucket), `connect the account to your Git provider <https://docs.readthedocs.com/platform/stable/guides/connecting-git-account.html>`__.
- In the root of your documentation repository, prepare the `.readthedocs.yaml <https://docs.readthedocs.com/platform/stable/config-file/index.html>`__ file.


Add your project to Read the Docs
---------------------------------

Log in to the `Read the Docs dashboard <https://readripman.readthedocs.io/en/latest/glossary.html#term-dashboard>`__ to add a project. If you are the repository administrator, `add the project automatically <https://docs.readthedocs.com/platform/stable/intro/add-project.html#automatically-add-your-project>`__. Follow the on-screen instructions to add your project. If you are not a repository administrator or your documentation is not hosted on a supported Git provider, `add the project manually <https://docs.readthedocs.com/platform/stable/intro/add-project.html#manually-add-your-project>`__. A build will be triggered after the project is added.

`Check the first build <https://docs.readthedocs.com/platform/stable/tutorial/index.html#checking-the-first-build>`__. After it completes successfully, you can view the live documentation from the project home page. 

If there are any build errors, fix them: 

- If your project is hosted in a private repository, your first build will fail because your repository is not configured to allow Read the Docs to clone the repository. To fix the access issue, follow the steps in `Configuring your repository <https://docs.readthedocs.com/platform/stable/guides/creating-project-private-repository.html#configuring-your-repository>`__.
- If your project is hosted from a public repository, your documentation should build successfully. If you get any errors, check the build log for indications on what the problem is.


Additional configuration
------------------------

Configurations in this section are all optional. Follow the instructions here to configure your Read the Docs project according to your preferences.


Enable automatic builds
^^^^^^^^^^^^^^^^^^^^^^^

Automatic builds are not supported on Launchpad because its webhooks aren't compatible with Read the Docs. Builds must be triggered manually on Read The Docs.

The Read the Docs integration webhook can automatically build your documentation when your GitHub repository changes. If you have permission to manage webhooks for the GitHub repository and added it to Read the Docs automatically, the integration webhook was created automatically. Otherwise, the webhook must be set up by someone with the appropriate permission. To manually set up the webhook, refer to `How to configure a Git repository integration manually <https://docs.readthedocs.com/platform/stable/guides/setup/git-repo-manual.html#how-to-manually-configure-a-git-repository-integration>`__.


Enable pull request builds
^^^^^^^^^^^^^^^^^^^^^^^^^^

To build and preview your documentation whenever a pull request is opened or updated, open the project Settings and select :guilabel:`Build pull requests` for this project.


Make your documentation public (RTD for Business only)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

By default, Read the Docs publishes your documentation for logged-in users only. 

To make your documentation publicly accessible, you must configure the privacy level for each version of the documentation separately. Navigate to the Versions tab and change the `Privacy Level <https://docs.readthedocs.com/platform/stable/guides/pull-requests.html#privacy-levels>`__ for each version.

If your documentation publishes tagged versions that should be public by default, add an `Automation Rule <https://docs.readthedocs.com/platform/stable/guides/automation-rules.html#adding-a-new-automation-rule>`__ under the project Settings with the following configuration:

.. list-table:: 
   :widths: 60 40
   :header-rows: 1

   * - Configuration field
     - Value
   * - Version type
     - Tag
   * - Version predefined match pattern
     - Any version
   * - Action
     - Make version public


Change URL versioning scheme
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The default versioning scheme is `Multiple versions with translations <https://docs.readthedocs.com/platform/stable/versioning-schemes.html#multiple-versions-with-translations>`__. If you don't have translations for your documentation, `change the URL versioning scheme <https://docs.readthedocs.com/platform/stable/versioning-schemes.html#how-to-change-the-url-versioning-scheme-of-your-project>`__.


Add support for Git Large File Storage
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

By default, Read the Docs can't access large files stored with Git LFS. If your docs project contains large files, `add support for Git LFS <https://docs.readthedocs.com/platform/stable/build-customization.html#support-git-lfs-large-file-storage>`__.