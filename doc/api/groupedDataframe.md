<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

### Table of Contents

-   [GroupedDataFrame][1]
    -   [toCollection][2]
    -   [show][3]
    -   [listGroups][4]
    -   [listHashs][5]
    -   [map][6]
    -   [filter][7]
    -   [chain][8]
    -   [aggregate][9]
    -   [pivot][10]
    -   [melt][11]

## GroupedDataFrame

[src/groupedDataframe.js:10-276][12]

Grouped DataFrame structure grouping DataFrame rows by column value.

**Parameters**

-   `df` **DataFrame** The DataFrame to group by.
-   `columnNames` **...any** 
-   `columnName` **[String][13]** The column used for the group by.

### toCollection

[src/groupedDataframe.js:76-78][14]

Convert GroupedDataFrame into collection (Array) of dictionnaries (Object).

**Examples**

```javascript
groupedDF.toCollection();
```

Returns **[Array][15]** An Array containing group: {groupKey, group}.

### show

[src/groupedDataframe.js:87-97][16]

Display the GroupedDataFrame as String Table.

**Parameters**

-   `quiet` **[Boolean][17]** Quiet mode. If true, it doesn't trigger console.log(). (optional, default `false`)

**Examples**

```javascript
groupedDf.show()
```

Returns **[String][13]** The GroupedDataFrame as String Table.

### listGroups

[src/groupedDataframe.js:105-107][18]

List GroupedDataFrame groups.

**Examples**

```javascript
gdf.listGroups()
```

Returns **[Array][15]** An Array containing GroupedDataFrame group names.

### listHashs

[src/groupedDataframe.js:115-117][19]

List GroupedDataFrame groups as a hashCode.

**Examples**

```javascript
gdf.listHashCodes()
```

Returns **[Array][15]** An Array containing GroupedDataFrame hash codes.

### map

[src/groupedDataframe.js:126-132][20]

Map on DataFrame groups.

**Parameters**

-   `func` **[Function][21]** The function to apply to each row of each group.

**Examples**

```javascript
groupedDF.map((row,i) => row.set('b', row.get('a')*i));
```

Returns **DataFrame** A new DataFrame containing the result.

### filter

[src/groupedDataframe.js:141-151][22]

Filter a grouped DataFrame.

**Parameters**

-   `condition` **[Function][21]** A filter function or a column/value object.

**Examples**

```javascript
groupedDF.filter((row,i) => (i === 0));
```

Returns **DataFrame** A new filtered DataFrame.

### chain

[src/groupedDataframe.js:166-172][23]

Chain maps and filters functions on DataFrame by optimizing their executions.
If a function returns boolean, it's a filter. Else it's a map.
It can be 10 - 100 x faster than standard chains of .map() and .filter().

**Parameters**

-   `funcs` **...[Function][21]** Functions to apply on the DataFrame rows taking the row as parameter.

**Examples**

```javascript
groupedDF.chain(
     (row, i) => (i === 0), // filter
     row => row.set('column1', 3),  // map
     row => row.get('column2') === '5' // filter
)
```

Returns **DataFrame** A new DataFrame with modified rows.

### aggregate

[src/groupedDataframe.js:182-190][24]

Create an aggregation from a function.

**Parameters**

-   `func` **[Function][21]** The aggregation function.
-   `columnName` **[String][13]** The column name created by the aggregation. (optional, default `'aggregation'`)

**Examples**

```javascript
groupedDF.aggregate(group => group.stat.sum('column1'));
```

Returns **DataFrame** A new DataFrame with a column 'aggregation' containing the result.

### pivot

[src/groupedDataframe.js:200-228][25]

Pivot a GroupedDataFrame.

**Parameters**

-   `columnToPivot` **[String][13]** The column which will be transposed as columns.
-   `func` **[Function][21]** The function to define each column value from a DataFrame. (optional, default `(gdf)=>gdf.count()`)

**Examples**

```javascript
df.groupBy('carType').pivot('carModel', values => values.stat.sum('kms'))
```

Returns **DataFrame** The pivot DataFrame.

### melt

[src/groupedDataframe.js:238-275][26]

Melt a DataFrame to make it tidy. It's the reverse of GroupedDataFrame.pivot().

**Parameters**

-   `variableColumnName` **[String][13]** The column name containing values. (optional, default `'value'`)
-   `valueColumnName`   (optional, default `"value"`)

**Examples**

```javascript
df.groupBy('carType').melt('kms')
```

Returns **DataFrame** The tidy DataFrame.

[1]: #groupeddataframe

[2]: #tocollection

[3]: #show

[4]: #listgroups

[5]: #listhashs

[6]: #map

[7]: #filter

[8]: #chain

[9]: #aggregate

[10]: #pivot

[11]: #melt

[12]: https://github.com/Gmousse/dataframe-js/blob/cef738e8a8e82e94515dfc49f015f842a8c410f2/src/groupedDataframe.js#L10-L276 "Source code on GitHub"

[13]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String

[14]: https://github.com/Gmousse/dataframe-js/blob/cef738e8a8e82e94515dfc49f015f842a8c410f2/src/groupedDataframe.js#L76-L78 "Source code on GitHub"

[15]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array

[16]: https://github.com/Gmousse/dataframe-js/blob/cef738e8a8e82e94515dfc49f015f842a8c410f2/src/groupedDataframe.js#L87-L97 "Source code on GitHub"

[17]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean

[18]: https://github.com/Gmousse/dataframe-js/blob/cef738e8a8e82e94515dfc49f015f842a8c410f2/src/groupedDataframe.js#L105-L107 "Source code on GitHub"

[19]: https://github.com/Gmousse/dataframe-js/blob/cef738e8a8e82e94515dfc49f015f842a8c410f2/src/groupedDataframe.js#L115-L117 "Source code on GitHub"

[20]: https://github.com/Gmousse/dataframe-js/blob/cef738e8a8e82e94515dfc49f015f842a8c410f2/src/groupedDataframe.js#L126-L132 "Source code on GitHub"

[21]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function

[22]: https://github.com/Gmousse/dataframe-js/blob/cef738e8a8e82e94515dfc49f015f842a8c410f2/src/groupedDataframe.js#L141-L151 "Source code on GitHub"

[23]: https://github.com/Gmousse/dataframe-js/blob/cef738e8a8e82e94515dfc49f015f842a8c410f2/src/groupedDataframe.js#L166-L172 "Source code on GitHub"

[24]: https://github.com/Gmousse/dataframe-js/blob/cef738e8a8e82e94515dfc49f015f842a8c410f2/src/groupedDataframe.js#L182-L190 "Source code on GitHub"

[25]: https://github.com/Gmousse/dataframe-js/blob/cef738e8a8e82e94515dfc49f015f842a8c410f2/src/groupedDataframe.js#L200-L228 "Source code on GitHub"

[26]: https://github.com/Gmousse/dataframe-js/blob/cef738e8a8e82e94515dfc49f015f842a8c410f2/src/groupedDataframe.js#L238-L275 "Source code on GitHub"
