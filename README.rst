OpenStorageNetwork (OSN) Documentation Repository
=================================================

This GitHub repo contains the sources for the Read the Docs hosted
OSN documentation website.

Resources:
----------
* `Read the Docs website <https://readthedocs.org>`_
* `OSN documentation website <https://openstoragenetwork.readthedocs.io/>`_
* `Docutil's authoritative reStructuredText reference <https://docutils.sourceforge.io/rst.html>`_
* `Sphinx's RST Primer <https://www.sphinx-doc.org/en/master/usage/restructuredtext/basics.html>`_
* `Sphinx's RST Cheatsheet <https://sphinx-tutorial.readthedocs.io/cheatsheet/>`_
* `Alternative RST Cheatsheet <https://github.com/ralsina/rst-cheatsheet/blob/master/rst-cheatsheet.rst>`_

Installing the Sphinx and RTD toolchain:
----------------------------------------

Sphinx and the RTD Sphinx theme can be installed using pip, conda, or brew (for Mac users).
In this example, we will use conda and assume miniconda is installed.

#. Clone the RTD-OSN git repo

	$ git clone git@github.com:OpenStorageNetwork/rtd-osn.git

#. Use the conda-generated environment.yml file to create your environment

	$ cd rtd-osn
        
	$ conda env create -f environment.yml

#. Whenever you need to build RTD-hosted documentation, first load the rtd environment

	$ conda activate rtd


**Note:** If you already have a conda environment named "rtd" or prefer a different name, use the -n option

	$ conda env create -n myname -f environment.yml

Previewing Changes Before Commiting
-----------------------------------

After you've made local changes to the documentation, please build and view before
checking in changes or submitting a PR.

* Change paths to the top level of the documentation 

	$ cd /path/to/git/rtd-osn/docs

* Build the documentation

	$ make html

* View the documentation in $PWD/build/docs/index.html

	$ open build/html/index.html  # works on a mac; use xdg-open on linux





