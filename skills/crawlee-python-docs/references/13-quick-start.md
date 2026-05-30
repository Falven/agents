# Quick start

This short tutorial will help you start scraping with Crawlee in just a minute or two. For an in-depth understanding of how Crawlee works, check out the [Introduction](https://crawlee.dev/python/python/docs/introduction.md) section, which provides a comprehensive step-by-step guide to creating your first scraper.

## Choose your crawler[​](#choose-your-crawler "Direct link to Choose your crawler")

Crawlee offers the following main crawler classes: [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md), [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md), and [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md). All crawlers share the same interface, providing maximum flexibility when switching between them.

Minimum Python version

Crawlee requires Python 3.10 or higher.

### BeautifulSoupCrawler[​](#beautifulsoupcrawler "Direct link to BeautifulSoupCrawler")

The [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md) is a plain HTTP crawler that parses HTML using the well-known [BeautifulSoup](https://pypi.org/project/beautifulsoup4/) library. It crawls the web using an HTTP client that mimics a browser. This crawler is very fast and efficient but cannot handle JavaScript rendering.

### ParselCrawler[​](#parselcrawler "Direct link to ParselCrawler")

The [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md) is similar to the [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md) but uses the [Parsel](https://pypi.org/project/parsel/) library for HTML parsing. Parsel is a lightweight library that provides a CSS selector-based API for extracting data from HTML documents. If you are familiar with the [Scrapy](https://scrapy.org/) framework, you will feel right at home with Parsel. As with the [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md), the [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md) cannot handle JavaScript rendering.

### PlaywrightCrawler[​](#playwrightcrawler "Direct link to PlaywrightCrawler")

The [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) uses a headless browser controlled by the [Playwright](https://playwright.dev/) library. It can manage Chromium, Firefox, Webkit, and other browsers. Playwright is the successor to the [Puppeteer](https://pptr.dev/) library and is becoming the de facto standard in headless browser automation. If you need a headless browser, choose Playwright.

## Installation[​](#installation "Direct link to Installation")

Crawlee is available the [`crawlee`](https://pypi.org/project/crawlee/) package on PyPI. This package includes the core functionality, while additional features are available as optional extras to keep dependencies and package size minimal.

You can install Crawlee with all features or choose only the ones you need. For installing it using the [pip](https://pip.pypa.io/en/stable/) package manager, run the following command:

```
python -m pip install 'crawlee[all]'
```

Verify that Crawlee is successfully installed:

```
python -c 'import crawlee; print(crawlee.__version__)'
```

If you plan to use the [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md), you'll need to install Playwright dependencies, including the browser binaries. To do this, run the following command:

```
playwright install
```

For detailed installation instructions, see the [Setting up](https://crawlee.dev/python/python/docs/introduction/setting-up.md) documentation page.

## Crawling[​](#crawling "Direct link to Crawling")

Run the following example to perform a recursive crawl of the Crawlee website using the selected crawler.

* BeautifulSoupCrawler
* ParselCrawler
* PlaywrightCrawler

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBCZWF1dGlmdWxTb3VwQ3Jhd2xlciBjcmF3bHMgdGhlIHdlYiB1c2luZyBIVFRQIHJlcXVlc3RzXFxuICAgICMgYW5kIHBhcnNlcyBIVE1MIHVzaW5nIHRoZSBCZWF1dGlmdWxTb3VwIGxpYnJhcnkuXFxuICAgIGNyYXdsZXIgPSBCZWF1dGlmdWxTb3VwQ3Jhd2xlcihtYXhfcmVxdWVzdHNfcGVyX2NyYXdsPTEwKVxcblxcbiAgICAjIERlZmluZSBhIHJlcXVlc3QgaGFuZGxlciB0byBwcm9jZXNzIGVhY2ggY3Jhd2xlZCBwYWdlXFxuICAgICMgYW5kIGF0dGFjaCBpdCB0byB0aGUgY3Jhd2xlciB1c2luZyBhIGRlY29yYXRvci5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG4gICAgICAgICMgRXh0cmFjdCByZWxldmFudCBkYXRhIGZyb20gdGhlIHBhZ2UgY29udGV4dC5cXG4gICAgICAgIGRhdGEgPSB7XFxuICAgICAgICAgICAgJ3VybCc6IGNvbnRleHQucmVxdWVzdC51cmwsXFxuICAgICAgICAgICAgJ3RpdGxlJzogY29udGV4dC5zb3VwLnRpdGxlLnN0cmluZyBpZiBjb250ZXh0LnNvdXAudGl0bGUgZWxzZSBOb25lLFxcbiAgICAgICAgfVxcbiAgICAgICAgIyBTdG9yZSB0aGUgZXh0cmFjdGVkIGRhdGEuXFxuICAgICAgICBhd2FpdCBjb250ZXh0LnB1c2hfZGF0YShkYXRhKVxcbiAgICAgICAgIyBFeHRyYWN0IGxpbmtzIGZyb20gdGhlIGN1cnJlbnQgcGFnZSBhbmQgYWRkIHRoZW0gdG8gdGhlIGNyYXdsaW5nIHF1ZXVlLlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5lbnF1ZXVlX2xpbmtzKClcXG5cXG4gICAgIyBBZGQgZmlyc3QgVVJMIHRvIHRoZSBxdWV1ZSBhbmQgc3RhcnQgdGhlIGNyYXdsLlxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vY3Jhd2xlZS5kZXYnXSlcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6MTAyNCwidGltZW91dCI6MTgwfX0.FYzSLWHZpPu5EwJQM8QlYHBOPN8ym0fJsoJsr5RP2AY\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


async def main() -> None:
    # BeautifulSoupCrawler crawls the web using HTTP requests
    # and parses HTML using the BeautifulSoup library.
    crawler = BeautifulSoupCrawler(max_requests_per_crawl=10)

    # Define a request handler to process each crawled page
    # and attach it to the crawler using a decorator.
    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')
        # Extract relevant data from the page context.
        data = {
            'url': context.request.url,
            'title': context.soup.title.string if context.soup.title else None,
        }
        # Store the extracted data.
        await context.push_data(data)
        # Extract links from the current page and add them to the crawling queue.
        await context.enqueue_links()

    # Add first URL to the queue and start the crawl.
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQYXJzZWxDcmF3bGVyLCBQYXJzZWxDcmF3bGluZ0NvbnRleHRcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgICMgUGFyc2VsQ3Jhd2xlciBjcmF3bHMgdGhlIHdlYiB1c2luZyBIVFRQIHJlcXVlc3RzXFxuICAgICMgYW5kIHBhcnNlcyBIVE1MIHVzaW5nIHRoZSBQYXJzZWwgbGlicmFyeS5cXG4gICAgY3Jhd2xlciA9IFBhcnNlbENyYXdsZXIobWF4X3JlcXVlc3RzX3Blcl9jcmF3bD0xMClcXG5cXG4gICAgIyBEZWZpbmUgYSByZXF1ZXN0IGhhbmRsZXIgdG8gcHJvY2VzcyBlYWNoIGNyYXdsZWQgcGFnZVxcbiAgICAjIGFuZCBhdHRhY2ggaXQgdG8gdGhlIGNyYXdsZXIgdXNpbmcgYSBkZWNvcmF0b3IuXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIHJlcXVlc3RfaGFuZGxlcihjb250ZXh0OiBQYXJzZWxDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG4gICAgICAgICMgRXh0cmFjdCByZWxldmFudCBkYXRhIGZyb20gdGhlIHBhZ2UgY29udGV4dC5cXG4gICAgICAgIGRhdGEgPSB7XFxuICAgICAgICAgICAgJ3VybCc6IGNvbnRleHQucmVxdWVzdC51cmwsXFxuICAgICAgICAgICAgJ3RpdGxlJzogY29udGV4dC5zZWxlY3Rvci54cGF0aCgnLy90aXRsZS90ZXh0KCknKS5nZXQoKSxcXG4gICAgICAgIH1cXG4gICAgICAgICMgU3RvcmUgdGhlIGV4dHJhY3RlZCBkYXRhLlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5wdXNoX2RhdGEoZGF0YSlcXG4gICAgICAgICMgRXh0cmFjdCBsaW5rcyBmcm9tIHRoZSBjdXJyZW50IHBhZ2UgYW5kIGFkZCB0aGVtIHRvIHRoZSBjcmF3bGluZyBxdWV1ZS5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQuZW5xdWV1ZV9saW5rcygpXFxuXFxuICAgICMgQWRkIGZpcnN0IFVSTCB0byB0aGUgcXVldWUgYW5kIHN0YXJ0IHRoZSBjcmF3bC5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2NyYXdsZWUuZGV2J10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.fShec9IocYPi2vw1j7Z_Sh3CczHHpm1VNpakilmAu44\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import ParselCrawler, ParselCrawlingContext


async def main() -> None:
    # ParselCrawler crawls the web using HTTP requests
    # and parses HTML using the Parsel library.
    crawler = ParselCrawler(max_requests_per_crawl=10)

    # Define a request handler to process each crawled page
    # and attach it to the crawler using a decorator.
    @crawler.router.default_handler
    async def request_handler(context: ParselCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')
        # Extract relevant data from the page context.
        data = {
            'url': context.request.url,
            'title': context.selector.xpath('//title/text()').get(),
        }
        # Store the extracted data.
        await context.push_data(data)
        # Extract links from the current page and add them to the crawling queue.
        await context.enqueue_links()

    # Add first URL to the queue and start the crawl.
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQbGF5d3JpZ2h0Q3Jhd2xlciwgUGxheXdyaWdodENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBQbGF5d3JpZ2h0Q3Jhd2xlciBjcmF3bHMgdGhlIHdlYiB1c2luZyBhIGhlYWRsZXNzIGJyb3dzZXJcXG4gICAgIyBjb250cm9sbGVkIGJ5IHRoZSBQbGF5d3JpZ2h0IGxpYnJhcnkuXFxuICAgIGNyYXdsZXIgPSBQbGF5d3JpZ2h0Q3Jhd2xlcigpXFxuXFxuICAgICMgRGVmaW5lIGEgcmVxdWVzdCBoYW5kbGVyIHRvIHByb2Nlc3MgZWFjaCBjcmF3bGVkIHBhZ2VcXG4gICAgIyBhbmQgYXR0YWNoIGl0IHRvIHRoZSBjcmF3bGVyIHVzaW5nIGEgZGVjb3JhdG9yLlxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiByZXF1ZXN0X2hhbmRsZXIoY29udGV4dDogUGxheXdyaWdodENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm9jZXNzaW5nIHtjb250ZXh0LnJlcXVlc3QudXJsfSAuLi4nKVxcbiAgICAgICAgIyBFeHRyYWN0IHJlbGV2YW50IGRhdGEgZnJvbSB0aGUgcGFnZSBjb250ZXh0LlxcbiAgICAgICAgZGF0YSA9IHtcXG4gICAgICAgICAgICAndXJsJzogY29udGV4dC5yZXF1ZXN0LnVybCxcXG4gICAgICAgICAgICAndGl0bGUnOiBhd2FpdCBjb250ZXh0LnBhZ2UudGl0bGUoKSxcXG4gICAgICAgIH1cXG4gICAgICAgICMgU3RvcmUgdGhlIGV4dHJhY3RlZCBkYXRhLlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5wdXNoX2RhdGEoZGF0YSlcXG4gICAgICAgICMgRXh0cmFjdCBsaW5rcyBmcm9tIHRoZSBjdXJyZW50IHBhZ2UgYW5kIGFkZCB0aGVtIHRvIHRoZSBjcmF3bGluZyBxdWV1ZS5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQuZW5xdWV1ZV9saW5rcygpXFxuXFxuICAgICMgQWRkIGZpcnN0IFVSTCB0byB0aGUgcXVldWUgYW5kIHN0YXJ0IHRoZSBjcmF3bC5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2NyYXdsZWUuZGV2J10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjQwOTYsInRpbWVvdXQiOjE4MH19.G_nYq646ERlU1yLA0hFR_p51rR_rKyMhqfEfogVXfh8\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext


async def main() -> None:
    # PlaywrightCrawler crawls the web using a headless browser
    # controlled by the Playwright library.
    crawler = PlaywrightCrawler()

    # Define a request handler to process each crawled page
    # and attach it to the crawler using a decorator.
    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')
        # Extract relevant data from the page context.
        data = {
            'url': context.request.url,
            'title': await context.page.title(),
        }
        # Store the extracted data.
        await context.push_data(data)
        # Extract links from the current page and add them to the crawling queue.
        await context.enqueue_links()

    # Add first URL to the queue and start the crawl.
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

When you run the example, you will see Crawlee automating the data extraction process in your terminal.

<!-- -->

## Running headful browser[​](#running-headful-browser "Direct link to Running headful browser")

By default, browsers controlled by Playwright run in headless mode (without a visible window). However, you can configure the crawler to run in a headful mode, which is useful during the development phase to observe the browser's actions. You can also switch from the default Chromium browser to Firefox or WebKit.

```
import asyncio

from crawlee.crawlers import PlaywrightCrawler


async def main() -> None:
    crawler = PlaywrightCrawler(
        # Run with a visible browser window.
        headless=False,
        # Switch to the Firefox browser.
        browser_type='firefox',
    )

    # ...


if __name__ == '__main__':
    asyncio.run(main())
```

When you run the example code, you'll see an automated browser navigating through the Crawlee website.

<!-- -->

## Results[​](#results "Direct link to Results")

By default, Crawlee stores data in the `./storage` directory within your current working directory. The results of your crawl will be saved as JSON files under `./storage/datasets/default/`.

To view the results, you can use the `cat` command:

```
cat ./storage/datasets/default/000000001.json
```

The JSON file will contain data similar to the following:

```
{
    "url": "https://crawlee.dev/",
    "title": "Crawlee · Build reliable crawlers. Fast. | Crawlee"
}
```

tip

If you want to change the storage directory, you can set the `CRAWLEE_STORAGE_DIR` environment variable to your preferred path.

## Examples and further reading[​](#examples-and-further-reading "Direct link to Examples and further reading")

For more examples showcasing various features of Crawlee, visit the [Examples](https://crawlee.dev/python/python/docs/examples.md) section of the documentation. To get a deeper understanding of Crawlee and its components, read the step-by-step [Introduction](https://crawlee.dev/python/python/docs/introduction.md) guide.

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/quick-start/index.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Next](https://crawlee.dev/python/python/docs/introduction.md)

[Introduction](https://crawlee.dev/python/python/docs/introduction.md)


---

## [📄️<!-- --> <!-- -->Upgrading to v0.x](https://crawlee.dev/python/python/docs/upgrading/upgrading-to-v0x.md)

[This page summarizes the breaking changes between Crawlee for Python zero-based versions.](https://crawlee.dev/python/python/docs/upgrading/upgrading-to-v0x.md)


---

* [](https://crawlee.dev/python/python)
* [Upgrading](https://crawlee.dev/python/python/docs/upgrading.md)
* Upgrading to v0.x

Version: 1.6

On this page

