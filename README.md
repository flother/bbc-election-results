Introduction, installation, and usage
-------------------------------------

This is a [Python 2] [1] and [Scrapy] [2]–based web scraper that collects the results of the 2015 general election from the BBC's website. A list of the constituencies is scraped from the [starting page] [3], and then for each constituency the candidates and their parties, votes, vote share, and swing are collected. The whole process takes less than two minutes.

To run it you need to first [install Scrapy] [4]. Clone this repo if you haven't already and make its root your current directory. Then run:

    scrapy crawl bbc -o output.csv

Where `output.csv` is the name of the file in which you want to store the scraper's data. Wait a couple of minutes and you'll have a file with the same content as [`data/candidates.csv`] [5].

Testing
-------

The code contains a minimal amount of testing in the form of [Scrapy contracts] [6] ([example] [7]). If you want to check that the data is scraped from the BBC as expected (i.e. their markup hasn't changed drastically), run:

    scrapy check bbc

If there are no errors it's a good indicator the data will be sound.

Licence
-------

This repository is released under the MIT Licence. See the [LICENSE] [8] file for details.

Support
-------

* Home page: https://github.com/flother/bbc-election-results
* Issues: https://github.com/flother/bbc-election-results/issues


[1]: https://www.python.org/
[2]: http://scrapy.org/
[3]: http://www.bbc.co.uk/news/politics/constituencies
[4]: http://doc.scrapy.org/en/1.0/intro/install.html
[5]: https://github.com/flother/bbc-election-results/blob/master/data/candidates.csv
[6]: http://doc.scrapy.org/en/latest/topics/contracts.html
[7]: https://github.com/flother/bbc-election-results/blob/6ab0a34f988d3b5cb22b95a39b0f1151064b7ddd/candidates/spiders/bbc.py#L37-L40
[8]: https://github.com/flother/bbc-election-results/blob/master/LICENSE