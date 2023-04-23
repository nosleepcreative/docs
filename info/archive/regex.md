# REGEX

## Recommended Readings

| **Item**                      | Links                                                                                                                                                                                                                                                                                                               |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Documentation / Tutorials** | <ul><li><a href="https://regexone.com/"><strong>https://regexone.com/</strong></a></li><li><a href="https://www.rexegg.com/">https://www.rexegg.com/</a></li><li><a href="https://www.regular-expressions.info/lookaround.html"><strong>https://www.regular-expressions.info/lookaround.h</strong>tml</a></li></ul> |
| Cheatsheet                    | <ul><li><a href="https://dev.to/catherinecodes/a-regex-cheatsheet-for-all-those-regex-haters-and-lovers--2cj1">https://dev.to/catherinecodes/a-regex-cheatsheet-for-all-those-regex-haters-and-lovers--2cj1</a></li></ul>                                                                                           |
| **Books**                     | <ul><li></li></ul>                                                                                                                                                                                                                                                                                                  |
| **Tester**                    | <p></p><ul><li><a href="https://regex101.com/">https://regex101.com/</a></li><li><a href="https://regexr.com/">https://regexr.com/</a></li><li><a href="https://regex101.com/r/gcC3ZQ/3/">My Dataset</a></li></ul>                                                                                                  |

## What is regular expression?

{% hint style="info" %}
**A regular expression is a sequence of** [**characters**](https://en.wikipedia.org/wiki/Character\_\(computing\)) **that define a search** [**pattern**](https://en.wikipedia.org/wiki/Pattern\_matching)**.** Usually such patterns are used by [string searching algorithms](https://en.wikipedia.org/wiki/String\_searching\_algorithm) for "find" or "find and replace" operations on [strings](https://en.wikipedia.org/wiki/String\_\(computer\_science\)), or for input validation. It is a technique developed in [theoretical computer science](https://en.wikipedia.org/wiki/Theoretical\_computer\_science) and [formal language](https://en.wikipedia.org/wiki/Formal\_language) theory. — Wikipedia \
\
It works similar to when we are searching something on Google but in a more advanced and specific way.&#x20;
{% endhint %}

### Why it matters?

* **Remove human errors** when it come to countless of data sorting or wrangling
* **Save you time and effort**  - once you written it once, it's reuable&#x20;

## The basics&#x20;

### Character class&#x20;

\[]





## Cookbook

```java
//1st word including hyphen eg.Bethune-Cookman
^\w+\b[-]{0,1}(\w+)?


1st 2 words with/without "'s" 
^\w+\s\w+[\']?s?

//2 words only
^\w+\s\w+$ 

// searching ???
.+\(.+\)

// Last word in parenthesis
\(([^)]*)\)[^(]*$
```

### HEX codes

```java
[A-Fa-f0-9]{6} // single 


// HEX codes from "Primary: 0050A3 Secondary: FFFFFF" 
 \s[a-zA-Z0-9]{6,} 
```

### NCAA

```java
// team names 
(\w*Alt\w*){0,1}((-\s)?\w*ALT\w*){0,1}","")

// breaking 
^\w+[-]?\w // catch hyphenated compound
^\w+\b[-]{0,1}[\w+]? // break two words 
^\w+[']?\w?\s\w+[\']?s?" // break words with apostrophe 

\w+\s\w+$ // capture last 2 words 
\w+$ // capture last word 

// optimized 
^[\w's&-.]+[ &]?[\w's&.]+


// workflow 
// 1. break school with State 
^[\w's&-.]+[ &]?[\w's&.]+ [State]+
^[\w's&-.]+[ &]?[\w's&.]+ [StateUniversity]+
```

