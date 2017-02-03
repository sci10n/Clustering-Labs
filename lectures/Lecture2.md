## Cluster Analysis

## What is cluster analysis?

* Cluster: a collection of data objects either similar with each other od dissimilar with object outside the cluster. Similarity is defined as the distance meassure.
* Cluster analysis: Finding similarities between data according to the characteristics found in the data and group the data based on these characteristics.
* Typical applications involves 'stand-alone tool' to get insight into data distributions or as 'preprocessing step' as help for other algorithms.

## Requirements of Clustering Data

* Our algorithms need to be scalable
* Ability to work with different types (kinds) of attributes (numerical, boolean, strings,...)
* Find clusters with arbirtrary shapes.
	* Convex shapes
	* Concave shapes
* We want as few parameters as possible for clustering
	* Partitional algorithms - fixed number of clusters
	* Hierachial algorithms - meassure based thershold
	* Density algorithms - density estimateion 
* Insenitive to the order of input records - The order of inputs shouldn't affect the result.
* High diemsionality - possibly objects with 100k features
* Incoporation of user-specified contraints 
* Ability for interperability and usability

## Types of data structures

* Data matrix (classic data set)
	* n objects, p attributes
	* every row represnets an objects

* Dissimilarity matrix ( distnace messures for each data point. Adacency matrix with distances as edges)
	* Distance table
		* Messure is symetric and therefore only values under the diagonal needs to be calculated


## Interval-valued variables

```
D = {1,2,6}
Avrg = (1+2+6) / 3 = 3
Devi = (2 + 1 + 3) / 3 = 2

Z-score_1 = (1 - Avrg) / Devi = -1
Z-score_2 = (2 - Avrg) / Devi = -0.5
Z-score_6 = (6 - Avrg) / Devi = 1.5
```

Z-score will be preprocessed before all exmples

## Distance between objects

```
d(i,j) >= 0
d(i,i) = 0
d(i,j) = d(j,i)
d(i,j) <= d(i,k) + d(k,j)
```

* Transporter distance

d(i,i) = 0
d(i,j) = 1 if i != j

* Euclidean distance
* Manhattan distance
* Minkowski distance - uses a q where q=1 -> manhattan distance, q=2 -> euclidean distance, It's very rare to use anything greater than 2. If q is less than 1 the triangle inequality doesn't work any more. 

## Binary variables
 
 * Symetric binary variables: both states are equally important
 * assymetric binary variables: one state is more important thannthe other.

 ### Contingency table

```
 +---+---+---+---+
 |   |1	 |2  |sum|
 +---+---+---+---+
 |1	 |a   b   
 +---+
 |2  |c   d
 +---+
 |sum| ...
 +---+
```

* Symetric - d(i,j) = (b+c) / (a+b+c+d)
* Assymetric - d(i,j) = (b+c)/(a+b+c)

Similarity = 1 - d(i,j), = a/(a+b+c)

## Nominal or categorical variables

* Simple mathcing, m = #matches, p= total # of variables
	d(i,j) = (p-m)/p
* Dummy coding: use a large number of binary varaibles, creating a new binary variable fo each of the M nominal states. !Assymetric!


## Ordinal Variables

* Can be discrete or continuous
* Order(nal) is imortant e.g. rank

```
 replace each data with its rank, r \in{1,...,M}
 z = (r-1)/M-1)
```
Then just use metrics such as euclidean.


## Ratio-Sclaed Variables
- A positive measurement on a nonlinear sclae, approximatley at exponential scale such as Ae^Bt

* Treat them like interval-scaled varaibles (not a good idea since the scale might be distorted)
* apply logratihmic tranformation y = log(x)
* treat them as continuous ordinal data, treat their rank as interval-scaled

## Mixed types

* Use a weighted formula to combine data of different types
	* Calculate the averages for all the attributes based on a delta value (weight) for each attributes. Missing values are treated as delta = 0. We also do this if there is a binary assymetric attribute with the 0-0 case.

## VEctor Objects

* Similarity(d,q) = (d * q) / (|d| x |q|), cosin similarity
	- The smaller the angle between two vectors, the closer thay are. 