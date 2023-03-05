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

We will create a folder named crapy_project and access it by typing:

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

Now that our virtual environment is created in the crapy_project folder, we will activate it.

* Acceder à l'environnement env dans le dossier scrapy_project

  ```apache
  192:crapy_project boubadiop$ cd env/
  192:env sogbedouno$ ls
  bin		include		lib		pyvenv.cfg

  ```
* Activate the virtual environment

  ```apache
  192:env sogbedouno$ source bin/activate
  (env) 192:env sogbedouno$
  ```

###### Install Crapy in your virtual environment

`(env) 192:env boubadiop$ pip install scrapy`

To check that scrapy has been installed you can type in your command prompt `pip list`.

```apache
(env) 192:env sogbedouno$ pip list
Package            Version
------------------ ---------
attrs              22.2.0
Automat            22.10.0
certifi            2022.12.7
cffi               1.15.1
charset-normalizer 3.0.1
constantly         15.1.0
cryptography       39.0.2
cssselect          1.2.0
filelock           3.9.0
hyperlink          21.0.0
idna               3.4
incremental        22.10.0
itemadapter        0.7.0
itemloaders        1.0.6
jmespath           1.0.1
lxml               4.9.2
packaging          23.0
parsel             1.7.0
pip                22.0.4
Protego            0.2.1
pyasn1             0.4.8
pyasn1-modules     0.2.8
pycparser          2.21
PyDispatcher       2.0.7
pyOpenSSL          23.0.0
queuelib           1.6.2
requests           2.28.2
requests-file      1.5.1
Scrapy             2.8.0
service-identity   21.1.0
setuptools         58.1.0
six                1.16.0
tldextract         3.4.0
Twisted            22.10.0
typing_extensions  4.5.0
urllib3            1.26.14
w3lib              2.1.1
zope.interface     5.5.2
```

### Step 2: Setup Our Scrapy Project

Now that we have our environment setup, we can get onto the fun stuff. Building our first Scrapy spider!.

###### Creating Our Scrapy Project

The first thing we need to do is create our Scrapy project. This project will hold all the code for our scrapers.

The command to create your scrapy project is:

`scrapy startproject <project_name>`

So in this case, as we're going to be scraping a chocolate website we will call our project chocolatescraper. But you can use any project name you would like.

`scrapy startproject chocolatescraper`

###### Understanding Scrapy Project Structure

To help you understand what we just did, and how Scrapy structures its projects, let’s take a break for a second.

First, we're going to see what the `scrapy startproject chocolatescraper` just did.

Enter the following commands into your command line:

```apache
(env) 192:env sogbedouno$ cd chocolatescraper/
tree
```

You should see something like this:

```apache
├── scrapy.cfg
└── chocolatescraper
    ├── __init__.py
    ├── items.py
    ├── middlewares.py
    ├── pipelines.py
    ├── settings.py
    └── spiders
        └── __init__.py
```

When we ran the command scrapy startproject chocolatescraper, Scrapy automatically generated a model project to use.

We will not use most of these files in this project but we will give a quick explanation of each because each has a specific purpose:

* **settings.py** is where all your project settings are contained, like activating pipelines, middlewares etc. Here you can change the delays, concurrency, and lots more things.
* **items.py** is a model for the extracted data. You can define a custom model (like a ProductItem) that will inherit the Scrapy Item class and contain your scraped data.
* **pipelines.py** is where the item yielded by the spider gets passed, it’s mostly used to clean the text and connect to file outputs or databases (CSV, JSON SQL, etc).
* **middlewares.py** is useful when you want to modify how the request is made and scrapy handles the response.
* **scrapy.cfg** is a configuration file to change some deployment settings, etc.

### Step 3: Creating Our Spider

Okay, we’ve created the overall structure of the project. Now we’re going to create our spider that will scrape.

Scrapy provides a number of different types of spiders, however, in this presentation we will cover the most common, generic spider. Some of the most common are:

* **Spider**: Takes a list of start_urls and scrapes each one with a `parse` method.
* **CrawlSpider**:  Designed to crawl a full website by following any links it finds.
* **SitemapSpider**:  Designed to extract URLs from a sitemap

To create a new generic spider, simply run the **genspider** command:

`sogbedouno$ scrapy genspider chocolatespider chocolate.co.uk`

A new spider will now have been added to your `spiders` folder, and it should look like this:

```apache
import scrapy


class ChocolatespiderSpider(scrapy.Spider):
    name = "chocolatespider"
    allowed_domains = ["chocolate.co.uk"]
    start_urls = ["http://chocolate.co.uk/"]

    def parse(self, response):
        pass

```

Here we see that the `genspider` command has created a template spider for us to use in the form of a `Spider` class. This spider class contains:

* **name**: a class attribute that gives a name to the spider. We will use this when running our spider later `scrapy crawl <spider_name>`.
* **allowed_domains**: a class attribute that tells Scrapy that it should only ever scrape pages of the `chocolate.co.uk` domain. This prevents the spider going rouge and scraping lots of websites. This is optional.
* **start_urls**: a class attribute that tells Scrapy the first url it should scrape. We will be changing this in a bit.
* **parse**: the `parse` function is called after a response has been recieved from the target website.


<pre tabindex="0" class="prism-code language-bash codeBlock_bY9V thin-scrollbar"><br class="Apple-interchange-newline"/></pre>
