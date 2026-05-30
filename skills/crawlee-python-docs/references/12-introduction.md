# Introduction

Crawlee covers your crawling and scraping end-to-end and helps you **build reliable scrapers. Fast.**

Your crawlers will appear human-like and fly under the radar of modern bot protections even with the default configuration. Crawlee gives you the tools to crawl the web for links, scrape data and persistently store it in machine-readable formats, without having to worry about the technical details. And thanks to rich configuration options, you can tweak almost any aspect of Crawlee to suit your project's needs if the default settings don't cut it.

## What you will learn[​](#what-you-will-learn "Direct link to What you will learn")

The goal of the introduction is to provide a step-by-step guide to the most important features of Crawlee. It will walk you through creating the simplest of crawlers that only prints text to console, all the way up to a full-featured scraper that collects links from a website and extracts data.

## 🛠 Features[​](#-features "Direct link to 🛠 Features")

Why Crawlee is the preferred choice for web scraping and crawling?

### Why use Crawlee instead of just a random HTTP library with an HTML parser?[​](#why-use-crawlee-instead-of-just-a-random-http-library-with-an-html-parser "Direct link to Why use Crawlee instead of just a random HTTP library with an HTML parser?")

* Unified interface for **HTTP & headless browser** crawling.
* Automatic **parallel crawling** based on available system resources.
* Written in Python with **type hints** - enhances DX (IDE autocompletion) and reduces bugs (static type checking).
* Automatic **retries** on errors or when you are getting blocked.
* Integrated **proxy rotation** and session management.
* Configurable **request routing** - direct URLs to the appropriate handlers.
* Persistent **queue for URLs** to crawl.
* Pluggable **storage** of both tabular data and files.
* Robust **error handling**.

### Why to use Crawlee rather than Scrapy?[​](#why-to-use-crawlee-rather-than-scrapy "Direct link to Why to use Crawlee rather than Scrapy?")

* Crawlee has out-of-the-box support for **headless browser** crawling (Playwright).
* Crawlee has a **minimalistic & elegant interface** - Set up your scraper with fewer than 10 lines of code.
* Complete **type hint** coverage.
* Based on standard **Asyncio**.

<!-- -->

<!-- -->

## Next steps[​](#next-steps "Direct link to Next steps")

Next, you will install Crawlee and learn how to bootstrap projects with the prepared Crawlee templates.

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/introduction/index.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/quick-start.md)

[Quick start](https://crawlee.dev/python/python/docs/quick-start.md)

[Next](https://crawlee.dev/python/python/docs/introduction/setting-up.md)

[Setting up](https://crawlee.dev/python/python/docs/introduction/setting-up.md)


---

* [](https://crawlee.dev/python/python)
* [Introduction](https://crawlee.dev/python/python/docs/introduction.md)
* Adding more URLs

Version: 1.6

On this page

# Adding more URLs

Previously you've built a very simple crawler that downloads HTML of a single page, reads its title and prints it to the console. This is the original source code:

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKClcXG5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICB1cmwgPSBjb250ZXh0LnJlcXVlc3QudXJsXFxuICAgICAgICB0aXRsZSA9IGNvbnRleHQuc291cC50aXRsZS5zdHJpbmcgaWYgY29udGV4dC5zb3VwLnRpdGxlIGVsc2UgJydcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidUaGUgdGl0bGUgb2Yge3VybH0gaXM6IHt0aXRsZX0uJylcXG5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2NyYXdsZWUuZGV2LyddKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.ODoXMKeR0XukKw7A0je4-vG9S7-AV4u1icmfr64tdsU\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


async def main() -> None:
    crawler = BeautifulSoupCrawler()

    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        url = context.request.url
        title = context.soup.title.string if context.soup.title else ''
        context.log.info(f'The title of {url} is: {title}.')

    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

Now you'll use the example from the previous section and improve on it. You'll add more URLs to the queue and thanks to that the crawler will keep going, finding new links, enqueuing them into the [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md) and then scraping them.

## How crawling works[​](#how-crawling-works "Direct link to How crawling works")

The process is simple:

1. Find new links on the page.
2. Filter only those pointing to the same domain, in this case [crawlee.dev](https://crawlee.dev/).
3. Enqueue (add) them to the [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md).
4. Visit the newly enqueued links.
5. Repeat the process.

In the following paragraphs you will learn about the [`enqueue_links`](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md) function which simplifies crawling to a single function call.

context awareness

The [`enqueue_links`](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md) function is context aware. It means that it will read the information about the currently crawled page from the context, and you don't need to explicitly provide any arguments. However, you can specify filtering criteria or an enqueuing strategy if desired. It will find the links and automatically add the links to the running crawler's [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md).

## Limit your crawls[​](#limit-your-crawls "Direct link to Limit your crawls")

When you're just testing your code or when your crawler could potentially find millions of links, it's very useful to set a maximum limit of crawled pages. The option is called [`max_requests_per_crawl`](https://crawlee.dev/python/python/api/class/BasicCrawlerOptions.md#max_requests_per_crawl), is available in all crawlers, and you can set it like this:

```
crawler = BeautifulSoupCrawler(max_requests_per_crawl=10)
```

This means that no new requests will be started after the 20th request is finished. The actual number of processed requests might be a little higher thanks to parallelization, because the running requests won't be forcefully aborted. It's not even possible in most cases.

## Finding new links[​](#finding-new-links "Direct link to Finding new links")

There are numerous approaches to finding links to follow when crawling the web. For our purposes, we will be looking for `<a>` elements that contain the `href` attribute because that's what you need in most cases. For example:

```
<a href="https://crawlee.dev/docs/introduction">This is a link to Crawlee introduction</a>
```

Since this is the most common case, it is also the [`enqueue_links`](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md) default.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBMZXQncyBsaW1pdCBvdXIgY3Jhd2xzIHRvIG1ha2Ugb3VyIHRlc3RzIHNob3J0ZXIgYW5kIHNhZmVyLlxcbiAgICBjcmF3bGVyID0gQmVhdXRpZnVsU291cENyYXdsZXIobWF4X3JlcXVlc3RzX3Blcl9jcmF3bD0xMClcXG5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICB1cmwgPSBjb250ZXh0LnJlcXVlc3QudXJsXFxuICAgICAgICB0aXRsZSA9IGNvbnRleHQuc291cC50aXRsZS5zdHJpbmcgaWYgY29udGV4dC5zb3VwLnRpdGxlIGVsc2UgJydcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidUaGUgdGl0bGUgb2Yge3VybH0gaXM6IHt0aXRsZX0uJylcXG5cXG4gICAgICAgICMgVGhlIGVucXVldWVfbGlua3MgZnVuY3Rpb24gaXMgYXZhaWxhYmxlIGFzIG9uZSBvZiB0aGUgZmllbGRzIG9mIHRoZSBjb250ZXh0LlxcbiAgICAgICAgIyBJdCBpcyBhbHNvIGNvbnRleHQgYXdhcmUsIHNvIGl0IGRvZXMgbm90IHJlcXVpcmUgYW55IHBhcmFtZXRlcnMuXFxuICAgICAgICBhd2FpdCBjb250ZXh0LmVucXVldWVfbGlua3MoKVxcblxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vY3Jhd2xlZS5kZXYvJ10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.ZRIb8tuYHWXWQAJZmUTEJVXfKUUFmysN3gXXbQw15KE\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


async def main() -> None:
    # Let's limit our crawls to make our tests shorter and safer.
    crawler = BeautifulSoupCrawler(max_requests_per_crawl=10)

    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        url = context.request.url
        title = context.soup.title.string if context.soup.title else ''
        context.log.info(f'The title of {url} is: {title}.')

        # The enqueue_links function is available as one of the fields of the context.
        # It is also context aware, so it does not require any parameters.
        await context.enqueue_links()

    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

If you need to override the default selection of elements in [`enqueue_links`](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md), you can use the `selector` argument.

```
await context.enqueue_links(selector='a.article-link')
```

## Filtering links to same domain[​](#filtering-links-to-same-domain "Direct link to Filtering links to same domain")

Websites typically contain a lot of links that lead away from the original page. This is normal, but when crawling a website, we usually want to crawl that one site and not let our crawler wander away to Google, Facebook and Twitter. Therefore, we need to filter out the off-domain links and only keep the ones that lead to the same domain.

```
# The default behavior of enqueue_links is to stay on the same hostname, so it does not require
# any parameters. This will ensure the subdomain stays the same.
await context.enqueue_links()
```

The default behavior of [`enqueue_links`](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md) is to stay on the same hostname. This **does not include subdomains**. To include subdomains in your crawl, use the `strategy` argument. The `strategy` argument is an instance of the `EnqueueStrategy` type alias.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTApXFxuXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIHJlcXVlc3RfaGFuZGxlcihjb250ZXh0OiBCZWF1dGlmdWxTb3VwQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ1Byb2Nlc3Npbmcge2NvbnRleHQucmVxdWVzdC51cmx9LicpXFxuXFxuICAgICAgICAjIFNlZSB0aGUgYEVucXVldWVTdHJhdGVneWAgdHlwZSBhbGlhcyBmb3IgbW9yZSBzdHJhdGVneSBvcHRpb25zLlxcbiAgICAgICAgIyBoaWdobGlnaHQtbmV4dC1saW5lXFxuICAgICAgICBhd2FpdCBjb250ZXh0LmVucXVldWVfbGlua3MoXFxuICAgICAgICAgICAgIyBoaWdobGlnaHQtbmV4dC1saW5lXFxuICAgICAgICAgICAgc3RyYXRlZ3k9J3NhbWUtZG9tYWluJyxcXG4gICAgICAgICAgICAjIGhpZ2hsaWdodC1uZXh0LWxpbmVcXG4gICAgICAgIClcXG5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2NyYXdsZWUuZGV2LyddKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.wsSkJOC86y2a9ATz3O9k5fJxr8I-GRgVHKBpNS8Xy40\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


async def main() -> None:
    crawler = BeautifulSoupCrawler(max_requests_per_crawl=10)

    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url}.')

        # See the `EnqueueStrategy` type alias for more strategy options.
        await context.enqueue_links(
            strategy='same-domain',
        )

    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

When you run the code, you will see the crawler log the **title** of the first page, then the **enqueueing** message showing number of URLs, followed by the **title** of the first enqueued page and so on and so on.

## Skipping duplicate URLs[​](#skipping-duplicate-urls "Direct link to Skipping duplicate URLs")

Skipping of duplicate URLs is critical, because visiting the same page multiple times would lead to duplicate results. This is automatically handled by the [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md) which deduplicates requests using their `unique_key`. This `unique_key` is automatically generated from the request's URL by lowercasing the URL, lexically ordering query parameters, removing fragments and a few other tweaks that ensure the queue only includes unique URLs.

## Advanced filtering arguments[​](#advanced-filtering-arguments "Direct link to Advanced filtering arguments")

While the defaults for [`enqueue_links`](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md) can be often exactly what you need, it also gives you fine-grained control over which URLs should be enqueued. One way we already mentioned above. It is using the `EnqueueStrategy` type alias. You can use the `all` strategy if you want to follow every single link, regardless of its domain, or you can enqueue links that target the same domain name with the `same-domain` strategy.

```
# Wanders the internet.
await context.enqueue_links(strategy='all')
```

### Filter URLs with patterns[​](#filter-urls-with-patterns "Direct link to Filter URLs with patterns")

For even more control, you can use the `include` or `exclude` parameters, either as glob patterns or regular expressions, to filter the URLs. Refer to the API documentation for [`enqueue_links`](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md) for detailed information on these and other available options.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBHbG9iXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTApXFxuXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIHJlcXVlc3RfaGFuZGxlcihjb250ZXh0OiBCZWF1dGlmdWxTb3VwQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ1Byb2Nlc3Npbmcge2NvbnRleHQucmVxdWVzdC51cmx9LicpXFxuXFxuICAgICAgICAjIEVucXVldWUgbGlua3MgdGhhdCBtYXRjaCB0aGUgJ2luY2x1ZGUnIGdsb2IgcGF0dGVybiBhbmRcXG4gICAgICAgICMgZG8gbm90IG1hdGNoIHRoZSAnZXhjbHVkZScgZ2xvYiBwYXR0ZXJuLlxcbiAgICAgICAgIyBoaWdobGlnaHQtbmV4dC1saW5lXFxuICAgICAgICBhd2FpdCBjb250ZXh0LmVucXVldWVfbGlua3MoXFxuICAgICAgICAgICAgIyBoaWdobGlnaHQtbmV4dC1saW5lXFxuICAgICAgICAgICAgaW5jbHVkZT1bR2xvYignaHR0cHM6Ly9zb21lcGxhY2UuY29tLyoqL2NhdHMnKV0sXFxuICAgICAgICAgICAgIyBoaWdobGlnaHQtbmV4dC1saW5lXFxuICAgICAgICAgICAgZXhjbHVkZT1bR2xvYignaHR0cHM6Ly8qKi9hcmNoaXZlLyoqJyldLFxcbiAgICAgICAgICAgICMgaGlnaGxpZ2h0LW5leHQtbGluZVxcbiAgICAgICAgKVxcblxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vY3Jhd2xlZS5kZXYvJ10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.RverXr-WKElrnHRMAk3t7ynOkuL5BklOPZ7K15X9TZE\&asrc=run_on_apify)

```
import asyncio

from crawlee import Glob
from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


async def main() -> None:
    crawler = BeautifulSoupCrawler(max_requests_per_crawl=10)

    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url}.')

        # Enqueue links that match the 'include' glob pattern and
        # do not match the 'exclude' glob pattern.
        await context.enqueue_links(
            include=[Glob('https://someplace.com/**/cats')],
            exclude=[Glob('https://**/archive/**')],
        )

    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

### Transform requests before enqueuing[​](#transform-requests-before-enqueuing "Direct link to Transform requests before enqueuing")

For cases where you need to modify or filter requests before they are enqueued, you can use the `transform_request_function` parameter. This function receives a [`RequestOptions`](https://crawlee.dev/python/python/api/class/RequestOptions.md) object and should return either a modified [`RequestOptions`](https://crawlee.dev/python/python/api/class/RequestOptions.md) object, or a string of type `RequestTransformAction`, which only allows the values `skip` and `unchanged`. Returning `skip` means the request will be skipped, while `unchanged` will add it without any changes

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImZyb20gX19mdXR1cmVfXyBpbXBvcnQgYW5ub3RhdGlvbnNcXG5cXG5pbXBvcnQgYXN5bmNpb1xcblxcbmZyb20gY3Jhd2xlZSBpbXBvcnQgSHR0cEhlYWRlcnMsIFJlcXVlc3RPcHRpb25zLCBSZXF1ZXN0VHJhbnNmb3JtQWN0aW9uXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmRlZiB0cmFuc2Zvcm1fcmVxdWVzdChcXG4gICAgcmVxdWVzdF9vcHRpb25zOiBSZXF1ZXN0T3B0aW9ucyxcXG4pIC0-IFJlcXVlc3RPcHRpb25zIHwgUmVxdWVzdFRyYW5zZm9ybUFjdGlvbjpcXG4gICAgIyBTa2lwIHJlcXVlc3RzIHRvIFBERiBmaWxlc1xcbiAgICBpZiByZXF1ZXN0X29wdGlvbnNbJ3VybCddLmVuZHN3aXRoKCcucGRmJyk6XFxuICAgICAgICByZXR1cm4gJ3NraXAnXFxuXFxuICAgIGlmICcvZG9jcycgaW4gcmVxdWVzdF9vcHRpb25zWyd1cmwnXTpcXG4gICAgICAgICMgQWRkIGN1c3RvbSBoZWFkZXJzIHRvIHJlcXVlc3RzIHRvIHNwZWNpZmljIFVSTHNcXG4gICAgICAgIHJlcXVlc3Rfb3B0aW9uc1snaGVhZGVycyddID0gSHR0cEhlYWRlcnMoeydDdXN0b20tSGVhZGVyJzogJ3ZhbHVlJ30pXFxuXFxuICAgIGVsaWYgJy9ibG9nJyBpbiByZXF1ZXN0X29wdGlvbnNbJ3VybCddOlxcbiAgICAgICAgIyBBZGQgbGFiZWwgZm9yIGNlcnRhaW4gVVJMc1xcbiAgICAgICAgcmVxdWVzdF9vcHRpb25zWydsYWJlbCddID0gJ0JMT0cnXFxuXFxuICAgIGVsc2U6XFxuICAgICAgICAjIFNpZ25hbCB0aGF0IHRoZSByZXF1ZXN0IHNob3VsZCBwcm9jZWVkIHdpdGhvdXQgYW55IHRyYW5zZm9ybWF0aW9uXFxuICAgICAgICByZXR1cm4gJ3VuY2hhbmdlZCdcXG5cXG4gICAgcmV0dXJuIHJlcXVlc3Rfb3B0aW9uc1xcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTApXFxuXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIHJlcXVlc3RfaGFuZGxlcihjb250ZXh0OiBCZWF1dGlmdWxTb3VwQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ1Byb2Nlc3Npbmcge2NvbnRleHQucmVxdWVzdC51cmx9LicpXFxuXFxuICAgICAgICAjIFRyYW5zZm9ybSByZXF1ZXN0IGJlZm9yZSBlbnF1ZXVlaW5nXFxuICAgICAgICBhd2FpdCBjb250ZXh0LmVucXVldWVfbGlua3ModHJhbnNmb3JtX3JlcXVlc3RfZnVuY3Rpb249dHJhbnNmb3JtX3JlcXVlc3QpXFxuXFxuICAgIEBjcmF3bGVyLnJvdXRlci5oYW5kbGVyKCdCTE9HJylcXG4gICAgYXN5bmMgZGVmIGJsb2dfaGFuZGxlcihjb250ZXh0OiBCZWF1dGlmdWxTb3VwQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ0Jsb2cgUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0uJylcXG5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2NyYXdsZWUuZGV2LyddKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.Jj6-CkvsDgLqWAS5AZRI0j5i-BPLOq7A3Oq9IT1iJbk\&asrc=run_on_apify)

```
from __future__ import annotations

import asyncio

from crawlee import HttpHeaders, RequestOptions, RequestTransformAction
from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


def transform_request(
    request_options: RequestOptions,
) -> RequestOptions | RequestTransformAction:
    # Skip requests to PDF files
    if request_options['url'].endswith('.pdf'):
        return 'skip'

    if '/docs' in request_options['url']:
        # Add custom headers to requests to specific URLs
        request_options['headers'] = HttpHeaders({'Custom-Header': 'value'})

    elif '/blog' in request_options['url']:
        # Add label for certain URLs
        request_options['label'] = 'BLOG'

    else:
        # Signal that the request should proceed without any transformation
        return 'unchanged'

    return request_options


async def main() -> None:
    crawler = BeautifulSoupCrawler(max_requests_per_crawl=10)

    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url}.')

        # Transform request before enqueueing
        await context.enqueue_links(transform_request_function=transform_request)

    @crawler.router.handler('BLOG')
    async def blog_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Blog Processing {context.request.url}.')

    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

## Next steps[​](#next-steps "Direct link to Next steps")

Next, you will start your project of scraping a production website and learn some more Crawlee tricks in the process.

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/introduction/03_adding_more_urls.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/introduction/first-crawler.md)

[First crawler](https://crawlee.dev/python/python/docs/introduction/first-crawler.md)

[Next](https://crawlee.dev/python/python/docs/introduction/real-world-project.md)

[Real-world project](https://crawlee.dev/python/python/docs/introduction/real-world-project.md)


---

* [](https://crawlee.dev/python/python)
* [Introduction](https://crawlee.dev/python/python/docs/introduction.md)
* Crawling

Version: 1.6

On this page

# Crawling

To crawl the whole [Warehouse store example](https://warehouse-theme-metal.myshopify.com/collections) and find all the data, you first need to visit all the pages with products - going through all categories available and also all the product detail pages.

## Crawling the listing pages[​](#crawling-the-listing-pages "Direct link to Crawling the listing pages")

In previous lessons, you used the [`enqueue_links`](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md) function like this:

```
await enqueue_links()
```

While useful in that scenario, you need something different now. Instead of finding all the `<a href="..">` elements with links to the same hostname, you need to find only the specific ones that will take your crawler to the next page of results. Otherwise, the crawler will visit a lot of other pages that you're not interested in. Using the power of DevTools and yet another [`enqueue_links`](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md) parameter, this becomes fairly easy.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQbGF5d3JpZ2h0Q3Jhd2xlciwgUGxheXdyaWdodENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IFBsYXl3cmlnaHRDcmF3bGVyKClcXG5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IFBsYXl3cmlnaHRDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0nKVxcblxcbiAgICAgICAgIyBXYWl0IGZvciB0aGUgY2F0ZWdvcnkgY2FyZHMgdG8gcmVuZGVyIG9uIHRoZSBwYWdlLiBUaGlzIGVuc3VyZXMgdGhhdFxcbiAgICAgICAgIyB0aGUgZWxlbWVudHMgd2Ugd2FudCB0byBpbnRlcmFjdCB3aXRoIGFyZSBwcmVzZW50IGluIHRoZSBET00uXFxuICAgICAgICBhd2FpdCBjb250ZXh0LnBhZ2Uud2FpdF9mb3Jfc2VsZWN0b3IoJy5jb2xsZWN0aW9uLWJsb2NrLWl0ZW0nKVxcblxcbiAgICAgICAgIyBFbnF1ZXVlIGxpbmtzIGZvdW5kIHdpdGhpbiBlbGVtZW50cyB0aGF0IG1hdGNoIHRoZSBzcGVjaWZpZWQgc2VsZWN0b3IuXFxuICAgICAgICAjIFRoZXNlIGxpbmtzIHdpbGwgYmUgYWRkZWQgdG8gdGhlIGNyYXdsaW5nIHF1ZXVlIHdpdGggdGhlIGxhYmVsIENBVEVHT1JZLlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5lbnF1ZXVlX2xpbmtzKFxcbiAgICAgICAgICAgIHNlbGVjdG9yPScuY29sbGVjdGlvbi1ibG9jay1pdGVtJyxcXG4gICAgICAgICAgICBsYWJlbD0nQ0FURUdPUlknLFxcbiAgICAgICAgKVxcblxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vd2FyZWhvdXNlLXRoZW1lLW1ldGFsLm15c2hvcGlmeS5jb20vY29sbGVjdGlvbnMnXSlcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6NDA5NiwidGltZW91dCI6MTgwfX0.X9WWCidJxivEV99HXElBusVeZZu2wf-ZTDSkyUZJ0Ew\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext


async def main() -> None:
    crawler = PlaywrightCrawler()

    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url}')

        # Wait for the category cards to render on the page. This ensures that
        # the elements we want to interact with are present in the DOM.
        await context.page.wait_for_selector('.collection-block-item')

        # Enqueue links found within elements that match the specified selector.
        # These links will be added to the crawling queue with the label CATEGORY.
        await context.enqueue_links(
            selector='.collection-block-item',
            label='CATEGORY',
        )

    await crawler.run(['https://warehouse-theme-metal.myshopify.com/collections'])


if __name__ == '__main__':
    asyncio.run(main())
```

The code should look pretty familiar to you. It's a very simple request handler where we log the currently processed URL to the console and enqueue more links. But there are also a few new, interesting additions. Let's break it down.

### The `selector` parameter of `enqueue_links`[​](#the-selector-parameter-of-enqueue_links "Direct link to the-selector-parameter-of-enqueue_links")

When you previously used [`enqueue_links`](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md), you were not providing any `selector` parameter, and it was fine, because you wanted to use the default value, which is `a` - finds all `<a>` elements. But now, you need to be more specific. There are multiple `<a>` links on the `Categories` page, and you're only interested in those that will take your crawler to the available list of results. Using the DevTools, you'll find that you can select the links you need using the `.collection-block-item` selector, which selects all the elements that have the `class=collection-block-item` attribute.

### The `label` of `enqueue_links`[​](#the-label-of-enqueue_links "Direct link to the-label-of-enqueue_links")

You will see `label` used often throughout Crawlee, as it's a convenient way of labelling a [`Request`](https://crawlee.dev/python/python/api/class/Request.md) instance for quick identification later. You can access it with `request.label` and it's a `string`. You can name your requests any way you want. Here, we used the label `CATEGORY` to note that we're enqueueing pages that represent a category of products. The [`enqueue_links`](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md) function will add this label to all requests before enqueueing them to the [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md). Why this is useful will become obvious in a minute.

## Crawling the detail pages[​](#crawling-the-detail-pages "Direct link to Crawling the detail pages")

In a similar fashion, you need to collect all the URLs to the product detail pages, because only from there you can scrape all the data you need. The following code only repeats the concepts you already know for another set of links.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQbGF5d3JpZ2h0Q3Jhd2xlciwgUGxheXdyaWdodENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IFBsYXl3cmlnaHRDcmF3bGVyKClcXG5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IFBsYXl3cmlnaHRDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0nKVxcblxcbiAgICAgICAgIyBXZSdyZSBub3QgcHJvY2Vzc2luZyBkZXRhaWwgcGFnZXMgeWV0LCBzbyB3ZSBqdXN0IHBhc3MuXFxuICAgICAgICBpZiBjb250ZXh0LnJlcXVlc3QubGFiZWwgPT0gJ0RFVEFJTCc6XFxuICAgICAgICAgICAgcGFzc1xcblxcbiAgICAgICAgIyBXZSBhcmUgbm93IG9uIGEgY2F0ZWdvcnkgcGFnZS4gV2UgY2FuIHVzZSB0aGlzIHRvIHBhZ2luYXRlIHRocm91Z2ggYW5kXFxuICAgICAgICAjIGVucXVldWUgYWxsIHByb2R1Y3RzLCBhcyB3ZWxsIGFzIGFueSBzdWJzZXF1ZW50IHBhZ2VzIHdlIGZpbmQuXFxuICAgICAgICBlbGlmIGNvbnRleHQucmVxdWVzdC5sYWJlbCA9PSAnQ0FURUdPUlknOlxcbiAgICAgICAgICAgICMgV2FpdCBmb3IgdGhlIHByb2R1Y3QgaXRlbXMgdG8gcmVuZGVyLlxcbiAgICAgICAgICAgIGF3YWl0IGNvbnRleHQucGFnZS53YWl0X2Zvcl9zZWxlY3RvcignLnByb2R1Y3QtaXRlbSA-IGEnKVxcblxcbiAgICAgICAgICAgICMgRW5xdWV1ZSBsaW5rcyBmb3VuZCB3aXRoaW4gZWxlbWVudHMgbWF0Y2hpbmcgdGhlIHByb3ZpZGVkIHNlbGVjdG9yLlxcbiAgICAgICAgICAgICMgVGhlc2UgbGlua3Mgd2lsbCBiZSBhZGRlZCB0byB0aGUgY3Jhd2xpbmcgcXVldWUgd2l0aCB0aGUgbGFiZWwgREVUQUlMLlxcbiAgICAgICAgICAgIGF3YWl0IGNvbnRleHQuZW5xdWV1ZV9saW5rcyhcXG4gICAgICAgICAgICAgICAgc2VsZWN0b3I9Jy5wcm9kdWN0LWl0ZW0gPiBhJyxcXG4gICAgICAgICAgICAgICAgbGFiZWw9J0RFVEFJTCcsXFxuICAgICAgICAgICAgKVxcblxcbiAgICAgICAgICAgICMgRmluZCB0aGUgXFxcIk5leHRcXFwiIGJ1dHRvbiB0byBwYWdpbmF0ZSB0aHJvdWdoIHRoZSBjYXRlZ29yeSBwYWdlcy5cXG4gICAgICAgICAgICBuZXh0X2J1dHRvbiA9IGF3YWl0IGNvbnRleHQucGFnZS5xdWVyeV9zZWxlY3RvcignYS5wYWdpbmF0aW9uX19uZXh0JylcXG5cXG4gICAgICAgICAgICAjIElmIGEgXFxcIk5leHRcXFwiIGJ1dHRvbiBpcyBmb3VuZCwgZW5xdWV1ZSB0aGUgbmV4dCBwYWdlIG9mIHJlc3VsdHMuXFxuICAgICAgICAgICAgaWYgbmV4dF9idXR0b246XFxuICAgICAgICAgICAgICAgIGF3YWl0IGNvbnRleHQuZW5xdWV1ZV9saW5rcyhcXG4gICAgICAgICAgICAgICAgICAgIHNlbGVjdG9yPSdhLnBhZ2luYXRpb25fX25leHQnLFxcbiAgICAgICAgICAgICAgICAgICAgbGFiZWw9J0NBVEVHT1JZJyxcXG4gICAgICAgICAgICAgICAgKVxcblxcbiAgICAgICAgIyBUaGlzIGluZGljYXRlcyB3ZSdyZSBvbiB0aGUgc3RhcnQgcGFnZSB3aXRoIG5vIHNwZWNpZmljIGxhYmVsLlxcbiAgICAgICAgIyBPbiB0aGUgc3RhcnQgcGFnZSwgd2Ugd2FudCB0byBlbnF1ZXVlIGFsbCB0aGUgY2F0ZWdvcnkgcGFnZXMuXFxuICAgICAgICBlbHNlOlxcbiAgICAgICAgICAgICMgV2FpdCBmb3IgdGhlIGNvbGxlY3Rpb24gY2FyZHMgdG8gcmVuZGVyLlxcbiAgICAgICAgICAgIGF3YWl0IGNvbnRleHQucGFnZS53YWl0X2Zvcl9zZWxlY3RvcignLmNvbGxlY3Rpb24tYmxvY2staXRlbScpXFxuXFxuICAgICAgICAgICAgIyBFbnF1ZXVlIGxpbmtzIGZvdW5kIHdpdGhpbiBlbGVtZW50cyBtYXRjaGluZyB0aGUgcHJvdmlkZWQgc2VsZWN0b3IuXFxuICAgICAgICAgICAgIyBUaGVzZSBsaW5rcyB3aWxsIGJlIGFkZGVkIHRvIHRoZSBjcmF3bGluZyBxdWV1ZSB3aXRoIHRoZSBsYWJlbCBDQVRFR09SWS5cXG4gICAgICAgICAgICBhd2FpdCBjb250ZXh0LmVucXVldWVfbGlua3MoXFxuICAgICAgICAgICAgICAgIHNlbGVjdG9yPScuY29sbGVjdGlvbi1ibG9jay1pdGVtJyxcXG4gICAgICAgICAgICAgICAgbGFiZWw9J0NBVEVHT1JZJyxcXG4gICAgICAgICAgICApXFxuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly93YXJlaG91c2UtdGhlbWUtbWV0YWwubXlzaG9waWZ5LmNvbS9jb2xsZWN0aW9ucyddKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5Ijo0MDk2LCJ0aW1lb3V0IjoxODB9fQ.moljdzO1LGX-DchS3DDHfhUU9aGpzgHDLeBfzX_Q76Q\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext


async def main() -> None:
    crawler = PlaywrightCrawler()

    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url}')

        # We're not processing detail pages yet, so we just pass.
        if context.request.label == 'DETAIL':
            pass

        # We are now on a category page. We can use this to paginate through and
        # enqueue all products, as well as any subsequent pages we find.
        elif context.request.label == 'CATEGORY':
            # Wait for the product items to render.
            await context.page.wait_for_selector('.product-item > a')

            # Enqueue links found within elements matching the provided selector.
            # These links will be added to the crawling queue with the label DETAIL.
            await context.enqueue_links(
                selector='.product-item > a',
                label='DETAIL',
            )

            # Find the "Next" button to paginate through the category pages.
            next_button = await context.page.query_selector('a.pagination__next')

            # If a "Next" button is found, enqueue the next page of results.
            if next_button:
                await context.enqueue_links(
                    selector='a.pagination__next',
                    label='CATEGORY',
                )

        # This indicates we're on the start page with no specific label.
        # On the start page, we want to enqueue all the category pages.
        else:
            # Wait for the collection cards to render.
            await context.page.wait_for_selector('.collection-block-item')

            # Enqueue links found within elements matching the provided selector.
            # These links will be added to the crawling queue with the label CATEGORY.
            await context.enqueue_links(
                selector='.collection-block-item',
                label='CATEGORY',
            )

    await crawler.run(['https://warehouse-theme-metal.myshopify.com/collections'])


if __name__ == '__main__':
    asyncio.run(main())
```

The crawling code is now complete. When you run the code, you'll see the crawler visit all the listing URLs and all the detail URLs.

## Next steps[​](#next-steps "Direct link to Next steps")

This concludes the Crawling lesson, because you have taught the crawler to visit all the pages it needs. Let's continue with scraping data.

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/introduction/05_crawling.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/introduction/real-world-project.md)

[Real-world project](https://crawlee.dev/python/python/docs/introduction/real-world-project.md)

[Next](https://crawlee.dev/python/python/docs/introduction/scraping.md)

[Scraping](https://crawlee.dev/python/python/docs/introduction/scraping.md)


---

* [](https://crawlee.dev/python/python)
* [Introduction](https://crawlee.dev/python/python/docs/introduction.md)
* Running in the Cloud

Version: 1.6

On this page

# Running your crawler in the Cloud

## Apify platform[​](#apify-platform "Direct link to Apify platform")

Crawlee is developed by [**Apify**](https://apify.com), the web scraping and automation platform. You could say it is the **home of Crawlee projects**. In this section you'll see how to deploy the crawler there with just a few simple steps. You can deploy a **Crawlee** project wherever you want, but using the [**Apify platform**](https://console.apify.com) will give you the best experience.

<!-- -->

With a few simple steps, you can convert your Crawlee project into a so-called **Actor**. Actors are serverless micro-apps that are easy to develop, run, share, and integrate. The infra, proxies, and storages are ready to go. [Learn more about Actors](https://apify.com/actors).

<!-- -->

## Dependencies[​](#dependencies "Direct link to Dependencies")

Before we get started, you'll need to install two new dependencies:

* [**Apify SDK**](https://pypi.org/project/apify/), a toolkit for working with the Apify platform. This will allow us to wire the storages (e.g. [`RequestQueue`](https://docs.apify.com/sdk/python/reference/class/RequestQueue) and [`Dataset`](https://docs.apify.com/sdk/python/reference/class/Dataset)) to the Apify cloud products. The Apify SDK, like Crawlee itself, is available as a PyPI package and can be installed with any Python package manager. To install it using [pip](https://pip.pypa.io/), run:

  ```
  pip install apify
  ```

* [**Apify CLI**](https://docs.apify.com/cli/), a command-line tool that will help us with authentication and deployment. It is a [Node.js](https://nodejs.org/) package, and can be installed using any Node.js package manager. In this guide, we will use [npm](https://npmjs.com/). We will install it globally, so you can use it across all your Crawlee and Apify projects. To install it using npm, run:

  ```
  npm install -g apify-cli
  ```

## Logging in to the Apify platform[​](#logging-in-to-the-apify-platform "Direct link to Logging in to the Apify platform")

The next step will be [creating your Apify account](https://console.apify.com/sign-up). Don't worry, we have a **free tier**, so you can try things out before you buy in! Once you have that, it's time to log in with the just-installed [Apify CLI](https://docs.apify.com/cli/). You will need your personal access token, which you can find at <https://console.apify.com/account#/integrations>.

```
apify login
```

## Adjusting the code[​](#adjusting-the-code "Direct link to Adjusting the code")

Now that you have your account set up, you will need to adjust the code a tiny bit. We will use the [Apify SDK](https://docs.apify.com/sdk/python/), which will help us to wire the Crawlee storages (like the [`RequestQueue`](https://docs.apify.com/sdk/python/reference/class/RequestQueue)) to their Apify platform counterparts - otherwise Crawlee would keep things only in memory.

Open your `src/main.py` file, and wrap everything in your `main` function with the [`Actor`](https://docs.apify.com/sdk/python/reference/class/Actor) context manager. Your code should look like this:

src/main.py

```
import asyncio

from apify import Actor

from crawlee.crawlers import PlaywrightCrawler

from .routes import router


async def main() -> None:
    async with Actor:
        crawler = PlaywrightCrawler(
            # Let's limit our crawls to make our tests shorter and safer.
            max_requests_per_crawl=10,
            # Provide our router instance to the crawler.
            request_handler=router,
        )

        await crawler.run(['https://warehouse-theme-metal.myshopify.com/collections'])


if __name__ == '__main__':
    asyncio.run(main())
```

The context manager will configure Crawlee to use the Apify API instead of its default memory storage interface. It also sets up few other things, like listening to the platform events via websockets. After the body is finished, it handles graceful shutdown.

Understanding `async with Actor` behavior with environment variables

The [`Actor`](https://docs.apify.com/sdk/python/reference/class/Actor) context manager works conditionally based on the environment variables, namely based on the `APIFY_IS_AT_HOME` env var, which is set to `true` on the Apify platform. This means that your project will remain working the same locally, but will use the Apify API when deployed to the Apify platform.

## Initializing the project[​](#initializing-the-project "Direct link to Initializing the project")

You will also need to initialize the project for Apify, to do that, use the Apify CLI again:

```
apify init
```

The CLI will check the project structure and guide you through the setup process. If prompted, follow the instructions and answer the questions to configure the project correctly. For more information follow the [Apify CLI documentation](https://docs.apify.com/cli/docs).

This will create a folder called `.actor`, and an `actor.json` file inside it - this file contains the configuration relevant to the Apify platform, namely the Actor name, version, build tag, and few other things. Check out the [relevant documentation](https://docs.apify.com/platform/actors/development/actor-definition/actor-json) to see all the different things you can set there up.

## Ship it\![​](#ship-it "Direct link to Ship it!")

And that's all, your project is now ready to be published on the Apify platform. You can use the Apify CLI once more to do that:

```
apify push
```

This command will create an archive from your project, upload it to the Apify platform and initiate a Docker build. Once finished, you will get a link to your new Actor on the platform.

## Learning more about web scraping[​](#learning-more-about-web-scraping "Direct link to Learning more about web scraping")

Explore Apify Academy Resources

If you want to learn more about web scraping and browser automation, check out the [Apify Academy](https://developers.apify.com/academy). It's full of courses and tutorials on the topic. From beginner to advanced. And the best thing: **It's free and open source** ❤️

## Thank you! 🎉[​](#thank-you- "Direct link to Thank you! 🎉")

That's it! Thanks for reading the whole introduction and if there's anything wrong, please 🙏 let us know on [GitHub](https://github.com/apify/crawlee-python) or in our [Discord community](https://discord.com/invite/jyEM2PRvMU). Happy scraping! 👋

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/introduction/09_running_in_cloud.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/introduction/refactoring.md)

[Refactoring](https://crawlee.dev/python/python/docs/introduction/refactoring.md)

[Next](https://crawlee.dev/python/python/docs/guides.md)

[Guides](https://crawlee.dev/python/python/docs/guides.md)


---

* [](https://crawlee.dev/python/python)
* [Introduction](https://crawlee.dev/python/python/docs/introduction.md)
* First crawler

Version: 1.6

On this page

# First crawler

Now, you will build your first crawler. But before you do, let's briefly introduce the Crawlee classes involved in the process.

## How Crawlee works[​](#how-crawlee-works "Direct link to How Crawlee works")

There are 3 main crawler classes available for use in Crawlee.

* [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md)
* [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md)
* [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md)

We'll talk about their differences later. Now, let's talk about what they have in common.

The general idea of each crawler is to go to a web page, open it, do some stuff there, save some results, continue to the next page, and repeat this process until the crawler's done its job. So the crawler always needs to find answers to two questions: *Where should I go?* and *What should I do there?* Answering those two questions is the only required setup. The crawlers have reasonable defaults for everything else.

### The where - `Request` and `RequestQueue`[​](#the-where---request-and-requestqueue "Direct link to the-where---request-and-requestqueue")

All crawlers use instances of the [`Request`](https://crawlee.dev/python/python/api/class/Request.md) class to determine where they need to go. Each request may hold a lot of information, but at the very least, it must hold a URL - a web page to open. But having only one URL would not make sense for crawling. Sometimes you have a pre-existing list of your own URLs that you wish to visit, perhaps a thousand. Other times you need to build this list dynamically as you crawl, adding more and more URLs to the list as you progress. Most of the time, you will use both options.

The requests are stored in a [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md), a dynamic queue of [`Request`](https://crawlee.dev/python/python/api/class/Request.md) instances. You can seed it with start URLs and also add more requests while the crawler is running. This allows the crawler to open one page, extract interesting data, such as links to other pages on the same domain, add them to the queue (called *enqueuing*) and repeat this process to build a queue of virtually unlimited number of URLs.

### The what - request handler[​](#the-what---request-handler "Direct link to The what - request handler")

In the request handler you tell the crawler what to do at each and every page it visits. You can use it to handle extraction of data from the page, processing the data, saving it, calling APIs, doing calculations and so on.

The request handler is a user-defined function, invoked automatically by the crawler for each [`Request`](https://crawlee.dev/python/python/api/class/Request.md) from the [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md). It always receives a single argument - [`BasicCrawlingContext`](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md) (or its descendants). Its properties change depending on the crawler class used, but it always includes the `request` property, which represents the currently crawled URL and related metadata.

## Building a crawler[​](#building-a-crawler "Direct link to Building a crawler")

Let's put the theory into practice and start with something easy. Visit a page and get its HTML title. In this tutorial, you'll scrape the Crawlee website <https://crawlee.dev>, but the same code will work for any website.

### Adding requests to the crawling queue[​](#adding-requests-to-the-crawling-queue "Direct link to Adding requests to the crawling queue")

Earlier you learned that the crawler uses a queue of requests as its source of URLs to crawl. Let's create it and add the first request.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLnN0b3JhZ2VzIGltcG9ydCBSZXF1ZXN0UXVldWVcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgICMgRmlyc3QgeW91IGNyZWF0ZSB0aGUgcmVxdWVzdCBxdWV1ZSBpbnN0YW5jZS5cXG4gICAgcnEgPSBhd2FpdCBSZXF1ZXN0UXVldWUub3BlbigpXFxuXFxuICAgICMgQW5kIHRoZW4geW91IGFkZCBvbmUgb3IgbW9yZSByZXF1ZXN0cyB0byBpdC5cXG4gICAgYXdhaXQgcnEuYWRkX3JlcXVlc3QoJ2h0dHBzOi8vY3Jhd2xlZS5kZXYnKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.xtEUDfrYe6CfTiKS1jtjFTW56R66WCsG8IPnIETMtKI\&asrc=run_on_apify)

```
import asyncio

from crawlee.storages import RequestQueue


async def main() -> None:
    # First you create the request queue instance.
    rq = await RequestQueue.open()

    # And then you add one or more requests to it.
    await rq.add_request('https://crawlee.dev')


if __name__ == '__main__':
    asyncio.run(main())
```

The [`RequestQueue.add_request`](https://crawlee.dev/python/python/api/class/RequestQueue.md#add_request) method automatically converts the object with URL string to a [`Request`](https://crawlee.dev/python/python/api/class/Request.md) instance. So now you have a [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md) that holds one request which points to `https://crawlee.dev`.

Bulk add requests

The code above is for illustration of the request queue concept. Soon you'll learn about the [`BasicCrawler.add_requests`](https://crawlee.dev/python/python/api/class/BasicCrawler.md#add_requests) method which allows you to skip this initialization code, and it also supports adding a large number of requests without blocking.

### Building a BeautifulSoupCrawler[​](#building-a-beautifulsoupcrawler "Direct link to Building a BeautifulSoupCrawler")

Crawlee comes with three main crawler classes: [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md), [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md), and [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md). You can read their short descriptions in the [Quick start](https://crawlee.dev/python/python/docs/quick-start.md) lesson.

Unless you have a good reason to start with a different one, you should try building a [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md) first. It is an HTTP crawler with HTTP2 support, anti-blocking features and integrated HTML parser - [BeautifulSoup](https://pypi.org/project/beautifulsoup4/). It's fast, simple, cheap to run and does not require complicated dependencies. The only downside is that it won't work out of the box for websites which require JavaScript rendering. But you might not need JavaScript rendering at all, because many modern websites use server-side rendering.

Let's continue with the earlier [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md) example.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuIyBBZGQgaW1wb3J0IG9mIGNyYXdsZXIgYW5kIGNyYXdsaW5nIGNvbnRleHQuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcbmZyb20gY3Jhd2xlZS5zdG9yYWdlcyBpbXBvcnQgUmVxdWVzdFF1ZXVlXFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICAjIEZpcnN0IHlvdSBjcmVhdGUgdGhlIHJlcXVlc3QgcXVldWUgaW5zdGFuY2UuXFxuICAgIHJxID0gYXdhaXQgUmVxdWVzdFF1ZXVlLm9wZW4oKVxcblxcbiAgICAjIEFuZCB0aGVuIHlvdSBhZGQgb25lIG9yIG1vcmUgcmVxdWVzdHMgdG8gaXQuXFxuICAgIGF3YWl0IHJxLmFkZF9yZXF1ZXN0KCdodHRwczovL2NyYXdsZWUuZGV2JylcXG5cXG4gICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKHJlcXVlc3RfbWFuYWdlcj1ycSlcXG5cXG4gICAgIyBEZWZpbmUgYSByZXF1ZXN0IGhhbmRsZXIgYW5kIGF0dGFjaCBpdCB0byB0aGUgY3Jhd2xlciB1c2luZyB0aGUgZGVjb3JhdG9yLlxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiByZXF1ZXN0X2hhbmRsZXIoY29udGV4dDogQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgICMgRXh0cmFjdCA8dGl0bGU-IHRleHQgd2l0aCBCZWF1dGlmdWxTb3VwLlxcbiAgICAgICAgIyBTZWUgQmVhdXRpZnVsU291cCBkb2N1bWVudGF0aW9uIGZvciBBUEkgZG9jcy5cXG4gICAgICAgIHVybCA9IGNvbnRleHQucmVxdWVzdC51cmxcXG4gICAgICAgIHRpdGxlID0gY29udGV4dC5zb3VwLnRpdGxlLnN0cmluZyBpZiBjb250ZXh0LnNvdXAudGl0bGUgZWxzZSAnJ1xcbiAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ1RoZSB0aXRsZSBvZiB7dXJsfSBpczoge3RpdGxlfS4nKVxcblxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bigpXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.zu1PyrE-eFAXkHO_Q-woIm6CoTDVJM0zBEz0PDdhNk8\&asrc=run_on_apify)

```
import asyncio

# Add import of crawler and crawling context.
from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext
from crawlee.storages import RequestQueue


async def main() -> None:
    # First you create the request queue instance.
    rq = await RequestQueue.open()

    # And then you add one or more requests to it.
    await rq.add_request('https://crawlee.dev')

    crawler = BeautifulSoupCrawler(request_manager=rq)

    # Define a request handler and attach it to the crawler using the decorator.
    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        # Extract <title> text with BeautifulSoup.
        # See BeautifulSoup documentation for API docs.
        url = context.request.url
        title = context.soup.title.string if context.soup.title else ''
        context.log.info(f'The title of {url} is: {title}.')

    await crawler.run()


if __name__ == '__main__':
    asyncio.run(main())
```

When you run the example, you will see the title of <https://crawlee.dev> printed to the log. What really happens is that [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md) first makes an HTTP request to `https://crawlee.dev`, then parses the received HTML with BeautifulSoup and makes it available as the `context` argument of the request handler.

```
[__main__] INFO  The title of "https://crawlee.dev" is "Crawlee · Build reliable crawlers. Fast. | Crawlee".
```

### Add requests faster[​](#add-requests-faster "Direct link to Add requests faster")

Earlier we mentioned that you'll learn how to use the [`BasicCrawler.add_requests`](https://crawlee.dev/python/python/api/class/BasicCrawler.md#add_requests) method to skip the request queue initialization. It's simple. Every crawler has an implicit [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md) instance, and you can add requests to it with the [`BasicCrawler.add_requests`](https://crawlee.dev/python/python/api/class/BasicCrawler.md#add_requests) method. In fact, you can go even further and just use the first parameter of `crawler.run()`!

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuIyBZb3UgZG9uJ3QgbmVlZCB0byBpbXBvcnQgUmVxdWVzdFF1ZXVlIGFueW1vcmUuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKClcXG5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICB1cmwgPSBjb250ZXh0LnJlcXVlc3QudXJsXFxuICAgICAgICB0aXRsZSA9IGNvbnRleHQuc291cC50aXRsZS5zdHJpbmcgaWYgY29udGV4dC5zb3VwLnRpdGxlIGVsc2UgJydcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidUaGUgdGl0bGUgb2Yge3VybH0gaXM6IHt0aXRsZX0uJylcXG5cXG4gICAgIyBTdGFydCB0aGUgY3Jhd2xlciB3aXRoIHRoZSBwcm92aWRlZCBVUkxzLlxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vY3Jhd2xlZS5kZXYvJ10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.YJB9IR7e81OHAGlrbpMZmTrephFxQmDSI2FHKWat7Qc\&asrc=run_on_apify)

```
import asyncio

# You don't need to import RequestQueue anymore.
from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


async def main() -> None:
    crawler = BeautifulSoupCrawler()

    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        url = context.request.url
        title = context.soup.title.string if context.soup.title else ''
        context.log.info(f'The title of {url} is: {title}.')

    # Start the crawler with the provided URLs.
    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

When you run this code, you'll see exactly the same output as with the earlier, longer example. The [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md) is still there, it's just managed by the crawler automatically.

info

This method not only makes the code shorter, it will help with performance too! Internally it calls [`RequestQueue.add_requests_batched`](https://crawlee.dev/python/python/api/class/RequestQueue.md#add_requests_batched) method. It will wait only for the initial batch of 1000 requests to be added to the queue before resolving, which means the processing will start almost instantly. After that, it will continue adding the rest of the requests in the background (again, in batches of 1000 items, once every second).

## Next steps[​](#next-steps "Direct link to Next steps")

Next, you'll learn about crawling links. That means finding new URLs on the pages you crawl and adding them to the [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md) for the crawler to visit.

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/introduction/02_first_crawler.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/introduction/setting-up.md)

[Setting up](https://crawlee.dev/python/python/docs/introduction/setting-up.md)

[Next](https://crawlee.dev/python/python/docs/introduction/adding-more-urls.md)

[Adding more URLs](https://crawlee.dev/python/python/docs/introduction/adding-more-urls.md)


---

* [](https://crawlee.dev/python/python)
* [Introduction](https://crawlee.dev/python/python/docs/introduction.md)
* Real-world project

Version: 1.6

On this page

# Real-world project

> *Hey, guys, you know, it's cool that we can scrape the `<title>` elements of web pages, but that's not very useful. Can we finally scrape some real data and save it somewhere in a machine-readable format? Because that's why I started reading this tutorial in the first place!*

We hear you, young padawan! First, learn how to crawl, you must. Only then, walk through data, you can!

## Making a production-grade crawler[​](#making-a-production-grade-crawler "Direct link to Making a production-grade crawler")

Making a production-grade crawler is not difficult, but there are many pitfalls of scraping that can catch you off guard. So for the real world project you'll learn how to scrape an [Warehouse store example](https://warehouse-theme-metal.myshopify.com/collections) instead of the Crawlee website. It contains a list of products of different categories, and each product has its own detail page.

The website requires JavaScript rendering, which allows us to showcase more features of Crawlee. We've also added some helpful tips that prepare you for the real-world issues that you will surely encounter when scraping at scale.

Not interested in theory?

If you're not interested in crawling theory, feel free to [skip to the next chapter](https://crawlee.dev/python/python/docs/introduction/crawling.md) and get right back to coding.

## Drawing a plan[​](#drawing-a-plan "Direct link to Drawing a plan")

Sometimes scraping is really straightforward, but most of the time, it really pays off to do a bit of research first and try to answer some of these questions:

* How is the website structured?
* Can I scrape it only with HTTP requests (read "with some [`HttpCrawler`](https://crawlee.dev/python/python/api/class/HttpCrawler.md), e.g. [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md)")?
* Do I need a headless browser for something?
* Are there any anti-scraping protections in place?
* Do I need to parse the HTML or can I get the data otherwise, such as directly from the website's API?

For the purposes of this tutorial, let's assume that the website cannot be scraped with [`HttpCrawler`](https://crawlee.dev/python/python/api/class/HttpCrawler.md). It actually can, but we would have to dive a bit deeper than this introductory guide allows. So for now we will make things easier for you, scrape it with [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md), and you'll learn about headless browsers in the process.

## Choosing the data you need[​](#choosing-the-data-you-need "Direct link to Choosing the data you need")

A good first step is to figure out what data you want to scrape and where to find it. For the time being, let's just agree that we want to scrape all products from all categories available on the [all collections page of the store](https://warehouse-theme-metal.myshopify.com/collections) and for each product we want to get its:

* URL
* Manufacturer
* SKU
* Title
* Current price
* Stock available

You will notice that some information is available directly on the list page, but for details such as "SKU" we'll also need to open the product's detail page.

![data to scrape](/python/assets/images/scraping-practice-c3a7bcc681e36946e25b1f8cfd090a8a.jpg "Overview of data to be scraped.")

### The start URL(s)[​](#the-start-urls "Direct link to The start URL(s)")

This is where you start your crawl. It's convenient to start as close to the data as possible. For example, it wouldn't make much sense to start at <https://warehouse-theme-metal.myshopify.com> and look for a `collections` link there, when we already know that everything we want to extract can be found at the <https://warehouse-theme-metal.myshopify.com/collections> page.

## Exploring the page[​](#exploring-the-page "Direct link to Exploring the page")

Let's take a look at the <https://warehouse-theme-metal.myshopify.com/collections> page more carefully. There are some **categories** on the page, and each category has a list of **items**. On some category pages, at the bottom you will notice there are links to the next pages of results. This is usually called **the pagination**.

### Categories and sorting[​](#categories-and-sorting "Direct link to Categories and sorting")

When you click the categories, you'll see that they load a page of products filtered by that category. By going through a few categories and observing the behavior, we can also observe that we can sort by different conditions (such as `Best selling`, or `Price, low to high`), but for this example, we will not be looking into those.

Limited pagination

Be careful, because on some websites, like [amazon.com](https://amazon.com), this is not true and the sum of products in categories is actually larger than what's available without filters. Learn more in our [tutorial on scraping websites with limited pagination](https://docs.apify.com/tutorials/scrape-paginated-sites).

### Pagination[​](#pagination "Direct link to Pagination")

The pagination of the demo Warehouse Store is simple enough. When switching between pages, you will see that the URL changes to:

```
https://warehouse-theme-metal.myshopify.com/collections/headphones?page=2
```

Try clicking on the link to page 4. You'll see that the pagination links update and show more pages. But can you trust that this will include all pages and won't stop at some point?

Test your assumptions

Similarly to the issue with filters explained above, the existence of pagination does not guarantee that you can simply paginate through all the results. Always test your assumptions about pagination. Otherwise, you might miss a chunk of results, and not even know about it.

At the time of writing the `Headphones` collection results counter showed 75 results - products. Quick count of products on one page of results makes 24. 6 rows times 4 products. This means that there are 4 pages of results.

If you're not convinced, you can visit a page somewhere in the middle, like `https://warehouse-theme-metal.myshopify.com/collections/headphones?page=2` and see how the pagination looks there.

## The crawling strategy[​](#the-crawling-strategy "Direct link to The crawling strategy")

Now that you know where to start and how to find all the collection details, let's look at the crawling process.

1. Visit the store page containing the list of categories (our start URL).

2. Enqueue all links to all categories.

3. Enqueue all product pages from the current page.

4. Enqueue links to next pages of results.

5. Open the next page in queue.

   <!-- -->

   * When it's a results list page, go to 2.
   * When it's a product page, scrape the data.

6. Repeat until all results pages and all products have been processed.

`PlaywrightCrawler` will make sure to visit the pages for you, if you provide the correct requests, and you already know how to enqueue pages, so this should be fairly easy. Nevertheless, there are few more tricks that we'd like to showcase.

## Sanity check[​](#sanity-check "Direct link to Sanity check")

Let's check that everything is set up correctly before writing the scraping logic itself. You might realize that something in your previous analysis doesn't quite add up, or the website might not behave exactly as you expected.

The example below creates a new crawler that visits the start URL and prints the text content of all the categories on that page. When you run the code, you will see the *very badly formatted* content of the individual category card.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuIyBJbnN0ZWFkIG9mIEJlYXV0aWZ1bFNvdXBDcmF3bGVyIGxldCdzIHVzZSBQbGF5d3JpZ2h0IHRvIGJlIGFibGUgdG8gcmVuZGVyIEphdmFTY3JpcHQuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQbGF5d3JpZ2h0Q3Jhd2xlciwgUGxheXdyaWdodENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IFBsYXl3cmlnaHRDcmF3bGVyKClcXG5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IFBsYXl3cmlnaHRDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICAjIFdhaXQgZm9yIHRoZSBjb2xsZWN0aW9uIGNhcmRzIHRvIHJlbmRlciBvbiB0aGUgcGFnZS4gVGhpcyBlbnN1cmVzIHRoYXRcXG4gICAgICAgICMgdGhlIGVsZW1lbnRzIHdlIHdhbnQgdG8gaW50ZXJhY3Qgd2l0aCBhcmUgcHJlc2VudCBpbiB0aGUgRE9NLlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5wYWdlLndhaXRfZm9yX3NlbGVjdG9yKCcuY29sbGVjdGlvbi1ibG9jay1pdGVtJylcXG5cXG4gICAgICAgICMgRXhlY3V0ZSBhIGZ1bmN0aW9uIHdpdGhpbiB0aGUgYnJvd3NlciBjb250ZXh0IHRvIHRhcmdldCB0aGUgY29sbGVjdGlvblxcbiAgICAgICAgIyBjYXJkIGVsZW1lbnRzIGFuZCBleHRyYWN0IHRoZWlyIHRleHQgY29udGVudCwgdHJpbW1pbmcgYW55IGxlYWRpbmcgb3JcXG4gICAgICAgICMgdHJhaWxpbmcgd2hpdGVzcGFjZS5cXG4gICAgICAgIGNhdGVnb3J5X3RleHRzID0gYXdhaXQgY29udGV4dC5wYWdlLmV2YWxfb25fc2VsZWN0b3JfYWxsKFxcbiAgICAgICAgICAgICcuY29sbGVjdGlvbi1ibG9jay1pdGVtJyxcXG4gICAgICAgICAgICAnKGVscykgPT4gZWxzLm1hcChlbCA9PiBlbC50ZXh0Q29udGVudC50cmltKCkpJyxcXG4gICAgICAgIClcXG5cXG4gICAgICAgICMgTG9nIHRoZSBleHRyYWN0ZWQgdGV4dHMuXFxuICAgICAgICBmb3IgaSwgdGV4dCBpbiBlbnVtZXJhdGUoY2F0ZWdvcnlfdGV4dHMpOlxcbiAgICAgICAgICAgIGNvbnRleHQubG9nLmluZm8oZidDQVRFR09SWV97aSArIDF9OiB7dGV4dH0nKVxcblxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vd2FyZWhvdXNlLXRoZW1lLW1ldGFsLm15c2hvcGlmeS5jb20vY29sbGVjdGlvbnMnXSlcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6NDA5NiwidGltZW91dCI6MTgwfX0.nz8wkvaqD3c-jvkrLLrNDSMO6beEwztdRb3xXdkiJTI\&asrc=run_on_apify)

```
import asyncio

# Instead of BeautifulSoupCrawler let's use Playwright to be able to render JavaScript.
from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext


async def main() -> None:
    crawler = PlaywrightCrawler()

    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        # Wait for the collection cards to render on the page. This ensures that
        # the elements we want to interact with are present in the DOM.
        await context.page.wait_for_selector('.collection-block-item')

        # Execute a function within the browser context to target the collection
        # card elements and extract their text content, trimming any leading or
        # trailing whitespace.
        category_texts = await context.page.eval_on_selector_all(
            '.collection-block-item',
            '(els) => els.map(el => el.textContent.trim())',
        )

        # Log the extracted texts.
        for i, text in enumerate(category_texts):
            context.log.info(f'CATEGORY_{i + 1}: {text}')

    await crawler.run(['https://warehouse-theme-metal.myshopify.com/collections'])


if __name__ == '__main__':
    asyncio.run(main())
```

If you're wondering how to get that `.collection-block-item` selector. We'll explain it in the next chapter on DevTools.

## DevTools - the scraper's toolbox[​](#devtools---the-scrapers-toolbox "Direct link to DevTools - the scraper's toolbox")

DevTool choice

We'll use Chrome DevTools here, since it's the most common browser, but feel free to use any other, they're all very similar.

Let's open DevTools by going to <https://warehouse-theme-metal.myshopify.com/collections> in Chrome and then right-clicking anywhere in the page and selecting **Inspect**, or by pressing **F12** or whatever your system prefers. With DevTools, you can inspect or manipulate any aspect of the currently open web page. You can learn more about DevTools in their [official documentation](https://developer.chrome.com/docs/devtools/).

## Selecting elements[​](#selecting-elements "Direct link to Selecting elements")

In the DevTools, choose the **Select an element** tool and try hovering over one of the Actor cards.

![select an element](/python/assets/images/select-an-element-64d58df5af5cde98d2d63ba3e57af890.jpg "Finding the select an element tool.")

You'll see that you can select different elements inside the card. Instead, select the whole card, not just some of its contents, such as its title or description.

![selected element](/python/assets/images/selected-element-b2a329cd79075402842c664410116454.jpg "Selecting an element by hovering over it.")

Selecting an element will highlight it in the DevTools HTML inspector. When carefully look at the elements, you'll see that there are some **classes** attached to the different HTML elements. Those are called **CSS classes**, and we can make a use of them in scraping.

Conversely, by hovering over elements in the HTML inspector, you will see them highlight on the page. Inspect the page's structure around the collection card. You'll see that all the card's data is displayed in an `<a>` element with a `class` attribute that includes **collection-block-item**. It should now make sense how we got that `.collection-block-item` selector. It's just a way to find all elements that are annotated with the `collection-block-item`.

It's always a good idea to double-check that you're not getting any unwanted elements with this class. To do that, go into the **Console** tab of DevTools and run:

```
document.querySelectorAll('.collection-block-item');
```

You will see that only the 31 collection cards will be returned, and nothing else.

Learn more about CSS selectors and DevTools

CSS selectors and DevTools are quite a big topic. If you want to learn more, visit the [Web scraping for beginners course](https://developers.apify.com/academy/web-scraping-for-beginners) in the Apify Academy. **It's free and open-source** ❤️.

## Next steps[​](#next-steps "Direct link to Next steps")

Next, you will crawl the whole store, including all the listing pages and all the product detail pages.

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/introduction/04_real_world_project.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/introduction/adding-more-urls.md)

[Adding more URLs](https://crawlee.dev/python/python/docs/introduction/adding-more-urls.md)

[Next](https://crawlee.dev/python/python/docs/introduction/crawling.md)

[Crawling](https://crawlee.dev/python/python/docs/introduction/crawling.md)


---

* [](https://crawlee.dev/python/python)
* [Introduction](https://crawlee.dev/python/python/docs/introduction.md)
* Refactoring

Version: 1.6

On this page

# Refactoring

It may seem that the data is extracted and the crawler is done, but honestly, this is just the beginning. For the sake of brevity, we've completely omitted error handling, proxies, logging, architecture, tests, documentation and other stuff that a reliable software should have. The good thing is, error handling is mostly done by Crawlee itself, so no worries on that front, unless you need some custom magic.

Navigating automatic bot-protextion avoidance

You might be wondering about the **anti-blocking, bot-protection avoiding stealthy features** and why we haven't highlighted them yet. The reason is straightforward: these features are **automatically used** within the default configuration, providing a smooth start without manual adjustments.

<!-- -->

To promote good coding practices, let's look at how you can use a [`Router`](https://crawlee.dev/python/python/api/class/Router.md) class to better structure your crawler code.

## Request routing[​](#request-routing "Direct link to Request routing")

In the following code, we've made several changes:

* Split the code into multiple files.
* Added custom instance of [`Router`](https://crawlee.dev/python/python/api/class/Router.md) to make our routing cleaner, without if clauses.
* Moved route definitions to a separate `routes.py` file.
* Simplified the `main.py` file to focus on the general structure of the crawler.

### Routes file[​](#routes-file "Direct link to Routes file")

First, let's define our routes in a separate file:

src/routes.py

```
from crawlee.crawlers import PlaywrightCrawlingContext
from crawlee.router import Router

router = Router[PlaywrightCrawlingContext]()


@router.default_handler
async def default_handler(context: PlaywrightCrawlingContext) -> None:
    # This is a fallback route which will handle the start URL.
    context.log.info(f'default_handler is processing {context.request.url}')

    await context.page.wait_for_selector('.collection-block-item')

    await context.enqueue_links(
        selector='.collection-block-item',
        label='CATEGORY',
    )


@router.handler('CATEGORY')
async def category_handler(context: PlaywrightCrawlingContext) -> None:
    # This replaces the context.request.label == CATEGORY branch of the if clause.
    context.log.info(f'category_handler is processing {context.request.url}')

    await context.page.wait_for_selector('.product-item > a')

    await context.enqueue_links(
        selector='.product-item > a',
        label='DETAIL',
    )

    next_button = await context.page.query_selector('a.pagination__next')

    if next_button:
        await context.enqueue_links(
            selector='a.pagination__next',
            label='CATEGORY',
        )


@router.handler('DETAIL')
async def detail_handler(context: PlaywrightCrawlingContext) -> None:
    # This replaces the context.request.label == DETAIL branch of the if clause.
    context.log.info(f'detail_handler is processing {context.request.url}')

    url_part = context.request.url.split('/').pop()
    manufacturer = url_part.split('-')[0]

    title = await context.page.locator('.product-meta h1').text_content()

    sku = await context.page.locator('span.product-meta__sku-number').text_content()

    price_element = context.page.locator('span.price', has_text='$').first
    current_price_string = await price_element.text_content() or ''
    raw_price = current_price_string.split('$')[1]
    price = float(raw_price.replace(',', ''))

    in_stock_element = context.page.locator(
        selector='span.product-form__inventory',
        has_text='In stock',
    ).first
    in_stock = await in_stock_element.count() > 0

    data = {
        'manufacturer': manufacturer,
        'title': title,
        'sku': sku,
        'price': price,
        'in_stock': in_stock,
    }

    await context.push_data(data)
```

### Main file[​](#main-file "Direct link to Main file")

Next, our main file becomes much simpler and cleaner:

src/main.py

```
import asyncio

from crawlee.crawlers import PlaywrightCrawler

from .routes import router


async def main() -> None:
    crawler = PlaywrightCrawler(
        # Let's limit our crawls to make our tests shorter and safer.
        max_requests_per_crawl=10,
        # Provide our router instance to the crawler.
        request_handler=router,
    )

    await crawler.run(['https://warehouse-theme-metal.myshopify.com/collections'])


if __name__ == '__main__':
    asyncio.run(main())
```

By structuring your code this way, you achieve better separation of concerns, making the code easier to read, manage and extend. The [`Router`](https://crawlee.dev/python/python/api/class/Router.md) class keeps your routing logic clean and modular, replacing if clauses with function decorators.

## Summary[​](#summary "Direct link to Summary")

Refactoring your crawler code with these practices enhances readability, maintainability, and scalability.

### Splitting your code into multiple files[​](#splitting-your-code-into-multiple-files "Direct link to Splitting your code into multiple files")

There's no reason not to split your code into multiple files and keep your logic separate. Less code in a single file means less complexity to handle at any time, which improves overall readability and maintainability. Consider further splitting the routes into separate files for even better organization.

### Using a router to structure your crawling[​](#using-a-router-to-structure-your-crawling "Direct link to Using a router to structure your crawling")

Initially, using a simple `if` / `else` statement for selecting different logic based on the crawled pages might appear more readable. However, this approach can become cumbersome with more than two types of pages, especially when the logic for each page extends over dozens or even hundreds of lines of code.

It's good practice in any programming language to split your logic into bite-sized chunks that are easy to read and reason about. Scrolling through a thousand line long `request_handler()` where everything interacts with everything and variables can be used everywhere is not a beautiful thing to do and a pain to debug. That's why we prefer the separation of routes into their own files.

## Next steps[​](#next-steps "Direct link to Next steps")

In the next and final step, you'll see how to deploy your Crawlee project to the cloud. If you used the CLI to bootstrap your project, you already have a `Dockerfile` ready, and the next section will show you how to deploy it to the [Apify platform](https://crawlee.dev/python/python/docs/deployment/apify-platform.md) with ease.

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/introduction/08_refactoring.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/introduction/saving-data.md)

[Saving data](https://crawlee.dev/python/python/docs/introduction/saving-data.md)

[Next](https://crawlee.dev/python/python/docs/introduction/deployment.md)

[Running in the Cloud](https://crawlee.dev/python/python/docs/introduction/deployment.md)


---

* [](https://crawlee.dev/python/python)
* [Introduction](https://crawlee.dev/python/python/docs/introduction.md)
* Saving data

Version: 1.6

On this page

# Saving data

A data extraction job would not be complete without saving the data for later use and processing. You've come to the final and most difficult part of this tutorial so make sure to pay attention very carefully!

## Save data to the dataset[​](#save-data-to-the-dataset "Direct link to Save data to the dataset")

Crawlee provides a [`Dataset`](https://crawlee.dev/python/python/api/class/Dataset.md) class, which acts as an abstraction over tabular storage, making it useful for storing scraping results. To get started:

* Add the necessary imports: Include the [`Dataset`](https://crawlee.dev/python/python/api/class/Dataset.md) and any required crawler classes at the top of your file.
* Create a Dataset instance: Use the asynchronous [`Dataset.open`](https://crawlee.dev/python/python/api/class/Dataset.md#open) constructor to initialize the dataset instance within your crawler's setup.

Here's an example:

```
import asyncio

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext
from crawlee.storages import Dataset

# ...


async def main() -> None:
    crawler = PlaywrightCrawler()
    dataset = await Dataset.open()

    # ...

    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        ...
        # ...


if __name__ == '__main__':
    asyncio.run(main())
```

Finally, instead of logging the extracted data to stdout, we can export them to the dataset:

```
# ...

    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        # ...

        data = {
            'manufacturer': manufacturer,
            'title': title,
            'sku': sku,
            'price': price,
            'in_stock': in_stock,
        }

        # Push the data to the dataset.
        await dataset.push_data(data)

        # ...
```

### Using a context helper[​](#using-a-context-helper "Direct link to Using a context helper")

Instead of importing a new class and manually creating an instance of the dataset, you can use the context helper [`context.push_data`](https://crawlee.dev/python/python/api/class/PushDataFunction.md). Remove the dataset import and instantiation, and replace `dataset.push_data` with the following:

```
# ...

    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        # ...

        data = {
            'manufacturer': manufacturer,
            'title': title,
            'sku': sku,
            'price': price,
            'in_stock': in_stock,
        }

        # Push the data to the dataset.
        await context.push_data(data)

        # ...
```

### Final code[​](#final-code "Direct link to Final code")

And that's it. Unlike earlier, we are being serious now. That's it, you're done. The final code looks like this:

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQbGF5d3JpZ2h0Q3Jhd2xlciwgUGxheXdyaWdodENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IFBsYXl3cmlnaHRDcmF3bGVyKFxcbiAgICAgICAgIyBMZXQncyBsaW1pdCBvdXIgY3Jhd2xzIHRvIG1ha2Ugb3VyIHRlc3RzIHNob3J0ZXIgYW5kIHNhZmVyLlxcbiAgICAgICAgbWF4X3JlcXVlc3RzX3Blcl9jcmF3bD0xMCxcXG4gICAgKVxcblxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiByZXF1ZXN0X2hhbmRsZXIoY29udGV4dDogUGxheXdyaWdodENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm9jZXNzaW5nIHtjb250ZXh0LnJlcXVlc3QudXJsfScpXFxuXFxuICAgICAgICAjIFdlJ3JlIG5vdCBwcm9jZXNzaW5nIGRldGFpbCBwYWdlcyB5ZXQsIHNvIHdlIGp1c3QgcGFzcy5cXG4gICAgICAgIGlmIGNvbnRleHQucmVxdWVzdC5sYWJlbCA9PSAnREVUQUlMJzpcXG4gICAgICAgICAgICAjIFNwbGl0IHRoZSBVUkwgYW5kIGdldCB0aGUgbGFzdCBwYXJ0IHRvIGV4dHJhY3QgdGhlIG1hbnVmYWN0dXJlci5cXG4gICAgICAgICAgICB1cmxfcGFydCA9IGNvbnRleHQucmVxdWVzdC51cmwuc3BsaXQoJy8nKS5wb3AoKVxcbiAgICAgICAgICAgIG1hbnVmYWN0dXJlciA9IHVybF9wYXJ0LnNwbGl0KCctJylbMF1cXG5cXG4gICAgICAgICAgICAjIEV4dHJhY3QgdGhlIHRpdGxlIHVzaW5nIHRoZSBjb21iaW5lZCBzZWxlY3Rvci5cXG4gICAgICAgICAgICB0aXRsZSA9IGF3YWl0IGNvbnRleHQucGFnZS5sb2NhdG9yKCcucHJvZHVjdC1tZXRhIGgxJykudGV4dF9jb250ZW50KClcXG5cXG4gICAgICAgICAgICAjIEV4dHJhY3QgdGhlIFNLVSB1c2luZyBpdHMgc2VsZWN0b3IuXFxuICAgICAgICAgICAgc2t1ID0gYXdhaXQgY29udGV4dC5wYWdlLmxvY2F0b3IoXFxuICAgICAgICAgICAgICAgICdzcGFuLnByb2R1Y3QtbWV0YV9fc2t1LW51bWJlcidcXG4gICAgICAgICAgICApLnRleHRfY29udGVudCgpXFxuXFxuICAgICAgICAgICAgIyBMb2NhdGUgdGhlIHByaWNlIGVsZW1lbnQgdGhhdCBjb250YWlucyB0aGUgJyQnIHNpZ24gYW5kIGZpbHRlciBvdXRcXG4gICAgICAgICAgICAjIHRoZSB2aXN1YWxseSBoaWRkZW4gZWxlbWVudHMuXFxuICAgICAgICAgICAgcHJpY2VfZWxlbWVudCA9IGNvbnRleHQucGFnZS5sb2NhdG9yKCdzcGFuLnByaWNlJywgaGFzX3RleHQ9JyQnKS5maXJzdFxcbiAgICAgICAgICAgIGN1cnJlbnRfcHJpY2Vfc3RyaW5nID0gYXdhaXQgcHJpY2VfZWxlbWVudC50ZXh0X2NvbnRlbnQoKSBvciAnJ1xcbiAgICAgICAgICAgIHJhd19wcmljZSA9IGN1cnJlbnRfcHJpY2Vfc3RyaW5nLnNwbGl0KCckJylbMV1cXG4gICAgICAgICAgICBwcmljZSA9IGZsb2F0KHJhd19wcmljZS5yZXBsYWNlKCcsJywgJycpKVxcblxcbiAgICAgICAgICAgICMgTG9jYXRlIHRoZSBlbGVtZW50IHRoYXQgY29udGFpbnMgdGhlIHRleHQgJ0luIHN0b2NrJyBhbmQgZmlsdGVyIG91dFxcbiAgICAgICAgICAgICMgb3RoZXIgZWxlbWVudHMuXFxuICAgICAgICAgICAgaW5fc3RvY2tfZWxlbWVudCA9IGNvbnRleHQucGFnZS5sb2NhdG9yKFxcbiAgICAgICAgICAgICAgICBzZWxlY3Rvcj0nc3Bhbi5wcm9kdWN0LWZvcm1fX2ludmVudG9yeScsXFxuICAgICAgICAgICAgICAgIGhhc190ZXh0PSdJbiBzdG9jaycsXFxuICAgICAgICAgICAgKS5maXJzdFxcbiAgICAgICAgICAgIGluX3N0b2NrID0gYXdhaXQgaW5fc3RvY2tfZWxlbWVudC5jb3VudCgpID4gMFxcblxcbiAgICAgICAgICAgICMgUHV0IGl0IGFsbCB0b2dldGhlciBpbiBhIGRpY3Rpb25hcnkuXFxuICAgICAgICAgICAgZGF0YSA9IHtcXG4gICAgICAgICAgICAgICAgJ21hbnVmYWN0dXJlcic6IG1hbnVmYWN0dXJlcixcXG4gICAgICAgICAgICAgICAgJ3RpdGxlJzogdGl0bGUsXFxuICAgICAgICAgICAgICAgICdza3UnOiBza3UsXFxuICAgICAgICAgICAgICAgICdwcmljZSc6IHByaWNlLFxcbiAgICAgICAgICAgICAgICAnaW5fc3RvY2snOiBpbl9zdG9jayxcXG4gICAgICAgICAgICB9XFxuXFxuICAgICAgICAgICAgIyBQdXNoIHRoZSBkYXRhIHRvIHRoZSBkYXRhc2V0LlxcbiAgICAgICAgICAgIGF3YWl0IGNvbnRleHQucHVzaF9kYXRhKGRhdGEpXFxuXFxuICAgICAgICAjIFdlIGFyZSBub3cgb24gYSBjYXRlZ29yeSBwYWdlLiBXZSBjYW4gdXNlIHRoaXMgdG8gcGFnaW5hdGUgdGhyb3VnaCBhbmRcXG4gICAgICAgICMgZW5xdWV1ZSBhbGwgcHJvZHVjdHMsIGFzIHdlbGwgYXMgYW55IHN1YnNlcXVlbnQgcGFnZXMgd2UgZmluZC5cXG4gICAgICAgIGVsaWYgY29udGV4dC5yZXF1ZXN0LmxhYmVsID09ICdDQVRFR09SWSc6XFxuICAgICAgICAgICAgIyBXYWl0IGZvciB0aGUgcHJvZHVjdCBpdGVtcyB0byByZW5kZXIuXFxuICAgICAgICAgICAgYXdhaXQgY29udGV4dC5wYWdlLndhaXRfZm9yX3NlbGVjdG9yKCcucHJvZHVjdC1pdGVtID4gYScpXFxuXFxuICAgICAgICAgICAgIyBFbnF1ZXVlIGxpbmtzIGZvdW5kIHdpdGhpbiBlbGVtZW50cyBtYXRjaGluZyB0aGUgcHJvdmlkZWQgc2VsZWN0b3IuXFxuICAgICAgICAgICAgIyBUaGVzZSBsaW5rcyB3aWxsIGJlIGFkZGVkIHRvIHRoZSBjcmF3bGluZyBxdWV1ZSB3aXRoIHRoZSBsYWJlbCBERVRBSUwuXFxuICAgICAgICAgICAgYXdhaXQgY29udGV4dC5lbnF1ZXVlX2xpbmtzKFxcbiAgICAgICAgICAgICAgICBzZWxlY3Rvcj0nLnByb2R1Y3QtaXRlbSA-IGEnLFxcbiAgICAgICAgICAgICAgICBsYWJlbD0nREVUQUlMJyxcXG4gICAgICAgICAgICApXFxuXFxuICAgICAgICAgICAgIyBGaW5kIHRoZSBcXFwiTmV4dFxcXCIgYnV0dG9uIHRvIHBhZ2luYXRlIHRocm91Z2ggdGhlIGNhdGVnb3J5IHBhZ2VzLlxcbiAgICAgICAgICAgIG5leHRfYnV0dG9uID0gYXdhaXQgY29udGV4dC5wYWdlLnF1ZXJ5X3NlbGVjdG9yKCdhLnBhZ2luYXRpb25fX25leHQnKVxcblxcbiAgICAgICAgICAgICMgSWYgYSBcXFwiTmV4dFxcXCIgYnV0dG9uIGlzIGZvdW5kLCBlbnF1ZXVlIHRoZSBuZXh0IHBhZ2Ugb2YgcmVzdWx0cy5cXG4gICAgICAgICAgICBpZiBuZXh0X2J1dHRvbjpcXG4gICAgICAgICAgICAgICAgYXdhaXQgY29udGV4dC5lbnF1ZXVlX2xpbmtzKFxcbiAgICAgICAgICAgICAgICAgICAgc2VsZWN0b3I9J2EucGFnaW5hdGlvbl9fbmV4dCcsXFxuICAgICAgICAgICAgICAgICAgICBsYWJlbD0nQ0FURUdPUlknLFxcbiAgICAgICAgICAgICAgICApXFxuXFxuICAgICAgICAjIFRoaXMgaW5kaWNhdGVzIHdlJ3JlIG9uIHRoZSBzdGFydCBwYWdlIHdpdGggbm8gc3BlY2lmaWMgbGFiZWwuXFxuICAgICAgICAjIE9uIHRoZSBzdGFydCBwYWdlLCB3ZSB3YW50IHRvIGVucXVldWUgYWxsIHRoZSBjYXRlZ29yeSBwYWdlcy5cXG4gICAgICAgIGVsc2U6XFxuICAgICAgICAgICAgIyBXYWl0IGZvciB0aGUgY29sbGVjdGlvbiBjYXJkcyB0byByZW5kZXIuXFxuICAgICAgICAgICAgYXdhaXQgY29udGV4dC5wYWdlLndhaXRfZm9yX3NlbGVjdG9yKCcuY29sbGVjdGlvbi1ibG9jay1pdGVtJylcXG5cXG4gICAgICAgICAgICAjIEVucXVldWUgbGlua3MgZm91bmQgd2l0aGluIGVsZW1lbnRzIG1hdGNoaW5nIHRoZSBwcm92aWRlZCBzZWxlY3Rvci5cXG4gICAgICAgICAgICAjIFRoZXNlIGxpbmtzIHdpbGwgYmUgYWRkZWQgdG8gdGhlIGNyYXdsaW5nIHF1ZXVlIHdpdGggdGhlIGxhYmVsIENBVEVHT1JZLlxcbiAgICAgICAgICAgIGF3YWl0IGNvbnRleHQuZW5xdWV1ZV9saW5rcyhcXG4gICAgICAgICAgICAgICAgc2VsZWN0b3I9Jy5jb2xsZWN0aW9uLWJsb2NrLWl0ZW0nLFxcbiAgICAgICAgICAgICAgICBsYWJlbD0nQ0FURUdPUlknLFxcbiAgICAgICAgICAgIClcXG5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL3dhcmVob3VzZS10aGVtZS1tZXRhbC5teXNob3BpZnkuY29tL2NvbGxlY3Rpb25zJ10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjQwOTYsInRpbWVvdXQiOjE4MH19.v7DDzHWFI6tkeduEq8uWmtO1WfUXHLloL-e5spzkZu4\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext


async def main() -> None:
    crawler = PlaywrightCrawler(
        # Let's limit our crawls to make our tests shorter and safer.
        max_requests_per_crawl=10,
    )

    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url}')

        # We're not processing detail pages yet, so we just pass.
        if context.request.label == 'DETAIL':
            # Split the URL and get the last part to extract the manufacturer.
            url_part = context.request.url.split('/').pop()
            manufacturer = url_part.split('-')[0]

            # Extract the title using the combined selector.
            title = await context.page.locator('.product-meta h1').text_content()

            # Extract the SKU using its selector.
            sku = await context.page.locator(
                'span.product-meta__sku-number'
            ).text_content()

            # Locate the price element that contains the '$' sign and filter out
            # the visually hidden elements.
            price_element = context.page.locator('span.price', has_text='$').first
            current_price_string = await price_element.text_content() or ''
            raw_price = current_price_string.split('$')[1]
            price = float(raw_price.replace(',', ''))

            # Locate the element that contains the text 'In stock' and filter out
            # other elements.
            in_stock_element = context.page.locator(
                selector='span.product-form__inventory',
                has_text='In stock',
            ).first
            in_stock = await in_stock_element.count() > 0

            # Put it all together in a dictionary.
            data = {
                'manufacturer': manufacturer,
                'title': title,
                'sku': sku,
                'price': price,
                'in_stock': in_stock,
            }

            # Push the data to the dataset.
            await context.push_data(data)

        # We are now on a category page. We can use this to paginate through and
        # enqueue all products, as well as any subsequent pages we find.
        elif context.request.label == 'CATEGORY':
            # Wait for the product items to render.
            await context.page.wait_for_selector('.product-item > a')

            # Enqueue links found within elements matching the provided selector.
            # These links will be added to the crawling queue with the label DETAIL.
            await context.enqueue_links(
                selector='.product-item > a',
                label='DETAIL',
            )

            # Find the "Next" button to paginate through the category pages.
            next_button = await context.page.query_selector('a.pagination__next')

            # If a "Next" button is found, enqueue the next page of results.
            if next_button:
                await context.enqueue_links(
                    selector='a.pagination__next',
                    label='CATEGORY',
                )

        # This indicates we're on the start page with no specific label.
        # On the start page, we want to enqueue all the category pages.
        else:
            # Wait for the collection cards to render.
            await context.page.wait_for_selector('.collection-block-item')

            # Enqueue links found within elements matching the provided selector.
            # These links will be added to the crawling queue with the label CATEGORY.
            await context.enqueue_links(
                selector='.collection-block-item',
                label='CATEGORY',
            )

    await crawler.run(['https://warehouse-theme-metal.myshopify.com/collections'])


if __name__ == '__main__':
    asyncio.run(main())
```

## What `push_data` does?[​](#what-push_data-does "Direct link to what-push_data-does")

A helper [`context.push_data`](https://crawlee.dev/python/python/api/class/PushDataFunction.md) saves data to the default dataset. You can provide additional arguments there like `id` or `name` to open a different dataset. Dataset is a storage designed to hold data in a format similar to a table. Each time you call [`context.push_data`](https://crawlee.dev/python/python/api/class/PushDataFunction.md) or direct [`Dataset.push_data`](https://crawlee.dev/python/python/api/class/Dataset.md#push_data) a new row in the table is created, with the property names serving as column titles. In the default configuration, the rows are represented as JSON files saved on your file system, but other backend storage systems can be plugged into Crawlee as well. More on that later.

Automatic dataset initialization

Each time you start Crawlee a default [`Dataset`](https://crawlee.dev/python/python/api/class/Dataset.md) is automatically created, so there's no need to initialize it or create an instance first. You can create as many datasets as you want and even give them names. For more details see the [`Dataset.open`](https://crawlee.dev/python/python/api/class/Dataset.md#open) function.

<!-- -->

## Finding saved data[​](#finding-saved-data "Direct link to Finding saved data")

Unless you changed the configuration that Crawlee uses locally, which would suggest that you knew what you were doing, and you didn't need this tutorial anyway, you'll find your data in the storage directory that Crawlee creates in the working directory of the running script:

```
{PROJECT_FOLDER}/storage/datasets/default/
```

The above folder will hold all your saved data in numbered files, as they were pushed into the dataset. Each file represents one invocation of [`Dataset.push_data`](https://crawlee.dev/python/python/api/class/Dataset.md#push_data) or one table row.

<!-- -->

## Next steps[​](#next-steps "Direct link to Next steps")

Next, you'll see some improvements that you can add to your crawler code that will make it more readable and maintainable in the long run.

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/introduction/07_saving_data.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/introduction/scraping.md)

[Scraping](https://crawlee.dev/python/python/docs/introduction/scraping.md)

[Next](https://crawlee.dev/python/python/docs/introduction/refactoring.md)

[Refactoring](https://crawlee.dev/python/python/docs/introduction/refactoring.md)


---

* [](https://crawlee.dev/python/python)
* [Introduction](https://crawlee.dev/python/python/docs/introduction.md)
* Scraping

Version: 1.6

On this page

# Scraping

In the [Real-world project](https://crawlee.dev/python/python/docs/introduction/real-world-project.md#choosing-the-data-you-need) chapter, you've created a list of the information you wanted to collect about the products in the example Warehouse store. Let's review that and figure out ways to access the data.

* URL
* Manufacturer
* SKU
* Title
* Current price
* Stock available

![data to scrape](/python/assets/images/scraping-practice-c3a7bcc681e36946e25b1f8cfd090a8a.jpg "Overview of data to be scraped.")

## Scraping the URL and manufacturer[​](#scraping-the-url-and-manufacturer "Direct link to Scraping the URL and manufacturer")

Some information is lying right there in front of us without even having to touch the product detail pages. The `URL` we already have - the `context.request.url`. And by looking at it carefully, we realize that we can also extract the manufacturer from the URL (as all product urls start with `/products/<manufacturer>`). We can just split the `string` and be on our way then!

url vs loaded url

You can use `request.loaded_url` as well. Remember the difference: `request.url` is what you enqueue, `request.loaded_url` is what gets processed (after possible redirects).

By splitting the `request.url`, we can extract the manufacturer name directly from the URL. This is done by first splitting the URL to get the product identifier and then splitting that identifier to get the manufacturer name.

```
# context.request.url:
# https://warehouse-theme-metal.myshopify.com/products/sennheiser-mke-440-professional-stereo-shotgun-microphone-mke-440

# Split the URL and get the last part.
url_part = context.request.url.split('/').pop()
# url_part: sennheiser-mke-440-professional-stereo-shotgun-microphone-mke-440

# Split the last part by '-' and get the first element.
manufacturer = url_part.split('-')[0]
# manufacturer: 'sennheiser'
```

Storing information

It's a matter of preference, whether to store this information separately in the resulting dataset, or not. Whoever uses the dataset can easily parse the `manufacturer` from the `URL`, so should you duplicate the data unnecessarily? Our opinion is that unless the increased data consumption would be too large to bear, it's better to make the dataset as rich as possible. For example, someone might want to filter by `manufacturer`.

Adapt and extract

One thing you may notice is that the `manufacturer` might have a `-` in its name. If that's the case, your best bet is extracting it from the details page instead, but it's not mandatory. At the end of the day, you should always adjust and pick the best solution for your use case, and website you are crawling.

Now it's time to add more data to the results. Let's open one of the product detail pages, for example the [Sony XBR-950G](https://warehouse-theme-metal.myshopify.com/products/sony-xbr-65x950g-65-class-64-5-diag-bravia-4k-hdr-ultra-hd-tv) page and use our DevTools-Fu 🥋 to figure out how to get the title of the product.

## Scraping title[​](#scraping-title "Direct link to Scraping title")

To scrape the product title from a webpage, you need to identify its location in the HTML structure. By using the element selector tool in your browser's DevTools, you can see that the title is within an `<h1>` tag, which is a common practice for important headers. This `<h1>` tag is enclosed in a `<div>` with the class product-meta. We can leverage this structure to create a combined selector `.product-meta h1`. This selector targets any `<h1>` element that is a child of an element with the class `product-meta`.

![product title](/python/assets/images/title-ead2d5aff4a326c2268db2b640d3db9d.jpg "Finding product title in DevTools.")

Verifying selectors with DevTools

Remember that you can press CTRL+F (or CMD+F on Mac) in the **Elements** tab of DevTools to open the search bar where you can quickly search for elements using their selectors. Always verify your scraping process and assumptions using the DevTools. It's faster than changing the crawler code all the time.

To get the title, you need to locate it using Playwright with the `.product-meta h1` selector. This selector specifically targets the `<h1>` element you need. If multiple elements match, it will throw an error, which is beneficial as it prevents returning incorrect data silently. Ensuring the accuracy of your selectors is crucial for reliable data extraction.

```
title = await context.page.locator('.product-meta h1').text_content()
```

## Scraping SKU[​](#scraping-sku "Direct link to Scraping SKU")

Using the DevTools, you can find that the product SKU is inside a `<span>` tag with the class `product-meta__sku-number`. Since there is no other `<span>` with that class on the page, you can safely use this selector to extract the SKU.

![product sku selector](/python/assets/images/sku-dbf299877f71a3c4a03fb52f01e1c202.jpg "Finding product SKU in DevTools.")

```
# Find the SKU element using the selector and get its text content.
sku = await context.page.locator('span.product-meta__sku-number').text_content()
```

## Scraping current price[​](#scraping-current-price "Direct link to Scraping current price")

Using DevTools, you can find that the current price is within a `<span>` element tagged with the `price` class. However, it is nested alongside another `<span>` element with the `visually-hidden` class. To avoid extracting the wrong text, you can filter the elements to get the correct one using the `has_text` helper.

![product current price selector](/python/assets/images/current-price-31a43915970fa9a766b57392b8f1f764.jpg "Finding product current price in DevTools.")

```
# Locate the price element and filter out the visually hidden elements.
price_element = context.page.locator('span.price', has_text='$').first

# Extract the text content of the price element.
current_price_string = await price_element.text_content() or ''
# current_price_string: 'Sale price$1,398.00'

# Split the string by the '$' sign to get the numeric part.
raw_price = current_price_string.split('$')[1]
# raw_price: '1,398.00'

# Convert the raw price string to a float after removing commas.
price = float(raw_price.replace(',', ''))
# price: 1398.00
```

It might look a little complex at first glance, but let's walk through what you did. First, you locate the correct part of the `price` span by filtering for elements containing the `$` sign. This ensures that you get the actual price element. Once you have the right element, you extract its text content, which gives you a string similar to `Sale price$1,398.00`. To get the numeric value, you split this string by the `$` sign. Next, you remove any commas from the resulting numeric string and convert it to a float, allowing you to work with the price as a number. This process ensures that you accurately extract and convert the current price from the product page.

## Scraping stock availability[​](#scraping-stock-availability "Direct link to Scraping stock availability")

The final step is to scrape the stock availability information. There is a `<span>` with the class `product-form__inventory`, which contains the text `In stock` if the product is available. You can use the `has_text` helper to filter out the correct element.

```
# Locate the element that contains the text 'In stock' and filter out other elements.
in_stock_element = context.page.locator(
    selector='span.product-form__inventory',
    has_text='In stock',
).first

# Check if the element exists by counting the matching elements.
in_stock = await in_stock_element.count() > 0
```

For this, all that matters is whether the element exists or not. You can use the `count()` method to check if any elements match the selector. If there are, it means the product is in stock.

## Trying it out[​](#trying-it-out "Direct link to Trying it out")

You have everything that is needed, so grab your newly created scraping logic, dump it into your original request handler and see the magic happen!

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQbGF5d3JpZ2h0Q3Jhd2xlciwgUGxheXdyaWdodENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IFBsYXl3cmlnaHRDcmF3bGVyKFxcbiAgICAgICAgIyBMZXQncyBsaW1pdCBvdXIgY3Jhd2xzIHRvIG1ha2Ugb3VyIHRlc3RzIHNob3J0ZXIgYW5kIHNhZmVyLlxcbiAgICAgICAgbWF4X3JlcXVlc3RzX3Blcl9jcmF3bD0xMCxcXG4gICAgKVxcblxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiByZXF1ZXN0X2hhbmRsZXIoY29udGV4dDogUGxheXdyaWdodENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm9jZXNzaW5nIHtjb250ZXh0LnJlcXVlc3QudXJsfScpXFxuXFxuICAgICAgICAjIFdlJ3JlIG5vdCBwcm9jZXNzaW5nIGRldGFpbCBwYWdlcyB5ZXQsIHNvIHdlIGp1c3QgcGFzcy5cXG4gICAgICAgIGlmIGNvbnRleHQucmVxdWVzdC5sYWJlbCA9PSAnREVUQUlMJzpcXG4gICAgICAgICAgICAjIFNwbGl0IHRoZSBVUkwgYW5kIGdldCB0aGUgbGFzdCBwYXJ0IHRvIGV4dHJhY3QgdGhlIG1hbnVmYWN0dXJlci5cXG4gICAgICAgICAgICB1cmxfcGFydCA9IGNvbnRleHQucmVxdWVzdC51cmwuc3BsaXQoJy8nKS5wb3AoKVxcbiAgICAgICAgICAgIG1hbnVmYWN0dXJlciA9IHVybF9wYXJ0LnNwbGl0KCctJylbMF1cXG5cXG4gICAgICAgICAgICAjIEV4dHJhY3QgdGhlIHRpdGxlIHVzaW5nIHRoZSBjb21iaW5lZCBzZWxlY3Rvci5cXG4gICAgICAgICAgICB0aXRsZSA9IGF3YWl0IGNvbnRleHQucGFnZS5sb2NhdG9yKCcucHJvZHVjdC1tZXRhIGgxJykudGV4dF9jb250ZW50KClcXG5cXG4gICAgICAgICAgICAjIEV4dHJhY3QgdGhlIFNLVSB1c2luZyBpdHMgc2VsZWN0b3IuXFxuICAgICAgICAgICAgc2t1ID0gYXdhaXQgY29udGV4dC5wYWdlLmxvY2F0b3IoXFxuICAgICAgICAgICAgICAgICdzcGFuLnByb2R1Y3QtbWV0YV9fc2t1LW51bWJlcidcXG4gICAgICAgICAgICApLnRleHRfY29udGVudCgpXFxuXFxuICAgICAgICAgICAgIyBMb2NhdGUgdGhlIHByaWNlIGVsZW1lbnQgdGhhdCBjb250YWlucyB0aGUgJyQnIHNpZ24gYW5kIGZpbHRlciBvdXRcXG4gICAgICAgICAgICAjIHRoZSB2aXN1YWxseSBoaWRkZW4gZWxlbWVudHMuXFxuICAgICAgICAgICAgcHJpY2VfZWxlbWVudCA9IGNvbnRleHQucGFnZS5sb2NhdG9yKCdzcGFuLnByaWNlJywgaGFzX3RleHQ9JyQnKS5maXJzdFxcbiAgICAgICAgICAgIGN1cnJlbnRfcHJpY2Vfc3RyaW5nID0gYXdhaXQgcHJpY2VfZWxlbWVudC50ZXh0X2NvbnRlbnQoKSBvciAnJ1xcbiAgICAgICAgICAgIHJhd19wcmljZSA9IGN1cnJlbnRfcHJpY2Vfc3RyaW5nLnNwbGl0KCckJylbMV1cXG4gICAgICAgICAgICBwcmljZSA9IGZsb2F0KHJhd19wcmljZS5yZXBsYWNlKCcsJywgJycpKVxcblxcbiAgICAgICAgICAgICMgTG9jYXRlIHRoZSBlbGVtZW50IHRoYXQgY29udGFpbnMgdGhlIHRleHQgJ0luIHN0b2NrJ1xcbiAgICAgICAgICAgICMgYW5kIGZpbHRlciBvdXQgb3RoZXIgZWxlbWVudHMuXFxuICAgICAgICAgICAgaW5fc3RvY2tfZWxlbWVudCA9IGNvbnRleHQucGFnZS5sb2NhdG9yKFxcbiAgICAgICAgICAgICAgICBzZWxlY3Rvcj0nc3Bhbi5wcm9kdWN0LWZvcm1fX2ludmVudG9yeScsXFxuICAgICAgICAgICAgICAgIGhhc190ZXh0PSdJbiBzdG9jaycsXFxuICAgICAgICAgICAgKS5maXJzdFxcbiAgICAgICAgICAgIGluX3N0b2NrID0gYXdhaXQgaW5fc3RvY2tfZWxlbWVudC5jb3VudCgpID4gMFxcblxcbiAgICAgICAgICAgICMgUHV0IGl0IGFsbCB0b2dldGhlciBpbiBhIGRpY3Rpb25hcnkuXFxuICAgICAgICAgICAgZGF0YSA9IHtcXG4gICAgICAgICAgICAgICAgJ21hbnVmYWN0dXJlcic6IG1hbnVmYWN0dXJlcixcXG4gICAgICAgICAgICAgICAgJ3RpdGxlJzogdGl0bGUsXFxuICAgICAgICAgICAgICAgICdza3UnOiBza3UsXFxuICAgICAgICAgICAgICAgICdwcmljZSc6IHByaWNlLFxcbiAgICAgICAgICAgICAgICAnaW5fc3RvY2snOiBpbl9zdG9jayxcXG4gICAgICAgICAgICB9XFxuXFxuICAgICAgICAgICAgIyBQcmludCB0aGUgZXh0cmFjdGVkIGRhdGEuXFxuICAgICAgICAgICAgY29udGV4dC5sb2cuaW5mbyhkYXRhKVxcblxcbiAgICAgICAgIyBXZSBhcmUgbm93IG9uIGEgY2F0ZWdvcnkgcGFnZS4gV2UgY2FuIHVzZSB0aGlzIHRvIHBhZ2luYXRlIHRocm91Z2ggYW5kXFxuICAgICAgICAjIGVucXVldWUgYWxsIHByb2R1Y3RzLCBhcyB3ZWxsIGFzIGFueSBzdWJzZXF1ZW50IHBhZ2VzIHdlIGZpbmQuXFxuICAgICAgICBlbGlmIGNvbnRleHQucmVxdWVzdC5sYWJlbCA9PSAnQ0FURUdPUlknOlxcbiAgICAgICAgICAgICMgV2FpdCBmb3IgdGhlIHByb2R1Y3QgaXRlbXMgdG8gcmVuZGVyLlxcbiAgICAgICAgICAgIGF3YWl0IGNvbnRleHQucGFnZS53YWl0X2Zvcl9zZWxlY3RvcignLnByb2R1Y3QtaXRlbSA-IGEnKVxcblxcbiAgICAgICAgICAgICMgRW5xdWV1ZSBsaW5rcyBmb3VuZCB3aXRoaW4gZWxlbWVudHMgbWF0Y2hpbmcgdGhlIHByb3ZpZGVkIHNlbGVjdG9yLlxcbiAgICAgICAgICAgICMgVGhlc2UgbGlua3Mgd2lsbCBiZSBhZGRlZCB0byB0aGUgY3Jhd2xpbmcgcXVldWUgd2l0aCB0aGUgbGFiZWwgREVUQUlMLlxcbiAgICAgICAgICAgIGF3YWl0IGNvbnRleHQuZW5xdWV1ZV9saW5rcyhcXG4gICAgICAgICAgICAgICAgc2VsZWN0b3I9Jy5wcm9kdWN0LWl0ZW0gPiBhJyxcXG4gICAgICAgICAgICAgICAgbGFiZWw9J0RFVEFJTCcsXFxuICAgICAgICAgICAgKVxcblxcbiAgICAgICAgICAgICMgRmluZCB0aGUgXFxcIk5leHRcXFwiIGJ1dHRvbiB0byBwYWdpbmF0ZSB0aHJvdWdoIHRoZSBjYXRlZ29yeSBwYWdlcy5cXG4gICAgICAgICAgICBuZXh0X2J1dHRvbiA9IGF3YWl0IGNvbnRleHQucGFnZS5xdWVyeV9zZWxlY3RvcignYS5wYWdpbmF0aW9uX19uZXh0JylcXG5cXG4gICAgICAgICAgICAjIElmIGEgXFxcIk5leHRcXFwiIGJ1dHRvbiBpcyBmb3VuZCwgZW5xdWV1ZSB0aGUgbmV4dCBwYWdlIG9mIHJlc3VsdHMuXFxuICAgICAgICAgICAgaWYgbmV4dF9idXR0b246XFxuICAgICAgICAgICAgICAgIGF3YWl0IGNvbnRleHQuZW5xdWV1ZV9saW5rcyhcXG4gICAgICAgICAgICAgICAgICAgIHNlbGVjdG9yPSdhLnBhZ2luYXRpb25fX25leHQnLFxcbiAgICAgICAgICAgICAgICAgICAgbGFiZWw9J0NBVEVHT1JZJyxcXG4gICAgICAgICAgICAgICAgKVxcblxcbiAgICAgICAgIyBUaGlzIGluZGljYXRlcyB3ZSdyZSBvbiB0aGUgc3RhcnQgcGFnZSB3aXRoIG5vIHNwZWNpZmljIGxhYmVsLlxcbiAgICAgICAgIyBPbiB0aGUgc3RhcnQgcGFnZSwgd2Ugd2FudCB0byBlbnF1ZXVlIGFsbCB0aGUgY2F0ZWdvcnkgcGFnZXMuXFxuICAgICAgICBlbHNlOlxcbiAgICAgICAgICAgICMgV2FpdCBmb3IgdGhlIGNvbGxlY3Rpb24gY2FyZHMgdG8gcmVuZGVyLlxcbiAgICAgICAgICAgIGF3YWl0IGNvbnRleHQucGFnZS53YWl0X2Zvcl9zZWxlY3RvcignLmNvbGxlY3Rpb24tYmxvY2staXRlbScpXFxuXFxuICAgICAgICAgICAgIyBFbnF1ZXVlIGxpbmtzIGZvdW5kIHdpdGhpbiBlbGVtZW50cyBtYXRjaGluZyB0aGUgcHJvdmlkZWQgc2VsZWN0b3IuXFxuICAgICAgICAgICAgIyBUaGVzZSBsaW5rcyB3aWxsIGJlIGFkZGVkIHRvIHRoZSBjcmF3bGluZyBxdWV1ZSB3aXRoIHRoZSBsYWJlbCBDQVRFR09SWS5cXG4gICAgICAgICAgICBhd2FpdCBjb250ZXh0LmVucXVldWVfbGlua3MoXFxuICAgICAgICAgICAgICAgIHNlbGVjdG9yPScuY29sbGVjdGlvbi1ibG9jay1pdGVtJyxcXG4gICAgICAgICAgICAgICAgbGFiZWw9J0NBVEVHT1JZJyxcXG4gICAgICAgICAgICApXFxuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly93YXJlaG91c2UtdGhlbWUtbWV0YWwubXlzaG9waWZ5LmNvbS9jb2xsZWN0aW9ucyddKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5Ijo0MDk2LCJ0aW1lb3V0IjoxODB9fQ.S0H-0OH57HUd7McisdrTLitNGpf_mV9o2tXD2JY1Vc4\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext


async def main() -> None:
    crawler = PlaywrightCrawler(
        # Let's limit our crawls to make our tests shorter and safer.
        max_requests_per_crawl=10,
    )

    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url}')

        # We're not processing detail pages yet, so we just pass.
        if context.request.label == 'DETAIL':
            # Split the URL and get the last part to extract the manufacturer.
            url_part = context.request.url.split('/').pop()
            manufacturer = url_part.split('-')[0]

            # Extract the title using the combined selector.
            title = await context.page.locator('.product-meta h1').text_content()

            # Extract the SKU using its selector.
            sku = await context.page.locator(
                'span.product-meta__sku-number'
            ).text_content()

            # Locate the price element that contains the '$' sign and filter out
            # the visually hidden elements.
            price_element = context.page.locator('span.price', has_text='$').first
            current_price_string = await price_element.text_content() or ''
            raw_price = current_price_string.split('$')[1]
            price = float(raw_price.replace(',', ''))

            # Locate the element that contains the text 'In stock'
            # and filter out other elements.
            in_stock_element = context.page.locator(
                selector='span.product-form__inventory',
                has_text='In stock',
            ).first
            in_stock = await in_stock_element.count() > 0

            # Put it all together in a dictionary.
            data = {
                'manufacturer': manufacturer,
                'title': title,
                'sku': sku,
                'price': price,
                'in_stock': in_stock,
            }

            # Print the extracted data.
            context.log.info(data)

        # We are now on a category page. We can use this to paginate through and
        # enqueue all products, as well as any subsequent pages we find.
        elif context.request.label == 'CATEGORY':
            # Wait for the product items to render.
            await context.page.wait_for_selector('.product-item > a')

            # Enqueue links found within elements matching the provided selector.
            # These links will be added to the crawling queue with the label DETAIL.
            await context.enqueue_links(
                selector='.product-item > a',
                label='DETAIL',
            )

            # Find the "Next" button to paginate through the category pages.
            next_button = await context.page.query_selector('a.pagination__next')

            # If a "Next" button is found, enqueue the next page of results.
            if next_button:
                await context.enqueue_links(
                    selector='a.pagination__next',
                    label='CATEGORY',
                )

        # This indicates we're on the start page with no specific label.
        # On the start page, we want to enqueue all the category pages.
        else:
            # Wait for the collection cards to render.
            await context.page.wait_for_selector('.collection-block-item')

            # Enqueue links found within elements matching the provided selector.
            # These links will be added to the crawling queue with the label CATEGORY.
            await context.enqueue_links(
                selector='.collection-block-item',
                label='CATEGORY',
            )

    await crawler.run(['https://warehouse-theme-metal.myshopify.com/collections'])


if __name__ == '__main__':
    asyncio.run(main())
```

When you run the crawler, you will see the crawled URLs and their scraped data printed to the console. The output will look something like this:

```
{
    "url": "https://warehouse-theme-metal.myshopify.com/products/sony-str-za810es-7-2-channel-hi-res-wi-fi-network-av-receiver",
    "manufacturer": "sony",
    "title": "Sony STR-ZA810ES 7.2-Ch Hi-Res Wi-Fi Network A/V Receiver",
    "sku": "SON-692802-STR-DE",
    "price": 698,
    "in_stock": true
}
```

## Next steps[​](#next-steps "Direct link to Next steps")

Next, you'll see how to save the data you scraped to the disk for further processing.

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/introduction/06_scraping.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/introduction/crawling.md)

[Crawling](https://crawlee.dev/python/python/docs/introduction/crawling.md)

[Next](https://crawlee.dev/python/python/docs/introduction/saving-data.md)

[Saving data](https://crawlee.dev/python/python/docs/introduction/saving-data.md)


---

* [](https://crawlee.dev/python/python)
* [Introduction](https://crawlee.dev/python/python/docs/introduction.md)
* Setting up

Version: 1.6

On this page

# Setting up

This guide will help you get started with Crawlee by setting it up on your computer. Follow the steps below to ensure a smooth installation process.

## Prerequisites[​](#prerequisites "Direct link to Prerequisites")

Before installing Crawlee itself, make sure that your system meets the following requirements:

* **Python 3.10 or higher**: Crawlee requires Python 3.10 or a newer version. You can download Python from the [official website](https://python.org/downloads/).
* **Python package manager**: While this guide uses [pip](https://pip.pypa.io/) (the most common package manager), you can also use any package manager you want. You can download pip from the [official website](https://pip.pypa.io/en/stable/installation/).

### Verifying prerequisites[​](#verifying-prerequisites "Direct link to Verifying prerequisites")

To check if Python and pip are installed, run the following commands:

```
python --version
```

```
python -m pip --version
```

If these commands return the respective versions, you're ready to continue.

## Installing Crawlee[​](#installing-crawlee "Direct link to Installing Crawlee")

Crawlee is available as [`crawlee`](https://pypi.org/project/crawlee/) package on PyPI. This package includes the core functionality, while additional features are available as optional extras to keep dependencies and package size minimal.

### Basic installation[​](#basic-installation "Direct link to Basic installation")

To install the core package, run:

```
python -m pip install crawlee
```

After installation, verify that Crawlee is installed correctly by checking its version:

```
python -c 'import crawlee; print(crawlee.__version__)'
```

### Full installation[​](#full-installation "Direct link to Full installation")

If you do not mind the package size, you can run the following command to install Crawlee with all optional features:

```
python -m pip install 'crawlee[all]'
```

### Installing specific extras[​](#installing-specific-extras "Direct link to Installing specific extras")

Depending on your use case, you may want to install specific extras to enable additional functionality:

For using the [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md), install the `beautifulsoup` extra:

```
python -m pip install 'crawlee[beautifulsoup]'
```

For using the [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md), install the `parsel` extra:

```
python -m pip install 'crawlee[parsel]'
```

For using the [`CurlImpersonateHttpClient`](https://crawlee.dev/python/python/api/class/CurlImpersonateHttpClient.md), install the `curl-impersonate` extra:

```
python -m pip install 'crawlee[curl-impersonate]'
```

If you plan to use a (headless) browser with [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md), install Crawlee with the `playwright` extra:

```
python -m pip install 'crawlee[playwright]'
```

After installing the playwright extra, install the necessary Playwright dependencies:

```
playwright install
```

### Installing multiple extras[​](#installing-multiple-extras "Direct link to Installing multiple extras")

You can install multiple extras at once by using a comma as a separator:

```
python -m pip install 'crawlee[beautifulsoup,curl-impersonate]'
```

## Start a new project[​](#start-a-new-project "Direct link to Start a new project")

The quickest way to get started with Crawlee is by using the Crawlee CLI and selecting one of the prepared templates. The CLI helps you set up a new project in seconds.

### Using Crawlee CLI with uv[​](#using-crawlee-cli-with-uv "Direct link to Using Crawlee CLI with uv")

First, ensure you have [uv](https://pypi.org/project/uv/) installed. You can check if it is installed by running:

```
uv --version
```

If [uv](https://pypi.org/project/uv/) is not installed, follow the official [installation guide](https://docs.astral.sh/uv/getting-started/installation/).

Then, run the Crawlee CLI using `uvx` and choose from the available templates:

```
uvx 'crawlee[cli]' create my-crawler
```

### Using Crawlee CLI directly[​](#using-crawlee-cli-directly "Direct link to Using Crawlee CLI directly")

If you already have `crawlee` installed, you can spin it up by running:

```
crawlee create my_crawler
```

Follow the interactive prompts in the CLI to choose a crawler type and set up your new project.

### Running your project[​](#running-your-project "Direct link to Running your project")

To run your newly created project, navigate to the project directory, activate the virtual environment, and execute the Python interpreter with the project module:

* Linux
* Windows

```
cd my_crawler/
```

```
source .venv/bin/activate
```

```
python -m my_crawler
```

```
cd my_crawler/
```

```
venv\Scripts\activate
```

```
python -m my_crawler
```

Congratulations! You have successfully set up and executed your first Crawlee project.

## Next steps[​](#next-steps "Direct link to Next steps")

Next, you will learn how to create a very simple crawler and Crawlee components while building it.

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/introduction/01_setting_up.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/introduction.md)

[Introduction](https://crawlee.dev/python/python/docs/introduction.md)

[Next](https://crawlee.dev/python/python/docs/introduction/first-crawler.md)

[First crawler](https://crawlee.dev/python/python/docs/introduction/first-crawler.md)


---

* [](https://crawlee.dev/python/python)
* Quick start

Version: 1.6

On this page

