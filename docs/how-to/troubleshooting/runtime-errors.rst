.. meta::
   :description: Troubleshooting guidance for runtime issues related to Sphinx rendering peculiarities or link configurations.

.. _runtime_errors_troubleshooting:

Runtime errors
==============

"&" character in the URL breaks links
--------------------------------------

A link in the documentation set is broken when the URL contains an "&" character. For example, a link to ``https://example.com/?param1=value1&param2=value2`` may be rendered as ``https://example.com/?param1=value1`` in the generated HTML, causing the link to break.

Possible cause
~~~~~~~~~~~~~~

In Markdown files of the type ``.md``, the "&" character is treated as a special character and is not rendered correctly in the generated HTML. This can cause links to break when they contain an "&" character.

Resolution
~~~~~~~~~~

In the documentation source code files of the type ``.rst``, use ``&`` directly in the URL. Sphinx escapes it correctly when generating HTML. For example, use ``https://example.com/?param1=value1&param2=value2``.

If you are using Markdown files of the type ``.md``, you can use the raw HTML syntax to include the link in the documentation. For example, you can use:

.. code:: html

     <a href="https://example.com/?param1=value1&amp;param2=value2">Link text</a>