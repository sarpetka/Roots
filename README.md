# Roots

All of the latest MATLAB files are located in the folder ROOTS/models/Rootbox_v6b/ROGER. These are the files we've been running on the ROGER computer. 

Older versions are located in ROOTS/models/Rootbox_v6b.


The "Rootbox" model and related code for the Root Systems Analyser and Parametrizer was taken from the following website:

https://www.csc.univie.ac.at/index.php?page=rootbox

Daniel Leitner's paper describing this model can be found in 

ROOTS/papers/A dynamic root system growth model based on L-Systems, Leitner-Klepsch-Bodner-Schnepf.pdf


We have modified this model to suit our project.
Major changes:
	+ Implemented various rhizotrons (cylindrical and helix-shaped) to interact with the plant models.
	+ ... (TBC - various adjustments to the defaults)

----------------------------------------------------------------

See the README folder in ROOTS/models/Rootbox_v6b/ROGER for an overview of the MATLAB files and data format.

# Data
Description of the data files (naming convention and format of the files):

Currently, the folder Trial_Data_010 contains the raw data for each of 160 runs of the file run_batch_crown_alldays.m on ROGER, as well as data for the cylindrical rhizotrons.

Trial_Data_011 contains data for the helix-shaped rhizotrons.



The raw output of run_batch_crown_alldays is organized slightly differently:

run_batch_crown_alldays.m takes as input the following:
 
	name:   what you want the files to be named. Currently, this is the job ID when the job is submitted to ROGER's queue.

	startingRootID: the ID used to randomly generate the roots.

	avoid:  whether the plants should try to avoid the rhizotrons.

	RSD: 	 relative standard deviation for the plants; the standard deviation as a percentage of the mean of each of the plant's parameters.


Then, the files are saved to ROGER/Trial Data/<name>/
into four folders:
	data:		data for volume, surface area, etc.
	points:	coordinates, radius, etc for all of the segments of the plants
	L-string:	The L-system string used to generate each plant. (Necessary if you want to produce the more detailed pictures).
	params:	The plant parameters and rhizotron parameters used in these trials.


DATA FILES:

Stored in 11 columns separated by spaces.

Each row represents a measurement for a specific plant by a specific rhizotron at a specific depth on a specific day. The first 5 columns are for identification, and the last 6 columns are the data extracted for that measurement.

Columns:
1. Root ID
2. Plant number
3. Rhizotron ID
4. Day number
5. Depth
6. Number of plant segments observed
7. Total length of all the observed plant segments
8. Total surface area of all the observed plant segments
9. Total volume of all the observed plant segments
10. Average radius of all the observed plant segments
11. Standard deviation of all of the observed plant segments.

Description:
1. The ROOT ID is what is used to seed the random number generator for the plant. This ID is unique to each plant. For the ROGER submissions, the IDs are given by 100000*(ROGER job ID) + 100*(Trial number within the job submission) + (plant number within the trial).

2. The PLANT NUMBER is used to locate where the plant is on the simulated plot. Each trial currently has 10 plants in a row (formerly 6), numbered as follows:

	1  2  3  4  5  6  7  8  9  10

where plant 1 is located at (0,0,0) and each successive plant is spaced 15cm away in the positive x direction.

3. The RHIZOTRON ID is used to determine which rhizotron the data corresponds to. Each rhizotron has a unique ID (exception: the rhizotron 'cylinder1-2' uses the same ID, 7,  for multiple angles and radii of the rhizotron). The parameters for each rhizotron ID are given in presetRhizotronParameters.m.

NOTE: We use rhizotron ID 0 to represent an 'omniscient' rhizotron, i.e. the data corresponding to rhizotron 0 is the full data.



