---
title: Data description
prev: "/"
next: network-analysis
---
The first step was to collect the data. This process was a longer one, but the gain over doing it from scratch was the choice of what data to collect, and what to discard. The data acquisition was completed in the following steps:
1. Get the packages of Pypi
2. Check for and retrieve the package's Github
3. Check for and retrieve information contained in a requirements file for dependencies
4. Check for and retireve the textual information in a README file.
5. Clean the collected information and make the edge list pairs.

The data acquisition was done while running asyncronic, and was done using the library **asyncio**. Here the _seraphore_ parameter was set to 500, which limits the number of concurrent tasks. Furthermore, _aiohttp_ was used to keep a session running, when requesting to the same website multiple times.

First of a list of packages on Pypi was collected through a client server thorugh the library _xmlrpc.client_. It was a simple process of calling the packages available at the client:
```
import xmlrpc.client as xc
client = xc.ServerProxy('http://pypi.python.org/pypi')
pypi_packages = client.list_packages()
```
In total over 500 thousand package names were retrived. Using _Beautiful Soup_ requests for the package's links were sent in the form of ```https://pypi.org/project/{package}/```, as this was the structure pypi was found to follow on their website. If this didn't exist, the package was discarded. By going through the website's structure, the relevant class name needed to check if a Github link existed, was located. If it did, it was saved, and if the package didn't have a Github, the package was still kept as it still could be pointed to as a dependency. This left around 350 thousand packages to then check for requirements and text.

When retrieving the README files and requirements a realization was made that a Github is structured, so that the user's content has a seperate URL starting with **https//raw.githubusercontent.com** follwed by the repository name, branch name, and then the file name. By checking Githubs of random small and big packages manually, it was found out that all of these had branches either named **main** or **master**, and README files ending with _.md, .rst or .txt_. Therefore, it was only necessary to check if any of these URLs exists for the given package. If a file is found it is cleaned through different Regular Expressions (RegEx) to streamline all the text for later analysis.

For the requirements file the same logic was applied. This time there was just more combinations to try, as the naming of the files varied more across the different Github repositories. From the ones we looked through a total of five different naming conventions were discovered:
* requirements-dev.txt
* dev-requiremtns.txt
* environment.yml
* pyproject.toml
* requirements.txt

Depending on the found file format, different RegEx combinations were used to properly filter and clean the retrieved text into a list of the dependent package names. Additionally, if no requirements or README file was found that variable was just set as _None_, and thereby still keeping the node in the network to get as detailed a network as possible even though, it couldn't be used later for textual analysis. The final data size for the later text analysis were None values were dropped, was a total of 48,077 rows of different packages with at the start three columns of attributes. These were:
* The name of the library
* A list of the requirements or empty
* The text as one string or empty

The URLs for pypi and Github were excluded from this dataframe, as that information was irrelevant for the analysis, but was still stored in other previous files made during data acquisition. Lastly the edge list was made to contian pairs of a requirement and the package it is used by. However, it was made sure to only allow dependency between packages that are originally on pypi, as this is the source investigated. So if a package is dependent on a package that can't be found on there, the pair is excluded. This list was afterwards used to create the directed graph.