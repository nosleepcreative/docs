# Webscraping

#### Documentation / Tutorials

* [XPath Syntax](https://www.w3schools.com/xml/xpath\_syntax.asp)

#### Python

* https://instaloader.github.io/index.html

#### Google sheets

* [Import XML Guide](https://zapier.com/blog/google-sheets-importxml-guide/)&#x20;
* [Monitor YouTube and Instagram data](https://martechwithme.com/monitoring-youtube-channels-subscribers-with-google-sheets/)

## **Why scrape?**

### Application

* General: Competitive and price analysis, Lead generation, Keyword research
* **Research:** Science Product reattach, Finding / filling a job, Government oversight
* **Financial:** Stock analysis, Insurance and risk management, News gathering and analysis

Scraping for a car scrape the car buying websites to find all the teslas Evaluate the price to find great deals Scrape airfares and adjust the deals for airfare expenses Send an email digest of the top deal each day

**Python libraries** • beautiful soup • Scrape • Selenium

**Process** • set a start\_url variable • download html • parse html • extract useful information • transform or aggregate • save the data • Go the the next url

**HTTP overview Request** > response via https Web address / verb / user agent GET - retrieves data POST - sends data to the server User agent identifies the browser or web scraper

```python
# URL hacking query string
# Python URL strings 
host =‘www.iseecars.com’ 
path = ‘/used-cars/used-tesla-for-sale’ 
location = ’66592’ 
query_string = f#LOcation={location}&Radius =all&Make = Tesla&Model=Model+3’ start_url = f’
http://{host}{path}{query_string}’

# Python requests 
import requests 
start_url = ‘’ downloaded_page requests.get(start_url)
print(downloaded_page.text)
```

HTML & CSS Selectors css=> ‘title’ h1 li - list item Ul - unordered list ol - ordered list

### CSS Selectors&#x20;

```css
li
title
h1 
'#vin3827' // HTML ID
',auto-listing'

ul li // 
//class selectors
'ul.listings li#vin3827'

```

```python
exmaple = open("example.html","r")
html = example.read()
#hyml = requests.get(url).text
example.close

from bs4 import BeautifulSoup
soup = BeautifulSoup(html)
print(soup.prettify())

soup.title
soup.li
spup.find_all('li')
```

### XPath

```python
//ul[@class='listings"]/li[@id="vin3827']
```

## Legal Risks

getting sued for copyright infringement  / private websites&#x20;

1. Safe
   1. public government website
   2. scraping for personal use
   3. aggregated data project and research
   4. terms & conditions that allows&#x20;
2. More risky&#x20;
   1. scraping for personal use even though prohibited by the terms and conditions
   2. scraping data you don't own while logged in
   3. large scale scraping to publish widely promoted "news" reports
3. Relatively risky
   1. large scale scraping for profit
   2. create a commercial product
   3. scraping large company websites for profit
   4. creating and selling derivatives works
   5. scraping personally identifiable data (PII)

case-study: hiQ vs LinkedIn

## Python

### Scraping environment with JupyterLab

{% tabs %}
{% tab title="DL page" %}
```
#Import packages
import requests
from bs4 import Beautiful Soup
import pandas as pd

# Download and parse the HTML
start_url = 'https://...'

# Download the HTML from start_url
downloaded_html - requests.get(start_url)

# Parse the HTML with BeautifulSoup and create a soup object 
soup = BeautifulSoup(downlaoded_html.text)

#save a local copy
with open('downloaded.html', 'w) as file:
    file.write(soup.prettify())
```
{% endtab %}

{% tab title="JupterlabEnv" %}
```python
# Setup & Install Packages
#pyenv install 3.74
#pyenv local 3.74

#pipenv --python 3.7.4
#pipenv install requests
#pipenv install beautifulsoup4
#pipenv install pandas

#pipenv intall jupyterlab

# Check Installation
# !pyenv local
# !python - V
# !pip list
```
{% endtab %}

{% tab title="pandas" %}
```
# SEelct table.wiki table

table_head = full_table.select('tr th')

print('----------')

```
{% endtab %}
{% endtabs %}

##
