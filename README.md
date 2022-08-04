# Developer Documentation for the Biomedical Data Translator

This repository hosts templates, scripts and contents for primary technical documentation for Developers within the [Biomedical Data Translator](https://ncats.nih.gov/translator) project [("Translator"; Fecho _et al,_ 2022)](https://ascpt.onlinelibrary.wiley.com/doi/10.1111/cts.13301) of the [National Center for Advancing Translational Sciences ("NCATS")](https://ncats.nih.gov).

The repository uses the [`mkdocs`](https://www.mkdocs.org/) tooling to generate and manage an indexed compendium of the documentation for [Open Access licensed](LICENSE) hosting on its [Official (ReadTheDocs) Site](https://translator-developer-documentation.readthedocs.io/en/latest/).

## Getting Started

The site uses Python (suggest 3.9 or better) and mkdocs. Assuming that you have python and pip on your machine, then install some requirements (including mkdocs) as follows:

```shell
pip install -r requirements.txt
```

The repository already has core `mkdocs` configuration and layout, within which additional content may be added. 

The following `mkdocs` commands are useful for the work:

* `mkdocs serve` - Start the live-reloading docs server on your computer.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.

### Project layout

The Translator `mkdocs` documentation is hierarchically structured as follows:

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # the documentation homepage.
        faq.md
        img/      # shared images
        architecture/  # overview of the Translator architecture
            index.md
            ...
        guide-for-developers/
            index.md   # specific hands-on developer documentation, tutorials directory
            ...
            tutorials/
                index.md   # tutorials/cookbook pages
                ...
        about/
            index.md  # project details about Translator
            ...
