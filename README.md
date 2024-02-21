# Docs for the Advanced Normalization Tools ecosystem

This repository contains docs for the ANTs ecosystem of packages and the ants.dev platform, as well as tutorials for medical image analysis featuring ANTs that include the same code snippets in bash, R, and Python.

## Repo structure

Each folder of the docs/ repo contains docs for different aspects of the ANTs ecosystem.

### architectures

These are docs for architectures available in ANTsPyNet, ANTsXNet, and on ants.dev.

### developer

These are code-based tutorials for using functionality of the ANTs ecosystem of packages through command-line (C++), R, or Python.

### models

These are docs for pre-trained models available in ANTsPyNet, ANTsXNet, and on ants.dev.

### packages

These are docs for packages in the ANTs ecosystem. Ideally, in the future API-level docs for all ANTs ecosystem packages will be compiled and stored here so that they are standardized. For now, it is mostly just general descriptions of each package.

### platform

These are tutorials / docs for how to use specific functionality on the ants.dev platform.

## Contributing

We gladly accept contributors of tutorials or other docs for the ANTs ecoysystem of packages Please try to follow the [style guide](https://www.github.com/ncullen93/docs/style.md) when writing docs, as we use a slightly expanded version of GitHub markdown.

For writing details of architectures and models, there are templates available (\_template-\*.md files)as a starting point to ensure all the relevant information is considered. Please consider using those to ensure consistency.

Images and other media can be stored in the \_assets/ folder.

## Other notes

- The ants.dev platform pulls from the raw files for the markdown documents, and these can take at least a few minutes to update once you actually commit changes to the repo. Keep that in mind in case you wonder why updates are not automatically showing up on ants.dev.
