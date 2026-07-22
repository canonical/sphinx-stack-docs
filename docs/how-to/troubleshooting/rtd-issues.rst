.. meta::
   :description: Troubleshooting guidance for issues related to building and publishing documentation using the Sphinx Stack at Read the Docs.

.. _rtd_troubleshooting:

Read the Docs failures
======================

In this guide, you will find information on how to troubleshoot issues related to building the documentation set at Read the Docs.

.. _stable-version-wont-build-from-latest-tag:

Stable version won't build from the latest tag
----------------------------------------------

If your project has the ``stable`` version configured to build from tags, such as with
the default `semantic versioning behavior
<https://docs.readthedocs.com/platform/stable/versions.html#versions-are-git-tags-and-branches>`_,
your ``stable`` version can become out-of-step and continue building a particular tag,
even when the repository has newer tags.


Possible causes
~~~~~~~~~~~~~~~

An unwanted tag might have been pushed to the repository and then removed. Once
ReadTheDocs creates a version from a tag, it doesn't later verify that the tag still
exists, so the version will persist and become a zombie.

If the unwanted tag is a higher iterator than any existing tag, the zombie version will
always take precedence. For example, if tag ``20.2.0`` was pushed by accident and then
replaced with ``2.20.0``, the corresponding version 20.2.0 will persist, and ``stable``
will continue pointing to it.


Diagnosis
~~~~~~~~~

There's a roundabout procedure to verify whether your project is affected. Start by
opening your project dashboard on ReadTheDocs.

On the **Builds** tab, locate the most recent ``stable`` build. For that version, hover
over the status indicator. In the hover box, open the **stable** link. If the resulting
GitHub page is a 404, then your project has a zombie version.

.. image:: /how-to/assets/troubleshoot-stable-zombie-version.png


Resolution
~~~~~~~~~~

On your project dashboard, open the **Versions** tab and click **Add version**.

Find the zombie version, deactivate it, then update it.

Rebuild ``stable`` by retriggering it on the dashboard or pushing a new tag to the
repository.


Issue tracking
~~~~~~~~~~~~~~

`readthedocs/readthedocs.org#12450
<https://github.com/readthedocs/readthedocs.org/issues/12450>`_

Inactive version is invisible in the web GUI and occupies a slug
----------------------------------------------------------------

There is no delete button in the web GUI of Read the Docs.
You can turn the **Active** switch off to make a version inactive, but there is no way to delete it.

Sometimes when you try to create a new version, you get an error that the slug is already in use,
even though you don't see the version occupying it.

Possible causes
~~~~~~~~~~~~~~~

When a version is deactivated
(see `Inactive versions <https://docs.readthedocs.com/platform/stable/versions.html#version-states>`_),
its documentation content is deleted and builds can no longer be triggered.
However, the version itself is not deleted. It still exists and retains its slug.
Such inactive versions may not appear in the **Versions** tab list,
making them effectively invisible in the web GUI while still occupying the slug.

Resolution
~~~~~~~~~~

The easiest way to deal with an invisible inactive version is to open its settings
page directly via URL:

.. code-block:: text

   https://app.readthedocs.com/dashboard/<project-name>/version/<slug>/edit/

For example:

.. code-block:: text

   https://app.readthedocs.com/dashboard/canonical-kafka-charm/version/latest/edit/

From there, you can make the version active again, which will make it visible in the
web GUI, or change its slug.

Build failures due to sudden authentication errors at Read the Docs
-------------------------------------------------------------------

At times, documentation projects that were earlier building successfully may suddenly experience build failures due to authentication issues with GitHub.

Possible cause
~~~~~~~~~~~~~~

The GitHub Webhook goes out of sync for some reason and misbehaves, resulting in random authentication failures and build errors.

Resolution
~~~~~~~~~~

Confirm that the git repository URL setting in Read the Docs points to a valid repository. Verify that the public SSH key from your Read the Docs project is installed as a deploy key on your GitHub repo. If these are already in place, then try to resync the webhook.

If that does not solve the problem, delete and `reinstate the webhook <https://docs.readthedocs.com/platform/latest/guides/setup/git-repo-manual.html#manual-integration-setup>`_.

`readthedocs.yaml` file issues
------------------------------

The GitHub pull request build fails stating the ``.readthedocs.yaml`` file is not accessible.

Probable cause
~~~~~~~~~~~~~~

During the GitHub PR build process, the ``.readthedocs.yaml`` file is not accessible to the build system. This can happen if the file is missing or if it is not in the root of the repository (default location).


Resolution
~~~~~~~~~~

Read the Docs requires a ``.readthedocs.yaml`` file in the repository root to trigger a build. If this file is missing, the build will fail. The Canonical Sphinx Stack assumes, by default, that documentation content lives under ``/docs/`` and that ``.readthedocs.yaml`` is in the repository root. However, neither location is a hard requirement.

If your project uses a different structure, ensure that ``.readthedocs.yaml`` exists in the repository root and update its configuration values, and/or the Sphinx ``conf.py`` file, to point to the correct documentation source folder.