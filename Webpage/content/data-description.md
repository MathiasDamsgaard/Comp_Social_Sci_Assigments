---
title: Data description
prev: "/"
next: network-analysis
---

The data acquisition was completed in the following steps:
1. Get the packages of Pypi
2. Check for and retrieve the package's Github
3. Check for and retrieve information contained in a requirements file for dependencies
4. Check for and retireve the textual information in a README file.
5. Clean the collected information and make the edge list pairs.

First of a list of packages on Pypi was collected through a client server thorugh the library _xmlrpc.client_. It was a simple process of calling the packages available at the client:
```
import xmlrpc.client as xc
client = xc.ServerProxy('http://pypi.python.org/pypi')
pypi_packages = client.list_packages()
```
We then retrieved a total of over 500 thousand package names. Using _Beautiful Soup_ we requested for the package link in the form of ```https://pypi.org/project/{package}/```, as this was the structure we could find most to every package had on their website. If this didn't exist, we discarded that package. By going through the website's structure we found the class name we needed to search for to then check if a Github link existed. If it did, we saved it, and if the package didn't have a Github, we again discarded the package as then then would have no way of connecting it to the network. This left us with over 300 thousand packages to then check for requirements and text.

When retrieving the README files and requirements, we realized that a Github is structured so that the user's content has a seperate URL starting with **https//raw.githubusercontent.com** follwed by the repository name, branch name, and then the file name. By checking Githubs of random small and big packages we found out that all of these had branches either named **main** or **master**, and README files ending with _.md, .rst or .txt_. Therefore, we just checked in any of these URLs exists for the given package. If a file is found it is cleaned through different Regular Expressions (RegEx) to streamline all the text for later analysis.

For the requirements file the same logic was applied. This time there was just more combinations to try, as the naming of the files varied more across the different Github repositories. From the ones we looked through a total of five different naming conventions were discovered:
* requirements-dev.txt
* dev-requiremtns.txt
* environment.yml
* pyproject.toml
* requirements.txt
Depending on the found file format, different RegEx combinations were used to properly filter and clean the retrieved text into a list of the dependent package names.

If no requirements file was found, the package was discarded, as it wouldn't be possible to connect it to the network. However, if it as only the README file, we weren't able to find or didn't exist, we still kept the node in the network to get as detailed a network as possible even though, it couldn't be used later for textual analysis.

Lastly we made the edge list contianing pairs of a requirement and the package it is used by. However, we make sure to only allow dependency between packages that are in the network. So if a package is dependent on a package that we couldn't find information on, we don't include that pair, as we would have no way of properly accessing the second package' actual value in the network without it's requirements file.