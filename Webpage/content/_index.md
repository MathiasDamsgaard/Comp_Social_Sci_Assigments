---
title: Home Page
layout: single
next: data-description
---
This project works to investigate a network constructed of _python packages' dependencies_ on each other. This is based on the available packages on [python package index (pypi)](https://pypi.org/). Inspiration of this project idea comes from seeing an older dataset on [Netzschleuder](https://networks.skewed.de/net/python_dependency) made by Kevin Gullikson. His [original blogpost](https://kgullikson88.github.io/blog/pypi-analysis.html) is from 2016, and will therefore be used as a baseline for comparing the networks on a timescale.
<img src="/images/pypi.svg" width="200">

The resulting network will be analysed based on theory for a directed network, where a package point to another package if the first package is dependent on the second one. This information was collected from the individual packages githubs. Further information on the data acquisition can be found in the data tab.

This research was conducted for investigating how the package library in Python has evolved over the years and further investigate which packages seem to be the hubs of all other packages. Creating libraries is a big part of programming to help make functions easier to use across files and users, and thus the goal with this website is to shine light on the insights gained when looking at the connections between the libraries and the groups these create.
By also analysing the text available in README files, understand of how programmers formulate themselves when writing documentation for their code, and the variation across different groups can be visualized. This is the main points of the research on this website, and the authors hope you find the reading enjoyable.

Here is a link to a webbased visual representation of the [notebook](explainer-notebook.html), which contain all the relevant code along with clarifications and explanations on the workflow and decisions taken.

In the end the research showed ...