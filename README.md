# THIS IS A FORK....

Notes:
* Apesmit was originally written by Florian Diesch at https://www.florian-diesch.de/software/apesmit/
* It was then forked to remove the Python3-only flag since it works with Python 2, ie https://pypi.org/project/apesmit-py2/
* 2017M12 - I then had to fork to change the PyPi link to https, due to https://mail.python.org/pipermail/distutils-sig/2017-October/031714.html
* 2018M03 - And to add support for image sitemaps, ie https://support.google.com/webmasters/answer/178636?hl=en

---


What is ApeSmit?
================

ApeSmit is a very simple Python module to create XML sitemaps
as defined at http://www.sitemaps.org. ApeSmit doesn't contain any web
spider or something like that, it just writes the data you provide to
a file using the proper syntax.


Usage
=====

First we create an instance of `SiteMap`:

```python
sm=Sitemap(changefreq='weekly')
```

The ``changefreq`` keyword sets a default value for that parameter.

Now we add some URL's to our sitemap:

```python
sm.add('http://www.example.com/')
```

We may use some parameters:

```python
sm.add('http://www.example.com/news/',
    changefreq='daily',
    priority=1.0, 
    lastmod='1891-1-1')
```

There's a shortcut for URL's that changed today:

```python
sm.add('http://www.example.org/about.html', lastmod='today')
```

We may add child image elements:

```python 
sm.add('http://www.example.com/news/', 
    changefreq='daily',
    priority=1.0,
    lastmod='1891-1-1',
    images = [{
        'loc': 'http://example.com/image.jpg',
        
        # These are optional
        'caption': 'Some caption',
        'geo_location': 'London, UK', 
        'title': 'Some title',
        'license': 'https://example.com/license'
     }]
)
```

That's all for now. Next we need a file to write the sitemap in:

```python
out=open('sitemap.xml', 'w')
``` 

Now we write our sitemap and then close the file:

```python
sm.write(out)
out.close()
```


And that's the content of our shiny new sitemap::

  <?xml version='1.0' encoding='UTF-8'?>
  <urlset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9
          http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd"
          xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
   <url>
    <loc>http://www.example.com/</loc>
    <changefreq>weekly</changefreq>
   </url>
   <url>
    <loc>http://www.example.com/news/</loc>
    <lastmod>1891-1-1</lastmod>
    <changefreq>daily</changefreq>
    <priority>1.0</priority>
   </url>
   <url>
    <loc>http://www.example.org/about.html</loc>
    <lastmod>2008-04-03</lastmod>
    <changefreq>weekly</changefreq>
   </url>
  </urlset>
