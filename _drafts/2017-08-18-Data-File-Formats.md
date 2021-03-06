---
layout: post
title: Basic Guide to Data File Formats
---

Something that I've noticed can be confusing - particularly for beginners like me - are the various acronyms for data formats and what they're used for. In this post I'll provide a quick introduction to some common file formats that you'll encounter in data science. Plain text files like CSVs are probably the most common type you'll see in data science projects. We'll take a look at the following [Sacramento crime records](http://samplecsvs.s3.amazonaws.com/SacramentocrimeJanuary2006.csv) table in several different file formats to see how the same data can be stored differently: 

<table>
<thead>
<tr>
<th>cdatetime</th>
<th>address</th>
<th>district</th>
<th>beat</th>
<th>grid</th>
<th>crimedescr</th>
<th>ucr_ncic_code</th>
<th>latitude</th>
<th>longitude</th>
</thead>
<tbody>
  <tr>
    <td>1/1/06 0:00</td>
    <td>3108 OCCIDENTAL DR</td> 
    <td>3</td>
    <td>3C</td>
    <td>1115</td> 
    <td>10851(A)VC TAKE VEH W/O OWNER</td>
    <td>2404</td>
    <td>38.55042047</td> 
    <td>-121.3914158</td>
  </tr>
    <tr>
    <td>1/1/06 0:00</td>
    <td>2082 EXPEDITION WAY</td> 
    <td>5</td>
    <td>5A</td>
    <td>1512</td> 
    <td>459 PC BURGLARY RESIDENCE</td>
    <td>2204</td>
    <td>38.47350069</td> 
    <td>-121.4901858</td>
  </tr>
    <tr>
    <td>1/1/06 0:00</td>
    <td>4 PALEN CT</td> 
    <td>2</td>
    <td>2A</td>
    <td>212</td> 
    <td>10851(A)VC TAKE VEH W/O OWNER</td>
    <td>2404</td>
    <td>38.65784584</td> 
    <td>-121.4621009</td>
  </tr>
</tbody>


[CSV](https://en.wikipedia.org/wiki/Comma-separated_values), Comma-Separated Values, files contain ASCII text in tabular format, with different fields separated by commas:
```
cdatetime,address,district,beat,grid,crimedescr,ucr_ncic_code,latitude,longitude
1/1/06 0:00,3108 OCCIDENTAL DR,3,3C,1115,10851(A)VC TAKE VEH W/O OWNER,2404,38.55042047,-121.3914158
1/1/06 0:00,2082 EXPEDITION WAY,5,5A,1512,459 PC BURGLARY RESIDENCE,2204,38.47350069,-121.4901858
1/1/06 0:00,4 PALEN CT,2,2A,212,10851(A)VC TAKE VEH W/O OWNER,2404,38.65784584,-121.4621009
```

[RDF](https://www.w3.org/RDF/)

```

```

[JSON](https://en.wikipedia.org/wiki/JSON), JavaScript Object Notation, files are constructed using JavaScript objects to hold various data types:
```
[{"cdatetime":"1/1/06 0:00","address":"3108 OCCIDENTAL DR","district":3,"beat":"3C","grid":1115,"crimedescr":"10851(A)VC TAKE VEH W/O OWNER","ucr_ncic_code":2404,"latitude":38.55042047,"longitude":-121.3914158},
{"cdatetime":"1/1/06 0:00","address":"2082 EXPEDITION WAY","district":5,"beat":"5A","grid":1512,"crimedescr":"459 PC BURGLARY RESIDENCE","ucr_ncic_code":2404,"latitude":38.47350069,"longitude":-121.4901858},
{"cdatetime":"1/1/06 0:00","address":"4 PALEN CT","district":2,"beat":"2A","grid":212,"crimedescr":"10851(A)VC TAKE VEH W/O OWNER","ucr_ncic_code":2404,"latitude":38.65784584,"longitude":-121.4621009}]
```
[XML](https://en.wikipedia.org/wiki/XML)

HTML

Database Files

Other Formats:
Geospatial Data
Language-specific formats such as SAS and SPSS

http://opendatahandbook.org/guide/en/appendices/file-formats/
