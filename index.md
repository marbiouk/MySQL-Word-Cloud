---
layout: default
---

*If you...*

- **have a blog...**  
- **have a database...**    
- **or have any data at all...**  

***and you just want a word cloud...then you have come to the right place!***   
<br>
####1. &nbsp; **Extract**####

Download the zip/tar or clone the [Git Repo](https://github.com/mattedgod/MySQL-Word-Cloud) into a directory in your jQuery enabled web site.  

<br>
####2. &nbsp; **Include**####

Add a `<SCRIPT>` tag for the jQuery plugin to the `<HEAD>` section of your site:
	
{% highlight html %}
<script type="text/javascript" src="wordcloud/jquery.wordcloud.js"></script>
{% endhighlight %}
	
and a `<CANVAS>` tag where you want the cloud to appear in the `<BODY>` section of your site:
	
{% highlight html %}
<canvas id="cloudcanvas" width="600" height="400"></canvas>
{% endhighlight %}

<br>
####3. &nbsp; **Connect**####

After the [DOM is ready](http://api.jquery.com/ready/), call the `wordCloud` function on the canvas jQuery object with your database credentials.
		
{% highlight js %}
$("#cloudcanvas").wordCloud({
	database: {
		dbHost: <your database host>,
		dbUser: <your datbase username>,
		dbPass: <your database password>,
		dbName: <your database name>,
		selectFields: <comma separated list of fields to select>,
		tableName: <database table to select from>
	}
});
{% endhighlight %}

<br>