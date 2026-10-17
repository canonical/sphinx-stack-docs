---
myst:
  html_meta:
    description: How to switch to the Ulwazi theme in a documentation project based on Sphinx Stack.
---

(how-to-test-ulwazi-theme)=
(how-to-switch-to-ulwazi)=
(how-to-configure-ulwazi)=

# Configure the Ulwazi theme

Sphinx Stack 3.0 introduced major improvements to the look and feel of Canonical
documentation with its new theme, Ulwazi. Because of this dramatic change, the update
requires more configuration changes than usual.

This guide covers the initial setup and configuration of Ulwazi. Applying the diff
between your project and Sphinx Stack 3.0 introduces the same changes described in these
sections, but for heavily modified projects, it helps to step through the changes one at
a time.

## Install and set up Ulwazi

The removed lines shown in the diffs are from Sphinx Stack 2.0, but the same basic
changes can be applied for projects upgrading from Sphinx Stack 1.3 and higher. If your
project is based on Sphinx Stack 1.2 or lower,
{ref}`update the entire project <update-new-sphinx-stack>`.

In the `docs/requirements.txt` file, replace the canonical-sphinx extension with Ulwazi.

```{code-block} diff
:caption: requirements.txt

- canonical-sphinx~=0.7
+ ulwazi~=1.0
```

Then, replace the `canonical_sphinx` module in your configuration file with `ulwazi`.
While you're here, you should also remove the `notfound.extension` module. Because the
sphinx-notfound-page extension affects 404 page style and layout, Ulwazi sets it up
automatically.

```{code-block} diff
:caption: conf\.py

  extensions = [
-     "canonical_sphinx",
-     "notfound.extension",
+     "ulwazi",
      # ...
  ]
```

If you write documentation with MyST markdown, add the MyST parser as well. This was
previously set up behind the scenes with the canonical-sphinx extension.

```{code-block} diff
:caption: conf\.py

  extensions = [
-     "canonical_sphinx",
-     "notfound.extension",
+     "ulwazi",
+     "myst_parser",
      # ...
  ]
```

If your project is based on Sphinx Stack 1.3 or higher, then the MyST parser is already
listed as a dependency.

Add the following line to your configuration:

```{code-block} python
:caption: conf\.py

html_theme = "ulwazi"
```

At this point, your documentation should build successfully, albeit with some rendering
quirks that we'll iron out shortly. In the `docs` directory, clean your
environment and make sure the documentation builds with:

```{code-block} bash
make clean html
```

## Add fundamental configuration

The documentation builds, but a lot of information is still missing. Ulwazi offers a lot
of freedom when it comes to elements in the banner and footer, but to align your docs
with Canonical standards, you must update your configuration according to this section.

To ensure that a persistent element tells users they're looking at product docs, append
"documentation" to the `project` string. This gets rendered on the banner and will serve
as the home page link once we're done.

```{code-block} diff
:caption: conf\.py

- project = "Ubuntu Server"
+ project = "Ubuntu Server documentation"
```

Then, update the `html_title` variable that gets appended to each page's title.

```{code-block} diff
:caption: conf\.py

- html_title = project + " documentation"
+ html_title = project
```

The rest of the Ulwazi configuration is done in the configuration file's `html_context`
dictionary. Start by replacing your current `html_context` dictionary as follows:

```{code-block} diff
:caption: conf\.py

- html_context = {
-     "product_page": "",
-     "discourse": "",
-     "mattermost": "",
-     "matrix": "",
-     "github_url": "",
-     "repo_default_branch": "main",
-     "repo_folder": "/docs/",
-     "display_contributors": False,
-     "github_issues": "enabled",
-     "author": author,
-     "license": {
-         "name": "",
-         "url": "",
-     },
- }
+ html_context = {
+     "discourse": "",
+     "mattermost": "",
+     "matrix": "",
+     "github_url": "",
+     "feedback": True,
+ }
```

Update each value with your project's URL for the platform. If your project does *not*
have a presence on one of the platforms, leave the entry intact and the string empty.

Next, add the following entries to configure the banner:

```{code-block} diff
:caption: conf\.py

  html_context = {
      "discourse": "",
      "mattermost": "",
      "matrix": "",
      "github_url": "",
      "feedback": True,
+     "logo_title": "Canonical",
+     "logo_link_URL": "https://canonical.com",
+     "logo_img_URL": "https://assets.ubuntu.com/v1/82818827-CoF_white.svg",
  }
```

The `logo_title` and `logo_link_URL` should match your project's parent product page.
For most projects, this will be the Canonical product page, so the previous values won't
need to be changed. However, for a project like the Charmcraft docs, which are hosted
under the Juju product page, these would be updated as follows:

```{code-block} diff
:caption: conf\.py

  html_context = {
      "discourse": "",
      "mattermost": "",
      "matrix": "",
      "github_url": "",
      "feedback": True,
-     "logo_title": "Canonical",
-     "logo_link_URL": "https://canonical.com",
+     "logo_title": "Juju",
+     "logo_link_URL": "https://canonical.com/juju",
      "logo_img_URL": "https://assets.ubuntu.com/v1/82818827-CoF_white.svg",
  }
```

Lastly, declare the license information to be displayed in the footer.

```{code-block} diff
:caption: conf\.py

  html_context = {
      "discourse": "",
      "mattermost": "",
      "matrix": "",
      "github_url": "",
      "feedback": True,
      "logo_title": "Canonical",
      "logo_link_URL": "https://canonical.com",
      "logo_img_URL": "https://assets.ubuntu.com/v1/82818827-CoF_white.svg",
+     "author": author,
+     "license": {
+         "name": "",
+         "url": "",
+     },
  }
```

Set `license.name` to the [SPDX identifier](https://spdx.org/licenses/) for your
project's license and `license.url` to the license file in your repository.

And that's it! At this point, you can rebuild your documentation and see how everything
looks.

While this is the minimal configuration expected for all Canonical documentation
projects, Ulwazi can be further catered to your project with optional configuration,
described in the Ulwazi [Configuration
reference](https://documentation.ubuntu.com/ulwazi/content/configuration/).

## Enable PDF builds

Unlike the canonical-sphinx theme, Ulwazi doesn't handle PDF builds. PDF builds should
now be handled with the `sphinx-modern-pdf-style` extension.

In the `docs/requirements.txt` file, add the extension.

```{code-block} diff
:caption: requirements.txt

+ sphinx-modern-pdf-style~=0.1
```

Then, set up and enable the extension by making the following changes to your project's
configuration file:

```{code-block} diff
:caption: conf\.py

  extensions = [
+     "sphinx_modern_pdf_style",
      # ...
  ]

+ set_modern_pdf_config = True
```
