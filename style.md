## Style Guide

These docs are hosted on ants.dev/docs. There are a few style considerations
to follow in order to ensure an ideal user experience on ants.dev.

- use two hashmarks (`##`) to denote major headers or sections in articles. This
  is because all two-hashmark headers are displayed in the right sidebar of ants.dev/docs
  to allow users to navigate within articles.

- in other words, don't use underlines to specify headers or bold-ness

- keep headers as short as possible, ideally 2 - 3 words. Omit unnecessary or redundant
  information in the header. For example, "Performing segmentation in ANTs" can be shortened
  to just "Performing segmentation" in a tutorial specifically about ANTs.

- github-flavored markdown is supported so anything that looks good on github should
  look good on ants.dev. If it doesn't, file an issue.

- using R markdown (.Rmd) is OK but they need to be converted to markdown to be useable.

- encourage the use of directives such as notes (:::note TEXT HERE :::), tips (:::tip TEXT HERE :::),
  and warnings (:::warning TEXT HERE :::) to give the articles a little color pop. They wont render on github but they will look nice on ants.dev/docs.

- for code blocks, use three backticks and `r` or `python` to denote languages. The languages
  should not be capitalized.

- use huggingface.co (e.g., https://huggingface.co/docs/transformers/index) for inspiration
  as to how good package documentation should be.

## Platform-specific markdown

There are certain markdown expressions that only render correctly at ants.dev/docs. Such expressions
will not cause any errors when viewing the markdown on github, and the expression will still be clear and legible on github, but they will not look as they should.

The following are examples of these expressions:

### Directives

Directives are a kind of alert that draw special attention from the reader by highlighting text
in color. The note, tip, and warning directives are available for ants.dev docs even though they
will not render as directives on github. They look like this:

:::note
this is a note directive
:::

:::tip
this is a tip directive
:::

:::warning
this is a warning directive

### Code tabs

Code tabs are another expression specific to ants.dev. Code tabs let you write the same code snippet
in multiple language, but wrapped in a tab where only one snippet is visible at a time. We use these
to show the same ANTs expression in bash, R, and Python. Code snippets are written like this:

```r|python
x <- 1
x <- x + 1
===
x = 1
```

As you can see, the first thing to do is write all the languages to be included in the tabs separated
by a vertical line with no spaces. The next thing to do is to separate the language snippets by exactly three equal signs (`===`). This will render correctly in the ants.dev docs. Do not use any brackets around the languages.
