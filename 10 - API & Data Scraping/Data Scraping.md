It's used when the website doesn't have an API or if the API is expensive or slow.
It's legal for personal use, otherwise not.

### Tool
The tools to data scraping are
- [[Selenium]]
	it was develop to **automate website testing** but at the end used for data scraping 
	It simulate **clicks, drags, scrolls** and **other interaction** with a website 
		or wait for a specific piece to load)
	[[DOM - Document Object Model]]

- [[BeautifulSoup]]
	Use HTML (XML) parser
	HTML (XML) parser
	Use **API to navigate in the webpage** and identify elements within the HTML code

### Comparison
The combination of the two presented modules is the basis for a web scraper
![[Pasted image 20250427103826.png]]

[[Selenium]] **interact** with the **webpage and simulate** **user interactions** and retrieves the final HTML content 

[[ BeautifulSoup]] **processes the structure** of HTML and **locates specific elements** and **extracts text, attributes, or other information** 
	 can save extracted data in the database

### Protection
Some sites have some protection against Data Scraping.
They are able to detect weird behaviors and prevent you from scraping!
	- Website changed the shape of HTML code (it might happens every time you load the website or after a long or short time)
	- some websites have **dynamic-generated content** (e.g.: like, reviews, comment) loaded only when you scroll or click a button.

#API