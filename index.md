---
layout: default
---

*If you...*

- **have a blog...**  
- **have a database...**    
- **or have any data at all...**  

***and you just want a word cloud...then you have come to the right place!***   
<br>
###HTML5 Word Cloud as easy as 1...2...3

1. **Extract**

	Download the zip/tar or clone the [Git Repo](https://github.com/mattedgod/MySQL-Word-Cloud) into a directory in your jQuery enabled web site.
	
2. **Include**

	Add a `<SCRIPT>` tag for the jQuery plugin to the `<HEAD>` section of your site:
	
	``` html
	<script type="text/javascript" src="wordcloud/jquery.wordcloud.js"></script>
	```
	
	and a `<CANVAS>` tag where you want the cloud to appear in the `<BODY>` section of your site:
	
	``` html
	<canvas id="cloudcanvas" width="600" height="400"></canvas>
	```

3. **Connect**

	After the [DOM is ready](http://api.jquery.com/ready/), call the `wordCloud` function on the canvas jQuery object with your database credentials.
		
	``` js
	$("#cloudcanvas").wordCloud({
		database: {
			dbHost: <your database host>,
			dbUser: <your datbase username>,
			dbPass: <your database password>,
			dbName: <your database name>,
			selectFields: <comma separated list of fields to select>,
			tableName: <database table to select from>,
		}
	});
	```