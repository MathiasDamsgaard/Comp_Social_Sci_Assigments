---
title: Home Page
layout: single
next: data-description
---

This project works to investigate a network constructed of _python packages' dependencies_ on each other. This is based on the available packages on [python package index (pypi)](https://pypi.org/). Inspiration of this project idea comes from seeing an older dataset on [Netzschleuder](https://networks.skewed.de/net/python_dependency) made by Kevin Gullikson. His [original blogpost](https://kgullikson88.github.io/blog/pypi-analysis.html) is from 2016, and will therefore be used as a baseline for comparing the networks on a timescale.
<img src="/images/pypi.svg" width="200">

The resulting network will be analysed based on theory for a directed network, where a package point to another package if the first package is a requirement for the second one. This information was collected from the individual packages githubs. Further information on the data acquisition can be found in the data tab.

## [Explainer Notebook](explainer-notebook.html)
Above is a webbased visual representation of the notebook containing all the relevant code along with clarifications and explanations on the workflow and decisions taken.