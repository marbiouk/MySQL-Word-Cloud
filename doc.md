---
layout: default
---

###Documentation###

The MySQL Word Cloud basically uses two steps to generate the word cloud in the HTML5 Canvas element. The configuration options for both steps are passed through the jQuery call to `wordCloud(...)`.

The first step in the process is done server-side via PHP and is responsible for connecting to the database and computing the frequency of words.

The second step in the process is done client-side via JavaScript/jQuery and is responsible for rendering an SVG word cloud inside of the canvas element specified. I cannot take credit for this part, most of it was done by [timdream](https://github.com/timdream).

####JavaScript Rendering Options####

The `wordCloud` jQuery function takes a javascript object as it's only parameter. This object can contain several parameters that control the appearance of the resulting word cloud.

Many of these parameters can be found in the [comments of the original wordcloud plugin](https://github.com/timdream/wordcloud/blob/master/jquery.wordcloud.js), developed by [timdream](https://github.com/timdream).

Some additional parameters have been added as well:

- **wordCoundUrl** : *(optional, but suggested)*

	The URL of the algorithm to use for the word frequency calculations. To use the bundled PHP frequency calculation algorithm pass `freq/wordcounter.php` in this parameter. If this parameter is ignored, left blank, or null, no ajax request will be executed and you will probably want to pass something to the **wordList** parameter if you expect to see anything in your word cloud.
	
- **biggestWord** : *(optional)*

	The SVG font size to use for the most frequently seen word. If this parameter is not included the font sizes will be equal to the number of times each word is detected. This is often not ideal because it is possible the most frequent word was seen a very high or very low number of times. All other words will be scaled accordingly. I personally like to use a number ~25-40% of my total canvas width in pixels here but you can experiment.

####Database Connection/Query Options####

The following options control the querying of the MySQL database. They are all passed to the `wordCloud` function along with other word cloud options under the `database : {}` object. 

- **dbHost** : *(default : the host specified in `freq/connections.php`)* 

	The database host. Note: If your database is on a different host than your web server, you may need to [enable MySQL Remote Access](http://www.cyberciti.biz/tips/how-do-i-enable-remote-access-to-mysql-database-server.html)

- **dbUser** : *(default : the username specified in `freq/connections.php`)* 

	The username used to connect to the database

- **dbPass** : *(default : the password specified in `freq/connections.php`)*
 
	The password used to connect to the database

- **dbName** : *(required)* 

	The name of the database to query

- **selectFields** : *(default : \*)* 

	A comma-separated list of fields to query. Every field specified in this list will be split and considered in the word frequency calculation. Therefore, it is probably unlikely that you want to select primary keys, dates, integers, etc. Use the **where** parameter as your friend.

- **tableName** : *(required)*

	The table name containing the data that will be used for word frequency calculation. Note: At this time only 1 table per word cloud is supported.

- **where** : *(default : TRUE)*

	A where clause to filter down the data returned by **table**. Columns included in the where clause will *not* necessarily be included in the word frequency calculation. Add them to **selectFields** if that is the intent.

- **limit** : *(default : 5000)*

	The maximum number of records in the table to process for word frequency calculations. Take caution in *raising* this number. Computing frequencies for many records can cause some significant strain on your PHP process if you aren't careful.

- **order** : *(default : NULL)*

	An optional order by clause to use in the query. You will probably only want to use this if you would be exceeding the **limit** in number of rows in your table.

- **excludedWords** : *(default : "")*

	A *space-separated* list of words to not include in the word frequency calculations. Note: There is a file `freq/stopwords.php` that contains common English words, this parameter is meant to be used for more specific scenarios (i.e. You have a blog about cats so you don't want to see the word "cat" in your word cloud)

- **maxWords** : *(default : 0)*

	The maximum number of words to return back in the word frequency calculation. Note that this paramter differs from **limit** in that it limits the number of returned words rather than the number of rows proceess. For example, a call with `limit = 5000` and `maxWords = 50` will return the 50 most-frequently-seen words in the first 5,000 records in the database. The words returned will always be the most-frequent. This means that at some point the word frequency calculation algorithm will have to compute the frequencies of *all* words, sort the list, and then return the top **maxWords** from it. 0 means no maximum, all words will be returned.