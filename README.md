# OscillationsData
In this folder you can find all the raw data from experiments and simulation. The main code is a Jupyter Notebook called oscilationsdata.ipynb

To run the full script you need to hav installed the following libraries:

## Language
python version 3.8.1

## Libraries
PyEcoLib uses as libraries:
* [Numpy](https://numpy.org/)
* [scipy](https://www.scipy.org/)
* [math](https://docs.python.org/3/library/math.html) 
* [Pandas](https://pandas.pydata.org/)
* [PyEcoLib](https://github.com/SystemsBiologyUniandes/PyEcoLib/wiki) Used to perform the simulations

 To download the PyEcoLib library you can put the command in your terminal (linux, mac)
 `python3 -m pip3 install PyEcoLib` or in your CMD (windows) with the command
 `pip install PyEcoLib`

## Experimental data
The Raw data obtained from image analysis can be found in the following files
* "awDataAdder.cvs": Corresponds to the size along the time for 3 replicas of MG1655 k12 E. coli bacteria strains growing in M9+Glucose

* "rawdata.cvs": Corresponds to the size along the time for 3 replicas of MG1655 k12 E. coli bacteria strains growing in M9+Glycerol

The data are presented in a format similar to this:

|mom	|area	|length|	width|	time|	Replica|
|-----|-----|-----|-----|-----|-----|
|0|	138|	30.6314116|	5.99385046|	0|	Rep1|
|0|	95|	21.46076479	|5.742836657|	20|	Rep1|
|0|	113|	25.25888493|	5.90558047|	40|	Rep1|

Where "mom" corresponds to the cell index. "area", "length" and "width" corresponds to the bacteria dimensions in that time instant. "time corresponds to the global time measured in minutes. "Replica" tells you in which experimental replica does the cell was measured.  Data with the same "mom" and same "Replica" values correspond to the same cell tracked along the time.

## Division strategy 

The script performs a data analysis producing the following data:

* "DSMdataAdder.csv": Corresponds to the information of all the cell cycles found in the trajectories satisfying the condition of having a Coefficient of determination (R2) higher to 0.9 in an exponential fitting.
* "DSMdataSizer.csv": The same for glycerol bacteria and with R2>0.8.

The data look like this:

|Sb	|Sd	|Added|	gr	|timediv|	timecycle|	score|	Replica|
|-----|-----|-----|-----|-----|-----|-----|-----|
|0.663593754|	1.843657099	|0.663593754	|0.817469029	|2.125	|1.09000759|	0.906011131	|1|
|0.924324795	|1.902916278	|0.924324795|	0.722079352	|3.25	|0.872006072	|0.993083882	|1|
|0.936685051	|2.543434852	|0.936685051	|0.665949099|	4.5	|1.308009108	|0.996426304	|1|
|1.343023667	|2.09071082	|1.343023667	|0.590107431	|5.625	|0.654004554	|0.99922354	|1|

where "Sb" is the size at the begining of the cycle, "Sd" is the size at division and "Added" is the added size, "gr" is the best fitted growth rate for that cycle, "timediv" is the ime respect to the global cronometer where the cell cycle occurred. "timecycle" is the time spend in that cycle. "Score" is the R2 correspond to that cycle and "Replica" is the experimental replica.

These data can be used to study the division strategy.

## Size along the time for the best cycles

The size data along the time are filtered only taking bacteria with three or more cycles with good fitting ( Coefficient of determination >0.9 to exponential growth). The resulting data are presented in the followeing files:

* "./CRMdataAdder.csv": The size along the time for the filtered cells growing in media with Glucose.
* "./CRMdataSizer.csv" :The size along the time for the filtered cells growing in media with Glycerol.
The data look like this:

|Mother|	time	|SizeFit|	Size	|gr|	score|	Replica|
|-----|-----|-----|-----|-----|-----|-----|
|0	|0|	0.677178323|	0.491098885|	0.667124072|	0.910636294|	1|
|0|	0.25|	0.800083149|	0.802907644	|0.667124072|	0.910636294|	1|
|0|	0.5|	0.945294649	|0.930426169|	0.667124072	|0.910636294|	1|

where, again, we present, the cell index ("Mother"), the global time ("time") in hours, The size fitted to an exponential funtion ("SizeFit"), the actual size measured ("Size"), the growth rate of that cell cycle ("gr"), the Coefficient of determination of that cycle ("score") and the experimental Replica ("Replica")

## Size along the time synchronized from the first division

The script also selects the size dynamics from the first division event for all the filtered cells. The data produced are:

* "CRMdataAddersyn.csv": The size along the time measured from the first division event for the filtered cells growing in media with Glucose.
* "CRMdataSizersyn.csv": The size along the time measured from the first division event for the filtered cells growing in media with Glycerol.

The data look like this:

|Mother|	time	|SizeFit|	Size	|gr|	score|	Replica|
|-----|-----|-----|-----|-----|-----|-----|
|0	|0|	0.677178323|	0.491098885|	0.667124072|	0.910636294|	1|
|0|	0.25|	0.800083149|	0.802907644	|0.667124072|	0.910636294|	1|
|0|	0.5|	0.945294649	|0.930426169|	0.667124072	|0.910636294|	1|

where, again, we present, the cell index ("Mother"), the global time ("time") in hours, The size fitted to an exponential funtion ("SizeFit"), the actual size measured ("Size"), the growth rate of that cell cycle ("gr"), the Coefficient of determination of that cycle ("score") and the experimental Replica ("Replica").

## Simulated Data

To compare the teory with experiments, the script also performs the simulations from the theory presented in the experiment. Some files containing data presented in the main research are:

* "dataCRM1.csv"

where the size along the time for a given number of simulated bacteria is presented (5000 cell in ouur case). The data look like:

|time|	Cell1|	Cell2|	Cell3|	Cell4|
|-----|-----|-----|-----|-----|
|0	|1|	1|	1|	1|
|1.8|	1.0717|	1.0717|	1.0717	|1.0717|
|3.6|	1.1486|	1.1486|	1.1486	|1.1486|
|5.4|	1.2311|	1.2311|	1.2311	|1.2311|

These data are used by the script to generate the trayectories of mean size and their fluctiuations.

* "dataFSP6.csv"

Where we present the central moments of the size distribution obtaining using the numeric solution of the master equation. The data look like this:

|time|	Meansize|	VarSize|
|-----|-----|-----|
|0|	0.998541205|	0.00986784|
|0.18|	1.005486608|	0.01000559|
|0.36|	1.01248032|	0.010145263|
|0.54|	1.019522678|	0.010286885|

where "time" is the time, "Meansize" is the mean of the size distribution at that time, "VarSize" is the Variance of the distribution at that time.

These data was obtained using the [PyEcoLib](https://github.com/SystemsBiologyUniandes/PyEcoLib/wiki) simulation library.



