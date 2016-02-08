Introduction, installation, and usage
-------------------------------------

This is a [Python 2] [1] and [Scrapy] [2]–based web scraper that collects the results of the 2015 general election from the BBC's website. A list of the constituencies is scraped from the [starting page] [3], and then for each constituency the candidates and their parties, votes, vote share, and swing are collected. The whole process takes less than two minutes.

To run it you need to first [install Scrapy] [4]. Clone this repo if you haven't already and make its root your current directory. Then run:

    scrapy crawl bbc -o output.csv

Where `output.csv` is the name of the file in which you want to store the scraper's data. Wait a couple of minutes and you'll have a file with the same content as [`data/candidates.csv`] [5].

Using the data
--------------

The latest version of the scraped data (a CSV file) is always available from `http://data.flother.is/uk-general-election-2015`. You can use this URL to access the data from anywhere, including the command-line — for example, let's list the constituencies that had ten or more candidates:

    $ curl -sL http://data.flother.is/uk-general-election-2015 | q -HOTd , "SELECT COUNT(constituency) AS num_candidates, constituency FROM - GROUP BY constituency HAVING num_candidates >= 10 ORDER BY num_candidates DESC"
    num_candidates	constituency
    13	Uxbridge & Ruislip South
    12	Witney
    11	Bethnal Green & Bow
    11	Camberwell & Peckham
    11	Hackney South & Shoreditch
    11	Thanet South
    10	Bridgend
    10	Lewisham Deptford
    10	North Down
    10	Sheffield Central
    10	Vauxhall

(Here I used [cURL] [6] and [q] [7] to download the data and run an SQL query on the CSV.)

Testing
-------

The code contains a minimal amount of testing in the form of [Scrapy contracts] [8] ([example] [9]). If you want to check that the data is scraped from the BBC as expected (i.e. their markup hasn't changed drastically), run:

    scrapy check bbc

If there are no errors it's a good indicator the data will be sound.

Licence
-------

This repository is released under the MIT Licence. See the [LICENSE] [10] file for details.

Support
-------

* Home page: https://github.com/flother/bbc-election-results
* Issues: https://github.com/flother/bbc-election-results/issues


[1]: https://www.python.org/
[2]: http://scrapy.org/
[3]: http://www.bbc.co.uk/news/politics/constituencies
[4]: http://doc.scrapy.org/en/1.0/intro/install.html
[5]: https://github.com/flother/bbc-election-results/blob/master/data/candidates.csv
[6]: https://curl.haxx.se/
[7]: https://github.com/harelba/q/
[8]: http://doc.scrapy.org/en/latest/topics/contracts.html
[9]: https://github.com/flother/bbc-election-results/blob/6ab0a34f988d3b5cb22b95a39b0f1151064b7ddd/candidates/spiders/bbc.py#L37-L40
[10]: https://github.com/flother/bbc-election-results/blob/master/LICENSE
