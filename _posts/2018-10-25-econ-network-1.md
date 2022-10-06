---
layout:     post
title:      A snapshot of economics, part 1 - getting the data
date:       2018-10-25
summary:    Downloading the JEL codes of each article published in the field of economics in 2014 to make a network of the subfields of economis.
tags:       network web scraping python EconLit EBSCOhost
---

Back in 2015 Olena Chystiakova and I did a project for a Network Science course that might be interesting from a web scraping or data visualization perspective. I am going to present this project in a series of three short articles: I will start with getting the data (web scraping), continue with the visualization of the network, and conclude with modelling the network (the actual network science stuff). This is the first part of the series.

## The task

The project we had to do had quite loose requirements: we had to obtain a real-life network and then analyze it. As is often the case when getting such tasks, the most difficult part was deciding what exactly to analyze. In the end, we settled on a network representing economics: the subfields of economics, connected by articles that belong to multiple subfields. 

Fortunately, the American Economic Association has a system for classifying academic content in Economics: the system of [JEL (Journal of Economic Literature)](https://www.aeaweb.org/econlit/jelCodes.php?view=jel) codes. The classifications are hierarchical: the codes consist of a letter (main category) followed by two numbers (subcategories). An example JEL code is the following:

* J: Labor and demographic economics
  * J2: Time Allocation, Work Behavior, and Employment Determination and Creation; Human capital
    * J22: Time allocation and Labor supply

Almost all of the articles published in the field of economics (and most of the working papers too) are associated with usually 2-5 (self-declared) JEL codes. With this information in mind, the layout of the network is clear:

* nodes will represent the subfields of economics (JEL codes), and
* edges will represent articles in which a pair of JEL codes is featured simultaneously (or more specifically, the weight of the edges will represent the number of papers in which a pair of JEL codes is featured together).

All we need now is the data: a bunch of articles identifiers with the associated JEL codes.

## Getting the data

### Can we just scrape it?

At the time of this project we were studying at the Central European University, and therefore had access to *EconLit*, an index from the American Economic Association. The problem was that the service the university signed up for was designed for searching articles through services like *EBSCOhost* and viewing them one-by one, not for downloading bulk information. But if we can view them one-by-one, Python can also do the same. There is no need for us to sit there, it is a classic job for web scraping. 

Or is it?

Regarding web scraping, the first question should always be whether we can do it. Not in the sense that 'are we capable to do it?' - we most likely are. It might take a bit of poking around and trial and error, but (with the possible exception of CAPTCHAs and some other advanced anti-scraping measures) a script can usually simulate a human well enough to in order to harvest data. The more difficult (for most peaople trying to write a web scraper anyways) question is legal: are we allowed to do it?

The problem is that web scraping is often a legal grey zone. Contrary to common sense, harvesting the data from a webpage using a script might be legally problematic even if doing so by hand would be perfectly fine. And in some cases, even doing it by hand may be prohibited! Also, the consequences can be quite serious if the owner of the data decides to seek legal action. [This article](https://benbernardblog.com/web-scraping-and-crawling-are-perfectly-legal-right/) is a highly recommended read for anyone considering web scraping.

To see if we are in the clear with this project, let's start with the obvious: reading the [terms of service](https://www.ebsco.com/terms-of-use). For us, the relevant part is I.C:

> Licensee and Authorized Users agree to abide by the Copyright Act of 1976 \[...\] **Downloading all or parts of the Databases or Services in a systematic or regular manner** so as to create a collection of materials comprising all or part of the Databases or Services **is strictly prohibited** whether or not such collection is in electronic or print form. **Notwithstanding the above restrictions, this paragraph shall not restrict the use of the materials under the doctrine of "fair use"** as defined under the laws of the United States. Publishers may impose their own conditions of use applicable only to their content. \[...\]

There are two important parts here:
* According to the first part, what we are trying to do is strictly prohibited.
* However, the first part does not restrict the use of materials falling under *fair use*.

Now [fair use](https://guides.nyu.edu/fairuse) is a grey area in itself: it has no well defined boundaries, and the actual outcome of a lawsuit concerning it might very well depend on the interpretation of the court. However, in this case there are a few circumstances that point to our project being fair use:
* published works and factual, non-fiction works are more likely to qualify for fair use
* the use most likely does not result in economic harm to the creator or copyright owner
* it is used to create a derivative work
* it is used for research purposes
* the downloaded dataset will not be made public

Still, as fair use is not a well-defined category, in cases such as this, contacting the copyright/website owner might be a good idea. Also, although I am pretty confident that it was actually fair use, I am not a lawyer, so I could be completely and utterly wrong, and my reasoning may not be worth a pair of dingo's kidneys. The point is, take the stuff I write with a grain of salt. (Taking any legal advice you get from strangers on the internet with a grain of salt might also be a good general rule.)

Also, I am sorry about not sharing the resulting dataset. I would really like to, as it has many possibilities for research and visualization, but I don't want to risk it. If [LinkedIn went after anonymous people scraping their site this seriously](https://digitalcommons.law.scu.edu/cgi/viewcontent.cgi?referer=https://benbernardblog.com/&httpsredir=1&article=2261&context=historical), I would not like to be on the wrong side of [academic publishers](https://arstechnica.com/tech-policy/2017/06/scientific-research-piracy-site-hit-with-15-million-fine/) and service providers.

### Let's just scrape it!

Now that we are past the poring part, it is time to get to the actual programming. One last warning though: I am not sharing this code to use it for scraping EBSCOhost specifically - I just want to illustrate how programmatically downloading complex sites can be done.

Scraping EBSCOhost is going to more challenging than doing the same with a simple static html resource. We will have to deal with user sessions, AJAX and such complications. In such a case, the elegant solution would be familiarizing ourselves with the site in order to replicate the necessary AJAX calls, and use a simple HTTP library such as `requests` to download make the, well, requests. In this particular case however, automating an actual web browser seemed like a much simpler (albeit probably slower, but one should not make too many requests too fast anyways) thing to do. The way EBSCOhost search works makes this strategy especially productive.

Now would be the time to include some screenshots of the site in question, but, alas, I do not have any, and do not have access to this service anymore. However, the most important aspects about how it works (or worked in 2015) can be easily summarized. You can make a search by using a set of filters, and you will get a paginated view of the resulting articles (just like google, really). If you click on one of them, you will get its details (such as the JEL codes, yay!) - no surprises this far. The best part come now: when a result is open, there are previous and next article buttons at the bottom of the page, with which you can cycle through the *search results*! Also, the link when an article is open can be safely copied to another browser, and you get the exact same situation (same search parameters, same article).

So in theory, the procedure should be quite simple:
1. Use your favourite browser to make a search with the desired filters (say, all articles published in 2014)
2. Open the first result
3. Navigate to the link of the first result using an automated browser
4. Keep saving the information on the current page and pressing the next button until no more articles are left

As there are going to be plenty of exceptions (internet connection error, expired session, etc.), it might be useful to make the scraper object a *context manager*, so that all resources are closed in case of an exception without the excessive use of `try...catch` blocks. Doing so only requires us to declare an `__enter__` and an `__exit__` method. The nice thing is that the latter will be executed even if an exception occurs.

The downloaded data is going to be stored in an SQLite database, and I am going to use `PhantomJS` automated by `selenium` as my web browser (Mr. Browser). The class starts like this:


```python
import time
import sqlite3
from selenium import webdriver
from selenium.common.exceptions import NoSuchElementException
from bs4 import BeautifulSoup
import re

class EbscoScraper:

    def __init__(self, start_url, database_path, first_parsed=False):

        self.start_url = start_url
        self.database_path = database_path
        self.parsed = first_parsed

        self.conn = None
        self.c = None
        self.mr_browser = None

    def __enter__(self):
        self.conn, self.c = self.init_database()
        self.mr_browser = self.init_browser()
        if self.parsed:
            self.load_next_page()
        return self    

    def __exit__(self, exc_type, exc_val, exc_tb):
        if self.conn is not None: self.conn.close()
        if self.mr_browser is not none: self.mr_browser.quit()
```

Nothing surprising in these methods. The constructor method needs a starting URL and a file path for the database. (The optional argument is there because it often happens that the last loaded article is successfully parsed, but the next one cannot be loaded. In that case, we want to restart it from the last known url, but do not want to parse and store it again.) The `__enter__` method initializes the database connection and the (headless) browser. Finally, the `__exit__` method closes both of them.

Next, the methods handling the database. The `CREATE TABLE IF NOT EXISTS` ensures that the same function can be used for creating a new database and reopening an existing one.


```python
    def init_database(self):
        """Open the connection to an sqlite database, and create the table articles
           if it does not exist."""
        conn = sqlite3.connect(self.database_path)
        c = self.conn.cursor()
        c.execute('''CREATE TABLE IF NOT EXISTS articles
                     (an INTEGER, author TEXT, title TEXT, jel TEXT, keywords TEXT)''')
        conn.commit()
        return (conn, c)
            
    def enter_into_db(self, dct):
        """Enter data from a dictionary into the open sqlite database."""
        try:
            self.c.execute('''INSERT INTO articles (an, author, title, jel, keywords)
                            VALUES (?, ?, ?, ?, ?)''', 
                            (dct['an'], dct['author'], dct['title'], dct['jel'], dct['keywords'])
                      )
            self.conn.commit()
        except sqlite3.OperationalError:
            print('Writing into the database has failed')
            print('current url: {}'.format(self.mr_browser.current_url))
            raise
```

Then the methods to control the browser. Both are quite self explanatory: `init_browser` opens a browser and loads the page under `start_url`, while `load_next_page` clicks the next article button. If it cannot find the button, we are probably not on the expected page. In that case it makes a screenshot, and reraises the exception to make the scraping stop.


```python
    def init_browser(self):
        """Initialize the browser and open the page under start_url."""
        mr_browser = webdriver.PhantomJS()
        mr_browser.set_window_size(1280, 1024)
        mr_browser.get(self.start_url)
        return mr_browser
        
    def load_next_page(self):
        """Find and click on the next article button."""
        try:
            next_btn = self.mr_browser.find_element_by_id(
                'ctl00_ctl00_MainContentArea_MainContentArea_topNavControl_btnNext'
                )
            next_btn.click()
        except NoSuchElementException:
            if self.mr_browser.current_url == 'about:blank':
                print('Please check your internet connection.')
            else:
                self.mr_browser.save_screenshot('error.png')
                print('The page is not as expected, screenshot saved.')
                print('url: {}'.format(self.mr_browser.current_url))
            raise
```

We use `BeautifulSoup4` to parse the page, find the necessary elements, and extract the information. One only needs to inspect the source HTML/XML to do it. The most important fields we pull are the JEL codes (obviously), the keywords and the authors, as all of these can be used to construct various networks.


```python
    def parse_page(self):

        soup = BeautifulSoup(self.mr_browser.page_source)

        dt_tags = soup.find_all('dt', attrs = {'data-auto': 'citation_field_label'})
        field_names = [tag.string[:-1] for tag in dt_tags]

        dd_tags = soup.find_all('dd', attrs = {'data-auto': 'citation_field_value'})
        field_values = [tag.text for tag in dd_tags]

        pagedict = dict(zip(field_names, field_values))

        needed_fields = ['Accession Number', 'Author', 'Title', 'Descriptors', 'Keywords']
        for field in needed_fields:
            if field not in pagedict.keys():
                pagedict[field] = ''

        re_pattern = r'\([A-Z]\d\d\)'
        descriptors_list = [item[1:-1] for item in re.findall(re_pattern, pagedict['Descriptors'])]
        descriptors = '; '.join(descriptors_list)
        keywords = ' '.join(pagedict['Keywords'].split())
        
        finaldict = {'an': pagedict['Accession Number'],
                     'author': pagedict['Author'],
                     'title': pagedict['Title'],
                     'jel': descriptors,
                     'keywords': keywords
                     }
                     
        return finaldict
```

Finally, we go through all of the pages and save the relevant information one by one. We do this in a loop.


```python
    def parse_n_pages(self, num_of_pages, interval=1):
        """Load and parse num_of_pages search results, including the current page."""

        for i in range(num_of_pages):

            t0 = time.time()

            dct = self.parse_page()
            if not all([key == '' for key in dct.keys()]):
                self.enter_into_db(dct)
            else:
                print('No useful information on {}.'.format(self.mr_browser.current_url))

            if i < num_of_pages - 1:
                self.load_next_page()

            if (i + 1) % 50 == 0:
                print('{} of {} articles parsed and saved.'.format(i + 1, num_of_pages))

            time.sleep(max(0, t0 + interval - time.time()))
        
        print('Finished saving and parsing all {} articles.'.format(num_of_pages))
```

The scraper is ready for action now. It can be used like this:

```python
with EbscoScraper(start_url, database_path) as mr_scraper:
    mr_scraper.parse_n_pages(num_of_pages)
```

Let it run for some hours, restart it a few times if it stops, and you will have the data in a convinient SQLite format. In our case, data on 37320 articles (all of the EBSCO search results for articles published in 2014).

In the next part of the series, I will continue with making a network out of this data, and visualizing that network. Stay tuned!
