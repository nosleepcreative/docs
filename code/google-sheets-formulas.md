# Google Sheets Formulas

## Recommended Readings

| **Item**                      | Links                                                                                                                                                                                                                                                                                                    |
| ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Documentation / Tutorials** | <ul><li><a href="https://www.ablebits.com/office-addins-blog/2019/04/30/google-sheets-compare-two-sheets-columns/">Comparing two columns </a></li><li><a href="https://infoinspired.com/google-docs/spreadsheet/use-trim-function-split-google-sheets/">Trim &#x26; Split functions</a></li></ul><p></p> |

## Counting

```java
// where $A:$A is your desiredrange

// if cell contains specific word
= countif($A:$A,"*_ALT*") // cannot be done with an arrayformula

// errors
=countif($A:$A,ISERROR())

// loading https://www.reddit.com/r/googlesheets/comments/aplwa6/importxml_loading/
=COUNTIF(ARRAYFORMULA(ISERR(A1:A1000)),true)
=TEXT(COUNTIF(ARRAYFORMULA(ISERR(A1:A1000)),false)/1000,"0%")

// whitespace
=COUNTA(SPLIT(A1, " "))

// count containing based on cell
=countif(A:A,"*"&A2&"*")
```

## Misc

```java
// if blank, no formula
= ARRAYFORMULA(IF(ISBLANK(A2:A),"",V2) 

// join header row & other row by each cell with delimiter (2rows)
= ARRAYFORMULA($B$1:$K$1&" — "&B2:K2))

// split by line break, transpose vertically, sort, flatten by 
= arrayformula(textjoin(char(10),1,sort(transpose(split(O2,char(10))))))
```

## REGEX

```java
// exclude first word
REGEXEXTRACT(trim(A2:A)," .+")

//first name
REGEXEXTRACT(A2,"^([\w\-]+)")
REGEXEXTRACT(A2, "\S+") 

// match text and filter range
https://stackoverflow.com/questions/42846220/regexmatch-with-regex-reference-to-cell
```

## Conditional formatting

### Searching for errors

```java
// custom formula
=iserror(B1)=true

// weekends where A1 is the first date in the column.
=or(WEEKDAY(A3)=1,WEEKDAY(A3)=7)
```

## Comparing two columns

```java
// list all matches from sheet 2 based on cell value
FILTER(sheet2!A:A, REGEXMATCH(sheets!A:A,A3)) 

// compare 2 columns for MATCHES / DIFFERENCE
=ArrayFormula(IF(A2:A=C2:C,"MATCH","DIFFER"))
```
