python-htmlparser
=================

Python 3.x HTMLParser extension with ElementTree support.


Why another Python HTML Parser?
-----

There is no HTML Parser in the Python Standard Library.
Actually, there is the html.parser.HTMLParser that simply traverses the DOM tree and allows us to be notified as each tag is being parsed.

Usually, when we parse HTML we want to query its elements and extract data from it.
The most simple way to do this is to use XPath expressions.
Python do support a simple (read limited) XPath engine into its ElementTree, but there is no way to parse an HTML document into XHTML and then use this library to query it.

This HTML Parser extends html.parser.HTMLParser returning an xml.etree.Element instance (the root element) which natively supports the ElementTree API.

You may use this code however you like.
You may even copy-paste it into your project in order to keep the result clean and simple (a comment to this source is welcome!).


But... wait!
-----

As the filename implies, this is a very naive approach to this problem.
If you really need (or may use) a fully-fledged parsing library, [lxml](http://lxml.de/) and [BeautifulSoup](http://www.crummy.com/software/BeautifulSoup/) are arguably the most used.


Example
-----

```python
html = """
<html>
  <head>
    <title>GitHub</title>
  </head>
  <body>
    <a href="https://github.com/marmelo">GitHub</a>
    <a href="https://github.com/marmelo/python-htmlparser">GitHub Project</a>
  </body>
</html>
"""

parser = NaiveHTMLParser()
root = parser.feed(html)
parser.close()

# root is an xml.etree.Element and supports the ElementTree API
# (e.g. you may use its limited support for XPath expressions)

# get title
print(root.find('head/title').text)

# get all anchors
for a in root.findall('.//a'):
    print(a.get('href'))

# for more information, see:
# http://docs.python.org/2/library/xml.etree.elementtree.html
# http://docs.python.org/2/library/xml.etree.elementtree.html#xpath-support
```

Output:
```
GitHub
https://github.com/marmelo
https://github.com/marmelo/python-htmlparser
```
