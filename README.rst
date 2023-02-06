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







