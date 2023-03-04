# Introduction

The World Wide Web is made up of billions of interconnected documents commonly referred to as "Internet sites". The source code of these websites is written in Hypertext Markup Language(HTML). [This HTML source code](https://www.ionos.fr/digitalguide/sites-internet/developpement-web/apprendre-le-html-le-tutoriel-pour-debutant/https://)  is a  **mixture of human-readable information and machine-readable code**  , known as beacons. The web browser – eg. Chrome, Firefox, Safari or Edge – processes the source code, interprets the tags and makes the information they contain available to the user.

Specific software is used in order to extract only from the source code the information of interest to the human being. These programs – known as 'web scrapers', 'crawlers', 'spiders' or simply 'bots' **crawl the source code of websites looking for patterns**  and extract the information there. The information obtained during [web scraping](https://www.ionos.fr/digitalguide/sites-internet/developpement-web/quest-ce-que-le-web-scraping/ "What is web scraping?") is gathered, combined, analyzed or saved for later use.

However there are several libraries allowing to quickly make web scraping hence the
**scrapy library**  that we will present in this article.

# Presentation

### What Is Crapy?

Developed by the co-founders of [Zyte](https://www.zyte.com/?rfsn=6335521.8097b3https://), Pablo Hoffman and Shane Evans, [Scrapy](https://scrapy.org/https://) is a python framework specifically for web scraping.

Using Scrapy you can easily build highly scalable scrapers that will retrieve a pages HTML, parse and process the data, and store it the file format and location of your choice.

### Why & When Should You Use Scrapy?

Although, there are other Python libraries also used for web scraping:

* [Python Requests](https://docs.python-requests.org/en/latest/https://)/[BeautifulSoup](https://beautiful-soup-4.readthedocs.io/en/latest/https://): Good for small scale web scraping where the data is returned in the HTML response. Would need to build you own spider management functionality to manage concurrency, retries, data cleaning, data storage.
* [Python Request-HTML](https://github.com/psf/requests-htmlhttps://)
