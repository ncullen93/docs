# Unified Documentation for Advanced Normalization Tools

This repository contains docs for the ANTsX ecosystem of packages and the
ants.dev platform, as well as tutorials for medical image analysis featuring
ANTs that are language-agnostic (i.e., include the same code snippets in bash,
R, and Python).

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

- encourage the use of notes (:::note TEXT HERE :::) and tips (:::tip TEXT HERE :::) to
  give the articles a little color pop

## Other notes

- The ants.dev platform pulls from the raw files for the markdown documents, and these
  can take at least a few minutes to update once you actually commit changes to the repo. Keep
  that in mind in case you wonder why updates are not automatically showing up on ants.dev.
