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
192:~ sogbedouno$ mkdir my_project_scrapy
192:~ sogbedouno$ cd my_project_scrapy/
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
  192:my_project_scrapy sogbedouno$ cd env
  192:env sogbedouno$ ls
  bin		include		lib		pyvenv.cfg

  ```
* Activate the virtual environment

  ```apache
  192:env sogbedouno$ source bin/activate
  (env) 192:env sogbedouno$
  ```

###### Install Crapy in your virtual environment

`(env) 192:env sogbedouno$ pip install scrapy`

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

So in this case, we are going to scrap the advertisements of apartments for rent from the expat dakar site, we will call our real apartmentscraper. But you can use any project name.

`scrapy startproject apartmentscraper`

###### Understanding Scrapy Project Structure

To help you understand what we just did, and how Scrapy structures its projects, let’s take a break for a second.

First, we're going to see what the `scrapy startproject apartmentscraper` just did.

Enter the following commands into your command line:

```apache
(env) 192:env sogbedouno$ cd apartmentscraper/
tree
```

You should see something like this:

```apache
├── scrapy.cfg
└── apartmentscraper
    ├── __init__.py
    ├── items.py
    ├── middlewares.py
    ├── pipelines.py
    ├── settings.py
    └── spiders
        └── __init__.py
```

When we run the command scrapy startproject expatimmobscraper, Scrapy automatically generated a model project to use.

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

```apache
crapy genspider apartmentspider expat-dakar.com
```

A new spider will now have been added to your `spiders` folder, and it should look like this:

```css
import scrapy

class ApartmentspiderSpider(scrapy.Spider):
    name = "apartmentspider"
    allowed_domains = ["expat-dakar.com"]
    start_urls = ["http://expat-dakar.com/"]

    def parse(self, response):
        pass

```

Here we see that the `genspider` command has created a template spider for us to use in the form of a `Spider` class. This spider class contains:

* **name**: a class attribute that gives a name to the spider. We will use this when running our spider later `scrapy crawl <spider_name>`.
* **allowed_domains**: a class attribute that tells Scrapy that it should only ever scrape pages of the `expat-dakar.com` domain. This prevents the spider going rouge and scraping lots of websites. This is optional.
* **start_urls**: a class attribute that tells Scrapy the first url it should scrape. We will be changing this in a bit.
* **parse**: the `parse` function is called after a response has been recieved from the target website.

To start using this Spider we will have to do two things:

1. Change the `start_urls` to the url we want to scrape

   [https://www.expat-dakar.com/appartements-a-louer](https://)
2. Insert our parsing code into the `parse` function.

### Step 4: Update Start Urls

This is pretty easy, we just need to replace the url in the `start_urls` array:

```css
import scrapy

class ApartmentspiderSpider(scrapy.Spider):
    name = "apartmentspider"
    allowed_domains = ["expat-dakar.com"]
    start_urls = ["https://www.expat-dakar.com/appartements-a-louer"]

    def parse(self, response):
        pass

```

Next, we need to create our CSS selectors to parse the data we want from the page. To do this, we will use Scrapy Shell.

### Step 5: Scrapy Shell: Finding Our Css Selectors

To extract data from an HTML page, we must use XPath or CSS selectors to tell Scrapy where the data is in the page. The XPath and CSS selectors are like small maps for Scrapy to navigate the DOM tree and find the location of the data we need. In this article, we will use CSS selectors to analyze page data. And to help us create these CSS selectors, we will use Scrapy Shell.

One of the great features of Scrapy is that it comes with an integrated shell that allows you to quickly test and debug your XPath & CSS selectors. Instead of having to launch your complete scraper to see if your XPath or CSS selectors are correct, you can enter them directly into your terminal and see the result.

To open Scrapy shell use this command:

```css
scrapy shell
```

And then edit your `scrapy.cfg` file like so:

```css
[settings]
default = apartmentscraper.settings
shell = ipython
```

with our scrapy shell open, you should see something like this:

```css
[s] Available Scrapy objects:
[s]   scrapy     scrapy module (contains scrapy.Request, scrapy.Selector, etc)
[s]   crawler    <scrapy.crawler.Crawler object at 0x107ec7550>
[s]   item       {}
[s]   settings   <scrapy.settings.Settings object at 0x107ec6d10>
[s] Useful shortcuts:
[s]   fetch(url[, redirect=True]) Fetch URL and update local objects (by default, redirects are followed)
[s]   fetch(req)                  Fetch a scrapy.Request and update local objects 
[s]   shelp()           Shell help (print this help)
[s]   view(response)    View response in a browser
2023-03-07 09:19:17 [asyncio] DEBUG: Using selector: KqueueSelector
In [1]: 
[s]   shelp()           Shell help (print this help)
[s]   view(response)    View response in a browser
2023-03-07 01:37:43 [asyncio] DEBUG: Using selector: KqueueSelector
In [1]: 
```

##### Fetch The Page

To create our CSS selectors we will be testing them on the following page.

IMAGE

The first thing we want to do is fetch the main products page of the chocolate site in our Scrapy shell.

`fetch('https://www.expat-dakar.com/appartements-a-louer')`

We should see a response like this:

```css
In [1]: fetch('https://www.expat-dakar.com/appartements-a-louer')
2023-03-07 09:22:58 [asyncio] DEBUG: Using selector: KqueueSelector
2023-03-07 09:22:58 [scrapy.core.engine] INFO: Spider opened
2023-03-07 09:22:58 [scrapy.core.engine] DEBUG: Crawled (200) <GET https://www.expat-dakar.com/robots.txt> (referer: None)
2023-03-07 09:22:59 [scrapy.core.engine] DEBUG: Crawled (200) <GET https://www.expat-dakar.com/appartements-a-louer> (referer: None)
```

As we can see, we successful retrieve the page from `expat-dakar.com`, and Scrapy shell has automatically saved the HTML response in the response variable.

```css
In [2]: response
Out[2]: <200 https://www.expat-dakar.com/appartements-a-louer>
```

### Find Product CSS Selectors

To find the correct CSS selectors to parse the product details we will first open the page in our browsers DevTools.

Open the [website](https://www.expat-dakar.com/appartements-a-louer), then open the developer tools console (right click on the page and click inspect).

IMAGE

Using the inspect element, hover over the item and look at the id's and classes on the individual apartment.

In this case we can see that each box of apartements has its own special component which is called `listings-cards__list-item`. We can just use this to reference our apartments (see above image).

Now using our Scrapy shell we can see if we can extract the apartment informaton using this class.

```css
response.css('div.listings-cards__list-item')
```

We can see that it has found all the elements that match this selector.

```css
In [3]: response.css('div.listings-cards__list-item')
Out[3]: 
[<Selector xpath="descendant-or-self::div[@class and contains(concat(' ', normalize-space(@class), ' '), ' listings-cards__list-item ')]" data='<div class="listings-cards__list-item...'>,
 <Selector xpath="descendant-or-self::div[@class and contains(concat(' ', normalize-space(@class), ' '), ' listings-cards__list-item ')]" data='<div class="listings-cards__list-item...'>,
 <Selector xpath="descendant-or-self::div[@class and contains(concat(' ', normalize-space(@class), ' '), ' listings-cards__list-item ')]" data='<div class="listings-cards__list-item...'>,
 <Selector xpath="descendant-or-self::div[@class and contains(concat(' ', normalize-space(@class), ' '), ' listings-cards__list-item ')]" data='<div class="listings-cards__list-item...'>,
 <Selector xpath="descendant-or-self::div[@class and contains(concat(' ', normalize-space(@class), ' '), ' listings-cards__list-item ')]" data='<div class="listings-cards__list-item...'>,
 <Selector xpath="descendant-or-self::div[@class and contains(concat(' ', normalize-space(@class), ' '), ' listings-cards__list-item ')]" data='<div class="listings-cards__list-item...'>,
 <Selector xpath="descendant-or-self::div[@class and contains(concat(' ', normalize-space(@class), ' '), ' listings-cards__list-item ')]" data='<div class="listings-cards__list-item...'>,
 <Selector xpath="descendant-or-self::div[@class and contains(concat(' ', normalize-space(@class), ' '), ' listings-cards__list-item ')]" data='<div class="listings-cards__list-item...'>,
 <Selector xpath="descendant-or-self::div[@class and contains(concat(' ', normalize-space(@class), ' '), ' listings-cards__list-item ')]" data='<div class="listings-cards__list-item...'>,
 <Selector xpath="descendant-or-self::div[@class and contains(concat(' ', normalize-space(@class), ' '), ' listings-cards__list-item ')]" data='<div class="listings-cards__list-item...'>,
 <Selector xpath="descendant-or-self::div[@class and contains(concat(' ', normalize-space(@class), ' '), ' listings-cards__list-item ')]" data='<div class="listings-cards__list-item...'>,
 <Selector xpath="descendant-or-self::div[@class and contains(concat(' ', normalize-space(@class), ' '), ' listings-cards__list-item ')]" data='<div class="listings-cards__list-item...'>]

In [4]:  
```

#### Get First Apartement

To just get the first apartement we use `.get()` appended to the end of the command.

`response.css('div.listings-cards__list-item').get()`

This returns all the HTML in this node of the DOM tree.

```css
In [4]: response.css('div.listings-cards__list-item').get()
Out[4]: '<div class="listings-cards__list-item "><div class="listing-card listing-card--tab listing-card--has-contact listing-card--has-content listing-card--priority listing-card--priority-gold listing-card--highlight-placeholder">
...
```

#### Get All Apartments

Now that we have found the DOM node that contains the apartment items, we will get all of them and save this data into a response variable and loop through the items and extract the data we need.

So can do this with the following command.

```
In [5]: apartments = response.css('div.listings-cards__list-item')
```

The apartments variable, is now an list of all the apartments on the page.

To check the length of the apartments variable we can see how many apartments are there.

`len(apartments)`

Here is the output:

```css
In [6]: len(apartments)
Out[6]: 12

```

#### Extract Apartments Details

Now lets extract the **title** , **adress**, **price** and **number of room** of each apartment from the list of apartments.

The apartments variable is a list of apartments. When we update our spider code, we will loop through this list, however, to find the correct selectors we will test the CSS selectors on the first element of the list `apartment = apartments[0]`.

##### Single Apartment - Get Single apartment

`apartment = apartments[0]`

##### Title - The apartment title can be found with

`apartment.css('div.listing-card__header__title::text').get()`

You can see that the data returned for the title has lots of extra HTML. We'll get rid of this in the next step.

```css
In [9]: apartment.css('div.listing-card__header__title::text').get()
Out[9]: '\nAppartements KALIA - Zone de captage\n'
```

To remove the extra div tags from our title we can use the `.replace()` method. The replace method can be useful when we need to clean up data.

Here we're going to replace the `<div>` sections with empty quotes `''`:

```css
apartment.css('div.listing-card__header__title::text').get().replace('\n', '')
```

```css
In [10]: apartment.css('div.listing-card__header__title::text').get().replace('\n', '')
Out[10]: 'Appartements KALIA - Zone de captage'

In [11]: 
```

##### Adress- The apartment adress can be found with

```css
apartment.css('div.listing-card__header__location::text').get()
```

You can see that the data returned for the title has lots of extra HTML. We'll get rid of this in the next step.

```css
In [12]: apartment.css('div.listing-card__header__location::text').get()
Out[12]: '\nZone de captage,\nDakar\n'
```

We will remove the div tags from our address as for the title with the `.replace()` method.

```css
apartment.css('div.listing-card__header__location::text').get().replace('\n', ''
```

```css
In [13]: apartment.css('div.listing-card__header__location::text').get().replace('\n', ''
    ...: )
Out[13]: 'Zone de captage,Dakar'
```

###### Price: the apartment price can be found with

`apartment.css('span.listing-card__price__value::text').get()`

```apache
In [16]: apartment.css('span.listing-card__price__value::text').get()
Out[16]: '\n500\u202f000 F Cfa\n'
```

We will also remove the div tags

```apache
In [19]: apartment.css('span.listing-card__price__value::text').get().replace('\n', '').r
    ...: eplace('\u202f', '').replace(' F Cfa', '')
Out[19]: '500000'
```

###### Number_of_room: the apartment number_of_room can be found with

`apartment.css('div.listing-card__header__tags::text').get()`

We will also remove thre div tags 😕. It's tiring but hey it's the only solution I've found for the moment.

```apache
In [28]: apartment.css('div.listing-card__header__tags').get().replace('<div class="listi
    ...: ng-card__header__tags"><span class="listing-card__header__tags__item listing-car
    ...: d__header__tags__item--no-of-bedrooms listing-card__header__tags__item--no-of-be
    ...: drooms_3">', '').replace('</span><span class="listing-card__header__tags__item l
    ...: isting-card__header__tags__item--square-metres listing-card__header__tags__item-
    ...: -square-metres_100">', '').replace('</span></div>', '')
Out[28]: '3 chambre100 m²'
```

#### Updated Spider

Now, that we've found the correct CSS selectors let's update our spider. Exit Scrapy shell with the `exit()` command.

Our updated Spider code should look like this:

```apache
import scrapy

class ChocolatespiderSpider(scrapy.Spider):
    #the name of the spider
    name = "chocolatespider"
  
    #the url of the first page that we will start scraping
    allowed_domains = ["chocolate.co.uk"]
    start_urls = ["https://www.chocolate.co.uk/collections/all."]

    def parse(self, response):
        #here we are looping through the products and extracting the name, price and url
        products = response.css('product-item')
        for product in products:
            #here we put the data returned into the format we want to output for our csv or json file
            yield{
                'name' : product.css('a.product-item-meta__title::text').get(),
                'price' : product.css('span.price').get().replace('<span class="price">\n              <span class="visually-hidden">Sale price</span>', '').replace('</span>', ''),
                'url' : product.css('div.product-item-meta a').attrib['href']
            }
```

Here, our spider does the following steps:

1. Makes a request to `'"https://www.expat-dakar.com/appartements-a-louer'`.
2. When it gets a response, it extracts all the products from the page using `apartments = response.css('div.listings-cards__list-item')`.
3. Loops through each apartment, and extracts the  **title** , **adress**, **price** and **number_of_room** using the CSS selectors we created.
4. Yields these items so they can be stored in a CSV, JSON, DB, etc.

### Step 5: Running Our Spider

Now that we have a spider we can run it by going to the top level in our scrapy project and running the following command.

```apache
scrapy crawl apartmentspider
```

It will run, and you should see the logs on your screen. Here are the final stats:

```css
2023-03-07 13:11:11 [scrapy.statscollectors] INFO: Dumping Scrapy stats:
{'downloader/request_bytes': 468,
 'downloader/request_count': 2,
 'downloader/request_method_count/GET': 2,
 'downloader/response_bytes': 22309,
 'downloader/response_count': 2,
 'downloader/response_status_count/200': 2,
 'elapsed_time_seconds': 0.983364,
 'finish_reason': 'finished',
 'finish_time': datetime.datetime(2023, 3, 7, 13, 11, 11, 48146),
 'httpcompression/response_bytes': 171794,
 'httpcompression/response_count': 2,
 'item_scraped_count': 12,
 'log_count/DEBUG': 17,
 'log_count/INFO': 10,
 'memusage/max': 57683968,
 'memusage/startup': 57683968,
 'response_received_count': 2,
 'robotstxt/request_count': 1,
 'robotstxt/response_count': 1,
 'robotstxt/response_status_count/200': 1,
 'scheduler/dequeued': 1,
 'scheduler/dequeued/memory': 1,
 'scheduler/enqueued': 1,
 'scheduler/enqueued/memory': 1,
 'start_time': datetime.datetime(2023, 3, 7, 13, 11, 10, 64782)}
```

We can see from the above stats that our spider scraped 24 items:

`'item_scraped_count': 12`

If we want to save the data to a JSON file we can use the `-O` option, followed by the name of file.

`scrapy crawl apartmentspider -O myscrapeddata.json`

Then a json file will be created in your project and that will contain your collection.

```css
[
{"title": "Appartements KALIA - Zone de captage", "adress": "Zone de captage,Dakar", "price": "500000", "number_of_room": null},
{"title": "Appartement neufs de standing à louer mamelles", "adress": "Almadies,Dakar", "price": "1100000", "number_of_room": null},
{"title": "Joli appartement à louer à ngor zone calme", "adress": "Ngor,Dakar ", "price": "650000", "number_of_room": null},
{"title": "Almadies proche King Fahd Palace beau F3 haut standing", "adress": "Almadies,Dakar", "price": "1700000", "number_of_room": null},
{"title": "VILLA NEUVE ET MODERNE DE R+2", "adress": "Sacré-cœur,Dakar", "price": "1600000", "number_of_room": null},
{"title": "F2 A LOUER A LA CITE APIX", "adress": "Niague,Dakar", "price": "200000", "number_of_room": null},
{"title": "Appartement à louer aux mamelles cité mbackiyou faye", "adress": "Mamelles,Dakar", "price": "650000", "number_of_room": null},
{"title": "Appartement haut standing point e", "adress": "Point-e,Dakar", "price": "750000", "number_of_room": null},
{"title": "Appartement F4 à sacré coeur 2", "adress": " Sacré-cœur,Dakar", "price": "500000", "number_of_room": null},
{"title": "Grand appartement f5 de 300 m2 à louer au virage", "adress": "Virage,Dakar", "price": "1500000", "number_of_room": null},
{"title": "Luxueux Appartements F2 et F3 à Hann Marinas", "adress": " Hann marinas,Dakar", "price": "500000", "number_of_room": null},
{"title": "Exceptionnel appartement neuf aux Almadies", "adress": "Almadies,Dakar", "price": "2800000", "number_of_room": null}
]
```

If we want to save the data to CSV file we can do so too.

`scrapy crawl apartmentspider -O myscrapeddata.csv`

### Step 6: Navigating to the "Next Page"

So far the code is working great but we're only getting the apartments from the first page of the site, the url which we have listed in the start_url variable.

So the next logical step is to go to the next page if there is one and scrape the item data from that too! So here's how we do that.

First, lets open our Scrapy shell again, fetch the page and find the correct selector to get the **next page** button.

`scrapy shell`

Then fetch the page again.

```css
In [1]: fetch('https://www.expat-dakar.com/appartements-a-louer')
```

And then get the href attribute that contains the url to the next page.

```css
response.css('[rel="next"] ::attr(href)').get()
```

```css
In [2]: response.css('[rel="next"] ::attr(href)').get()
Out[2]: 'https://www.expat-dakar.com/appartements-a-louer?page=2'
```

Now, we just need to update our spider to request this page after it has parsed all items from a page.

```css
import scrapy


class ApartmentspiderSpider(scrapy.Spider):
    #the name of the spider
    name = "apartmentspider"
    allowed_domains = ["expat-dakar.com"]
    #the url of the first page that we will start scraping
    start_urls = ["https://www.expat-dakar.com/appartements-a-louer"]

    def parse(self, response):
        #here we are looping through the apartments and extracting the title, adress, price and number_of_room
        apartments = response.css('div.listings-cards__list-item')
        for apartment in apartments:
            yield{
                'title' : apartment.css('div.listing-card__header__title::text').get().replace('\n', ''),
                'adress' : apartment.css('div.listing-card__header__location::text').get().replace('\n', ''),
                'price' : apartment.css('span.listing-card__price__value::text').get().replace('\n', '').replace('\u202f', '').replace(' F Cfa', ''),
                "number_of_room": apartment.css('div.listing-card__header__tags::text').get()
                        
            }
    
        next_page = response.css('[rel="next"] ::attr(href)').get()
        if next_page is not None:
            next_page_url = "https://www.expat-dakar.com/appartements-a-louer" + next_page
            yield response.follow(next_page_url, callback =self.parse)
    
    
    

```

Here we see that our spider now, finds the URL of the next page and if it isn't none it appends it to the base URL and makes another request.

Now in our Scrapy stats we see that we have scraped 5 pages, and extracted 73 items:

```css
2023-03-06 23:11:33 [scrapy.statscollectors] INFO: Dumping Scrapy stats:
{'downloader/request_bytes': 3509,
 'downloader/request_count': 5,
 'downloader/request_method_count/GET': 5,
 'downloader/response_bytes': 170647,
 'downloader/response_count': 5,
 'downloader/response_status_count/200': 5,
 'elapsed_time_seconds': 4.839079,
 'finish_reason': 'finished',
 'finish_time': datetime.datetime(2023, 3, 6, 23, 11, 33, 395120),
 'httpcompression/response_bytes': 853126,
 'httpcompression/response_count': 5,
 'item_scraped_count': 89,
 'log_count/DEBUG': 97,
 'log_count/INFO': 10,
 'memusage/max': 57798656,
 'memusage/startup': 57794560,
 'request_depth_max': 3,
 'response_received_count': 5,
 'robotstxt/request_count': 1,
 'robotstxt/response_count': 1,
 'robotstxt/response_status_count/200': 1,
 'scheduler/dequeued': 4,
 'scheduler/dequeued/memory': 4,
 'scheduler/enqueued': 4,
 'scheduler/enqueued/memory': 4,
 'start_time': datetime.datetime(2023, 3, 6, 23, 11, 28, 556041)}
2023-03-06 23:11:33 [scrapy.core.engine] INFO: Spider closed (finished)
```

## Next Steps

In the second part, we will work on data cleaning. Web data can sometimes be very messy, unstructured, and have many edge cases so will make our spider robust to these edge cases, using articles, Itemloaders and Item Pipelines.
