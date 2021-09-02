### Complex Query
```
index=airbnb 
| where Price > 100 and Beds > 2 
| sort Beds desc 
| stats avg(Beds) as AvgBed, max(Price), min(Price), count  by Neighbourhood 
| sort AvgBed desc
```

### Search
```
index=airbnb 
| search Pretty
```
This will search for the term Pretty in the raw text of the event

### Fields
```
index=airbnb 
| fields + Beds,Price
```
This will remove all the fields other than Beds and Price to make it more narrow. Equivalent to the Select list of SQL


### Dedup
```
index=airbnb 
| dedup Neighbourhood
```
This one returned events with unique Neighborhoods . Dont know what criteria it used to search the event for each neighborhood

### Rename
```
index=airbnb 
| rename Beds as BHK, Price as Rent
```
This functioned like As in the select list of a SQL

### Where
```
index=airbnb 
| tail 100
| where Beds > 2 and  Price < 100
```
Just like a SQL were clause. Not necessary it seems. Its like the default operator. But if you pipe the commands as shown and need further filtering then would be useful

### Head
```
index=airbnb 
| sort Price desc
| head 20
```
Performs like top in SQL query

### Tail
```
index=airbnb 
| sort Price desc
| tail 20
```
Its opposite of top, like brings last 20 recs

### Reverse
```
index=airbnb 
| sort Price desc
| head 20 
| reverse
```
Reverses the order. Just like Array.Reverse

### Table
```
index=airbnb 
| sort Price desc
| head 20 
| reverse 
| table Beds, Price
```
Printed a nice table with the fields specified. This can be maually done too.

### Top
```
index=airbnb 
| top limit=10 Price
```
Printed top unique values of price. This is equivalent to `Select top 10 distinct Price from table order by Price desc`

### Rare
```
index=airbnb 
| rare limit=10 Price
```
Printed less frequently occuring unique values of price. Opposite of top

### Contingency
```
index=airbnb 
| contingency Neighbourhood "Property Type"
```
This actually printed a table in statistics tab with columns as Property Types and Rows as Neighbourhoods and the intersecting cells as the count of each intersection

|Neighbourhood|Apartments|Boat|
|Brooklyn|1000|200|
|Manhattan|1001|20|


### stats commands
```
index=airbnb 
| stats avg(Beds), avg(Price) by Neighbourhood
```
This printed a table equivalent to ` Select Neighbourhood, AVG(Beds), AVG(Price) from table Group by Neighbourhood`
The following operators also works the same way.  
`sum`, `count`, `min`, `max`

### Chart commands
```
index=airbnb 
| chart avg(Beds) by Neighbourhood
```
Printed a line chart with Neighbourhood on x-axis and Avg of beds on y-axis  
Can be substituted with `timechart` to plot against time stamp on x axis

### To Do
look ups


