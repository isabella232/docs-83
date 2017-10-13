---
layout: default
title: {{ site.name }}
---

# <a name="content" class="anchor">Content</a>
 
Jekyll transforms plain text into static websites and blogs. Here, we will briefly cover how to override Jekyll's layout and write content.

### <a name="sass" class="anchor">Liquid</a>

Our Jekyll installation uses Liquid for template processing. You can learn more about overriding default You can also add any of your modifications there.

### <a name="images" class="anchor">Images and Other Assets</a>

All images can be placed in the images directory under a logical organizational structure, as needed. If you have videos, you can create a videos directory and it should be likewise detected and added to the generated web content. You can learn how to reference images in the [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet).

### <a name="jekyll" class="anchor">Jekyll</a>

You can learn more about how to customize Jekyll [here](https://jekyllrb.com/).

## <a name="markdown" class="anchor">Markdown</a>

Our [Jekyll configuration](setup.html#jekyll_config) uses the Kramdown engine for Markdown processing. You can find many references online to help you get started like the [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet). Markdown allows you to apply structure to your text documents. The Kramdown engine will process all *.md files into html and place them in the _site directory to be served as web content. You can place all of your Markdown files in the root of the project directory.

You will see that this template structure contains index.md, background.md, setup.md, etc. These can be used as examples.
