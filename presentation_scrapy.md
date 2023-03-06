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

To start using this Spider we will have to do two things:

1. Change the `start_urls` to the url we want to scrape [https://www.chocolate.co.uk/collections/all](https://www.chocolate.co.uk/collections/all).
2. Insert our parsing code into the `parse` function.

### Step 4: Update Start Urls

This is pretty easy, we just need to replace the url in the `start_urls` array:

```apache
import scrapy

class ChocolatespiderSpider(scrapy.Spider):
    name = "chocolatespider"
    allowed_domains = ["chocolate.co.uk"]
    start_urls = ["https://www.chocolate.co.uk/collections/all."]

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
default = chocolatescraper.settings
shell = ipython
```

with our scrapy shell open, you should see something like this:

```css
s] Available Scrapy objects:
[s]   scrapy     scrapy module (contains scrapy.Request, scrapy.Selector, etc)
[s]   crawler    <scrapy.crawler.Crawler object at 0x10b9eb520>
[s]   item       {}
[s]   settings   <scrapy.settings.Settings object at 0x10b9eace0>
[s] Useful shortcuts:
[s]   fetch(url[, redirect=True]) Fetch URL and update local objects (by default, redirects are followed)
[s]   fetch(req)                  Fetch a scrapy.Request and update local objects 
[s]   shelp()           Shell help (print this help)
[s]   view(response)    View response in a browser
In [1]: 
```

##### Fetch The Page

To create our CSS selectors we will be testing them on the following page.

IMAGE

The first thing we want to do is fetch the main products page of the chocolate site in our Scrapy shell.

`fetch('https://www.chocolate.co.uk/collections/all')`

We should see a response like this:

```css
In [1]: fetch('https://www.chocolate.co.uk/collections/all')
2023-03-06 01:29:39 [asyncio] DEBUG: Using selector: KqueueSelector
2023-03-06 01:29:39 [scrapy.core.engine] INFO: Spider opened
2023-03-06 01:29:40 [urllib3.connectionpool] DEBUG: Starting new HTTPS connection (1): publicsuffix.org:443
2023-03-06 01:29:40 [urllib3.connectionpool] DEBUG: https://publicsuffix.org:443 "GET /list/public_suffix_list.dat HTTP/1.1" 200 81598
2023-03-06 01:29:41 [scrapy.core.engine] DEBUG: Crawled (200) <GET https://www.chocolate.co.uk/robots.txt> (referer: None)
2023-03-06 01:29:41 [scrapy.core.engine] DEBUG: Crawled (200) <GET https://www.chocolate.co.uk/collections/all> (referer: None)
```

As we can see, we successful retrieve the page from `chocolate.co.uk`, and Scrapy shell has automatically saved the HTML response in the response variable.

```css
In [2]: response
Out[2]: <200 https://www.chocolate.co.uk/collections/all>
```

### Find Product CSS Selectors

To find the correct CSS selectors to parse the product details we will first open the page in our browsers DevTools.

Open the [website](https://www.chocolate.co.uk/collections/all), then open the developer tools console (right click on the page and click inspect).

IMAGE

Using the inspect element, hover over the item and look at the id's and classes on the individual products.

In this case we can see that each box of chocolates has its own special component which is called `product-item`. We can just use this to reference our products (see above image).

Now using our Scrapy shell we can see if we can extract the product informaton using this class.

```css
response.css('product-item')
```

We can see that it has found all the elements that match this selector.

```css
In [3]: response.css('product-item')
Out[3]: 
[<Selector xpath='descendant-or-self::product-item' data='<product-item class="product-item " r...'>,
 <Selector xpath='descendant-or-self::product-item' data='<product-item class="product-item " r...'>,
 <Selector xpath='descendant-or-self::product-item' data='<product-item class="product-item " r...'>,
 <Selector xpath='descendant-or-self::product-item' data='<product-item class="product-item " r...'>,
 <Selector xpath='descendant-or-self::product-item' data='<product-item class="product-item " r...'>,
 <Selector xpath='descendant-or-self::product-item' data='<product-item class="product-item " r...'>,
 <Selector xpath='descendant-or-self::product-item' data='<product-item class="product-item " r...'>,
 <Selector xpath='descendant-or-self::product-item' data='<product-item class="product-item " r...'>,
 <Selector xpath='descendant-or-self::product-item' data='<product-item class="product-item " r...'>,
 <Selector xpath='descendant-or-self::product-item' data='<product-item class="product-item pro...'>,
 <Selector xpath='descendant-or-self::product-item' data='<product-item class="product-item pro...'>,
 <Selector xpath='descendant-or-self::product-item' data='<product-item class="product-item " r...'>,
 <Selector xpath='descendant-or-self::product-item' data='<product-item class="product-item " r...'>,
 <Selector xpath='descendant-or-self::product-item' data='<product-item class="product-item " r...'>,
 <Selector xpath='descendant-or-self::product-item' data='<product-item class="product-item " r...'>,
 <Selector xpath='descendant-or-self::product-item' data='<product-item class="product-item " r...'>,
 <Selector xpath='descendant-or-self::product-item' data='<product-item class="product-item " r...'>,
 <Selector xpath='descendant-or-self::product-item' data='<product-item class="product-item " r...'>,
 <Selector xpath='descendant-or-self::product-item' data='<product-item class="product-item " r...'>,
 <Selector xpath='descendant-or-self::product-item' data='<product-item class="product-item " r...'>,
 <Selector xpath='descendant-or-self::product-item' data='<product-item class="product-item pro...'>,
 <Selector xpath='descendant-or-self::product-item' data='<product-item class="product-item " r...'>,
 <Selector xpath='descendant-or-self::product-item' data='<product-item class="product-item " r...'>,
 <Selector xpath='descendant-or-self::product-item' data='<product-item class="product-item " r...'>]

In [4]: 
```

#### Get First Product

To just get the first product we use `.get()` appended to the end of the command.

`response.css('product-item').get()`

This returns all the HTML in this node of the DOM tree.

```css
In [4]: response.css('product-item').get()
Out[4]: '<product-item class="product-item " reveal><div class="product-item__image-wrapper product-item__image-wrapper--multiple"><div class="product-item__label-list label-list"><span class="label label--custom">New</span></div><a href="/products/100-dark-hot-chocolate-flakes" class="product-item__aspect-ratio aspect-ratio aspect-ratio--square" style="padding-bottom: 100.0%; --aspect-ratio: 1.0">\n 
...
```

#### Get All Products

Now that we have found the DOM node that contains the product items, we will get all of them and save this data into a response variable and loop through the items and extract the data we need.

So can do this with the following command.

```
In [5]: products = response.css('product-item')
```

The products variable, is now an list of all the products on the page.

To check the length of the products variable we can see how many products are there.

`len(products)`

Here is the output:

```css
In [6]: len(products)
Out[6]: 24

```

#### Extract Product Details

Now lets extract the  **name** , **price** and **url** of each product from the list of products.

The products variable is a list of products. When we update our spider code, we will loop through this list, however, to find the correct selectors we will test the CSS selectors on the first element of the list `products[0]`.

##### Single Product - Get Single Product

`In [7]: product = products[0]`

##### Name - The product name can be found with

`product.css('a.product-item-meta__title::tex').get()`

```css
In [8]: product.css('a.product-item-meta__title::text').get()
Out[8]: '100% Dark Hot Chocolate Flakes'
```

##### Price - The product price can be found with

```css
product.css('span.price').get()
```

You can see that the data returned for the price has lots of extra HTML. We'll get rid of this in the next step.

```css
In [9]: product.css('span.price').get()
Out[9]: '<span class="price">\n              <span class="visually-hidden">Sale price</span>£9.95</span>'
```

To remove the extra span tags from our price we can use the `.replace()` method. The replace method can be useful when we need to clean up data.

Here we're going to replace the `<span>` sections with empty quotes `''`:

```css
product.css('span.price').get().replace(''<span class="price">\n              <span class="visually-hidden">Sale price</span>£9.95</span>', '').replace('</span', '')
```

```css
In [13]: product.css('span.price').get().replace('<span class="price">\n              <span class="visually-hidden">Sale price</span>', '').replace('</span>', '')
Out[13]: '£9.95'
```

**Product URL** - Next lets see how we can extract the product url for each individual product. To do that we can use the attrib function on the end of

```css
product.css('div.product-item-meta a').attrib['href']
```

```css
In [14]: product.css('div.product-item-meta a').attrib['href']
Out[14]: '/products/100-dark-hot-chocolate-flakes'
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

1. Makes a request to `'https://www.chocolate.co.uk/collections/all'`.
2. When it gets a response, it extracts all the products from the page using `products = response.css('product-item')`.
3. Loops through each product, and extracts the  **name** , **price** and **url** using the CSS selectors we created.
4. Yields these items so they can be stored in a CSV, JSON, DB, etc.

### Step 5: Running Our Spider

Now that we have a spider we can run it by going to the top level in our scrapy project and running the following command.

```apache
scrapy crawl chocolatespider
```

It will run, and you should see the logs on your screen. Here are the final stats:

```css
2023-03-06 16:40:41 [scrapy.statscollectors] INFO: Dumping Scrapy stats:
{'downloader/request_bytes': 960,
 'downloader/request_count': 2,
 'downloader/request_method_count/GET': 2,
 'downloader/response_bytes': 45614,
 'downloader/response_count': 2,
 'downloader/response_status_count/200': 2,
 'elapsed_time_seconds': 0.828502,
 'feedexport/success_count/FileFeedStorage': 1,
 'finish_reason': 'finished',
 'finish_time': datetime.datetime(2023, 3, 6, 16, 40, 41, 823425),
 'httpcompression/response_bytes': 222310,
 'httpcompression/response_count': 2,
 'item_scraped_count': 24,
 'log_count/DEBUG': 29,
 'log_count/INFO': 11,
 'memusage/max': 57987072,
 'memusage/startup': 57982976,
 'response_received_count': 2,
 'robotstxt/request_count': 1,
 'robotstxt/response_count': 1,
 'robotstxt/response_status_count/200': 1,
 'scheduler/dequeued': 1,
 'scheduler/dequeued/memory': 1,
 'scheduler/enqueued': 1,
 'scheduler/enqueued/memory': 1,
 'start_time': datetime.datetime(2023, 3, 6, 16, 40, 40, 994923)}
2023-03-06 16:40:41 [scrapy.core.engine] INFO: Spider closed (finished)
```

We can see from the above stats that our spider scraped 24 items:

`'item_scraped_count': 24`

If we want to save the data to a JSON file we can use the `-0` option, followed by the name of file.

`scrapy crawl chocolatespider -0 myscrapeddata.json`

Then a json file will be created in your project and that will contain your collection.

```css
[
{"name": "100% Dark Hot Chocolate Flakes", "price": "£9.95", "url": "/products/100-dark-hot-chocolate-flakes"},
{"name": "2.5kg Bulk 41% Milk Hot Chocolate Drops", "price": "£45.00", "url": "/products/2-5kg-bulk-of-our-41-milk-hot-chocolate-drops"},
{"name": "2.5kg Bulk 61% Dark Hot Chocolate Drops", "price": "£45.00", "url": "/products/2-5kg-of-our-best-selling-61-dark-hot-chocolate-drops"},
{"name": "41% Milk Hot Chocolate Drops", "price": "£8.75", "url": "/products/41-colombian-milk-hot-chocolate-drops"},
{"name": "61% Dark Hot Chocolate Drops", "price": "£8.75", "url": "/products/62-dark-hot-chocolate"},
{"name": "70% Dark Hot Chocolate Flakes", "price": "£9.95", "url": "/products/70-dark-hot-chocolate-flakes"},
{"name": "Almost Perfect", "price": "From £1.50\n", "url": "/products/almost-perfect"},
{"name": "Assorted Chocolate Malt Balls", "price": "£9.00", "url": "/products/assorted-chocolate-malt-balls"},
{"name": "Blonde Caramel", "price": "£5.00", "url": "/products/blonde-caramel-chocolate-bar"},
{"name": "Blonde Chocolate Honeycomb", "price": "£9.00", "url": "/products/blonde-chocolate-honeycomb"},
{"name": "Blonde Chocolate Honeycomb - Bag", "price": "£8.50", "url": "/products/blonde-chocolate-sea-salt-honeycomb"},
{"name": "Blonde Chocolate Malt Balls", "price": "£9.00", "url": "/products/blonde-chocolate-malt-balls"},
{"name": "Blonde Chocolate Truffles", "price": "£19.95", "url": "/products/blonde-chocolate-truffles"},
{"name": "Blonde Hot Chocolate Flakes", "price": "£9.95", "url": "/products/blonde-hot-chocolate-flakes"},
{"name": "Bulk 41% Milk Hot Chocolate Drops 750 grams", "price": "£17.50", "url": "/products/bulk-41-milk-hot-chocolate-drops-750-grams"},
{"name": "Bulk 61% Dark Hot Chocolate Drops 750 grams", "price": "£17.50", "url": "/products/750-gram-bulk-61-dark-hot-chocolate-drops"},
{"name": "Caramelised Milk", "price": "£5.00", "url": "/products/caramelised-milk-chocolate-bar"},
{"name": "Caramelised Milk Chocolate Tarte Tatin Chocolate Easter Egg", "price": "£29.95", "url": "/products/pre-order-toasted-sourdough-sea-salt-dark-chocolate-easter-egg"},
{"name": "Chocolate Caramelised Pecan Nuts", "price": "£8.95", "url": "/products/chocolate-caramelised-pecan-nuts"},
{"name": "Chocolate Celebration Hamper", "price": "£55.00", "url": "/products/celebration-hamper"},
{"name": "Christmas Truffle Selection", "price": "£19.95", "url": "/products/pre-order-christmas-truffle-selection"},
{"name": "Cinnamon Toast", "price": "£5.00", "url": "/products/cinnamon-toast-chocolate-bar"},
{"name": "Coconut Easter Egg", "price": "£29.95", "url": "/products/coconut-easter-egg"},
{"name": "Collection of 4 of our Best Selling Chocolate Malt Balls", "price": "£30.00", "url": "/products/collection-of-our-best-selling-chocolate-malt-balls"}
]
```

If we want to save the data to CSV file we can do so too.

`scrapy crawl chocolatespider -O myscrapeddata.csv`

### Step 6: Navigating to the "Next Page"

So far the code is working great but we're only getting the products from the first page of the site, the url which we have listed in the start_url variable.

So the next logical step is to go to the next page if there is one and scrape the item data from that too! So here's how we do that.

First, lets open our Scrapy shell again, fetch the page and find the correct selector to get the **next page** button.

`scrapy shell`
