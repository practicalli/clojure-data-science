# Data Science with Clojure

```none
██████╗ ██████╗  █████╗  ██████╗████████╗██╗ ██████╗ █████╗ ██╗     ██╗     ██╗
██╔══██╗██╔══██╗██╔══██╗██╔════╝╚══██╔══╝██║██╔════╝██╔══██╗██║     ██║     ██║
██████╔╝██████╔╝███████║██║        ██║   ██║██║     ███████║██║     ██║     ██║
██╔═══╝ ██╔══██╗██╔══██║██║        ██║   ██║██║     ██╔══██║██║     ██║     ██║
██║     ██║  ██║██║  ██║╚██████╗   ██║   ██║╚██████╗██║  ██║███████╗███████╗██║
╚═╝     ╚═╝  ╚═╝╚═╝  ╚═╝ ╚═════╝   ╚═╝   ╚═╝ ╚═════╝╚═╝  ╚═╝╚══════╝╚══════╝╚═╝
```

## Book status

[![MegaLinter](https://github.com/practicalli/clojure-data-science/actions/workflows/megalinter.yaml/badge.svg)](https://github.com/practicalli/clojure-data-science/actions/workflows/megalinter.yaml)
[![Publish Book](https://github.com/practicalli/clojure-data-science/actions/workflows/publish-book.yaml/badge.svg)](https://github.com/practicalli/clojur-data-sciencee/actions/workflows/publish-book.yaml)
[![pages-build-deployment](https://github.com/practicalli/clojur-data-sciencee/actions/workflows/pages/pages-build-deployment/badge.svg)](https://github.com/practicalli/clojur-data-sciencee/actions/workflows/pages/pages-build-deployment)

[![Ideas & Issues](https://img.shields.io/github/issues/practicalli/clojure-data-science?label=content%20ideas%20and%20issues&logoColor=green&style=for-the-badge)](https://github.com/practicalli/clojure-data-science/issues)
[![Pull requests](https://img.shields.io/github/issues-pr/practicalli/clojure-data-science?style=for-the-badge)](https://github.com/practicalli/clojure-data-science/pulls)

![GitHub commit activity](https://img.shields.io/github/commit-activity/m/practicalli/clojure-practicalli-content?style=for-the-badge)
![GitHub contributors](https://img.shields.io/github/contributors/practicalli/clojure?style=for-the-badge&label=github%20contributors)

## Creative commons license

<div style="width:95%; margin:auto;">
  <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a>
  This work is licensed under a Creative Commons Attribution 4.0 ShareAlike License (including images & stylesheets).
</div>

## Overview

A guide to writing services and applications in the context of data science

Introduces libraries and tools useful for creating those applications

Visualization of data

Integration with other data science tooling

Reference to useful mathematical techniques

This guide does not claim to make any attempt to teach you how to be a professional data scientist.

![Practicalli Data Science book banner](https://raw.githubusercontent.com/practicalli/graphic-design/live/book-covers/practicalli-clojure-data-science-book-banner-alpha.png)

> Alpha stage book - very early concept capturing experiences of data science work from the last 3 commercial engagments by the Practicalli team


A practical guide to data mining, data wrangling and visualisation tools, techniques and libraries.  Guides will take a story telling approach to ensure a meaningful context in which design decisions are taken.

A starting point for Clojure developers on their journey into Data Science.  As Data Science is such a vast subject area, no one resource can cover such diversity, so this guide will recommend numerous resources that go far deeper into specific areas.


## Target Audience

This guide is aimed at software engineers interested in data science or working as data analysts or with data science teams.  No data science experience is expected and the authors of this guide are not data science experts.

Mathematics concepts underpin much of data science and will be explained as they are used, or recommend resources linked to.  Mathematics experience should also notbe required.

## Contributing

Issues and pull requests are most welcome.  Please detail issues as much as you can.  Pull requests are simpler to work with when they are specific to a page or at most a section.  The smaller the change the quicker it is to review and merge.

Please [see the detailed contributing section of the book](contributing.html) before raising an issue or pull request

* [Current Issues](https://github.com/practicalli/clojure-data-science/issues)
* [Current pull requests](https://github.com/practicalli/clojure-data-science/pulls)

[Practicalli Clojure CLI Config](clojure/clojure-cli/practicalli-config.md) provides a user level configuration used in this guide and issues and pull requests can also be made there.

By submitting content ideas and corrections you are agreeing they can be used in this workshop under the [Creative Commons Attribution ShareAlike 4.0 International license](https://creativecommons.org/licenses/by-sa/4.0/).  Attribution will be detailed via [GitHub contributors](https://github.com/practicalli/clojure-data-science/graphs/contributors).


## Sponsor Practicalli

[![Sponsor Practicalli via GitHub](https://raw.githubusercontent.com/practicalli/graphic-design/live/buttons/practicalli-github-sponsors-button.png)](https://github.com/sponsors/practicalli-johnny/)

All sponsorship funds are used to support the continued development of [Practicalli series of books and videos](https://practical.li/), although most work is done at personal cost and time.

Thanks to [Cognitect](https://www.cognitect.com/), [Nubank](https://nubank.com.br/) and a wide range of other [sponsors](https://github.com/sponsors/practicalli-johnny#sponsors) for your continued support


## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=practicalli/clojure-data-science&type=Date)](https://star-history.com/#practicalli/clojure-data-science&Date)


## GitHub Actions

The megalinter GitHub actions will run when a pull request is created,checking basic markdown syntax.

A review of the change will be carried out by the Practicalli team and the PR merged if the change is acceptable.

The Publish Book GitHub action will run when PR's are merged into main (or the Practicalli team pushes changes to the default branch).

Publish book workflow installs Material for MkDocs version 9


## Local development

Install mkdocs version 9 using the Python pip package manager

```bash
pip install mkdocs-material=="9.*"
```

Install the plugins used by the Practicalli site using Pip (these are also installed in the GitHub Action workflow)

```bash
pip3 install mkdocs-material mkdocs-callouts mkdocs-glightbox mkdocs-git-revision-date-localized-plugin mkdocs-redirects pillow cairosvg
```

> pillow and cairosvg python packages are required for [Social Cards](https://squidfunk.github.io/mkdocs-material/setup/setting-up-social-cards/)

Fork the GitHub repository and clone that fork to your computer,

```bash
git clone https://github.com/<your-github-account>/<repository>.git

```

Run a local server from the root of the cloned project

```bash
mkdocs serve
```

The website will open at <http://localhost:8000>
