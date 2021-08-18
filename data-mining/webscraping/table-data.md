# Webscraping HTML table data

Data is often published using HTML tables, as its a very simple language that non-developers can easily pick up.



## Data in a pre tag
Using pre to create a table in a web page is similar to using a CSV except whitespace is used instead of commas to demarcated the individual elements.

Data can be put into a vector, optionally grouping each line as a vector within a vector using ``partition`.

If data should be associated with a name, then use the `map` function to convert the


#### Example data
Tables without headings
* [Riverflow reconstructions for England and Wales](https://crudata.uea.ac.uk/cru/data/riverflow/) - University of Eas Anglia Climactic Research Unit

Tables with headings and comments
* [Cloud Cover by Country](https://crudata.uea.ac.uk/cru/data/hrg/cru_ts_4.01/crucy.1709191757.v4.01/countries/cld/) - University of Eas Anglia Climactic Research Unit
