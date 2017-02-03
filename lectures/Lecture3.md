
# Lecture 3 - Cluster Analysis cont.

## Major clustering approaches

### Partitioning approach

* Partition your set of data objects into groups with the 
	* Every data object belongs to a group.
	* There should be no overlap between the groups.
* Typical methods: k.means, k-medoids, CLARANS
* Typical Parameters: k

Construct a partition of a database D of n

```
\sum_{m=1}^{k}\sum_ {t_mi \in Km}(C_m -t_{mi})^2
```
where C is the cluster centroid and t is a data point. You want the things in the same cluster to have as a small distance as possible.

To reach global optimal requires exhaustive evaluation of possible clusters. The k-means and k-medoids algorithms are heuristic algorithms.

#### K-means

Example: 

[link to slide 32 http://www.ida.liu.se/~732A61/material/fo-cluster.pdf]

_strength_

* K-means is relatively efficient O(tkn), n = #objects, k = #clusters, t = #iterations
* You will get to a optimum but not guaranteed global optimum. This can be improved by adding deterministic annealing or genetic algorithms.

_weakness_ 

* Only applicable if mean is defined, this means that the algorithm may not work for categorical data. 
* k needs to be specified.
* unable to handle noisy data and outliers
* not suitable to discover clusters with non-convex shapes

### k-medoids (PAM, CLARA, CLARANS) THIS IS IMPORTANT FOR EXAM!!

 Example: 

[link to slide 36 http://www.ida.liu.se/~732A61/material/fo-cluster.pdf]

* Select k objects
* For each pair of non-selected objects h and selected object i we calculate the total swapping closest TC_ih
* Select a pair i and h which corresponds to the minimum swapping cost
	* if TC < 0, i is replaced by h
	* Then assign each non.selected object to the most similar representative object
* repeat step 2-3.

The cost of replacing medoid i with object h: 

```
\sum_{i=1}^{d}|x_i - i_i |
```

__strength__

PAM is more robust than k-meas to noise and outliers and works efficiently on small data sets.

__weakness__

Do not scale well for large data sets O(k(n-k(^2))

#### CLARA

From all data that you have, take a sample of size '4' and only work on the sample. Do Pam on the sample set and assign the excluded objects to the cluster which is closest.

We repeat the algorithms '5' times and check which of the '5' that are best clusters.

#### CLARANS

Searches the original graph and has an additional paramters where we specifythe number of local minimas it should find.

It takes a random start and look at the neighbors. If the neighbors are positive we go to the next neighbor. If a path is negative it will take it without evaluating the rest. 

It has a parameters MAX_NEGHBORS, if it cant find a negative neighbor it will stop after a limit.

DO this iteratively to not get bad results compared to PAM.


#### Graph abstraction

Create a graph where each node represents a way to cluster the data. k = '2', n = 4 {a,b,c,d}

Represent the different solutions we can have for clustering by giving the medoids 
{a,b}, 	{a,c},	 {a,d}, 	{b,c},	 {b,d}, 	{c,d}
connect the noes if the objects deffer es by one object.

{a,b}---{a,c}
	 ---{a,d}
	 ...{b,c}
	 ---{b,d}
...



### Hierarchal approach

* Allow clusterings to overlap i.e. big clusters may have more refined groupings inside.
* Typical methods: Diana, Agnes, BIRCH, ROCK (specific for classified data), CAMELEON
* Typical Parameters: t

#### ROCK

* Works for categorical data
* Need similarity, defined as link between data.

#### CHAMELEON

* Not completely hierarchical, leafs are allowed to be any other type of algorithms (example PAM).
* Measure the similarity based on a dynamic model.
* Two faces, first create a graph into relativity small sub clusters (k-nearest neighbor graph), secondly we find the genuine clusters by using a agglomerative hierarchal clustering algorithms.

* First we create a graph using the k-nearest neighbor graph algorithm.
* Partition the graph: cut the graph into two different pieces, cut so that we minimize the edge cut (minimize the number of links we need to cut based on similarity labels) (minimum size for the clusters, when this is reached we stop cutting)(in general each cluster should have 1-5% of the data).

* Interconnectivity - the sum similarity between connected nodes in two clusters, normalized by the value of internal edge cuts (the edge cut when dividing a cluster into two approximately equal pieces.)
* Closeness - average similarity between connected nodes in two clusters.

* Able to provide cluster with non-convex shape.

### Density-based approach

* Objects can be close to one another based on some measure of density. 
* Typical methods: DBSCAN, OptICS, DenClue
* Typical methods: \epsilon, minpoints


* Two input parameters \epsilon - maximum radius of the neighborhood, MinPts - Minimum number of points in an \epsilon neighborhood of that point.

* Directly density-reachable - a point is directly density-reachable if p belongs the neighborhood of q. + q needs to be a core-point (At least MinPts number of points in its neighborhood).
* Density-reachable - a point p is directly reachable from q if there is a chain of core-points between p and q, if the last point is not a core-point you can't go back.

* Density-connected - point p and q are density-connected if there is a point o with has both p and q being density-reachable.

We will not look at Grid-based, Model-based, Frequent pattern-based, User-guided or constraint-based approaches.

#### DBSCAN

Put all point that are density-connected into the same cluster.

* Start from a arbitrary point
* Take all density-reachable point from start
* If start is a core point we have a cluster, else not
* Continue the process until all points have been processed


#### OPTICS [visual](https://en.wikipedia.org/wiki/OPTICS_algorithm#/media/File:OPTICS.svg)

Gives a visual image of how the clusters would look like given a value of \epsilon. 

* Core distance of p wrt to MinPts - smallest distance \epsilon between p and an object in its neighborhood such that p would be a core object for \epsilon and MinPts, UNdefeind for non core-points.

* Reachability distance of p wrt o - Max(cd(o),d(o,p)) if o is core object, undefined for non core-objects.

* Select new point,
* Find neighbors
* Compute Core-distance
* Write point to ordered file and mark as processed
* if point wasn't a core object, go to start
* Put neighbors of o in Seedlist and order
	* If neighbor n is not in Seedlist add (n, reachability from 0) else reachability from 0 < current reachability, then update reachability + order Seedlist wrt reachability. (look for example [example](https://en.wikipedia.org/wiki/OPTICS_algorithm))
* Take new object from Seedlist with smallest reachability and restart at 2.

* Typically has to use optics + one dbscan

#### DENCLUE

* DENsity-based CLUstEring
* Statistical density functions 
* Major features
	* Solid Math
	* Good for noisy data sets


* Create a grid over the data
* Keep the cells with at least N data points + neighboring cells

( See slide 84 in http://www.ida.liu.se/~732A61/material/fo-cluster.pdf for mathematical representation)

* Influence function - describe the data space can be calculated as the inpact fo data points within its neighborhood.

* Overall density of the data space can be calculated as the sum of the influence function of all data points.

* Density attractors are local maxima of the overall density function (gradient). Significant density attractors are defined as a density attractor with a density over a certain value. All point attracted a a density attractor are considered as members of that cluster. 

* We are allowed to make chains of attractors if we can walk from one to another with out crossing the k-line (threshold)

#### CLIQUE

## How can we define distance between clusters?

Single link distance: Looks at all the distances from each data object in one cluster to all data objects in another and take the smallest distance


Complete link: largest distance between an element in one cluster and a element in the other.


Average link: average distance from each element in one cluster to an element in another cluster


Centroid: distance between the centroids of two clusters, centroids can be found by calculating the mean for all elements in a cluster. 

```
C_m = \sqrt{\sum_{i=1}{N}(t_{ip}-c_m)^2}
```

Medoid: the distance between the medoids of two cluster, medoid can be found by calculating the centroid for a cluster and picking the real element closest to the centroid. 

