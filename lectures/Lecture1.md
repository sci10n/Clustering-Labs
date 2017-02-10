# Lecture 1

Course book: Data Mining: Concepts and Techniques (http://romisatriawahono.net/lecture/dm/book/Han%20-%20Data%20Mining%20Concepts%20and%20Techniques%203rd%20Edition%20-%202012.pdf)

Lecture, Labs and TEN1. Labs will be in pairs.

## Why data mining?

* The amount of data has grown significantly the last couple of years (from tera to petabytes)
* New ways to collect data: from databases, web-crawling, sensors etc.
	Sources:
	* Web, e-commerce, transactions, stocks
	* Remote sensing, bio informatics, simulations
	* new, digital cameras, YouTube ...
* We currently have huge amount of data and for many cases we do not know how to extract the knowledge from the data.

### Ex:
For market analysis it's very important to analyse the purchasing patterns of consumers. 

For fraud detection by outliers analysis or clustering.
	Auto insurance fraud though ring of collisions.
	Money laundering monitoring through suspicious transactions.

## Evolution of Database Technology

* Database creation started in the 1960s with IMS and networked DBMS
* During the 70s the relational models came into use (currently the largest model used in industry due to tried and true technology)
* During the 80s Advanced data models such as extended-relations, OO, deductive)
* The 90s Data mining and data warehousing started taking of together with the wwww.
* The last decade have focused on Stream data management - where you only look at a small part or only look at a data point only once, data mining, and integration of web technologies.
* During the 2010s we get distributed databases, NoSQL, NewSQL and semantic web.

## What is data mining?

* Extraction of "interesting" patterns or knowledge from huge amount of data.
	Interesting data should be: non-trivial, implicit, previously unknown and potentially useful)
* Data mining has also been called: Knowledge mining/data archeology/data dredging, pattern analysis.

## Knowledge Discovery Process

Databases --[Data Cleaning]-> Data Warehouse --[Selection and transformation]-> Task-relevant data --[Selection and transformation / Data mining] --[Pattern evaluation and presentation]-> Knowledge

In many cases the majority of time and effort is put on preprocessing of the data just to get it ready for analysis.

## Why data preprocessing

Data in the real world is dirty, 
	* Incomplete - lacking attribute values, lacking attributes, memory corruption
		* ex: occupation=""
	* Noisy - errors or outliers in the data
		* ex: salary="-10"
	* Inconsistent - containing discrepancies in codes or names, having multiple attributes that contradicts each other
		* ex: age="42" Birth date="03/07/1997", rating = {1,2,3} rating = {a,b,c}

## Why is data dirty

* Incomplete data may come from "Not applicable" values during collection, different considerations between time of collection and analysis

* Noise data may come from faulty data collection instruments, human or computer error during data entry, error in transmission

* Inconsistent data may come from integration of different data sources, functional dependency violations

* We also need to clean duplicates from the data.

## Why is Data pre-processing important?

No quality data will yield no quality results, Descriptions need to be based on quality data. Data warehouses need to be kept concise and up-to-date.

## Typical data mining system

```
+-----------+
| 	GUI		|
+-----------+
  |		|
+------------+
|Pattern eval|
+------------+
  |		|
+-------------+
| Data Mining |
+-------------+
  |		|
+-----------+
| Databases |
+-----------+
  	  |
(Cleaning and integration)
```

The reason for the arrows in both direction is that we might want to use parts of the data mining in the previous steps. Similar to a compiler

## Why not traditional data analysis?

* Huge amount of data means the algorithms need to be highly scalable.
* High dimensionality causes micro arrays that may have tens of thousands of dimensions. 
* High complexity of the data such
	* Time series data - sequential data
	* Data streams and sensor data
	* Structured data - graphs, multi-linked 
	* Heterogeneous databases and legacy systems
	* Spatial, multimedia, text and web data

## Classification Schemes

* General functionality
	* Descriptive data - can i find some common properties for my current data
	* Predictive data - can i find some rules or associations that make me be able to predict future data points

## What kind of data?

* Relational databases and warehouses that are database oriented data sets - data related to products, 

* Advanced data sets such as OR-databases, Time series, Spatial, Text, Streams, and www data
	These sets will result in more complex management, such as keeping track of object relations, everything that requires the application to manage the evolution of data over certain dimensions.

## What kind of patterns?

Concept/class descriptions:
	* Characterization: summarizing the data of the class under observation in general terms
		Characteristics of customers who spend more than a certain amount...
	* Discrimination: comparing target class with other classes, checking contrasts and outlines of different classes.
		Compare different product categories on whether they increase or decrease in sales.

Frquentits patterns, association, correlations
	* Frequent itemset
	* Frequent sequential pattern
	* Frequent structured pattern

ex:
```
buy(X,"Diapers") -> buy(X,"Beer") [support=0.5%,confidence=75%]
```
For a large majority this relation does not need to apply, what in this case is important is that we have found that given that someone buys diapers, a high confidence that they also will buy beer.

Classification and prediction

Construct models that describe and distinguish classes or concepts for future prediction
predict some unknown or missing numerical values

* Cluster analysis
* Outlier analysis
* Trend and evolution analysis


An important aspect of data mining is that it might generate thousands of patterns that may not be of interest or useful. A suggested approach is to be human centered, query based, focused on mining to help the algorithm.

A pattern is interesting if it is easily understood by humans, valid for new data points, potentially useful, novel, or validates an hypothesis we seek to confirm.

The interestingness can be evaluated either objectively by statistics and structures of pattern or subjective based on user belief in the data.

## Fina all or only interesting patterns

Heuristic vs exhaustive search
Association vs classification vs clustering
