Cookie Audit
============

Ed Crewe, 18 July 2011

UK and European Cookie laws
---------------------------

The current UK Law requires full compliance by May 2012

http://www.ico.gov.uk/news/current_topics/website_changes_pecr.aspx

Auditing tools
--------------

The main audit tool that is currently available is browser based only

http://www.primelife.eu/results/opensource/76-dashboard

a plugin for Firefox. Although very useful it is not so suited to a
full automatic audit of a website, since it is dependent on the user manually 
clicking around the site. 

It could potentially be automated by, for example, installing the plugin then
driving Firefox with spidering system* and the privacy dashboard plugin across a whole site, 
but this seems a rather top heavy inelegant way of doing it, when spiders themselves
can retrieve the cookies.

This software is a set of configuration scripts for one such spider, Scrapy.

http://scrapy.org/ 

Installation details on the site, or alternatively install fabric and virtualenv
then run the fabfile in this directory.

* Scrapy has the option to use Firefox as its client for crawls, 
  alternatively Selenium could also be used to drive it.    

Auditing your domain
--------------------

The aim of this package is to provide a crawler that will 
provide a full audit of cookie usage across a domain.

As a first step in ensuring compliance with UK law by the deadline.

Code details
------------

The cookie scraper is in the subfolder cookie_audit whilst cookie_report is
a django reporting tool for the audit.

COOKIES

Cookie audit works by enabling Scrapy's cookie handling, this uses the standard
python cookielib library in scrapy/http/cookies.py

The cookie middleware simply opens the crawler's cookie jar and writes the cookielib 
properties of each cookie out, along with the page heading and url of the page
that set it. This cookie writing middleware can be applied to any spidering.

DOMAIN SPIDER

Each URL crawled is also recorded, within spiders/domain_spider, a recursive spider
that you set to crawl DOMAINS = ['yourdomain.com','yourotherdomain.com'] in 
cookie_audit/settings.py
URLs crawled and their associated metadata are recorded.

JSON PIPELINE

If it is not desired to run a full Django reporting tool, then the JSON pipeline can be 
used to just write results to a cookies.json and crawled.json file.

COOKIE REPORT

This uses Scrapy's DjangoItem to provide models to django for building reports and
providing a default admin interface for cookie browsing.

The report allows selection of cookies by type etc.

 
