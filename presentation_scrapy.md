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
* [Python Request-HTML](https://github.com/psf/requests-htmlhttps://): Combining Python requests with a parsing library, Request-HTML is a middle-ground between the Python Requests/BeautifulSoup combo and Scrapy.

* [Python Selenium](https://selenium-python.readthedocs.io/https://): Use if you are scraping a site if it only returns the target data after the Javascript has rendered, or you need to interact with page elements to get the data.

**[Python Scrapy](https://scrapy.org/)** has lots more functionality and is great for large scale scraping right out of the box:

* CSS Selector & XPath Expressions Parsing
* Data formating (CSV, JSON, XML) and Storage (FTP, S3, local filesystem)
* Robust Encoding Support
* Concurrency Managment
* Automatic Retries
* Cookies and Session Handling
* Crawl Spiders & In-Built Pagination Support

You just need to customise it in your settings file or add in one of the many Scrapy extensions and middlewares that developers have open sourced.

The learning curve is initially steeper than using the Python Requests/BeautifulSoup combo, however, it will save you a lot of time in the long run when deploying production scrapers and scraping at scale.

### Starting

#### Step 1: Setup your Python Environment

Before installing scrapy in your system the first thing to do is to create a virtual environment. 

But for a well organized job, start creating a folder that will contain your srapy project in your terminal by typing the command:

`mkdir folder_name`

We will create a folder named crapy_test and access it by typing:

```
192:~ sogbedouno$ mkdir crapy_project
192:~ sogbedouno$ cd crapy_project/
```

###### Create the virtual environment

Now that the folder is created we will begin.

Depending on your machine’s operating system, these controls will be slightly different.

In general under **Mac Os, Windows and Linux** the command to create a virtual environment is the following.

`python -m venv env`

###### Activate the virtual environment

Now that our virtual environment is created in the crapy_test folder, we will activate it.

* Acceder à l'environnement env dans le dossier scrapy_test

  ```
  192:crapy_project boubadiop$ cd env/
  192:env sogbedouno$ ls
  bin		include		lib		pyvenv.cfg

  ```
* Activate the virtual environment

  ```
  192:env sogbedouno$ source bin/activate
  (env) 192:env sogbedouno$
  ```

**###### Install Scrapy in our virtual environment**





<pre tabindex="0" class="prism-code language-bash codeBlock_bY9V thin-scrollbar"><br class="Apple-interchange-newline"/></pre>
