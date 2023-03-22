Tutorials
=========

These exercises are to demonstrate common workflows using OSN. You may use your Mac or Linux
machine to complete these exerciese or use the binder-based Linux desktop linked below.



.. image:: https://mybinder.org/badge_logo.svg
 :target: https://mybinder.org/v2/gh/mghpcsim/osn-desktop.git/HEAD

The above binder is based on Ubuntu 18.04 LTS and XFCE. 

Exercise 1
----------

To use your own machine for this exercise, you will need git, wget, and gnuplot.


Pull down the workflow from GitHub: 
""""""""""""""""""""""""""""""""""
::

	$ git clone https://github.com/mghpcsim/osn-tutorial.git

.. note::

   If you are using the above binder, the Git repo has already been cloned

Change directories to the exercise directory:
""""""""""""""""""""""""""""""""""""""""""""

::

	$ cd osn-tutorial/exercise1


Workflow step 0, download data from OSN:
"""""""""""""""""""""""""""""""""""""""

::

	#!/bin/bash

	CMD="wget https://mghp.osn.xsede.org/cis220170-bucket01/anscombe.txt"
	echo ""
	echo running $CMD
	echo ""
	
	$CMD >& /dev/null
	
	ret=$?
	if [ $ret -ne 0 ]; then
        	echo "wget failed ... HALP "
		echo ""
	else
        	echo "Data retrieved successfully"
		echo ""
	fi

Execute the download data script: 

::

	$ ./00-download-data.sh 
	
	running wget https://mghp.osn.xsede.org/cis220170-bucket01/anscombe.txt
	
	Data retrieved successfully


Workflow step 1, process the data:
""""""""""""""""""""""""""""""""""

::

	#!/bin/bash
	
	echo "running gnuplot using the anscombe.gnu script"
	echo " $ gnuplot < anscombe.gnu"
	
	gnuplot < anscombe.gnu
	echo ""
	ret=$?
	if [ $ret -ne 0 ]; then
        	echo "Data processing failed ... HALP "
        	echo ""
	else
        	echo "Data processed successfully"
        	echo ""
	fi
	     

Run the process data script:

::

	$ ./01-process-data.sh 
	running gnuplot using the anscombe.gnu script
 	$ gnuplot < anscombe.gnu

	Data processed successfully


Workflow step 2, visualize the results:
""""""""""""""""""""""""""""""""""""""

::

	#!/bin/bash
	
	unameOut="$(uname -s)"
	case "${unameOut}" in
    	Linux*)     machine=Linux;;
    	Darwin*)    machine=Mac;;
    	CYGWIN*)    machine=Cygwin;;
    	MINGW*)     machine=MinGw;;
    	*)          machine="UNKNOWN:${unameOut}"
	esac
	#echo ${machine}
	
	if [ $machine == Mac ]; then
    	  open *.png
	elif [ $machine == Linux ]; then
  	  ristretto anscombe1.png
	else
  	  echo "I dont know you"
	fi

Finally, visualize the data:

::

	$ ./02-viz-data.sh




Exercise 2
----------
