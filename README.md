# Simple Web Crawler

This repository contains a web crawler built using the Scrapy framework. The crawler is designed to scrape book information from the website [Books to Scrape](http://books.toscrape.com/). 

## Installation

1. Clone the repository:
    ```bash
    git clone https://github.com/MuniirAhmadi/web-crawler-python.git
    cd mycrawler
    ```

2. Install the required dependencies:
    ```bash
    pip install scrapy
    ```

## Usage

To start the crawler and save the output in a JSON file, run the following command:
```bash
scrapy crawl mycrawler -o output.json
```

## Configuration

### Proxy Server Setup

To use a proxy server, you need to configure the `settings.py` and `middlewares.py` files.

1. Open `settings.py` and uncomment the `DOWNLOADER_MIDDLEWARES` section:
    ```python
    DOWNLOADER_MIDDLEWARES = {
        "scrapy.downloadermiddlewares.httpproxy.HttpProxyMiddleware": 1,
        "mycrawler.middlewares.WebscraperDownloaderMiddleware": 543,
    }
    ```

2. Open `middlewares.py` and modify the `process_request` method:
    ```python
    def process_request(self, request, spider):
        request.meta['proxy'] = "actual_proxy_server_address"
    ```
    Replace `actual_proxy_server_address` with the address of your proxy server.

## Customizing the Crawler

The crawler can be customized by modifying the `CrawlingSpider` class in `spiders/crawling_spider.py`.

To test XPath and CSS selectors in the Scrapy shell, you can use:
```bash
scrapy shell https://books.toscrape.com/index.html
```

In the Scrapy shell, you can try out different selectors:
```
response
response.css("h1")
response.css("a::text").getall()
response.css(".page-header").get()
response.xpath("//a/text()")
```
