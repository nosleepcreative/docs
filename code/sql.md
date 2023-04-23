# SQL

## Recommended Readings

| **Item**                                                              | Links                                                                                                                                                                                                                                                                      |
| --------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Documentation / Tutorials**                                         | <ul><li><a href="https://www.youtube.com/watch?v=YufocuHbYZo">SQL for Beginners</a></li><li><a href="https://online.maryville.edu/online-bachelors-degrees/management-information-systems/careers/">Management Information Systems Careers</a></li></ul>                   |
| <p><strong>Industry /</strong> <br><strong>Case-studies</strong> </p> | <ul><li></li></ul>                                                                                                                                                                                                                                                         |
| **Books**                                                             | <ul><li></li></ul>                                                                                                                                                                                                                                                         |
| **Cheatsheet**                                                        | <p></p><ul><li><a href="https://www.sqltutorial.org/sql-cheat-sheet/">https://www.sqltutorial.org/sql-cheat-sheet/</a></li><li><strong>Luke Harrison:</strong> <a href="https://websitesetup.org/sql-cheat-sheet/">https://websitesetup.org/sql-cheat-sheet/</a></li></ul> |

```
select
from
where
order by [desc]
```

## Google Sheets

### [Multiple contains ](https://infoinspired.com/google-docs/spreadsheet/multiple-contains-in-where-clause-in-query/)

```
=QUERY(A1:A,"Select * Where not A Matches '.*AB.*|.*DJ.*' ",1)
=query(C323:C335,"Select C where not C contains 'soccer'")
=QUERY(C:C,"Select C Where not C Matches '.*ezoic.*|.*soccer.*' ",1)

```

### Referencing cells in query&#x20;

```
query(sheet2!A:G,"select A where G contains '"&L3&"'")

=query(SX_Sessions!$B$2:$E$120, 
"select B,D 
where E ='" &B3&"' 
AND C = '"&$B$1&"'")
```

### Hyperlinks

```
=IMPORTXML(B3, "//a/@href")
```
