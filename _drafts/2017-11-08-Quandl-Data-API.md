---
layout: post
title: Using Quandl Data and API
---

## Using Quandl for Financial and Economic Data

[Quandl](https://www.quandl.com/) is a repository of data for investment professionals, and they have a stunning 20 million datasets from more than 500 sources. Their API is free to use unless you want access to premium datasets. They provide extensive [documentation](https://docs.quandl.com/) for their API and how to use different languages to access their data. There are many ways to access Quandl data, including in the browser and using an Excel extension, but in this post I'm going to cover the basics of accessing Quandl data using their API and the Quandl Python module.

It's pretty simple to install the Quandl library for Python from the command line with:

```
pip install quandl
import quandl
``` 

or 

```
pip3 install quandl
import quandl
```

### API Key
The next order of business is to [sign up for a Quandl account](https://www.quandl.com/users/login) and set an API key. You can set the key in Jupyter notebooks like this:

```
quandl.ApiConfig.api_key = "YOURAPIKEY"
```

### Finding Your Data
For a full (searchable) list of data products Quandl offers, you can check [here](https://www.quandl.com/search?query=), but the [Data Organization page](https://docs.quandl.com/docs/data-organization) provides a bit clearer look at the available tables. You'll need to locate the Quandl code for the dataset you wish to retrieve via the API. For example, the currency exchange rate time series for the USA and Japan has a Quandl code of [CUR/JPY](https://www.quandl.com/data/CUR/JPY). 

### Retrieving Data
You can download an entire time series data set using `quandl.bulkdownload("CUR/JPY")`, but it's typically more useful to use Quandl's _get_table_ method to retrieve the table of your choice: `data = quandl.get_table('CUR/JPY', paginate=True)` or `data = quandl.get("CUR/JPY", authtoken="YOURAPIKEY")` if you haven't previously set an API key. If you want to return a Numpy array, you can specify that using the _returns_ argument: `data = quandl.get("CUR/JPY", returns="numpy")`. 

Many tables are too large to download as a whole and will require you to narrow the request using one or more filters. Keep in mind that not all columns are filterable. The table's documentation page will indicate whether a column can be used for filtering. 

### Filtering the Data
You can filter data by filtering on one or more columns, but first check in the table's documentation page to make sure a particular column can be used as a filter criteria. 

```
https://www.quandl.com/api/v3/datatables/{datatable_code}/metadata.{format}
```

there are also methods for parsing data prior to retrieval. You can specify a date range using the _start_date_ and _end_date_ arguments: `mydata = quandl.get("CUR/JPY", start_date="2016-06-15", end_date="2016-06-30")`. Here is what the requested data looks like:

```
                  RATE
DATE                  
2016-06-15  105.941000
2016-06-16  104.663100
2016-06-17  104.300001
2016-06-18  104.205800
2016-06-19  104.168200
2016-06-20  104.235501
2016-06-21  104.573700
2016-06-22  104.468400
2016-06-23  105.532701
2016-06-24  102.837901
2016-06-25  102.403899
2016-06-26  102.243799
2016-06-27  101.893199
2016-06-28  102.524101
2016-06-29  102.646501
2016-06-30  102.712900
```

You can even request a certain number of rows with the optional _rows_ argument: `data = quandl.get("CUR/JPY", rows=5)`. Quandl additionally provides a _returns_ argument that returns a Numpy array: `data = quandl.get("CUR/JPY", returns="numpy")`. Quandl allows you to perform some basic calculations on the data, like so: `data = quandl.get("FRED/GDP", transformation="rdiff")`.

### HTTP Request with cURL
It's also possible to create a command line curl request from within a Jupyter notebook using the exclamation mark:

```
!curl "https://www.quandl.com/api/v3/datasets/FRED/GDP.csv?collapse=annual&rows=6&order=asc&column_index=1&api_key=YOURAPIKEY"
```

You can create a metadata request for a data table in a similar manner:

```
!curl "https://www.quandl.com/api/v3/datatables/AR/MWCS/metadata.json?api_key=YOURAPIKEY"
```
In order to use a shell command like this, simply concatenate (1) the requested data set URL, (2) the number of rows, (3) the sorting order, (4) the column index, and (5) the user's API key. You can find more details on the elements of this call [here](https://docs.quandl.com/docs/quick-start-examples-1). Not all of these parameters are required. A more detailed explanation of the [composition of a call](https://docs.quandl.com/docs/quick-start-examples-9) is provided on the Quandl website:

<table>
<thead>
<tr>
<th>URL COMPONENT</th>
<th>EXPLANATION</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>https://www.quandl.com/api/v3/datatables/MER/F1.xml</code></td>
<td>This portion of the call queries the MER/F1 table and returns the data in XML format.</td>
</tr>
<tr>
<td><code>mapcode=-5370</code></td>
<td>This filter removes everything except for where the mapcode = -5370 (this is the identifier used by Mergent for revenue per share)</td>
</tr>
<tr>
<td><code>compnumber=39102</code></td>
<td>This filter removes everything except for the rows where compnumber=39102 (39102 = Nokia).</td>
</tr>
<tr>
<td><code>reporttype=A</code></td>
<td>This filter removes everything except for the rows showing records for the &quot;annual&quot; report type  (A = annual).</td>
</tr>
<tr>
<td><code>qopts.columns=reportdate,amount</code></td>
<td>This argument filters the data based on the “report date” and &quot;amount&quot; columns.</td>
</tr>
<tr>
<td><code>api_key=&lt;YOURAPIKEY&gt;</code></td>
<td>This part of the call authenticates you as a Quandl user. Replace the placeholder text <code>&lt;YOURAPIKEY&gt;</code> with your personal API Key.</td>
</tr>
</tbody>
</table>

### Useful Links
Full list of [time series parameters and table transformations](https://docs.quandl.com/docs/parameters-2)
