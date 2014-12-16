Sorting and Paging
==================

Many of the calls within the Carvoyant API return sets of data.  In some cases, very large sets of data.  For a number of reasons, it would not be feasible return the entire data set at once (we have some vehicles with over 100,000 data points after only 4-5 months of being on our system).  In order to address this, we have standardized the mechanism to sort and page results.  Any API call that supports sorting or pagination will do so as described here.

Sorting
-------

In most cases, the objects being listed will sort based on a timesamp.  It might be the time that the trip was started or the time a data point was collected.  The documentation for the individual API call will indicate how the results are sorted.  In order to control the sort order of that field, you can include the following field in your query string:

``sortOrder=asc`` will return the results in ascending order

``sortOrder=desc`` will return the results in descending order

Paging
------

Paging is the mechanism by which the number of results returned are limited and the ability to retrieve the "next" set of data in the list.  There are two pieces of data important in specifying a paging mechanism.  The size of the data set returned and the starting point in the full data set where the returned results will begin.

``searchLimit=<x>`` will specify how many results are included in the response

``searchOffset=<y>`` will specify the offset from the beginning of the data set that is returned

Generally, you will not need to figure out the values for the paging links manually.  They will be specified in the actions array of the return as "next" and "previous".
