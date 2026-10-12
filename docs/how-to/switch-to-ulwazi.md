---
myst:
  html_meta:
    description: How to switch to the Ulwazi theme in a documentation project based on Sphinx Stack.
relatedlinks: "[Ulwazi&#32;on&#32;PyPI](https://pypi.org/project/ulwazi), [Vanilla](https://vanillaframework.org), [sphinx-basic-ng](https://github.com/pradyunsg/sphinx-basic-ng)"
---

(how-to-test-ulwazi-theme)=
(how-to-switch-to-ulwazi)=

# Switch to the Ulwazi theme

Ulwazi is a Sphinx theme built on Vanilla, with the base layout and functionality
derived from sphinx-basic-ng.

To start using Ulwazi, upgrade your project to Sphinx Stack 3.0 or later. This is the
supported way to adopt and maintain the theme. Installing Ulwazi without Sphinx Stack
is no longer supported; the manual instructions below are retained for existing custom
setups. If your project already uses Ulwazi, see how to update it from PyPI.

Create a branch for the change. Build the documentation locally and check the changes in
the Read the Docs (RTD) preview of a pull request before merging.

## Upgrade Sphinx Stack to 3.0 or later

To get Ulwazi as part of the Sphinx Stack, {ref}`update your Sphinx Stack
<update-sphinx-stacks>` to version 3.0 or later. Bring the updated requirements and
configuration into your project, preserving your project-specific settings and
extensions. Updating the Stack's version number alone does not update files already
copied into your repository.

After the upgrade, check that `conf.py` selects `html_theme = "ulwazi"` and the
`extensions` list includes `"ulwazi"`. You do not need to follow the manual installation
steps below as well.

## Manual installation for existing setups (unsupported)

These steps are provided for projects that already manage Ulwazi separately from Sphinx
Stack. Manual installations without Sphinx Stack are no longer supported. For a new
migration, upgrade Sphinx Stack instead. If you maintain an existing manual setup,
check the [Ulwazi releases](https://github.com/canonical/ulwazi/releases) for the
configuration and dependencies that correspond to the package installed from
[PyPI](https://pypi.org/project/ulwazi/). The sample configuration on the development
branch may differ from the published package.

### Update the dependencies

In the requirements file used by your documentation build, replace the Canonical Sphinx
theme package with Ulwazi from PyPI:

```{code-block} diff
:caption: requirements.txt

- canonical-sphinx
+ ulwazi
```

If your existing `canonical-sphinx` requirement has a version constraint, replace the
whole requirement. Ulwazi installs its own runtime dependencies; you do not need to list
those packages again just to use the theme. Keep the separately installed extensions
and tools that your project needs, such as `myst-parser` for Markdown,
`sphinx-design` for tabs and cards, `sphinx-sitemap` for a sitemap, and
`sphinx-autobuild` for `make run`. Do not replace your entire requirements file with a
sample from another project.

Check whether the sample for the **release you installed** lists
`canonical_sphinx_config`. If it does, install the corresponding
`canonical-sphinx-config` package as instructed by that release; otherwise, do not add
it just because an older sample does. Avoid a dependency on a moving Git branch.

### Update the configuration

There are two ways to update `conf.py`:

* Start with Ulwazi's [sample `conf.py`](https://github.com/canonical/ulwazi/tags),
  selecting the tag that matches your installed package and opening
  `docs/default-conf.py` at that tag.
* Adapt your existing configuration if it has substantial customisation you need to
  preserve.

Neither option replaces your project's own paths, redirects, license, extensions,
metadata, or build settings. Review custom HTML templates originally written for the
Canonical Sphinx/Furo layout: they may need to be removed or adapted for Ulwazi.

#### Start from the sample configuration

To use the sample as a starting point:

1. Save your existing `conf.py` outside the Sphinx source directory so Sphinx does not
   process it as a documentation file.
2. Open the sample `docs/default-conf.py` at the Git tag matching the Ulwazi package
   you installed. Copy it to your documentation directory as `conf.py`.
3. Compare both files and carry over your project name, license, repository URLs,
   extensions, source paths, redirects, sitemap and other project-specific settings.
   Check that any referenced `_static`, `_templates`, or included files exist in your
   project. Replace the sample's placeholder values rather than publishing them.

#### Adapt your existing configuration

The following instructions describe the modifications needed to support Ulwazi in an
existing `conf.py` file. Use this approach if you want to preserve as much of your
original `conf.py` as possible, for example in a heavily customised deployment or when
troubleshooting a configuration issue.

For an example of a project-specific migration, see the [Charmed Apache Kafka Ulwazi PR](https://github.com/canonical/kafka-operator/pull/444/files#diff-85933aa74a2d66c3e4dcdf7a9ad8397f5a7971080d34ef1108296a7c6b69e7e3).

##### Set the theme

Tell Sphinx to use Ulwazi as the theme:

```{code-block} python
:caption: conf\.py

html_theme = "ulwazi"
```

##### Update the extensions

In the `extensions` list, replace the Canonical Sphinx **module** with Ulwazi. Keep
other extensions your content and builds use; for example, keep `"myst_parser"` if you
have Markdown source files and `"sphinx_design"` if you use its tabs or cards.

```{code-block} diff
:caption: `extensions` in conf\.py

-"canonical_sphinx",
+"ulwazi",
```

The package name in `requirements.txt` and the import name in `extensions` are not
always the same. Add or retain `"canonical_sphinx_config"` only if the sample for your
installed Ulwazi release uses it. Similarly, check whether that release enables
`notfound.extension` automatically before removing an explicit entry.

Ulwazi uses `sphinx-design` tab sets. If you still use `sphinx-tabs` directives (`tabs`
and `tab`), convert them to `tab-set` and `tab-item` before removing
`"sphinx_tabs.tabs"` and the `sphinx-tabs` package.

##### Configure navigation, source links and the footer

Review your existing `html_context` against the sample for the installed release. The
following example shows how to configure the project details and GitHub links; replace
the example repository, product URL, and license with your own. `product_page` is a
hostname without `https://` in this example.

```{code-block} python
:caption: conf\.py

github_repo = "https://github.com/your-org/your-repo"
source_branch = "main"  # Use the branch containing your docs source files.
repo_folder = "/docs/"  # Adjust if the docs live elsewhere in the repository.
default_source_extension = ".rst"  # Use ".md" for Markdown fallback pages.

html_context = {
    "project": project,
    "author": author,
    "product_page": "documentation.example.com",
    "github_url": github_repo,
    "repo_branch": source_branch,
    "repo_folder": repo_folder,
    "feedback": True,
    "default_source_extension": default_source_extension,
    "default_edit_url": github_repo + "/edit/" + source_branch
    + repo_folder + "index" + default_source_extension,
    "default_view_url": github_repo + "/blob/" + source_branch
    + repo_folder + "index" + default_source_extension,
    "license": {
        "name": "YOUR-LICENSE-ID",  # Use your actual license identifier.
        "url": github_repo + "/blob/" + source_branch + "/LICENSE",
    },
    "footer": {"product": True, "license": True, "entries": []},
    "logo_link_URL": "https://documentation.example.com",
    "logo_img_URL": "https://assets.ubuntu.com/v1/82818827-CoF_white.svg",
    "logo_title": "Canonical",
}
```

Set `repo_branch` and `repo_folder` to the actual source location used for edit/view
links. For Read the Docs branch builds, consult the matching sample for choosing the
source branch; pull-request identifiers and tags are not editable Git branches.
`default_edit_url` and `default_view_url` are fallbacks for generated pages. If your
docs mix reST and Markdown, choose the fallback extension for your index page; source
links for ordinary pages should use their actual file extensions. If you do not enable
feedback, omit the feedback and fallback settings. Set the logo and footer values only
after checking how your installed Ulwazi release uses them.

Keep the project's real license separate from its `copyright` string; if the footer
displays both, a copyright year (or year range) avoids repeating the license name.
Review any custom CSS, JavaScript, templates, and analytics settings before copying
values from the sample configuration.

##### Review optional features

* **Sitemap:** If you use `sphinx-sitemap`, keep its `html_baseurl` and URL scheme
  configured for your hosted site. `sitemap_show_lastmod = True` is a setting for that
  extension, not a requirement of Ulwazi.
* **Not-found page:** Check whether your installed release activates
  `notfound.extension` itself. If it does and your docs are hosted below a path such as
  `/your-product/`, consult that release's guidance for setting `slug` in `conf.py`.
  Exclude `404/` from the sitemap when the page is generated.
* **PDF:** If you publish PDF documentation, install `sphinx-modern-pdf-style` and add
  `"sphinx_modern_pdf_style"` **after** `"ulwazi"` in `extensions` when the installed
  release requires that order for PDF branding. Follow the matching sample for
  `set_modern_pdf_config = True`. If you convert SVG images for PDF, keep
  `sphinxcontrib-svg2pdfconverter[CairoSVG]` in your requirements and
  `"sphinxcontrib.cairosvgconverter"` in `extensions`. A local PDF build also needs
  the required system LaTeX tools.

## Update Ulwazi from PyPI

Use this route when your project already uses Ulwazi, whether you installed it
manually or adopted it through a Sphinx Stack upgrade.

1. Find the latest published package on [PyPI](https://pypi.org/project/ulwazi/) and
   read its [release notes](https://github.com/canonical/ulwazi/releases). Compare the
   tagged configuration with the one your project currently uses. Check dependency,
   extension, template, and PDF changes before updating.
2. Update the `ulwazi` requirement in the file your project actually installs (for
   example, `docs/requirements.txt`), applying your project's pinning policy. If it is
   pinned or constrained below the latest available release, change the constraint;
   if it is unpinned, a fresh install can already select the latest release. Update
  and sync a dependency lock file if your project uses one. Do not rely on an upgrade
  in a local virtual environment alone: the next build may reinstall the declared
  requirement.
3. Recreate or synchronise the documentation environment. If you manage the environment
  directly with pip, `python -m pip install --upgrade ulwazi` updates that environment,
  but does not update a pinned requirement or lock file. Confirm which release was
  installed with `python -m pip show ulwazi` (or your package manager's equivalent),
  and apply any configuration or content changes called for by that release. Then
  follow the tests below before merging.

## Test the documentation

Make sure each enabled extension's Python package is installed, and that packages you
removed from `requirements.txt` are not still referenced in `conf.py`. In a project
using the Sphinx Stack Makefile, `make clean` removes the existing documentation
virtual environment as well as build output; `make clean-doc` alone does not reinstall
changed dependencies. Build HTML with warnings treated as errors, then preview it:

```shell
cd docs
make clean
make html
make run
```

Open http://127.0.0.1:8000 in your browser. Check navigation, source and feedback links,
tabs, footer and license, redirects, sitemap, 404 page, and custom templates and assets.
Check that contributors, related links and last-updated information render if your
project depends on them: a successful build does not guarantee those features appear.
If you publish PDFs and have the system prerequisites, also run `make pdf` and check the
resulting document. Review both HTML and PDF in the RTD pull-request preview where
applicable. If a build fails, resolve missing extensions, incompatible requirements or
configuration values, and rebuild.

Report issues or feature requests in the [Ulwazi GitHub
repository](https://github.com/canonical/ulwazi/issues/new).