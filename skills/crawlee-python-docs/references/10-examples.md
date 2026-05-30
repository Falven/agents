# Adaptive Playwright crawler

This example demonstrates how to use [`AdaptivePlaywrightCrawler`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md). An [`AdaptivePlaywrightCrawler`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md) is a combination of [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) and some implementation of HTTP-based crawler such as [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md) or [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md). It uses a more limited crawling context interface so that it is able to switch to HTTP-only crawling when it detects that it may bring a performance benefit.

A [pre-navigation hook](https://crawlee.dev/python/python/docs/guides/adaptive-playwright-crawler.md#page-configuration-with-pre-navigation-hooks) can be used to perform actions before navigating to the URL. This hook provides further flexibility in controlling environment and preparing for navigation. Hooks will be executed both for the pages crawled by HTTP-bases sub crawler and playwright based sub crawler. Use `playwright_only=True` to mark hooks that should be executed only for playwright sub crawler.

For more detailed description please see [Adaptive Playwright crawler guide](https://crawlee.dev/python/python/docs/guides/adaptive-playwright-crawler.md)

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuZnJvbSBkYXRldGltZSBpbXBvcnQgdGltZWRlbHRhXFxuXFxuZnJvbSBwbGF5d3JpZ2h0LmFzeW5jX2FwaSBpbXBvcnQgUm91dGVcXG5cXG5mcm9tIGNyYXdsZWUuY3Jhd2xlcnMgaW1wb3J0IChcXG4gICAgQWRhcHRpdmVQbGF5d3JpZ2h0Q3Jhd2xlcixcXG4gICAgQWRhcHRpdmVQbGF5d3JpZ2h0Q3Jhd2xpbmdDb250ZXh0LFxcbiAgICBBZGFwdGl2ZVBsYXl3cmlnaHRQcmVOYXZDcmF3bGluZ0NvbnRleHQsXFxuKVxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBDcmF3bGVyIGNyZWF0ZWQgYnkgZm9sbG93aW5nIGZhY3RvcnkgbWV0aG9kIHdpbGwgdXNlIGBiZWF1dGlmdWxzb3VwYFxcbiAgICAjIGZvciBwYXJzaW5nIHN0YXRpYyBjb250ZW50LlxcbiAgICBjcmF3bGVyID0gQWRhcHRpdmVQbGF5d3JpZ2h0Q3Jhd2xlci53aXRoX2JlYXV0aWZ1bHNvdXBfc3RhdGljX3BhcnNlcihcXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsICAjIExpbWl0IHRoZSBtYXggcmVxdWVzdHMgcGVyIGNyYXdsLlxcbiAgICAgICAgcGxheXdyaWdodF9jcmF3bGVyX3NwZWNpZmljX2t3YXJncz17J2hlYWRsZXNzJzogRmFsc2V9LFxcbiAgICApXFxuXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIHJlcXVlc3RfaGFuZGxlcl9mb3JfbGFiZWwoXFxuICAgICAgICBjb250ZXh0OiBBZGFwdGl2ZVBsYXl3cmlnaHRDcmF3bGluZ0NvbnRleHQsXFxuICAgICkgLT4gTm9uZTpcXG4gICAgICAgICMgRG8gc29tZSBwcm9jZXNzaW5nIHVzaW5nIGBwYXJzZWRfY29udGVudGBcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oY29udGV4dC5wYXJzZWRfY29udGVudC50aXRsZSlcXG5cXG4gICAgICAgICMgTG9jYXRlIGVsZW1lbnQgaDIgd2l0aGluIDUgc2Vjb25kc1xcbiAgICAgICAgaDIgPSBhd2FpdCBjb250ZXh0LnF1ZXJ5X3NlbGVjdG9yX29uZSgnaDInLCB0aW1lZGVsdGEobWlsbGlzZWNvbmRzPTUwMDApKVxcbiAgICAgICAgIyBEbyBzdHVmZiB3aXRoIGVsZW1lbnQgZm91bmQgYnkgdGhlIHNlbGVjdG9yXFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGgyKVxcblxcbiAgICAgICAgIyBGaW5kIG1vcmUgbGlua3MgYW5kIGVucXVldWUgdGhlbS5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQuZW5xdWV1ZV9saW5rcygpXFxuICAgICAgICAjIFNhdmUgc29tZSBkYXRhLlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5wdXNoX2RhdGEoeydWaXNpdGVkIHVybCc6IGNvbnRleHQucmVxdWVzdC51cmx9KVxcblxcbiAgICBAY3Jhd2xlci5wcmVfbmF2aWdhdGlvbl9ob29rXFxuICAgIGFzeW5jIGRlZiBob29rKGNvbnRleHQ6IEFkYXB0aXZlUGxheXdyaWdodFByZU5hdkNyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIFxcXCJcXFwiXFxcIkhvb2sgZXhlY3V0ZWQgYm90aCBpbiBzdGF0aWMgc3ViIGNyYXdsZXIgYW5kIHBsYXl3cmlnaHQgc3ViIGNyYXdsZXIuXFxuXFxuICAgICAgICBUcnlpbmcgdG8gYWNjZXNzIGBjb250ZXh0LnBhZ2VgIGluIHRoaXMgaG9vayB3b3VsZCByYWlzZSBgQWRhcHRpdmVDb250ZXh0RXJyb3JgXFxuICAgICAgICBmb3IgcGFnZXMgY3Jhd2xlZCB3aXRob3V0IHBsYXl3cmlnaHQuXFxcIlxcXCJcXFwiXFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYncHJlIG5hdmlnYXRpb24gaG9vayBmb3I6IHtjb250ZXh0LnJlcXVlc3QudXJsfSAuLi4nKVxcblxcbiAgICBAY3Jhd2xlci5wcmVfbmF2aWdhdGlvbl9ob29rKHBsYXl3cmlnaHRfb25seT1UcnVlKVxcbiAgICBhc3luYyBkZWYgaG9va19wbGF5d3JpZ2h0KGNvbnRleHQ6IEFkYXB0aXZlUGxheXdyaWdodFByZU5hdkNyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIFxcXCJcXFwiXFxcIkhvb2sgZXhlY3V0ZWQgb25seSBpbiBwbGF5d3JpZ2h0IHN1YiBjcmF3bGVyLlxcblxcbiAgICAgICAgSXQgaXMgc2FmZSB0byBhY2Nlc3MgYHBhZ2VgIG9iamVjdC5cXG4gICAgICAgIFxcXCJcXFwiXFxcIlxcblxcbiAgICAgICAgYXN5bmMgZGVmIHNvbWVfcm91dGluZ19mdW5jdGlvbihyb3V0ZTogUm91dGUpIC0-IE5vbmU6XFxuICAgICAgICAgICAgYXdhaXQgcm91dGUuY29udGludWVfKClcXG5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQucGFnZS5yb3V0ZSgnKi8qKicsIHNvbWVfcm91dGluZ19mdW5jdGlvbilcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oXFxuICAgICAgICAgICAgZidQbGF5d3JpZ2h0IG9ubHkgcHJlIG5hdmlnYXRpb24gaG9vayBmb3I6IHtjb250ZXh0LnJlcXVlc3QudXJsfSAuLi4nXFxuICAgICAgICApXFxuXFxuICAgICMgUnVuIHRoZSBjcmF3bGVyIHdpdGggdGhlIGluaXRpYWwgbGlzdCBvZiBVUkxzLlxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vd2FyZWhvdXNlLXRoZW1lLW1ldGFsLm15c2hvcGlmeS5jb20vJ10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjQwOTYsInRpbWVvdXQiOjE4MH19.4pgH-y_44EVj8dv6WPyF2CDxoTjsXeU7_mXFXQN8qzA\&asrc=run_on_apify)

```
import asyncio
from datetime import timedelta

from playwright.async_api import Route

from crawlee.crawlers import (
    AdaptivePlaywrightCrawler,
    AdaptivePlaywrightCrawlingContext,
    AdaptivePlaywrightPreNavCrawlingContext,
)


async def main() -> None:
    # Crawler created by following factory method will use `beautifulsoup`
    # for parsing static content.
    crawler = AdaptivePlaywrightCrawler.with_beautifulsoup_static_parser(
        max_requests_per_crawl=10,  # Limit the max requests per crawl.
        playwright_crawler_specific_kwargs={'headless': False},
    )

    @crawler.router.default_handler
    async def request_handler_for_label(
        context: AdaptivePlaywrightCrawlingContext,
    ) -> None:
        # Do some processing using `parsed_content`
        context.log.info(context.parsed_content.title)

        # Locate element h2 within 5 seconds
        h2 = await context.query_selector_one('h2', timedelta(milliseconds=5000))
        # Do stuff with element found by the selector
        context.log.info(h2)

        # Find more links and enqueue them.
        await context.enqueue_links()
        # Save some data.
        await context.push_data({'Visited url': context.request.url})

    @crawler.pre_navigation_hook
    async def hook(context: AdaptivePlaywrightPreNavCrawlingContext) -> None:
        """Hook executed both in static sub crawler and playwright sub crawler.

        Trying to access `context.page` in this hook would raise `AdaptiveContextError`
        for pages crawled without playwright."""
        context.log.info(f'pre navigation hook for: {context.request.url} ...')

    @crawler.pre_navigation_hook(playwright_only=True)
    async def hook_playwright(context: AdaptivePlaywrightPreNavCrawlingContext) -> None:
        """Hook executed only in playwright sub crawler.

        It is safe to access `page` object.
        """

        async def some_routing_function(route: Route) -> None:
            await route.continue_()

        await context.page.route('*/**', some_routing_function)
        context.log.info(
            f'Playwright only pre navigation hook for: {context.request.url} ...'
        )

    # Run the crawler with the initial list of URLs.
    await crawler.run(['https://warehouse-theme-metal.myshopify.com/'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/examples/playwright_crawler_adaptive.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/examples/playwright-crawler.md)

[Playwright crawler](https://crawlee.dev/python/python/docs/examples/playwright-crawler.md)

[Next](https://crawlee.dev/python/python/docs/examples/playwright-crawler-with-block-requests.md)

[Playwright crawler with block requests](https://crawlee.dev/python/python/docs/examples/playwright-crawler-with-block-requests.md)


---

* [](https://crawlee.dev/python/python)
* [Examples](https://crawlee.dev/python/python/docs/examples.md)
* Add data to dataset

Version: 1.6

# Add data to dataset

This example demonstrates how to store extracted data into datasets using the [`context.push_data`](https://crawlee.dev/python/python/api/class/PushDataFunction.md#open) helper function. If the specified dataset does not already exist, it will be created automatically. Additionally, you can save data to custom datasets by providing `dataset_id` or `dataset_name` parameters to the [`push_data`](https://crawlee.dev/python/python/api/class/PushDataFunction.md#open) function.

* BeautifulSoupCrawler
* PlaywrightCrawler

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKClcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgICAgICMgRXh0cmFjdCBkYXRhIGZyb20gdGhlIHBhZ2UuXFxuICAgICAgICBkYXRhID0ge1xcbiAgICAgICAgICAgICd1cmwnOiBjb250ZXh0LnJlcXVlc3QudXJsLFxcbiAgICAgICAgICAgICd0aXRsZSc6IGNvbnRleHQuc291cC50aXRsZS5zdHJpbmcgaWYgY29udGV4dC5zb3VwLnRpdGxlIGVsc2UgTm9uZSxcXG4gICAgICAgICAgICAnaHRtbCc6IHN0cihjb250ZXh0LnNvdXApWzoxMDAwXSxcXG4gICAgICAgIH1cXG5cXG4gICAgICAgICMgUHVzaCB0aGUgZXh0cmFjdGVkIGRhdGEgdG8gdGhlIGRlZmF1bHQgZGF0YXNldC5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQucHVzaF9kYXRhKGRhdGEpXFxuXFxuICAgICMgUnVuIHRoZSBjcmF3bGVyIHdpdGggdGhlIGluaXRpYWwgbGlzdCBvZiByZXF1ZXN0cy5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oXFxuICAgICAgICBbXFxuICAgICAgICAgICAgJ2h0dHBzOi8vY3Jhd2xlZS5kZXYnLFxcbiAgICAgICAgICAgICdodHRwczovL2FwaWZ5LmNvbScsXFxuICAgICAgICAgICAgJ2h0dHBzOi8vZXhhbXBsZS5jb20nLFxcbiAgICAgICAgXVxcbiAgICApXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.RvFu_JfZLAarvVGZAglvUsLRgOuYEyRQ2dLDLWXWowY\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


async def main() -> None:
    crawler = BeautifulSoupCrawler()

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Extract data from the page.
        data = {
            'url': context.request.url,
            'title': context.soup.title.string if context.soup.title else None,
            'html': str(context.soup)[:1000],
        }

        # Push the extracted data to the default dataset.
        await context.push_data(data)

    # Run the crawler with the initial list of requests.
    await crawler.run(
        [
            'https://crawlee.dev',
            'https://apify.com',
            'https://example.com',
        ]
    )


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQbGF5d3JpZ2h0Q3Jhd2xlciwgUGxheXdyaWdodENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IFBsYXl3cmlnaHRDcmF3bGVyKClcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IFBsYXl3cmlnaHRDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgICAgICMgRXh0cmFjdCBkYXRhIGZyb20gdGhlIHBhZ2UuXFxuICAgICAgICBkYXRhID0ge1xcbiAgICAgICAgICAgICd1cmwnOiBjb250ZXh0LnJlcXVlc3QudXJsLFxcbiAgICAgICAgICAgICd0aXRsZSc6IGF3YWl0IGNvbnRleHQucGFnZS50aXRsZSgpLFxcbiAgICAgICAgICAgICdodG1sJzogc3RyKGF3YWl0IGNvbnRleHQucGFnZS5jb250ZW50KCkpWzoxMDAwXSxcXG4gICAgICAgIH1cXG5cXG4gICAgICAgICMgUHVzaCB0aGUgZXh0cmFjdGVkIGRhdGEgdG8gdGhlIGRlZmF1bHQgZGF0YXNldC5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQucHVzaF9kYXRhKGRhdGEpXFxuXFxuICAgICMgUnVuIHRoZSBjcmF3bGVyIHdpdGggdGhlIGluaXRpYWwgbGlzdCBvZiByZXF1ZXN0cy5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oXFxuICAgICAgICBbXFxuICAgICAgICAgICAgJ2h0dHBzOi8vY3Jhd2xlZS5kZXYnLFxcbiAgICAgICAgICAgICdodHRwczovL2FwaWZ5LmNvbScsXFxuICAgICAgICAgICAgJ2h0dHBzOi8vZXhhbXBsZS5jb20nLFxcbiAgICAgICAgXVxcbiAgICApXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjQwOTYsInRpbWVvdXQiOjE4MH19.cAWi5POLfQg3ZzjnbP0dbeLAqtYxUxnSD1pOqBiDh_M\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext


async def main() -> None:
    crawler = PlaywrightCrawler()

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Extract data from the page.
        data = {
            'url': context.request.url,
            'title': await context.page.title(),
            'html': str(await context.page.content())[:1000],
        }

        # Push the extracted data to the default dataset.
        await context.push_data(data)

    # Run the crawler with the initial list of requests.
    await crawler.run(
        [
            'https://crawlee.dev',
            'https://apify.com',
            'https://example.com',
        ]
    )


if __name__ == '__main__':
    asyncio.run(main())
```

Each item in the dataset will be stored in its own file within the following directory:

```
{PROJECT_FOLDER}/storage/datasets/default/
```

For more control, you can also open a dataset manually using the asynchronous constructor [`Dataset.open`](https://crawlee.dev/python/python/api/class/Dataset.md#open)

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLnN0b3JhZ2VzIGltcG9ydCBEYXRhc2V0XFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICAjIE9wZW4gZGF0YXNldCBtYW51YWxseSB1c2luZyBhc3luY2hyb25vdXMgY29uc3RydWN0b3Igb3BlbigpLlxcbiAgICBkYXRhc2V0ID0gYXdhaXQgRGF0YXNldC5vcGVuKClcXG5cXG4gICAgIyBJbnRlcmFjdCB3aXRoIGRhdGFzZXQgZGlyZWN0bHkuXFxuICAgIGF3YWl0IGRhdGFzZXQucHVzaF9kYXRhKHsna2V5JzogJ3ZhbHVlJ30pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.Ay6uDGaTtwq5w3hr8Gv9wqcyINpGQ3vnx-7A2EvgykY\&asrc=run_on_apify)

```
import asyncio

from crawlee.storages import Dataset


async def main() -> None:
    # Open dataset manually using asynchronous constructor open().
    dataset = await Dataset.open()

    # Interact with dataset directly.
    await dataset.push_data({'key': 'value'})


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/examples/add_data_to_dataset.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/examples.md)

[Examples](https://crawlee.dev/python/python/docs/examples.md)

[Next](https://crawlee.dev/python/python/docs/examples/beautifulsoup-crawler.md)

[BeautifulSoup crawler](https://crawlee.dev/python/python/docs/examples/beautifulsoup-crawler.md)


---

* [](https://crawlee.dev/python/python)
* [Examples](https://crawlee.dev/python/python/docs/examples.md)
* BeautifulSoup crawler

Version: 1.6

# BeautifulSoup crawler

This example demonstrates how to use [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md) to crawl a list of URLs, load each URL using a plain HTTP request, parse the HTML using the [BeautifulSoup](https://pypi.org/project/beautifulsoup4/) library and extract some data from it - the page title and all `<h1>`, `<h2>` and `<h3>` tags. This setup is perfect for scraping specific elements from web pages. Thanks to the well-known BeautifulSoup, you can easily navigate the HTML structure and retrieve the data you need with minimal code. It also shows how you can add optional pre-navigation hook to the crawler. Pre-navigation hooks are user defined functions that execute before sending the request.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuZnJvbSBkYXRldGltZSBpbXBvcnQgdGltZWRlbHRhXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCAoXFxuICAgIEJhc2ljQ3Jhd2xpbmdDb250ZXh0LFxcbiAgICBCZWF1dGlmdWxTb3VwQ3Jhd2xlcixcXG4gICAgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dCxcXG4pXFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICAjIENyZWF0ZSBhbiBpbnN0YW5jZSBvZiB0aGUgQmVhdXRpZnVsU291cENyYXdsZXIgY2xhc3MsIGEgY3Jhd2xlciB0aGF0IGF1dG9tYXRpY2FsbHlcXG4gICAgIyBsb2FkcyB0aGUgVVJMcyBhbmQgcGFyc2VzIHRoZWlyIEhUTUwgdXNpbmcgdGhlIEJlYXV0aWZ1bFNvdXAgbGlicmFyeS5cXG4gICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKFxcbiAgICAgICAgIyBPbiBlcnJvciwgcmV0cnkgZWFjaCBwYWdlIGF0IG1vc3Qgb25jZS5cXG4gICAgICAgIG1heF9yZXF1ZXN0X3JldHJpZXM9MSxcXG4gICAgICAgICMgSW5jcmVhc2UgdGhlIHRpbWVvdXQgZm9yIHByb2Nlc3NpbmcgZWFjaCBwYWdlIHRvIDMwIHNlY29uZHMuXFxuICAgICAgICByZXF1ZXN0X2hhbmRsZXJfdGltZW91dD10aW1lZGVsdGEoc2Vjb25kcz0zMCksXFxuICAgICAgICAjIExpbWl0IHRoZSBjcmF3bCB0byBtYXggcmVxdWVzdHMuIFJlbW92ZSBvciBpbmNyZWFzZSBpdCBmb3IgY3Jhd2xpbmcgYWxsIGxpbmtzLlxcbiAgICAgICAgbWF4X3JlcXVlc3RzX3Blcl9jcmF3bD0xMCxcXG4gICAgKVxcblxcbiAgICAjIERlZmluZSB0aGUgZGVmYXVsdCByZXF1ZXN0IGhhbmRsZXIsIHdoaWNoIHdpbGwgYmUgY2FsbGVkIGZvciBldmVyeSByZXF1ZXN0LlxcbiAgICAjIFRoZSBoYW5kbGVyIHJlY2VpdmVzIGEgY29udGV4dCBwYXJhbWV0ZXIsIHByb3ZpZGluZyB2YXJpb3VzIHByb3BlcnRpZXMgYW5kXFxuICAgICMgaGVscGVyIG1ldGhvZHMuIEhlcmUgYXJlIGEgZmV3IGtleSBvbmVzIHdlIHVzZSBmb3IgZGVtb25zdHJhdGlvbjpcXG4gICAgIyAtIHJlcXVlc3Q6IGFuIGluc3RhbmNlIG9mIHRoZSBSZXF1ZXN0IGNsYXNzIGNvbnRhaW5pbmcgZGV0YWlscyBzdWNoIGFzIHRoZSBVUkxcXG4gICAgIyAgIGJlaW5nIGNyYXdsZWQgYW5kIHRoZSBIVFRQIG1ldGhvZCB1c2VkLlxcbiAgICAjIC0gc291cDogdGhlIEJlYXV0aWZ1bFNvdXAgb2JqZWN0IGNvbnRhaW5pbmcgdGhlIHBhcnNlZCBIVE1MIG9mIHRoZSByZXNwb25zZS5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgICAgICMgRXh0cmFjdCBkYXRhIGZyb20gdGhlIHBhZ2UuXFxuICAgICAgICBkYXRhID0ge1xcbiAgICAgICAgICAgICd1cmwnOiBjb250ZXh0LnJlcXVlc3QudXJsLFxcbiAgICAgICAgICAgICd0aXRsZSc6IGNvbnRleHQuc291cC50aXRsZS5zdHJpbmcgaWYgY29udGV4dC5zb3VwLnRpdGxlIGVsc2UgTm9uZSxcXG4gICAgICAgICAgICAnaDFzJzogW2gxLnRleHQgZm9yIGgxIGluIGNvbnRleHQuc291cC5maW5kX2FsbCgnaDEnKV0sXFxuICAgICAgICAgICAgJ2gycyc6IFtoMi50ZXh0IGZvciBoMiBpbiBjb250ZXh0LnNvdXAuZmluZF9hbGwoJ2gyJyldLFxcbiAgICAgICAgICAgICdoM3MnOiBbaDMudGV4dCBmb3IgaDMgaW4gY29udGV4dC5zb3VwLmZpbmRfYWxsKCdoMycpXSxcXG4gICAgICAgIH1cXG5cXG4gICAgICAgICMgUHVzaCB0aGUgZXh0cmFjdGVkIGRhdGEgdG8gdGhlIGRlZmF1bHQgZGF0YXNldC4gSW4gbG9jYWwgY29uZmlndXJhdGlvbixcXG4gICAgICAgICMgdGhlIGRhdGEgd2lsbCBiZSBzdG9yZWQgYXMgSlNPTiBmaWxlcyBpbiAuL3N0b3JhZ2UvZGF0YXNldHMvZGVmYXVsdC5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQucHVzaF9kYXRhKGRhdGEpXFxuXFxuICAgICMgUmVnaXN0ZXIgcHJlIG5hdmlnYXRpb24gaG9vayB3aGljaCB3aWxsIGJlIGNhbGxlZCBiZWZvcmUgZWFjaCByZXF1ZXN0LlxcbiAgICAjIFRoaXMgaG9vayBpcyBvcHRpb25hbCBhbmQgZG9lcyBub3QgbmVlZCB0byBiZSBkZWZpbmVkIGF0IGFsbC5cXG4gICAgQGNyYXdsZXIucHJlX25hdmlnYXRpb25faG9va1xcbiAgICBhc3luYyBkZWYgc29tZV9ob29rKGNvbnRleHQ6IEJhc2ljQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgcGFzc1xcblxcbiAgICAjIFJ1biB0aGUgY3Jhd2xlciB3aXRoIHRoZSBpbml0aWFsIGxpc3Qgb2YgVVJMcy5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2NyYXdsZWUuZGV2J10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.QX6SZQM_PCRRv7mJDhsUm9gVU-cYhiI742glMNzez8E\&asrc=run_on_apify)

```
import asyncio
from datetime import timedelta

from crawlee.crawlers import (
    BasicCrawlingContext,
    BeautifulSoupCrawler,
    BeautifulSoupCrawlingContext,
)


async def main() -> None:
    # Create an instance of the BeautifulSoupCrawler class, a crawler that automatically
    # loads the URLs and parses their HTML using the BeautifulSoup library.
    crawler = BeautifulSoupCrawler(
        # On error, retry each page at most once.
        max_request_retries=1,
        # Increase the timeout for processing each page to 30 seconds.
        request_handler_timeout=timedelta(seconds=30),
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
    )

    # Define the default request handler, which will be called for every request.
    # The handler receives a context parameter, providing various properties and
    # helper methods. Here are a few key ones we use for demonstration:
    # - request: an instance of the Request class containing details such as the URL
    #   being crawled and the HTTP method used.
    # - soup: the BeautifulSoup object containing the parsed HTML of the response.
    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Extract data from the page.
        data = {
            'url': context.request.url,
            'title': context.soup.title.string if context.soup.title else None,
            'h1s': [h1.text for h1 in context.soup.find_all('h1')],
            'h2s': [h2.text for h2 in context.soup.find_all('h2')],
            'h3s': [h3.text for h3 in context.soup.find_all('h3')],
        }

        # Push the extracted data to the default dataset. In local configuration,
        # the data will be stored as JSON files in ./storage/datasets/default.
        await context.push_data(data)

    # Register pre navigation hook which will be called before each request.
    # This hook is optional and does not need to be defined at all.
    @crawler.pre_navigation_hook
    async def some_hook(context: BasicCrawlingContext) -> None:
        pass

    # Run the crawler with the initial list of URLs.
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/examples/beautifulsoup_crawler.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/examples/add-data-to-dataset.md)

[Add data to dataset](https://crawlee.dev/python/python/docs/examples/add-data-to-dataset.md)

[Next](https://crawlee.dev/python/python/docs/examples/capture-screenshots-using-playwright.md)

[Capture screenshots using Playwright](https://crawlee.dev/python/python/docs/examples/capture-screenshots-using-playwright.md)


---

* [](https://crawlee.dev/python/python)
* [Examples](https://crawlee.dev/python/python/docs/examples.md)
* Capture screenshots using Playwright

Version: 1.6

# Capture screenshots using Playwright

This example demonstrates how to capture screenshots of web pages using [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) and store them in the key-value store.

The [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) is configured to automate the browsing and interaction with web pages. It uses headless Chromium as the browser type to perform these tasks. Each web page specified in the initial list of URLs is visited sequentially, and a screenshot of the page is captured using Playwright's `page.screenshot()` method.

The captured screenshots are stored in the key-value store, which is suitable for managing and storing files in various formats. In this case, screenshots are stored as PNG images with a unique key generated from the URL of the page.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQbGF5d3JpZ2h0Q3Jhd2xlciwgUGxheXdyaWdodENyYXdsaW5nQ29udGV4dFxcbmZyb20gY3Jhd2xlZS5zdG9yYWdlcyBpbXBvcnQgS2V5VmFsdWVTdG9yZVxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IFBsYXl3cmlnaHRDcmF3bGVyKFxcbiAgICAgICAgIyBMaW1pdCB0aGUgY3Jhd2wgdG8gbWF4IHJlcXVlc3RzLiBSZW1vdmUgb3IgaW5jcmVhc2UgaXQgZm9yIGNyYXdsaW5nIGFsbCBsaW5rcy5cXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsXFxuICAgICAgICAjIEhlYWRsZXNzIG1vZGUsIHNldCB0byBGYWxzZSB0byBzZWUgdGhlIGJyb3dzZXIgaW4gYWN0aW9uLlxcbiAgICAgICAgaGVhZGxlc3M9RmFsc2UsXFxuICAgICAgICAjIEJyb3dzZXIgdHlwZXMgc3VwcG9ydGVkIGJ5IFBsYXl3cmlnaHQuXFxuICAgICAgICBicm93c2VyX3R5cGU9J2Nocm9taXVtJyxcXG4gICAgKVxcblxcbiAgICAjIE9wZW4gdGhlIGRlZmF1bHQga2V5LXZhbHVlIHN0b3JlLlxcbiAgICBrdnMgPSBhd2FpdCBLZXlWYWx1ZVN0b3JlLm9wZW4oKVxcblxcbiAgICAjIERlZmluZSB0aGUgZGVmYXVsdCByZXF1ZXN0IGhhbmRsZXIsIHdoaWNoIHdpbGwgYmUgY2FsbGVkIGZvciBldmVyeSByZXF1ZXN0LlxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiByZXF1ZXN0X2hhbmRsZXIoY29udGV4dDogUGxheXdyaWdodENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm9jZXNzaW5nIHtjb250ZXh0LnJlcXVlc3QudXJsfSAuLi4nKVxcblxcbiAgICAgICAgIyBDYXB0dXJlIHRoZSBzY3JlZW5zaG90IG9mIHRoZSBwYWdlIHVzaW5nIFBsYXl3cmlnaHQncyBBUEkuXFxuICAgICAgICBzY3JlZW5zaG90ID0gYXdhaXQgY29udGV4dC5wYWdlLnNjcmVlbnNob3QoKVxcbiAgICAgICAgbmFtZSA9IGNvbnRleHQucmVxdWVzdC51cmwuc3BsaXQoJy8nKVstMV1cXG5cXG4gICAgICAgICMgU3RvcmUgdGhlIHNjcmVlbnNob3QgaW4gdGhlIGtleS12YWx1ZSBzdG9yZS5cXG4gICAgICAgIGF3YWl0IGt2cy5zZXRfdmFsdWUoXFxuICAgICAgICAgICAga2V5PWYnc2NyZWVuc2hvdC17bmFtZX0nLFxcbiAgICAgICAgICAgIHZhbHVlPXNjcmVlbnNob3QsXFxuICAgICAgICAgICAgY29udGVudF90eXBlPSdpbWFnZS9wbmcnLFxcbiAgICAgICAgKVxcblxcbiAgICAjIFJ1biB0aGUgY3Jhd2xlciB3aXRoIHRoZSBpbml0aWFsIGxpc3Qgb2YgVVJMcy5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oXFxuICAgICAgICBbXFxuICAgICAgICAgICAgJ2h0dHBzOi8vY3Jhd2xlZS5kZXYnLFxcbiAgICAgICAgICAgICdodHRwczovL2FwaWZ5LmNvbScsXFxuICAgICAgICAgICAgJ2h0dHBzOi8vZXhhbXBsZS5jb20nLFxcbiAgICAgICAgXVxcbiAgICApXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjQwOTYsInRpbWVvdXQiOjE4MH19.mBqeQhHjqeb04hGJ0iLUcBEQYYh1xXwQUF-gBFkXSio\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext
from crawlee.storages import KeyValueStore


async def main() -> None:
    crawler = PlaywrightCrawler(
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
        # Headless mode, set to False to see the browser in action.
        headless=False,
        # Browser types supported by Playwright.
        browser_type='chromium',
    )

    # Open the default key-value store.
    kvs = await KeyValueStore.open()

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Capture the screenshot of the page using Playwright's API.
        screenshot = await context.page.screenshot()
        name = context.request.url.split('/')[-1]

        # Store the screenshot in the key-value store.
        await kvs.set_value(
            key=f'screenshot-{name}',
            value=screenshot,
            content_type='image/png',
        )

    # Run the crawler with the initial list of URLs.
    await crawler.run(
        [
            'https://crawlee.dev',
            'https://apify.com',
            'https://example.com',
        ]
    )


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/examples/capture_screenshot_using_playwright.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/examples/beautifulsoup-crawler.md)

[BeautifulSoup crawler](https://crawlee.dev/python/python/docs/examples/beautifulsoup-crawler.md)

[Next](https://crawlee.dev/python/python/docs/examples/capturing-page-snapshots-with-error-snapshotter.md)

[Capturing page snapshots with ErrorSnapshotter](https://crawlee.dev/python/python/docs/examples/capturing-page-snapshots-with-error-snapshotter.md)


---

* [](https://crawlee.dev/python/python)
* [Examples](https://crawlee.dev/python/python/docs/examples.md)
* Capturing page snapshots with ErrorSnapshotter

Version: 1.6

# Capturing page snapshots with ErrorSnapshotter

This example demonstrates how to capture page snapshots on first occurrence of each unique error. The capturing happens automatically if you set `save_error_snapshots=True` in the crawler's [`Statistics`](https://crawlee.dev/python/python/api/class/Statistics.md). The error snapshot can contain `html` file and `jpeg` file that are created from the page where the unhandled exception was raised. Captured error snapshot files are saved to the default key-value store. Both [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) and [HTTP crawlers](https://crawlee.dev/python/python/docs/guides/http-crawlers.md) are capable of capturing the html file, but only [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) is able to capture page screenshot as well.

* ParselCrawler
* PlaywrightCrawler

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuZnJvbSByYW5kb20gaW1wb3J0IGNob2ljZVxcblxcbmZyb20gY3Jhd2xlZS5jcmF3bGVycyBpbXBvcnQgUGFyc2VsQ3Jhd2xlciwgUGFyc2VsQ3Jhd2xpbmdDb250ZXh0XFxuZnJvbSBjcmF3bGVlLnN0YXRpc3RpY3MgaW1wb3J0IFN0YXRpc3RpY3NcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgIGNyYXdsZXIgPSBQYXJzZWxDcmF3bGVyKFxcbiAgICAgICAgc3RhdGlzdGljcz1TdGF0aXN0aWNzLndpdGhfZGVmYXVsdF9zdGF0ZShzYXZlX2Vycm9yX3NuYXBzaG90cz1UcnVlKVxcbiAgICApXFxuXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIHJlcXVlc3RfaGFuZGxlcihjb250ZXh0OiBQYXJzZWxDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG4gICAgICAgICMgU2ltdWxhdGUgdmFyaW91cyBlcnJvcnMgdG8gZGVtb25zdHJhdGUgYEVycm9yU25hcHNob3R0ZXJgXFxuICAgICAgICAjIHNhdmluZyBvbmx5IHRoZSBmaXJzdCBvY2N1cnJlbmNlIG9mIHVuaXF1ZSBlcnJvci5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQuZW5xdWV1ZV9saW5rcygpXFxuICAgICAgICByYW5kb21fbnVtYmVyID0gY2hvaWNlKHJhbmdlKDEwKSlcXG4gICAgICAgIGlmIHJhbmRvbV9udW1iZXIgPT0gMTpcXG4gICAgICAgICAgICByYWlzZSBLZXlFcnJvcignU29tZSBLZXlFcnJvcicpXFxuICAgICAgICBpZiByYW5kb21fbnVtYmVyID09IDI6XFxuICAgICAgICAgICAgcmFpc2UgVmFsdWVFcnJvcignU29tZSBWYWx1ZUVycm9yJylcXG4gICAgICAgIGlmIHJhbmRvbV9udW1iZXIgPT0gMzpcXG4gICAgICAgICAgICByYWlzZSBSdW50aW1lRXJyb3IoJ1NvbWUgUnVudGltZUVycm9yJylcXG5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2NyYXdsZWUuZGV2J10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.rzq04cxbj_wC1rrXRoR9OXGrFXDSvCuZumSWvl_x_NI\&asrc=run_on_apify)

```
import asyncio
from random import choice

from crawlee.crawlers import ParselCrawler, ParselCrawlingContext
from crawlee.statistics import Statistics


async def main() -> None:
    crawler = ParselCrawler(
        statistics=Statistics.with_default_state(save_error_snapshots=True)
    )

    @crawler.router.default_handler
    async def request_handler(context: ParselCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')
        # Simulate various errors to demonstrate `ErrorSnapshotter`
        # saving only the first occurrence of unique error.
        await context.enqueue_links()
        random_number = choice(range(10))
        if random_number == 1:
            raise KeyError('Some KeyError')
        if random_number == 2:
            raise ValueError('Some ValueError')
        if random_number == 3:
            raise RuntimeError('Some RuntimeError')

    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuZnJvbSByYW5kb20gaW1wb3J0IGNob2ljZVxcblxcbmZyb20gY3Jhd2xlZS5jcmF3bGVycyBpbXBvcnQgUGxheXdyaWdodENyYXdsZXIsIFBsYXl3cmlnaHRDcmF3bGluZ0NvbnRleHRcXG5mcm9tIGNyYXdsZWUuc3RhdGlzdGljcyBpbXBvcnQgU3RhdGlzdGljc1xcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IFBsYXl3cmlnaHRDcmF3bGVyKFxcbiAgICAgICAgc3RhdGlzdGljcz1TdGF0aXN0aWNzLndpdGhfZGVmYXVsdF9zdGF0ZShzYXZlX2Vycm9yX3NuYXBzaG90cz1UcnVlKVxcbiAgICApXFxuXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIHJlcXVlc3RfaGFuZGxlcihjb250ZXh0OiBQbGF5d3JpZ2h0Q3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ1Byb2Nlc3Npbmcge2NvbnRleHQucmVxdWVzdC51cmx9IC4uLicpXFxuICAgICAgICAjIFNpbXVsYXRlIHZhcmlvdXMgZXJyb3JzIHRvIGRlbW9uc3RyYXRlIGBFcnJvclNuYXBzaG90dGVyYFxcbiAgICAgICAgIyBzYXZpbmcgb25seSB0aGUgZmlyc3Qgb2NjdXJyZW5jZSBvZiB1bmlxdWUgZXJyb3IuXFxuICAgICAgICBhd2FpdCBjb250ZXh0LmVucXVldWVfbGlua3MoKVxcbiAgICAgICAgcmFuZG9tX251bWJlciA9IGNob2ljZShyYW5nZSgxMCkpXFxuICAgICAgICBpZiByYW5kb21fbnVtYmVyID09IDE6XFxuICAgICAgICAgICAgcmFpc2UgS2V5RXJyb3IoJ1NvbWUgS2V5RXJyb3InKVxcbiAgICAgICAgaWYgcmFuZG9tX251bWJlciA9PSAyOlxcbiAgICAgICAgICAgIHJhaXNlIFZhbHVlRXJyb3IoJ1NvbWUgVmFsdWVFcnJvcicpXFxuICAgICAgICBpZiByYW5kb21fbnVtYmVyID09IDM6XFxuICAgICAgICAgICAgcmFpc2UgUnVudGltZUVycm9yKCdTb21lIFJ1bnRpbWVFcnJvcicpXFxuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9jcmF3bGVlLmRldiddKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5Ijo0MDk2LCJ0aW1lb3V0IjoxODB9fQ.xf1Hv32X5keYsnW12cNYzQ0skfMt-o1rJ7RPfzUT3KA\&asrc=run_on_apify)

```
import asyncio
from random import choice

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext
from crawlee.statistics import Statistics


async def main() -> None:
    crawler = PlaywrightCrawler(
        statistics=Statistics.with_default_state(save_error_snapshots=True)
    )

    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')
        # Simulate various errors to demonstrate `ErrorSnapshotter`
        # saving only the first occurrence of unique error.
        await context.enqueue_links()
        random_number = choice(range(10))
        if random_number == 1:
            raise KeyError('Some KeyError')
        if random_number == 2:
            raise ValueError('Some ValueError')
        if random_number == 3:
            raise RuntimeError('Some RuntimeError')

    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/examples/capturing_page_snapshots_with_error_snapshotter.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/examples/capture-screenshots-using-playwright.md)

[Capture screenshots using Playwright](https://crawlee.dev/python/python/docs/examples/capture-screenshots-using-playwright.md)

[Next](https://crawlee.dev/python/python/docs/examples/crawl-all-links-on-website.md)

[Crawl all links on website](https://crawlee.dev/python/python/docs/examples/crawl-all-links-on-website.md)


---

* [](https://crawlee.dev/python/python)
* [Examples](https://crawlee.dev/python/python/docs/examples.md)
* Сonfigure JSON logging

Version: 1.6

# Сonfigure JSON logging

This example demonstrates how to configure JSON line (JSONL) logging with Crawlee. By using the `use_table_logs=False` parameter, you can disable table-formatted statistics logs, which makes it easier to parse logs with external tools or to serialize them as JSON.

The example shows how to integrate with the popular [`loguru`](https://github.com/delgan/loguru) library to capture Crawlee logs and format them as JSONL (one JSON object per line). This approach works well when you need to collect logs for analysis, monitoring, or when integrating with logging platforms like ELK Stack, Grafana Loki, or similar systems.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImZyb20gX19mdXR1cmVfXyBpbXBvcnQgYW5ub3RhdGlvbnNcXG5cXG5pbXBvcnQgYXN5bmNpb1xcbmltcG9ydCBpbnNwZWN0XFxuaW1wb3J0IGxvZ2dpbmdcXG5pbXBvcnQgc3lzXFxuZnJvbSB0eXBpbmcgaW1wb3J0IFRZUEVfQ0hFQ0tJTkdcXG5cXG5mcm9tIGxvZ3VydSBpbXBvcnQgbG9nZ2VyXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBIdHRwQ3Jhd2xlciwgSHR0cENyYXdsaW5nQ29udGV4dFxcblxcbmlmIFRZUEVfQ0hFQ0tJTkc6XFxuICAgIGZyb20gbG9ndXJ1IGltcG9ydCBSZWNvcmRcXG5cXG5cXG4jIENvbmZpZ3VyZSBsb2d1cnUgaW50ZXJjZXB0b3IgdG8gY2FwdHVyZSBzdGFuZGFyZCBsb2dnaW5nIG91dHB1dFxcbmNsYXNzIEludGVyY2VwdEhhbmRsZXIobG9nZ2luZy5IYW5kbGVyKTpcXG4gICAgZGVmIGVtaXQoc2VsZiwgcmVjb3JkOiBsb2dnaW5nLkxvZ1JlY29yZCkgLT4gTm9uZTpcXG4gICAgICAgICMgR2V0IGNvcnJlc3BvbmRpbmcgTG9ndXJ1IGxldmVsIGlmIGl0IGV4aXN0c1xcbiAgICAgICAgdHJ5OlxcbiAgICAgICAgICAgIGxldmVsOiBzdHIgfCBpbnQgPSBsb2dnZXIubGV2ZWwocmVjb3JkLmxldmVsbmFtZSkubmFtZVxcbiAgICAgICAgZXhjZXB0IFZhbHVlRXJyb3I6XFxuICAgICAgICAgICAgbGV2ZWwgPSByZWNvcmQubGV2ZWxub1xcblxcbiAgICAgICAgIyBGaW5kIGNhbGxlciBmcm9tIHdoZXJlIG9yaWdpbmF0ZWQgdGhlIGxvZ2dlZCBtZXNzYWdlXFxuICAgICAgICBmcmFtZSwgZGVwdGggPSBpbnNwZWN0LmN1cnJlbnRmcmFtZSgpLCAwXFxuICAgICAgICB3aGlsZSBmcmFtZTpcXG4gICAgICAgICAgICBmaWxlbmFtZSA9IGZyYW1lLmZfY29kZS5jb19maWxlbmFtZVxcbiAgICAgICAgICAgIGlzX2xvZ2dpbmcgPSBmaWxlbmFtZSA9PSBsb2dnaW5nLl9fZmlsZV9fXFxuICAgICAgICAgICAgaXNfZnJvemVuID0gJ2ltcG9ydGxpYicgaW4gZmlsZW5hbWUgYW5kICdfYm9vdHN0cmFwJyBpbiBmaWxlbmFtZVxcbiAgICAgICAgICAgIGlmIGRlcHRoID4gMCBhbmQgbm90IChpc19sb2dnaW5nIHwgaXNfZnJvemVuKTpcXG4gICAgICAgICAgICAgICAgYnJlYWtcXG4gICAgICAgICAgICBmcmFtZSA9IGZyYW1lLmZfYmFja1xcbiAgICAgICAgICAgIGRlcHRoICs9IDFcXG5cXG4gICAgICAgIGR1bW15X3JlY29yZCA9IGxvZ2dpbmcuTG9nUmVjb3JkKCdkdW1teScsIDAsICdkdW1teScsIDAsICdkdW1teScsIE5vbmUsIE5vbmUpXFxuICAgICAgICBzdGFuZGFyZF9hdHRycyA9IHNldChkdW1teV9yZWNvcmQuX19kaWN0X18ua2V5cygpKVxcbiAgICAgICAgZXh0cmFfZGljdCA9IHtcXG4gICAgICAgICAgICBrZXk6IHZhbHVlXFxuICAgICAgICAgICAgZm9yIGtleSwgdmFsdWUgaW4gcmVjb3JkLl9fZGljdF9fLml0ZW1zKClcXG4gICAgICAgICAgICBpZiBrZXkgbm90IGluIHN0YW5kYXJkX2F0dHJzXFxuICAgICAgICB9XFxuXFxuICAgICAgICAoXFxuICAgICAgICAgICAgbG9nZ2VyLmJpbmQoKipleHRyYV9kaWN0KVxcbiAgICAgICAgICAgIC5vcHQoZGVwdGg9ZGVwdGgsIGV4Y2VwdGlvbj1yZWNvcmQuZXhjX2luZm8pXFxuICAgICAgICAgICAgLnBhdGNoKGxhbWJkYSBsb2d1cnVfcmVjb3JkOiBsb2d1cnVfcmVjb3JkLnVwZGF0ZSh7J25hbWUnOiByZWNvcmQubmFtZX0pKVxcbiAgICAgICAgICAgIC5sb2cobGV2ZWwsIHJlY29yZC5nZXRNZXNzYWdlKCkpXFxuICAgICAgICApXFxuXFxuXFxuIyBDb25maWd1cmUgbG9ndXJ1IGZvcm1hdHRlclxcbmRlZiBmb3JtYXR0ZXIocmVjb3JkOiBSZWNvcmQpIC0-IHN0cjpcXG4gICAgYmFzaWNfZm9ybWF0ID0gJ1t7bmFtZX1dIHwgPGxldmVsPntsZXZlbDogXjh9PC9sZXZlbD4gfCAtIHttZXNzYWdlfSdcXG4gICAgaWYgcmVjb3JkWydleHRyYSddOlxcbiAgICAgICAgYmFzaWNfZm9ybWF0ID0gYmFzaWNfZm9ybWF0ICsgJyB7ZXh0cmF9J1xcbiAgICByZXR1cm4gZid7YmFzaWNfZm9ybWF0fVxcXFxuJ1xcblxcblxcbiMgUmVtb3ZlIGRlZmF1bHQgbG9ndXJ1IGxvZ2dlclxcbmxvZ2dlci5yZW1vdmUoKVxcblxcbiMgU2V0IHVwIGxvZ3VydSB3aXRoIEpTT05MIHNlcmlhbGl6YXRpb24gaW4gZmlsZSBgY3Jhd2xlci5sb2dgXFxubG9nZ2VyLmFkZCgnY3Jhd2xlci5sb2cnLCBmb3JtYXQ9Zm9ybWF0dGVyLCBzZXJpYWxpemU9VHJ1ZSwgbGV2ZWw9J0lORk8nKVxcblxcbiMgU2V0IHVwIGxvZ3VydSBsb2dnZXIgZm9yIGNvbnNvbGVcXG5sb2dnZXIuYWRkKHN5cy5zdGRlcnIsIGZvcm1hdD1mb3JtYXR0ZXIsIGNvbG9yaXplPVRydWUsIGxldmVsPSdJTkZPJylcXG5cXG4jIENvbmZpZ3VyZSBzdGFuZGFyZCBsb2dnaW5nIHRvIHVzZSBvdXIgaW50ZXJjZXB0b3JcXG5sb2dnaW5nLmJhc2ljQ29uZmlnKGhhbmRsZXJzPVtJbnRlcmNlcHRIYW5kbGVyKCldLCBsZXZlbD1sb2dnaW5nLklORk8sIGZvcmNlPVRydWUpXFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICAjIEluaXRpYWxpemUgY3Jhd2xlciB3aXRoIGRpc2FibGVkIHRhYmxlIGxvZ3NcXG4gICAgY3Jhd2xlciA9IEh0dHBDcmF3bGVyKFxcbiAgICAgICAgY29uZmlndXJlX2xvZ2dpbmc9RmFsc2UsICAjIERpc2FibGUgZGVmYXVsdCBsb2dnaW5nIGNvbmZpZ3VyYXRpb25cXG4gICAgICAgIHN0YXRpc3RpY3NfbG9nX2Zvcm1hdD0naW5saW5lJywgICMgU2V0IGlubGluZSBmb3JtYXR0aW5nIGZvciBzdGF0aXN0aWNzIGxvZ3NcXG4gICAgKVxcblxcbiAgICAjIERlZmluZSB0aGUgZGVmYXVsdCByZXF1ZXN0IGhhbmRsZXIsIHdoaWNoIHdpbGwgYmUgY2FsbGVkIGZvciBldmVyeSByZXF1ZXN0LlxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiByZXF1ZXN0X2hhbmRsZXIoY29udGV4dDogSHR0cENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm9jZXNzaW5nIHtjb250ZXh0LnJlcXVlc3QudXJsfSAuLi4nKVxcblxcbiAgICAjIFJ1biB0aGUgY3Jhd2xlclxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vd3d3LmNyYXdsZWUuZGV2LyddKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.40HidvfIqPs3TfRnOv7seJdNH5Eofw6rBSIxYmX-JwQ\&asrc=run_on_apify)

```
from __future__ import annotations

import asyncio
import inspect
import logging
import sys
from typing import TYPE_CHECKING

from loguru import logger

from crawlee.crawlers import HttpCrawler, HttpCrawlingContext

if TYPE_CHECKING:
    from loguru import Record


# Configure loguru interceptor to capture standard logging output
class InterceptHandler(logging.Handler):
    def emit(self, record: logging.LogRecord) -> None:
        # Get corresponding Loguru level if it exists
        try:
            level: str | int = logger.level(record.levelname).name
        except ValueError:
            level = record.levelno

        # Find caller from where originated the logged message
        frame, depth = inspect.currentframe(), 0
        while frame:
            filename = frame.f_code.co_filename
            is_logging = filename == logging.__file__
            is_frozen = 'importlib' in filename and '_bootstrap' in filename
            if depth > 0 and not (is_logging | is_frozen):
                break
            frame = frame.f_back
            depth += 1

        dummy_record = logging.LogRecord('dummy', 0, 'dummy', 0, 'dummy', None, None)
        standard_attrs = set(dummy_record.__dict__.keys())
        extra_dict = {
            key: value
            for key, value in record.__dict__.items()
            if key not in standard_attrs
        }

        (
            logger.bind(**extra_dict)
            .opt(depth=depth, exception=record.exc_info)
            .patch(lambda loguru_record: loguru_record.update({'name': record.name}))
            .log(level, record.getMessage())
        )


# Configure loguru formatter
def formatter(record: Record) -> str:
    basic_format = '[{name}] | <level>{level: ^8}</level> | - {message}'
    if record['extra']:
        basic_format = basic_format + ' {extra}'
    return f'{basic_format}\n'


# Remove default loguru logger
logger.remove()

# Set up loguru with JSONL serialization in file `crawler.log`
logger.add('crawler.log', format=formatter, serialize=True, level='INFO')

# Set up loguru logger for console
logger.add(sys.stderr, format=formatter, colorize=True, level='INFO')

# Configure standard logging to use our interceptor
logging.basicConfig(handlers=[InterceptHandler()], level=logging.INFO, force=True)


async def main() -> None:
    # Initialize crawler with disabled table logs
    crawler = HttpCrawler(
        configure_logging=False,  # Disable default logging configuration
        statistics_log_format='inline',  # Set inline formatting for statistics logs
    )

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: HttpCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

    # Run the crawler
    await crawler.run(['https://www.crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

Here's an example of what a crawler statistics log entry in JSONL format.

```
{
    "text": "[HttpCrawler] |   INFO   | - Final request statistics: {'requests_finished': 1, 'requests_failed': 0, 'retry_histogram': [1], 'request_avg_failed_duration': None, 'request_avg_finished_duration': 3.57098, 'requests_finished_per_minute': 17, 'requests_failed_per_minute': 0, 'request_total_duration': 3.57098, 'requests_total': 1, 'crawler_runtime': 3.59165}\n",
    "record": {
        "elapsed": { "repr": "0:00:05.604568", "seconds": 5.604568 },
        "exception": null,
        "extra": {
            "requests_finished": 1,
            "requests_failed": 0,
            "retry_histogram": [1],
            "request_avg_failed_duration": null,
            "request_avg_finished_duration": 3.57098,
            "requests_finished_per_minute": 17,
            "requests_failed_per_minute": 0,
            "request_total_duration": 3.57098,
            "requests_total": 1,
            "crawler_runtime": 3.59165
        },
        "file": {
            "name": "_basic_crawler.py",
            "path": "/crawlers/_basic/_basic_crawler.py"
        },
        "function": "run",
        "level": { "icon": "ℹ️", "name": "INFO", "no": 20 },
        "line": 583,
        "message": "Final request statistics:",
        "module": "_basic_crawler",
        "name": "HttpCrawler",
        "process": { "id": 198383, "name": "MainProcess" },
        "thread": { "id": 135312814966592, "name": "MainThread" },
        "time": {
            "repr": "2025-03-17 17:14:45.339150+00:00",
            "timestamp": 1742231685.33915
        }
    }
}
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/examples/json_logging.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/examples/fill-and-submit-web-form.md)

[Fill and submit web form](https://crawlee.dev/python/python/docs/examples/fill-and-submit-web-form.md)

[Next](https://crawlee.dev/python/python/docs/examples/parsel-crawler.md)

[Parsel crawler](https://crawlee.dev/python/python/docs/examples/parsel-crawler.md)


---

* [](https://crawlee.dev/python/python)
* [Examples](https://crawlee.dev/python/python/docs/examples.md)
* Crawl all links on website

Version: 1.6

# Crawl all links on website

This example uses the [`enqueue_links`](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md) helper to add new links to the [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md) as the crawler navigates from page to page. By automatically discovering and enqueuing all links on a given page, the crawler can systematically scrape an entire website. This approach is ideal for web scraping tasks where you need to collect data from multiple interconnected pages.

tip

If no options are given, by default the method will only add links that are under the same subdomain. This behavior can be controlled with the `strategy` option, which is an instance of the `EnqueueStrategy` type alias. You can find more info about this option in the [Crawl website with relative links](https://crawlee.dev/python/python/docs/examples/crawl-website-with-relative-links.md) example.

* BeautifulSoupCrawler
* PlaywrightCrawler

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKFxcbiAgICAgICAgIyBMaW1pdCB0aGUgY3Jhd2wgdG8gbWF4IHJlcXVlc3RzLiBSZW1vdmUgb3IgaW5jcmVhc2UgaXQgZm9yIGNyYXdsaW5nIGFsbCBsaW5rcy5cXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsXFxuICAgIClcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgICAgICMgRW5xdWV1ZSBhbGwgbGlua3MgZm91bmQgb24gdGhlIHBhZ2UuXFxuICAgICAgICBhd2FpdCBjb250ZXh0LmVucXVldWVfbGlua3MoKVxcblxcbiAgICAjIFJ1biB0aGUgY3Jhd2xlciB3aXRoIHRoZSBpbml0aWFsIGxpc3Qgb2YgcmVxdWVzdHMuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9jcmF3bGVlLmRldiddKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.lSt7qyAaWXSmCLPn1sY6PeFyHo5dqq4yiDcGtaqJi-o\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


async def main() -> None:
    crawler = BeautifulSoupCrawler(
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
    )

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Enqueue all links found on the page.
        await context.enqueue_links()

    # Run the crawler with the initial list of requests.
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQbGF5d3JpZ2h0Q3Jhd2xlciwgUGxheXdyaWdodENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IFBsYXl3cmlnaHRDcmF3bGVyKFxcbiAgICAgICAgIyBMaW1pdCB0aGUgY3Jhd2wgdG8gbWF4IHJlcXVlc3RzLiBSZW1vdmUgb3IgaW5jcmVhc2UgaXQgZm9yIGNyYXdsaW5nIGFsbCBsaW5rcy5cXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsXFxuICAgIClcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IFBsYXl3cmlnaHRDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgICAgICMgRW5xdWV1ZSBhbGwgbGlua3MgZm91bmQgb24gdGhlIHBhZ2UuXFxuICAgICAgICBhd2FpdCBjb250ZXh0LmVucXVldWVfbGlua3MoKVxcblxcbiAgICAjIFJ1biB0aGUgY3Jhd2xlciB3aXRoIHRoZSBpbml0aWFsIGxpc3Qgb2YgcmVxdWVzdHMuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9jcmF3bGVlLmRldiddKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5Ijo0MDk2LCJ0aW1lb3V0IjoxODB9fQ.AyoRlmpsRm0aRX45DCCNcO7YVJaaIyJRCrNtqP_u6p0\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext


async def main() -> None:
    crawler = PlaywrightCrawler(
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
    )

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Enqueue all links found on the page.
        await context.enqueue_links()

    # Run the crawler with the initial list of requests.
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/examples/crawl_all_links_on_website.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/examples/capturing-page-snapshots-with-error-snapshotter.md)

[Capturing page snapshots with ErrorSnapshotter](https://crawlee.dev/python/python/docs/examples/capturing-page-snapshots-with-error-snapshotter.md)

[Next](https://crawlee.dev/python/python/docs/examples/crawl-multiple-urls.md)

[Crawl multiple URLs](https://crawlee.dev/python/python/docs/examples/crawl-multiple-urls.md)


---

* [](https://crawlee.dev/python/python)
* [Examples](https://crawlee.dev/python/python/docs/examples.md)
* Crawl multiple URLs

Version: 1.6

# Crawl multiple URLs

This example demonstrates how to crawl a specified list of URLs using different crawlers. You'll learn how to set up the crawler, define a request handler, and run the crawler with multiple URLs. This setup is useful for scraping data from multiple pages or websites concurrently.

* BeautifulSoupCrawler
* PlaywrightCrawler

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKClcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgIyBSdW4gdGhlIGNyYXdsZXIgd2l0aCB0aGUgaW5pdGlhbCBsaXN0IG9mIHJlcXVlc3RzLlxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihcXG4gICAgICAgIFtcXG4gICAgICAgICAgICAnaHR0cHM6Ly9jcmF3bGVlLmRldicsXFxuICAgICAgICAgICAgJ2h0dHBzOi8vYXBpZnkuY29tJyxcXG4gICAgICAgICAgICAnaHR0cHM6Ly9leGFtcGxlLmNvbScsXFxuICAgICAgICBdXFxuICAgIClcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6MTAyNCwidGltZW91dCI6MTgwfX0._DjrfeMOXTbjpa3FD-n7bTupa-6jlV6VMq4KPP_vGlo\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


async def main() -> None:
    crawler = BeautifulSoupCrawler()

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

    # Run the crawler with the initial list of requests.
    await crawler.run(
        [
            'https://crawlee.dev',
            'https://apify.com',
            'https://example.com',
        ]
    )


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQbGF5d3JpZ2h0Q3Jhd2xlciwgUGxheXdyaWdodENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IFBsYXl3cmlnaHRDcmF3bGVyKClcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IFBsYXl3cmlnaHRDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgIyBSdW4gdGhlIGNyYXdsZXIgd2l0aCB0aGUgaW5pdGlhbCBsaXN0IG9mIHJlcXVlc3RzLlxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihcXG4gICAgICAgIFtcXG4gICAgICAgICAgICAnaHR0cHM6Ly9jcmF3bGVlLmRldicsXFxuICAgICAgICAgICAgJ2h0dHBzOi8vYXBpZnkuY29tJyxcXG4gICAgICAgICAgICAnaHR0cHM6Ly9leGFtcGxlLmNvbScsXFxuICAgICAgICBdXFxuICAgIClcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6NDA5NiwidGltZW91dCI6MTgwfX0.CNHeABCayXpKLyTdzPrZz25XZZwmxCJs7WayWxx3AlA\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext


async def main() -> None:
    crawler = PlaywrightCrawler()

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

    # Run the crawler with the initial list of requests.
    await crawler.run(
        [
            'https://crawlee.dev',
            'https://apify.com',
            'https://example.com',
        ]
    )


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/examples/crawl_multiple_urls.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/examples/crawl-all-links-on-website.md)

[Crawl all links on website](https://crawlee.dev/python/python/docs/examples/crawl-all-links-on-website.md)

[Next](https://crawlee.dev/python/python/docs/examples/crawl-specific-links-on-website.md)

[Crawl specific links on website](https://crawlee.dev/python/python/docs/examples/crawl-specific-links-on-website.md)


---

* [](https://crawlee.dev/python/python)
* [Examples](https://crawlee.dev/python/python/docs/examples.md)
* Crawl specific links on website

Version: 1.6

On this page

# Crawl specific links on website

This example demonstrates how to crawl a website while targeting specific patterns of links. By utilizing the [`enqueue_links`](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md) helper, you can pass `include` or `exclude` parameters to improve your crawling strategy. This approach ensures that only the links matching the specified patterns are added to the [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md). Both `include` and `exclude` support lists of globs or regular expressions. This functionality is great for focusing on relevant sections of a website and avoiding scraping unnecessary or irrelevant content.

* BeautifulSoupCrawler
* PlaywrightCrawler

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBHbG9iXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKFxcbiAgICAgICAgIyBMaW1pdCB0aGUgY3Jhd2wgdG8gbWF4IHJlcXVlc3RzLiBSZW1vdmUgb3IgaW5jcmVhc2UgaXQgZm9yIGNyYXdsaW5nIGFsbCBsaW5rcy5cXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsXFxuICAgIClcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgICAgICMgRW5xdWV1ZSBhbGwgdGhlIGRvY3VtZW50YXRpb24gbGlua3MgZm91bmQgb24gdGhlIHBhZ2UsIGV4Y2VwdCBmb3IgdGhlIGV4YW1wbGVzLlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5lbnF1ZXVlX2xpbmtzKFxcbiAgICAgICAgICAgIGluY2x1ZGU9W0dsb2IoJ2h0dHBzOi8vY3Jhd2xlZS5kZXYvZG9jcy8qKicpXSxcXG4gICAgICAgICAgICBleGNsdWRlPVtHbG9iKCdodHRwczovL2NyYXdsZWUuZGV2L2RvY3MvZXhhbXBsZXMnKV0sXFxuICAgICAgICApXFxuXFxuICAgICMgUnVuIHRoZSBjcmF3bGVyIHdpdGggdGhlIGluaXRpYWwgbGlzdCBvZiByZXF1ZXN0cy5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2NyYXdsZWUuZGV2J10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.rlkWZP9u1OCmWj6gKRu_2L58lROJhvmOkdWhGjLrkQE\&asrc=run_on_apify)

```
import asyncio

from crawlee import Glob
from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


async def main() -> None:
    crawler = BeautifulSoupCrawler(
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
    )

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Enqueue all the documentation links found on the page, except for the examples.
        await context.enqueue_links(
            include=[Glob('https://crawlee.dev/docs/**')],
            exclude=[Glob('https://crawlee.dev/docs/examples')],
        )

    # Run the crawler with the initial list of requests.
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBHbG9iXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQbGF5d3JpZ2h0Q3Jhd2xlciwgUGxheXdyaWdodENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IFBsYXl3cmlnaHRDcmF3bGVyKFxcbiAgICAgICAgIyBMaW1pdCB0aGUgY3Jhd2wgdG8gbWF4IHJlcXVlc3RzLiBSZW1vdmUgb3IgaW5jcmVhc2UgaXQgZm9yIGNyYXdsaW5nIGFsbCBsaW5rcy5cXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsXFxuICAgIClcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IFBsYXl3cmlnaHRDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgICAgICMgRW5xdWV1ZSBhbGwgdGhlIGRvY3VtZW50YXRpb24gbGlua3MgZm91bmQgb24gdGhlIHBhZ2UsIGV4Y2VwdCBmb3IgdGhlIGV4YW1wbGVzLlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5lbnF1ZXVlX2xpbmtzKFxcbiAgICAgICAgICAgIGluY2x1ZGU9W0dsb2IoJ2h0dHBzOi8vY3Jhd2xlZS5kZXYvZG9jcy8qKicpXSxcXG4gICAgICAgICAgICBleGNsdWRlPVtHbG9iKCdodHRwczovL2NyYXdsZWUuZGV2L2RvY3MvZXhhbXBsZXMnKV0sXFxuICAgICAgICApXFxuXFxuICAgICMgUnVuIHRoZSBjcmF3bGVyIHdpdGggdGhlIGluaXRpYWwgbGlzdCBvZiByZXF1ZXN0cy5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2NyYXdsZWUuZGV2J10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjQwOTYsInRpbWVvdXQiOjE4MH19.U24aYDP_2bvpDUU4JCG1KmDoiAJKQU-c89ka5sqKUbc\&asrc=run_on_apify)

```
import asyncio

from crawlee import Glob
from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext


async def main() -> None:
    crawler = PlaywrightCrawler(
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
    )

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Enqueue all the documentation links found on the page, except for the examples.
        await context.enqueue_links(
            include=[Glob('https://crawlee.dev/docs/**')],
            exclude=[Glob('https://crawlee.dev/docs/examples')],
        )

    # Run the crawler with the initial list of requests.
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

## Even more control over the enqueued links[​](#even-more-control-over-the-enqueued-links "Direct link to Even more control over the enqueued links")

[`enqueue_links`](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md) is a convenience helper and internally it calls [`extract_links`](https://crawlee.dev/python/python/api/class/ExtractLinksFunction.md) to find the links and [`add_requests`](https://crawlee.dev/python/python/api/class/AddRequestsFunction.md) to add them to the queue. If you need some additional custom filtering of the extracted links before enqueuing them, then consider using [`extract_links`](https://crawlee.dev/python/python/api/class/ExtractLinksFunction.md) and [`add_requests`](https://crawlee.dev/python/python/api/class/AddRequestsFunction.md) instead of the [`enqueue_links`](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md)

* BeautifulSoupCrawler
* PlaywrightCrawler

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBHbG9iXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKFxcbiAgICAgICAgIyBMaW1pdCB0aGUgY3Jhd2wgdG8gbWF4IHJlcXVlc3RzLiBSZW1vdmUgb3IgaW5jcmVhc2UgaXQgZm9yIGNyYXdsaW5nIGFsbCBsaW5rcy5cXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsXFxuICAgIClcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgICAgICMgRXh0cmFjdCBhbGwgdGhlIGRvY3VtZW50YXRpb24gbGlua3MgZm91bmQgb24gdGhlIHBhZ2UsIGV4Y2VwdCBmb3IgdGhlIGV4YW1wbGVzLlxcbiAgICAgICAgZXh0cmFjdGVkX2xpbmtzID0gYXdhaXQgY29udGV4dC5leHRyYWN0X2xpbmtzKFxcbiAgICAgICAgICAgIGluY2x1ZGU9W0dsb2IoJ2h0dHBzOi8vY3Jhd2xlZS5kZXYvZG9jcy8qKicpXSxcXG4gICAgICAgICAgICBleGNsdWRlPVtHbG9iKCdodHRwczovL2NyYXdsZWUuZGV2L2RvY3MvZXhhbXBsZXMnKV0sXFxuICAgICAgICApXFxuICAgICAgICAjIFNvbWUgdmVyeSBjdXN0b20gZmlsdGVyaW5nIHdoaWNoIGNhbid0IGJlIGFjaGlldmVkIGJ5IGBleHRyYWN0X2xpbmtzYCBhcmd1bWVudHMuXFxuICAgICAgICBtYXhfbGlua19sZW5ndGggPSAzMFxcbiAgICAgICAgZmlsdGVyZWRfbGlua3MgPSBbXFxuICAgICAgICAgICAgbGluayBmb3IgbGluayBpbiBleHRyYWN0ZWRfbGlua3MgaWYgbGVuKGxpbmsudXJsKSA8IG1heF9saW5rX2xlbmd0aFxcbiAgICAgICAgXVxcbiAgICAgICAgIyBBZGQgZmlsdGVyZWQgbGlua3MgdG8gdGhlIHJlcXVlc3QgcXVldWUuXFxuICAgICAgICBhd2FpdCBjb250ZXh0LmFkZF9yZXF1ZXN0cyhmaWx0ZXJlZF9saW5rcylcXG5cXG4gICAgIyBSdW4gdGhlIGNyYXdsZXIgd2l0aCB0aGUgaW5pdGlhbCBsaXN0IG9mIHJlcXVlc3RzLlxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vY3Jhd2xlZS5kZXYnXSlcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6MTAyNCwidGltZW91dCI6MTgwfX0.6rS0L_JHbdCcihG9B_By_-sgy9KS54Ip7SfFRWh8VvQ\&asrc=run_on_apify)

```
import asyncio

from crawlee import Glob
from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


async def main() -> None:
    crawler = BeautifulSoupCrawler(
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
    )

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Extract all the documentation links found on the page, except for the examples.
        extracted_links = await context.extract_links(
            include=[Glob('https://crawlee.dev/docs/**')],
            exclude=[Glob('https://crawlee.dev/docs/examples')],
        )
        # Some very custom filtering which can't be achieved by `extract_links` arguments.
        max_link_length = 30
        filtered_links = [
            link for link in extracted_links if len(link.url) < max_link_length
        ]
        # Add filtered links to the request queue.
        await context.add_requests(filtered_links)

    # Run the crawler with the initial list of requests.
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBHbG9iXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQbGF5d3JpZ2h0Q3Jhd2xlciwgUGxheXdyaWdodENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IFBsYXl3cmlnaHRDcmF3bGVyKFxcbiAgICAgICAgIyBMaW1pdCB0aGUgY3Jhd2wgdG8gbWF4IHJlcXVlc3RzLiBSZW1vdmUgb3IgaW5jcmVhc2UgaXQgZm9yIGNyYXdsaW5nIGFsbCBsaW5rcy5cXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsXFxuICAgIClcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IFBsYXl3cmlnaHRDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgICAgICMgRXh0cmFjdCBhbGwgdGhlIGRvY3VtZW50YXRpb24gbGlua3MgZm91bmQgb24gdGhlIHBhZ2UsIGV4Y2VwdCBmb3IgdGhlIGV4YW1wbGVzLlxcbiAgICAgICAgZXh0cmFjdGVkX2xpbmtzID0gYXdhaXQgY29udGV4dC5leHRyYWN0X2xpbmtzKFxcbiAgICAgICAgICAgIGluY2x1ZGU9W0dsb2IoJ2h0dHBzOi8vY3Jhd2xlZS5kZXYvZG9jcy8qKicpXSxcXG4gICAgICAgICAgICBleGNsdWRlPVtHbG9iKCdodHRwczovL2NyYXdsZWUuZGV2L2RvY3MvZXhhbXBsZXMnKV0sXFxuICAgICAgICApXFxuICAgICAgICAjIFNvbWUgdmVyeSBjdXN0b20gZmlsdGVyaW5nIHdoaWNoIGNhbid0IGJlIGFjaGlldmVkIGJ5IGBleHRyYWN0X2xpbmtzYCBhcmd1bWVudHMuXFxuICAgICAgICBtYXhfbGlua19sZW5ndGggPSAzMFxcbiAgICAgICAgZmlsdGVyZWRfbGlua3MgPSBbXFxuICAgICAgICAgICAgbGluayBmb3IgbGluayBpbiBleHRyYWN0ZWRfbGlua3MgaWYgbGVuKGxpbmsudXJsKSA8IG1heF9saW5rX2xlbmd0aFxcbiAgICAgICAgXVxcbiAgICAgICAgIyBBZGQgZmlsdGVyZWQgbGlua3MgdG8gdGhlIHJlcXVlc3QgcXVldWUuXFxuICAgICAgICBhd2FpdCBjb250ZXh0LmFkZF9yZXF1ZXN0cyhmaWx0ZXJlZF9saW5rcylcXG5cXG4gICAgIyBSdW4gdGhlIGNyYXdsZXIgd2l0aCB0aGUgaW5pdGlhbCBsaXN0IG9mIHJlcXVlc3RzLlxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vY3Jhd2xlZS5kZXYnXSlcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6NDA5NiwidGltZW91dCI6MTgwfX0.83OITwBV2EVOdkdWaZ4WJYlFUgcYUveLEQW01YtXeHE\&asrc=run_on_apify)

```
import asyncio

from crawlee import Glob
from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext


async def main() -> None:
    crawler = PlaywrightCrawler(
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
    )

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Extract all the documentation links found on the page, except for the examples.
        extracted_links = await context.extract_links(
            include=[Glob('https://crawlee.dev/docs/**')],
            exclude=[Glob('https://crawlee.dev/docs/examples')],
        )
        # Some very custom filtering which can't be achieved by `extract_links` arguments.
        max_link_length = 30
        filtered_links = [
            link for link in extracted_links if len(link.url) < max_link_length
        ]
        # Add filtered links to the request queue.
        await context.add_requests(filtered_links)

    # Run the crawler with the initial list of requests.
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/examples/crawl_specific_links_on_website.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/examples/crawl-multiple-urls.md)

[Crawl multiple URLs](https://crawlee.dev/python/python/docs/examples/crawl-multiple-urls.md)

[Next](https://crawlee.dev/python/python/docs/examples/crawl-website-with-relative-links.md)

[Crawl website with relative links](https://crawlee.dev/python/python/docs/examples/crawl-website-with-relative-links.md)


---

* [](https://crawlee.dev/python/python)
* [Examples](https://crawlee.dev/python/python/docs/examples.md)
* Crawl website with relative links

Version: 1.6

# Crawl website with relative links

When crawling a website, you may encounter various types of links that you wish to include in your crawl. To facilitate this, we provide the [`enqueue_links`](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md) method on the crawler context, which will automatically find and add these links to the crawler's [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md). This method simplifies the process of handling different types of links, including relative links, by automatically resolving them based on the page's context.

note

For these examples, we are using the [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md). However, the same method is available for other crawlers as well. You can use it in exactly the same way.

`EnqueueStrategy` type alias provides four distinct strategies for crawling relative links:

* `all` - Enqueues all links found, regardless of the domain they point to. This strategy is useful when you want to follow every link, including those that navigate to external websites.
* `same-domain` - Enqueues all links found that share the same domain name, including any possible subdomains. This strategy ensures that all links within the same top-level and base domain are included.
* `same-hostname` - Enqueues all links found for the exact same hostname. This is the **default** strategy, and it restricts the crawl to links that have the same hostname as the current page, excluding subdomains.
* `same-origin` - Enqueues all links found that share the same origin. The same origin refers to URLs that share the same protocol, domain, and port, ensuring a strict scope for the crawl.

- All links
- Same domain
- Same hostname
- Same origin

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKFxcbiAgICAgICAgIyBMaW1pdCB0aGUgY3Jhd2wgdG8gbWF4IHJlcXVlc3RzLiBSZW1vdmUgb3IgaW5jcmVhc2UgaXQgZm9yIGNyYXdsaW5nIGFsbCBsaW5rcy5cXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsXFxuICAgIClcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgICAgICMgRW5xdWV1ZSBhbGwgbGlua3MgZm91bmQgb24gdGhlIHBhZ2UuIEFueSBVUkxzIGZvdW5kIHdpbGwgYmUgbWF0Y2hlZCBieVxcbiAgICAgICAgIyB0aGlzIHN0cmF0ZWd5LCBldmVuIGlmIHRoZXkgZ28gb2ZmIHRoZSBzaXRlIHlvdSBhcmUgY3VycmVudGx5IGNyYXdsaW5nLlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5lbnF1ZXVlX2xpbmtzKHN0cmF0ZWd5PSdhbGwnKVxcblxcbiAgICAjIFJ1biB0aGUgY3Jhd2xlciB3aXRoIHRoZSBpbml0aWFsIGxpc3Qgb2YgcmVxdWVzdHMuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9jcmF3bGVlLmRldiddKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.yQpvn-pVLXiMLj_rceTXra7Imdx35s56gBCaIqvhCM4\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


async def main() -> None:
    crawler = BeautifulSoupCrawler(
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
    )

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Enqueue all links found on the page. Any URLs found will be matched by
        # this strategy, even if they go off the site you are currently crawling.
        await context.enqueue_links(strategy='all')

    # Run the crawler with the initial list of requests.
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKFxcbiAgICAgICAgIyBMaW1pdCB0aGUgY3Jhd2wgdG8gbWF4IHJlcXVlc3RzLiBSZW1vdmUgb3IgaW5jcmVhc2UgaXQgZm9yIGNyYXdsaW5nIGFsbCBsaW5rcy5cXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsXFxuICAgIClcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgICAgICMgU2V0dGluZyB0aGUgc3RyYXRlZ3kgdG8gc2FtZSBkb21haW4gd2lsbCBlbnF1ZXVlIGFsbCBsaW5rcyBmb3VuZCB0aGF0XFxuICAgICAgICAjIGFyZSBvbiB0aGUgc2FtZSBob3N0bmFtZSBhcyByZXF1ZXN0LmxvYWRlZF91cmwgb3IgcmVxdWVzdC51cmwuXFxuICAgICAgICBhd2FpdCBjb250ZXh0LmVucXVldWVfbGlua3Moc3RyYXRlZ3k9J3NhbWUtZG9tYWluJylcXG5cXG4gICAgIyBSdW4gdGhlIGNyYXdsZXIgd2l0aCB0aGUgaW5pdGlhbCBsaXN0IG9mIHJlcXVlc3RzLlxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vY3Jhd2xlZS5kZXYnXSlcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6MTAyNCwidGltZW91dCI6MTgwfX0.Jy-UTdyIlK9eZC0vqQOKoNemVfvQHZ2pHDkmfqLPj5M\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


async def main() -> None:
    crawler = BeautifulSoupCrawler(
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
    )

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Setting the strategy to same domain will enqueue all links found that
        # are on the same hostname as request.loaded_url or request.url.
        await context.enqueue_links(strategy='same-domain')

    # Run the crawler with the initial list of requests.
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKFxcbiAgICAgICAgIyBMaW1pdCB0aGUgY3Jhd2wgdG8gbWF4IHJlcXVlc3RzLiBSZW1vdmUgb3IgaW5jcmVhc2UgaXQgZm9yIGNyYXdsaW5nIGFsbCBsaW5rcy5cXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsXFxuICAgIClcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgICAgICMgU2V0dGluZyB0aGUgc3RyYXRlZ3kgdG8gc2FtZSBob3N0bmFtZSB3aWxsIGVucXVldWUgYWxsIGxpbmtzIGZvdW5kIHRoYXQgYXJlIG9uXFxuICAgICAgICAjIHRoZSBzYW1lIGhvc3RuYW1lIChpbmNsdWRpbmcgc3ViZG9tYWlucykgYXMgcmVxdWVzdC5sb2FkZWRfdXJsIG9yIHJlcXVlc3QudXJsLlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5lbnF1ZXVlX2xpbmtzKHN0cmF0ZWd5PSdzYW1lLWhvc3RuYW1lJylcXG5cXG4gICAgIyBSdW4gdGhlIGNyYXdsZXIgd2l0aCB0aGUgaW5pdGlhbCBsaXN0IG9mIHJlcXVlc3RzLlxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vY3Jhd2xlZS5kZXYnXSlcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6MTAyNCwidGltZW91dCI6MTgwfX0.iYM_Fx4YYiXDxA5EywEXwbWA2cL0vx7Bsus9buZWbRc\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


async def main() -> None:
    crawler = BeautifulSoupCrawler(
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
    )

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Setting the strategy to same hostname will enqueue all links found that are on
        # the same hostname (including subdomains) as request.loaded_url or request.url.
        await context.enqueue_links(strategy='same-hostname')

    # Run the crawler with the initial list of requests.
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKFxcbiAgICAgICAgIyBMaW1pdCB0aGUgY3Jhd2wgdG8gbWF4IHJlcXVlc3RzLiBSZW1vdmUgb3IgaW5jcmVhc2UgaXQgZm9yIGNyYXdsaW5nIGFsbCBsaW5rcy5cXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsXFxuICAgIClcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgICAgICMgU2V0dGluZyB0aGUgc3RyYXRlZ3kgdG8gc2FtZSBvcmlnaW4gd2lsbCBlbnF1ZXVlIGFsbCBsaW5rcyBmb3VuZCB0aGF0IGFyZSBvblxcbiAgICAgICAgIyB0aGUgc2FtZSBvcmlnaW4gYXMgcmVxdWVzdC5sb2FkZWRfdXJsIG9yIHJlcXVlc3QudXJsLlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5lbnF1ZXVlX2xpbmtzKHN0cmF0ZWd5PSdzYW1lLW9yaWdpbicpXFxuXFxuICAgICMgUnVuIHRoZSBjcmF3bGVyIHdpdGggdGhlIGluaXRpYWwgbGlzdCBvZiByZXF1ZXN0cy5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2NyYXdsZWUuZGV2J10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.r9dWziEUkvwaVr0UB62KtXoU5TU7lElDbEi6phJOHQU\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


async def main() -> None:
    crawler = BeautifulSoupCrawler(
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
    )

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Setting the strategy to same origin will enqueue all links found that are on
        # the same origin as request.loaded_url or request.url.
        await context.enqueue_links(strategy='same-origin')

    # Run the crawler with the initial list of requests.
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/examples/crawl_website_with_relative_links.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/examples/crawl-specific-links-on-website.md)

[Crawl specific links on website](https://crawlee.dev/python/python/docs/examples/crawl-specific-links-on-website.md)

[Next](https://crawlee.dev/python/python/docs/examples/crawler-keep-alive.md)

[Keep a Crawler alive waiting for more requests](https://crawlee.dev/python/python/docs/examples/crawler-keep-alive.md)


---

* [](https://crawlee.dev/python/python)
* [Examples](https://crawlee.dev/python/python/docs/examples.md)
* Keep a Crawler alive waiting for more requests

Version: 1.6

# Keep a Crawler alive waiting for more requests

This example demonstrates how to keep crawler alive even when there are no requests at the moment by using `keep_alive=True` argument of [`BasicCrawler.__init__`](https://crawlee.dev/python/python/api/class/BasicCrawler.md#__init__). This is available to all crawlers that inherit from [`BasicCrawler`](https://crawlee.dev/python/python/api/class/BasicCrawler.md) and in the example below it is shown on [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md). To stop the crawler that was started with `keep_alive=True` you can call `crawler.stop()`.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLl90eXBlcyBpbXBvcnQgQmFzaWNDcmF3bGluZ0NvbnRleHRcXG5mcm9tIGNyYXdsZWUuY3Jhd2xlcnMgaW1wb3J0IEJlYXV0aWZ1bFNvdXBDcmF3bGVyXFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICBjcmF3bGVyID0gQmVhdXRpZnVsU291cENyYXdsZXIoXFxuICAgICAgICAjIEtlZXAgdGhlIGNyYXdsZXIgYWxpdmUgZXZlbiB3aGVuIHRoZXJlIGFyZSBubyByZXF1ZXN0cyB0byBiZSBwcm9jZXNzZWQgbm93LlxcbiAgICAgICAga2VlcF9hbGl2ZT1UcnVlLFxcbiAgICApXFxuXFxuICAgIGRlZiBzdG9wX2NyYXdsZXJfaWZfdXJsX3Zpc2l0ZWQoY29udGV4dDogQmFzaWNDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBcXFwiXFxcIlxcXCJTdG9wIGNyYXdsZXIgb25jZSBzcGVjaWZpYyB1cmwgaXMgdmlzaXRlZC5cXG5cXG4gICAgICAgIEV4YW1wbGUgb2YgZ3VhcmQgY29uZGl0aW9uIHRvIHN0b3AgdGhlIGNyYXdsZXIuXFxcIlxcXCJcXFwiXFxuICAgICAgICBpZiBjb250ZXh0LnJlcXVlc3QudXJsID09ICdodHRwczovL2NyYXdsZWUuZGV2L2RvY3MvZXhhbXBsZXMnOlxcbiAgICAgICAgICAgIGNyYXdsZXIuc3RvcChcXG4gICAgICAgICAgICAgICAgJ1N0b3AgY3Jhd2xlciB0aGF0IHdhcyBpbiBrZWVwX2FsaXZlIHN0YXRlIGFmdGVyIHNwZWNpZmljIHVybCB3YXMgdmlzaXRlJ1xcbiAgICAgICAgICAgIClcXG4gICAgICAgIGVsc2U6XFxuICAgICAgICAgICAgY29udGV4dC5sb2cuaW5mbygna2VlcF9hbGl2ZT1UcnVlLCB3YWl0aW5nIGZvciBtb3JlIHJlcXVlc3RzIHRvIGNvbWUuJylcXG5cXG4gICAgYXN5bmMgZGVmIGFkZF9yZXF1ZXN0X2xhdGVyKHVybDogc3RyLCBhZnRlcl9zOiBpbnQpIC0-IE5vbmU6XFxuICAgICAgICBcXFwiXFxcIlxcXCJBZGQgcmVxdWVzdHMgdG8gdGhlIHF1ZXVlIGFmdGVyIHNvbWUgdGltZS4gQ2FuIGJlIGRvbmUgYnkgZXh0ZXJuYWwgY29kZS5cXFwiXFxcIlxcXCJcXG4gICAgICAgICMgSnVzdCBhbiBleGFtcGxlIG9mIHJlcXVlc3QgYmVpbmcgYWRkZWQgdG8gdGhlIGNyYXdsZXIgbGF0ZXIsXFxuICAgICAgICAjIHdoZW4gaXQgaXMgd2FpdGluZyBkdWUgdG8gYGtlZXBfYWxpdmU9VHJ1ZWAuXFxuICAgICAgICBhd2FpdCBhc3luY2lvLnNsZWVwKGFmdGVyX3MpXFxuICAgICAgICBhd2FpdCBjcmF3bGVyLmFkZF9yZXF1ZXN0cyhbdXJsXSlcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IEJhc2ljQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ1Byb2Nlc3Npbmcge2NvbnRleHQucmVxdWVzdC51cmx9IC4uLicpXFxuXFxuICAgICAgICAjIFN0b3AgY3Jhd2xlciBpZiBzb21lIGd1YXJkIGNvbmRpdGlvbiBoYXMgYmVlbiBtZXQuXFxuICAgICAgICBzdG9wX2NyYXdsZXJfaWZfdXJsX3Zpc2l0ZWQoY29udGV4dClcXG5cXG4gICAgIyBTdGFydCBzb21lIHRhc2tzIHRoYXQgd2lsbCBhZGQgc29tZSByZXF1ZXN0cyBsYXRlciB0byBzaW11bGF0ZSByZWFsIHNpdHVhdGlvbixcXG4gICAgIyB3aGVyZSByZXF1ZXN0cyBhcmUgYWRkZWQgbGF0ZXIgYnkgZXh0ZXJuYWwgY29kZS5cXG4gICAgYWRkX3JlcXVlc3RfbGF0ZXJfdGFzazEgPSBhc3luY2lvLmNyZWF0ZV90YXNrKFxcbiAgICAgICAgYWRkX3JlcXVlc3RfbGF0ZXIodXJsPSdodHRwczovL2NyYXdsZWUuZGV2JywgYWZ0ZXJfcz0xKVxcbiAgICApXFxuICAgIGFkZF9yZXF1ZXN0X2xhdGVyX3Rhc2syID0gYXN5bmNpby5jcmVhdGVfdGFzayhcXG4gICAgICAgIGFkZF9yZXF1ZXN0X2xhdGVyKHVybD0naHR0cHM6Ly9jcmF3bGVlLmRldi9kb2NzL2V4YW1wbGVzJywgYWZ0ZXJfcz01KVxcbiAgICApXFxuXFxuICAgICMgUnVuIHRoZSBjcmF3bGVyIHdpdGhvdXQgdGhlIGluaXRpYWwgbGlzdCBvZiByZXF1ZXN0cy5cXG4gICAgIyBXYWl0IGZvciBtb3JlIHJlcXVlc3RzIHRvIGJlIGFkZGVkIHRvIHRoZSBxdWV1ZSBsYXRlciBkdWUgdG8gYGtlZXBfYWxpdmU9VHJ1ZWAuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKClcXG5cXG4gICAgYXdhaXQgYXN5bmNpby5nYXRoZXIoYWRkX3JlcXVlc3RfbGF0ZXJfdGFzazEsIGFkZF9yZXF1ZXN0X2xhdGVyX3Rhc2syKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.VHt2OCamVIE_FgmCMto_GVRC87SGX-vpEw8-iOrTQ18\&asrc=run_on_apify)

```
import asyncio

from crawlee._types import BasicCrawlingContext
from crawlee.crawlers import BeautifulSoupCrawler


async def main() -> None:
    crawler = BeautifulSoupCrawler(
        # Keep the crawler alive even when there are no requests to be processed now.
        keep_alive=True,
    )

    def stop_crawler_if_url_visited(context: BasicCrawlingContext) -> None:
        """Stop crawler once specific url is visited.

        Example of guard condition to stop the crawler."""
        if context.request.url == 'https://crawlee.dev/docs/examples':
            crawler.stop(
                'Stop crawler that was in keep_alive state after specific url was visite'
            )
        else:
            context.log.info('keep_alive=True, waiting for more requests to come.')

    async def add_request_later(url: str, after_s: int) -> None:
        """Add requests to the queue after some time. Can be done by external code."""
        # Just an example of request being added to the crawler later,
        # when it is waiting due to `keep_alive=True`.
        await asyncio.sleep(after_s)
        await crawler.add_requests([url])

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: BasicCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Stop crawler if some guard condition has been met.
        stop_crawler_if_url_visited(context)

    # Start some tasks that will add some requests later to simulate real situation,
    # where requests are added later by external code.
    add_request_later_task1 = asyncio.create_task(
        add_request_later(url='https://crawlee.dev', after_s=1)
    )
    add_request_later_task2 = asyncio.create_task(
        add_request_later(url='https://crawlee.dev/docs/examples', after_s=5)
    )

    # Run the crawler without the initial list of requests.
    # Wait for more requests to be added to the queue later due to `keep_alive=True`.
    await crawler.run()

    await asyncio.gather(add_request_later_task1, add_request_later_task2)


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/examples/crawler_keep_alive.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/examples/crawl-website-with-relative-links.md)

[Crawl website with relative links](https://crawlee.dev/python/python/docs/examples/crawl-website-with-relative-links.md)

[Next](https://crawlee.dev/python/python/docs/examples/crawler-stop.md)

[Stopping a Crawler with stop method](https://crawlee.dev/python/python/docs/examples/crawler-stop.md)


---

* [](https://crawlee.dev/python/python)
* [Examples](https://crawlee.dev/python/python/docs/examples.md)
* Stopping a Crawler with stop method

Version: 1.6

# Stopping a Crawler with stop method

This example demonstrates how to use `stop` method of [`BasicCrawler`](https://crawlee.dev/python/python/api/class/BasicCrawler.md) to stop crawler once the crawler finds what it is looking for. This method is available to all crawlers that inherit from [`BasicCrawler`](https://crawlee.dev/python/python/api/class/BasicCrawler.md) and in the example below it is shown on [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md). Simply call `crawler.stop()` to stop the crawler. It will not continue to crawl through new requests. Requests that are already being concurrently processed are going to get finished. It is possible to call `stop` method with optional argument `reason` that is a string that will be used in logs and it can improve logs readability especially if you have multiple different conditions for triggering `stop`.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBDcmVhdGUgYW4gaW5zdGFuY2Ugb2YgdGhlIEJlYXV0aWZ1bFNvdXBDcmF3bGVyIGNsYXNzLCBhIGNyYXdsZXIgdGhhdCBhdXRvbWF0aWNhbGx5XFxuICAgICMgbG9hZHMgdGhlIFVSTHMgYW5kIHBhcnNlcyB0aGVpciBIVE1MIHVzaW5nIHRoZSBCZWF1dGlmdWxTb3VwIGxpYnJhcnkuXFxuICAgIGNyYXdsZXIgPSBCZWF1dGlmdWxTb3VwQ3Jhd2xlcigpXFxuXFxuICAgICMgRGVmaW5lIHRoZSBkZWZhdWx0IHJlcXVlc3QgaGFuZGxlciwgd2hpY2ggd2lsbCBiZSBjYWxsZWQgZm9yIGV2ZXJ5IHJlcXVlc3QuXFxuICAgICMgVGhlIGhhbmRsZXIgcmVjZWl2ZXMgYSBjb250ZXh0IHBhcmFtZXRlciwgcHJvdmlkaW5nIHZhcmlvdXMgcHJvcGVydGllcyBhbmRcXG4gICAgIyBoZWxwZXIgbWV0aG9kcy4gSGVyZSBhcmUgYSBmZXcga2V5IG9uZXMgd2UgdXNlIGZvciBkZW1vbnN0cmF0aW9uOlxcbiAgICAjIC0gcmVxdWVzdDogYW4gaW5zdGFuY2Ugb2YgdGhlIFJlcXVlc3QgY2xhc3MgY29udGFpbmluZyBkZXRhaWxzIHN1Y2ggYXMgdGhlIFVSTFxcbiAgICAjICAgYmVpbmcgY3Jhd2xlZCBhbmQgdGhlIEhUVFAgbWV0aG9kIHVzZWQuXFxuICAgICMgLSBzb3VwOiB0aGUgQmVhdXRpZnVsU291cCBvYmplY3QgY29udGFpbmluZyB0aGUgcGFyc2VkIEhUTUwgb2YgdGhlIHJlc3BvbnNlLlxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiByZXF1ZXN0X2hhbmRsZXIoY29udGV4dDogQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm9jZXNzaW5nIHtjb250ZXh0LnJlcXVlc3QudXJsfSAuLi4nKVxcblxcbiAgICAgICAgIyBDcmVhdGUgY3VzdG9tIGNvbmRpdGlvbiB0byBzdG9wIGNyYXdsZXIgb25jZSBpdCBmaW5kcyB3aGF0IGl0IGlzIGxvb2tpbmcgZm9yLlxcbiAgICAgICAgaWYgJ2NyYXdsZWUnIGluIGNvbnRleHQucmVxdWVzdC51cmw6XFxuICAgICAgICAgICAgY3Jhd2xlci5zdG9wKFxcbiAgICAgICAgICAgICAgICByZWFzb249J01hbnVhbCBzdG9wIG9mIGNyYXdsZXIgYWZ0ZXIgZmluZGluZyBgY3Jhd2xlZWAgaW4gdGhlIHVybC4nXFxuICAgICAgICAgICAgKVxcblxcbiAgICAgICAgIyBFeHRyYWN0IGRhdGEgZnJvbSB0aGUgcGFnZS5cXG4gICAgICAgIGRhdGEgPSB7XFxuICAgICAgICAgICAgJ3VybCc6IGNvbnRleHQucmVxdWVzdC51cmwsXFxuICAgICAgICB9XFxuXFxuICAgICAgICAjIFB1c2ggdGhlIGV4dHJhY3RlZCBkYXRhIHRvIHRoZSBkZWZhdWx0IGRhdGFzZXQuIEluIGxvY2FsIGNvbmZpZ3VyYXRpb24sXFxuICAgICAgICAjIHRoZSBkYXRhIHdpbGwgYmUgc3RvcmVkIGFzIEpTT04gZmlsZXMgaW4gLi9zdG9yYWdlL2RhdGFzZXRzL2RlZmF1bHQuXFxuICAgICAgICBhd2FpdCBjb250ZXh0LnB1c2hfZGF0YShkYXRhKVxcblxcbiAgICAjIFJ1biB0aGUgY3Jhd2xlciB3aXRoIHRoZSBpbml0aWFsIGxpc3Qgb2YgVVJMcy5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2NyYXdsZWUuZGV2J10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.8nR1VL0ZQ3LE-drX-JiqGfIyEX5htSweXCXwflerbNo\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


async def main() -> None:
    # Create an instance of the BeautifulSoupCrawler class, a crawler that automatically
    # loads the URLs and parses their HTML using the BeautifulSoup library.
    crawler = BeautifulSoupCrawler()

    # Define the default request handler, which will be called for every request.
    # The handler receives a context parameter, providing various properties and
    # helper methods. Here are a few key ones we use for demonstration:
    # - request: an instance of the Request class containing details such as the URL
    #   being crawled and the HTTP method used.
    # - soup: the BeautifulSoup object containing the parsed HTML of the response.
    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Create custom condition to stop crawler once it finds what it is looking for.
        if 'crawlee' in context.request.url:
            crawler.stop(
                reason='Manual stop of crawler after finding `crawlee` in the url.'
            )

        # Extract data from the page.
        data = {
            'url': context.request.url,
        }

        # Push the extracted data to the default dataset. In local configuration,
        # the data will be stored as JSON files in ./storage/datasets/default.
        await context.push_data(data)

    # Run the crawler with the initial list of URLs.
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/examples/crawler_stop.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/examples/crawler-keep-alive.md)

[Keep a Crawler alive waiting for more requests](https://crawlee.dev/python/python/docs/examples/crawler-keep-alive.md)

[Next](https://crawlee.dev/python/python/docs/examples/export-entire-dataset-to-file.md)

[Export entire dataset to file](https://crawlee.dev/python/python/docs/examples/export-entire-dataset-to-file.md)


---

* [](https://crawlee.dev/python/python)
* [Examples](https://crawlee.dev/python/python/docs/examples.md)
* Export entire dataset to file

Version: 1.6

# Export entire dataset to file

This example demonstrates how to use the [`BasicCrawler.export_data`](https://crawlee.dev/python/python/api/class/BasicCrawler.md#export_data) method of the crawler to export the entire default dataset to a single file. This method supports exporting data in either CSV or JSON format and also accepts additional keyword arguments so you can fine-tune the underlying `json.dump` or `csv.writer` behavior.

note

For these examples, we are using the [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md). However, the same method is available for other crawlers as well. You can use it in exactly the same way.

* JSON
* CSV

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKFxcbiAgICAgICAgIyBMaW1pdCB0aGUgY3Jhd2wgdG8gbWF4IHJlcXVlc3RzLiBSZW1vdmUgb3IgaW5jcmVhc2UgaXQgZm9yIGNyYXdsaW5nIGFsbCBsaW5rcy5cXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsXFxuICAgIClcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgICAgICMgRXh0cmFjdCBkYXRhIGZyb20gdGhlIHBhZ2UuXFxuICAgICAgICBkYXRhID0ge1xcbiAgICAgICAgICAgICd1cmwnOiBjb250ZXh0LnJlcXVlc3QudXJsLFxcbiAgICAgICAgICAgICd0aXRsZSc6IGNvbnRleHQuc291cC50aXRsZS5zdHJpbmcgaWYgY29udGV4dC5zb3VwLnRpdGxlIGVsc2UgTm9uZSxcXG4gICAgICAgIH1cXG5cXG4gICAgICAgICMgRW5xdWV1ZSBhbGwgbGlua3MgZm91bmQgb24gdGhlIHBhZ2UuXFxuICAgICAgICBhd2FpdCBjb250ZXh0LmVucXVldWVfbGlua3MoKVxcblxcbiAgICAgICAgIyBQdXNoIHRoZSBleHRyYWN0ZWQgZGF0YSB0byB0aGUgZGVmYXVsdCBkYXRhc2V0LlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5wdXNoX2RhdGEoZGF0YSlcXG5cXG4gICAgIyBSdW4gdGhlIGNyYXdsZXIgd2l0aCB0aGUgaW5pdGlhbCBsaXN0IG9mIFVSTHMuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9jcmF3bGVlLmRldiddKVxcblxcbiAgICAjIEV4cG9ydCB0aGUgZW50aXJlIGRhdGFzZXQgdG8gYSBKU09OIGZpbGUuXFxuICAgICMgU2V0IGVuc3VyZV9hc2NpaT1GYWxzZSB0byBhbGxvdyBVbmljb2RlIGNoYXJhY3RlcnMgaW4gdGhlIG91dHB1dC5cXG4gICAgYXdhaXQgY3Jhd2xlci5leHBvcnRfZGF0YShwYXRoPSdyZXN1bHRzLmpzb24nLCBlbnN1cmVfYXNjaWk9RmFsc2UpXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.ZxVpcZcM0BQAeS3bkGsCq2AAMGAB3vCY9IpysrkvVSo\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


async def main() -> None:
    crawler = BeautifulSoupCrawler(
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
    )

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Extract data from the page.
        data = {
            'url': context.request.url,
            'title': context.soup.title.string if context.soup.title else None,
        }

        # Enqueue all links found on the page.
        await context.enqueue_links()

        # Push the extracted data to the default dataset.
        await context.push_data(data)

    # Run the crawler with the initial list of URLs.
    await crawler.run(['https://crawlee.dev'])

    # Export the entire dataset to a JSON file.
    # Set ensure_ascii=False to allow Unicode characters in the output.
    await crawler.export_data(path='results.json', ensure_ascii=False)


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKFxcbiAgICAgICAgIyBMaW1pdCB0aGUgY3Jhd2wgdG8gbWF4IHJlcXVlc3RzLiBSZW1vdmUgb3IgaW5jcmVhc2UgaXQgZm9yIGNyYXdsaW5nIGFsbCBsaW5rcy5cXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsXFxuICAgIClcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgICAgICMgRXh0cmFjdCBkYXRhIGZyb20gdGhlIHBhZ2UuXFxuICAgICAgICBkYXRhID0ge1xcbiAgICAgICAgICAgICd1cmwnOiBjb250ZXh0LnJlcXVlc3QudXJsLFxcbiAgICAgICAgICAgICd0aXRsZSc6IGNvbnRleHQuc291cC50aXRsZS5zdHJpbmcgaWYgY29udGV4dC5zb3VwLnRpdGxlIGVsc2UgTm9uZSxcXG4gICAgICAgIH1cXG5cXG4gICAgICAgICMgRW5xdWV1ZSBhbGwgbGlua3MgZm91bmQgb24gdGhlIHBhZ2UuXFxuICAgICAgICBhd2FpdCBjb250ZXh0LmVucXVldWVfbGlua3MoKVxcblxcbiAgICAgICAgIyBQdXNoIHRoZSBleHRyYWN0ZWQgZGF0YSB0byB0aGUgZGVmYXVsdCBkYXRhc2V0LlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5wdXNoX2RhdGEoZGF0YSlcXG5cXG4gICAgIyBSdW4gdGhlIGNyYXdsZXIgd2l0aCB0aGUgaW5pdGlhbCBsaXN0IG9mIFVSTHMuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9jcmF3bGVlLmRldiddKVxcblxcbiAgICAjIEV4cG9ydCB0aGUgZW50aXJlIGRhdGFzZXQgdG8gYSBDU1YgZmlsZS5cXG4gICAgIyBVc2Ugc2VtaWNvbG9uIGFzIGRlbGltaXRlciBhbmQgYWx3YXlzIHF1b3RlIHN0cmluZ3MuXFxuICAgIGF3YWl0IGNyYXdsZXIuZXhwb3J0X2RhdGEocGF0aD0ncmVzdWx0cy5jc3YnLCBkZWxpbWl0ZXI9JzsnLCBxdW90aW5nPSdhbGwnKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.75zi4waNk8862Kds46G2AbFIx22gxWwzqPkf7vw_b2U\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


async def main() -> None:
    crawler = BeautifulSoupCrawler(
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
    )

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Extract data from the page.
        data = {
            'url': context.request.url,
            'title': context.soup.title.string if context.soup.title else None,
        }

        # Enqueue all links found on the page.
        await context.enqueue_links()

        # Push the extracted data to the default dataset.
        await context.push_data(data)

    # Run the crawler with the initial list of URLs.
    await crawler.run(['https://crawlee.dev'])

    # Export the entire dataset to a CSV file.
    # Use semicolon as delimiter and always quote strings.
    await crawler.export_data(path='results.csv', delimiter=';', quoting='all')


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/examples/export_entire_dataset_to_file.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/examples/crawler-stop.md)

[Stopping a Crawler with stop method](https://crawlee.dev/python/python/docs/examples/crawler-stop.md)

[Next](https://crawlee.dev/python/python/docs/examples/fill-and-submit-web-form.md)

[Fill and submit web form](https://crawlee.dev/python/python/docs/examples/fill-and-submit-web-form.md)


---

* [](https://crawlee.dev/python/python)
* [Examples](https://crawlee.dev/python/python/docs/examples.md)
* Fill and submit web form

Version: 1.6

On this page

# Fill and submit web form

This example demonstrates how to fill and submit a web form using the [`HttpCrawler`](https://crawlee.dev/python/python/api/class/HttpCrawler.md) crawler. The same approach applies to any crawler that inherits from it, such as the [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md) or [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md).

We are going to use the [httpbin.org](https://httpbin.org) website to demonstrate how it works.

## Investigate the form fields[​](#investigate-the-form-fields "Direct link to Investigate the form fields")

First, we need to examine the form fields and the form's action URL. You can do this by opening the [httpbin.org/forms/post](https://httpbin.org/forms/post) page in a browser and inspecting the form fields.

In Chrome, right-click on the page and select "Inspect" or press `Ctrl+Shift+I`. Use the element selector (`Ctrl+Shift+C`) to click on the form element you want to inspect.

![HTML input element name](/python/assets/images/00-09050baf5e41c08fcfb503d69eaf0d90.jpg "HTML input element name.")

Identify the field names. For example, the customer name field is `custname`, the email field is `custemail`, and the phone field is `custtel`.

Now navigate to the "Network" tab in developer tools and submit the form by clicking the "Submit order" button.

![Submitting the form](/python/assets/images/01-4330cf02ef7bd8377001e62c52d01e1d.jpg "Submitting the form.")

Find the form submission request and examine its details. The "Headers" tab will show the submission URL, in this case, it is `https://httpbin.org/post`.

![Network request investigation](/python/assets/images/02-49f57112a93ccc713639e7366cd7da3f.jpg "Network request investigation.")

The "Payload" tab will display the form fields and their submitted values. This method could be an alternative to inspecting the HTML source code directly.

![Network payload investigation](/python/assets/images/03-0e4ea695ba635556486b4484633f8845.jpg "Network payload investigation.")

## Preparing a POST request[​](#preparing-a-post-request "Direct link to Preparing a POST request")

Now, let's create a POST request with the form fields and their values using the [`Request`](https://crawlee.dev/python/python/api/class/Request.md) class, specifically its [`Request.from_url`](https://crawlee.dev/python/python/api/class/Request.md#from_url) constructor:

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuZnJvbSB1cmxsaWIucGFyc2UgaW1wb3J0IHVybGVuY29kZVxcblxcbmZyb20gY3Jhd2xlZSBpbXBvcnQgUmVxdWVzdFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBQcmVwYXJlIGEgUE9TVCByZXF1ZXN0IHRvIHRoZSBmb3JtIGVuZHBvaW50LlxcbiAgICByZXF1ZXN0ID0gUmVxdWVzdC5mcm9tX3VybChcXG4gICAgICAgIHVybD0naHR0cHM6Ly9odHRwYmluLm9yZy9wb3N0JyxcXG4gICAgICAgIG1ldGhvZD0nUE9TVCcsXFxuICAgICAgICBoZWFkZXJzPXsnY29udGVudC10eXBlJzogJ2FwcGxpY2F0aW9uL3gtd3d3LWZvcm0tdXJsZW5jb2RlZCd9LFxcbiAgICAgICAgcGF5bG9hZD11cmxlbmNvZGUoXFxuICAgICAgICAgICAge1xcbiAgICAgICAgICAgICAgICAnY3VzdG5hbWUnOiAnSm9obiBEb2UnLFxcbiAgICAgICAgICAgICAgICAnY3VzdHRlbCc6ICcxMjM0NTY3ODkwJyxcXG4gICAgICAgICAgICAgICAgJ2N1c3RlbWFpbCc6ICdqb2huZG9lQGV4YW1wbGUuY29tJyxcXG4gICAgICAgICAgICAgICAgJ3NpemUnOiAnbGFyZ2UnLFxcbiAgICAgICAgICAgICAgICAndG9wcGluZyc6IFsnYmFjb24nLCAnY2hlZXNlJywgJ211c2hyb29tJ10sXFxuICAgICAgICAgICAgICAgICdkZWxpdmVyeSc6ICcxMzowMCcsXFxuICAgICAgICAgICAgICAgICdjb21tZW50cyc6ICdQbGVhc2UgcmluZyB0aGUgZG9vcmJlbGwgdXBvbiBhcnJpdmFsLicsXFxuICAgICAgICAgICAgfVxcbiAgICAgICAgKS5lbmNvZGUoKSxcXG4gICAgKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.j6C9eDcSpJFNTHwshV97IVSwyRWN_epbHm4BVEOfe04\&asrc=run_on_apify)

```
import asyncio
from urllib.parse import urlencode

from crawlee import Request


async def main() -> None:
    # Prepare a POST request to the form endpoint.
    request = Request.from_url(
        url='https://httpbin.org/post',
        method='POST',
        headers={'content-type': 'application/x-www-form-urlencoded'},
        payload=urlencode(
            {
                'custname': 'John Doe',
                'custtel': '1234567890',
                'custemail': 'johndoe@example.com',
                'size': 'large',
                'topping': ['bacon', 'cheese', 'mushroom'],
                'delivery': '13:00',
                'comments': 'Please ring the doorbell upon arrival.',
            }
        ).encode(),
    )


if __name__ == '__main__':
    asyncio.run(main())
```

Alternatively, you can send form data as URL parameters using the `url` argument. It depends on the form and how it is implemented. However, sending the data as a POST request body using the `payload` is generally a better approach.

## Implementing the crawler[​](#implementing-the-crawler "Direct link to Implementing the crawler")

Finally, let's implement the crawler and run it with the prepared request. Although we are using the [`HttpCrawler`](https://crawlee.dev/python/python/api/class/HttpCrawler.md), the process is the same for any crawler that inherits from it.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuZnJvbSB1cmxsaWIucGFyc2UgaW1wb3J0IHVybGVuY29kZVxcblxcbmZyb20gY3Jhd2xlZSBpbXBvcnQgUmVxdWVzdFxcbmZyb20gY3Jhd2xlZS5jcmF3bGVycyBpbXBvcnQgSHR0cENyYXdsZXIsIEh0dHBDcmF3bGluZ0NvbnRleHRcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgIGNyYXdsZXIgPSBIdHRwQ3Jhd2xlcigpXFxuXFxuICAgICMgRGVmaW5lIHRoZSBkZWZhdWx0IHJlcXVlc3QgaGFuZGxlciwgd2hpY2ggd2lsbCBiZSBjYWxsZWQgZm9yIGV2ZXJ5IHJlcXVlc3QuXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIHJlcXVlc3RfaGFuZGxlcihjb250ZXh0OiBIdHRwQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ1Byb2Nlc3Npbmcge2NvbnRleHQucmVxdWVzdC51cmx9IC4uLicpXFxuICAgICAgICByZXNwb25zZSA9IChhd2FpdCBjb250ZXh0Lmh0dHBfcmVzcG9uc2UucmVhZCgpKS5kZWNvZGUoJ3V0Zi04JylcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidSZXNwb25zZToge3Jlc3BvbnNlfScpICAjIFRvIHNlZSB0aGUgcmVzcG9uc2UgaW4gdGhlIGxvZ3MuXFxuXFxuICAgICMgUHJlcGFyZSBhIFBPU1QgcmVxdWVzdCB0byB0aGUgZm9ybSBlbmRwb2ludC5cXG4gICAgcmVxdWVzdCA9IFJlcXVlc3QuZnJvbV91cmwoXFxuICAgICAgICB1cmw9J2h0dHBzOi8vaHR0cGJpbi5vcmcvcG9zdCcsXFxuICAgICAgICBtZXRob2Q9J1BPU1QnLFxcbiAgICAgICAgaGVhZGVycz17J2NvbnRlbnQtdHlwZSc6ICdhcHBsaWNhdGlvbi94LXd3dy1mb3JtLXVybGVuY29kZWQnfSxcXG4gICAgICAgIHBheWxvYWQ9dXJsZW5jb2RlKFxcbiAgICAgICAgICAgIHtcXG4gICAgICAgICAgICAgICAgJ2N1c3RuYW1lJzogJ0pvaG4gRG9lJyxcXG4gICAgICAgICAgICAgICAgJ2N1c3R0ZWwnOiAnMTIzNDU2Nzg5MCcsXFxuICAgICAgICAgICAgICAgICdjdXN0ZW1haWwnOiAnam9obmRvZUBleGFtcGxlLmNvbScsXFxuICAgICAgICAgICAgICAgICdzaXplJzogJ2xhcmdlJyxcXG4gICAgICAgICAgICAgICAgJ3RvcHBpbmcnOiBbJ2JhY29uJywgJ2NoZWVzZScsICdtdXNocm9vbSddLFxcbiAgICAgICAgICAgICAgICAnZGVsaXZlcnknOiAnMTM6MDAnLFxcbiAgICAgICAgICAgICAgICAnY29tbWVudHMnOiAnUGxlYXNlIHJpbmcgdGhlIGRvb3JiZWxsIHVwb24gYXJyaXZhbC4nLFxcbiAgICAgICAgICAgIH1cXG4gICAgICAgICkuZW5jb2RlKCksXFxuICAgIClcXG5cXG4gICAgIyBSdW4gdGhlIGNyYXdsZXIgd2l0aCB0aGUgaW5pdGlhbCBsaXN0IG9mIHJlcXVlc3RzLlxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbcmVxdWVzdF0pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.YczBNFlsfbImUrJ1cnoZR4aEPAfXcUeAZ2nkAVAB7gs\&asrc=run_on_apify)

```
import asyncio
from urllib.parse import urlencode

from crawlee import Request
from crawlee.crawlers import HttpCrawler, HttpCrawlingContext


async def main() -> None:
    crawler = HttpCrawler()

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: HttpCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')
        response = (await context.http_response.read()).decode('utf-8')
        context.log.info(f'Response: {response}')  # To see the response in the logs.

    # Prepare a POST request to the form endpoint.
    request = Request.from_url(
        url='https://httpbin.org/post',
        method='POST',
        headers={'content-type': 'application/x-www-form-urlencoded'},
        payload=urlencode(
            {
                'custname': 'John Doe',
                'custtel': '1234567890',
                'custemail': 'johndoe@example.com',
                'size': 'large',
                'topping': ['bacon', 'cheese', 'mushroom'],
                'delivery': '13:00',
                'comments': 'Please ring the doorbell upon arrival.',
            }
        ).encode(),
    )

    # Run the crawler with the initial list of requests.
    await crawler.run([request])


if __name__ == '__main__':
    asyncio.run(main())
```

## Running the crawler[​](#running-the-crawler "Direct link to Running the crawler")

Finally, run your crawler. Your logs should show something like this:

```
...
[crawlee.http_crawler._http_crawler] INFO  Processing https://httpbin.org/post ...
[crawlee.http_crawler._http_crawler] INFO  Response: {
  "args": {},
  "data": "",
  "files": {},
  "form": {
    "comments": "Please ring the doorbell upon arrival.",
    "custemail": "johndoe@example.com",
    "custname": "John Doe",
    "custtel": "1234567890",
    "delivery": "13:00",
    "size": "large",
    "topping": [
      "bacon",
      "cheese",
      "mushroom"
    ]
  },
  "headers": {
    "Accept": "*/*",
    "Accept-Encoding": "gzip, deflate, br",
    "Content-Length": "190",
    "Content-Type": "application/x-www-form-urlencoded",
    "Host": "httpbin.org",
    "User-Agent": "python-httpx/0.27.0",
    "X-Amzn-Trace-Id": "Root=1-66c849d6-1ae432fb7b4156e6149ff37f"
  },
  "json": null,
  "origin": "78.80.81.196",
  "url": "https://httpbin.org/post"
}

[crawlee._autoscaling.autoscaled_pool] INFO  Waiting for remaining tasks to finish
[crawlee.http_crawler._http_crawler] INFO  Final request statistics:
┌───────────────────────────────┬──────────┐
│ requests_finished             │ 1        │
│ requests_failed               │ 0        │
│ retry_histogram               │ [1]      │
│ request_avg_failed_duration   │ None     │
│ request_avg_finished_duration │ 0.678442 │
│ requests_finished_per_minute  │ 85       │
│ requests_failed_per_minute    │ 0        │
│ request_total_duration        │ 0.678442 │
│ requests_total                │ 1        │
│ crawler_runtime               │ 0.707666 │
└───────────────────────────────┴──────────┘
```

This log output confirms that the crawler successfully submitted the form and processed the response. Congratulations! You have successfully filled and submitted a web form using the [`HttpCrawler`](https://crawlee.dev/python/python/api/class/HttpCrawler.md).

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/examples/fill_and_submit_web_form.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/examples/export-entire-dataset-to-file.md)

[Export entire dataset to file](https://crawlee.dev/python/python/docs/examples/export-entire-dataset-to-file.md)

[Next](https://crawlee.dev/python/python/docs/examples/configure-json-logging.md)

[Сonfigure JSON logging](https://crawlee.dev/python/python/docs/examples/configure-json-logging.md)


---

* [](https://crawlee.dev/python/python)
* [Examples](https://crawlee.dev/python/python/docs/examples.md)
* Parsel crawler

Version: 1.6

# Parsel crawler

This example shows how to use [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md) to crawl a website or a list of URLs. Each URL is loaded using a plain HTTP request and the response is parsed using [Parsel](https://pypi.org/project/parsel/) library which supports CSS and XPath selectors for HTML responses and JMESPath for JSON responses. We can extract data from all kinds of complex HTML structures using XPath. In this example, we will use Parsel to crawl github.com and extract page title, URL and emails found in the webpage. The default handler will scrape data from the current webpage and enqueue all the links found in the webpage for continuous scraping. It also shows how you can add optional pre-navigation hook to the crawler. Pre-navigation hooks are user defined functions that execute before sending the request.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCYXNpY0NyYXdsaW5nQ29udGV4dCwgUGFyc2VsQ3Jhd2xlciwgUGFyc2VsQ3Jhd2xpbmdDb250ZXh0XFxuXFxuIyBSZWdleCBmb3IgaWRlbnRpZnlpbmcgZW1haWwgYWRkcmVzc2VzIG9uIGEgd2VicGFnZS5cXG5FTUFJTF9SRUdFWCA9IHInW2EtekEtWjAtOS5fJSstXStAW2EtekEtWjAtOS4tXStcXFxcLlthLXpBLVpdezIsfSdcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgIGNyYXdsZXIgPSBQYXJzZWxDcmF3bGVyKFxcbiAgICAgICAgIyBMaW1pdCB0aGUgY3Jhd2wgdG8gbWF4IHJlcXVlc3RzLiBSZW1vdmUgb3IgaW5jcmVhc2UgaXQgZm9yIGNyYXdsaW5nIGFsbCBsaW5rcy5cXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsXFxuICAgIClcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IFBhcnNlbENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm9jZXNzaW5nIHtjb250ZXh0LnJlcXVlc3QudXJsfSAuLi4nKVxcblxcbiAgICAgICAgIyBFeHRyYWN0IGRhdGEgZnJvbSB0aGUgcGFnZS5cXG4gICAgICAgIGRhdGEgPSB7XFxuICAgICAgICAgICAgJ3VybCc6IGNvbnRleHQucmVxdWVzdC51cmwsXFxuICAgICAgICAgICAgJ3RpdGxlJzogY29udGV4dC5zZWxlY3Rvci54cGF0aCgnLy90aXRsZS90ZXh0KCknKS5nZXQoKSxcXG4gICAgICAgICAgICAnZW1haWxfYWRkcmVzc19saXN0JzogY29udGV4dC5zZWxlY3Rvci5yZShFTUFJTF9SRUdFWCksXFxuICAgICAgICB9XFxuXFxuICAgICAgICAjIFB1c2ggdGhlIGV4dHJhY3RlZCBkYXRhIHRvIHRoZSBkZWZhdWx0IGRhdGFzZXQuXFxuICAgICAgICBhd2FpdCBjb250ZXh0LnB1c2hfZGF0YShkYXRhKVxcblxcbiAgICAgICAgIyBFbnF1ZXVlIGFsbCBsaW5rcyBmb3VuZCBvbiB0aGUgcGFnZS5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQuZW5xdWV1ZV9saW5rcygpXFxuXFxuICAgICMgUmVnaXN0ZXIgcHJlIG5hdmlnYXRpb24gaG9vayB3aGljaCB3aWxsIGJlIGNhbGxlZCBiZWZvcmUgZWFjaCByZXF1ZXN0LlxcbiAgICAjIFRoaXMgaG9vayBpcyBvcHRpb25hbCBhbmQgZG9lcyBub3QgbmVlZCB0byBiZSBkZWZpbmVkIGF0IGFsbC5cXG4gICAgQGNyYXdsZXIucHJlX25hdmlnYXRpb25faG9va1xcbiAgICBhc3luYyBkZWYgc29tZV9ob29rKGNvbnRleHQ6IEJhc2ljQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgcGFzc1xcblxcbiAgICAjIFJ1biB0aGUgY3Jhd2xlciB3aXRoIHRoZSBpbml0aWFsIGxpc3Qgb2YgVVJMcy5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2dpdGh1Yi5jb20nXSlcXG5cXG4gICAgIyBFeHBvcnQgdGhlIGVudGlyZSBkYXRhc2V0IHRvIGEgSlNPTiBmaWxlLlxcbiAgICBhd2FpdCBjcmF3bGVyLmV4cG9ydF9kYXRhKHBhdGg9J3Jlc3VsdHMuanNvbicpXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.TjMZMRURMlSHu2KvfZTwix0NJhOLqVxFb0xYXpj89_I\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BasicCrawlingContext, ParselCrawler, ParselCrawlingContext

# Regex for identifying email addresses on a webpage.
EMAIL_REGEX = r'[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}'


async def main() -> None:
    crawler = ParselCrawler(
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
    )

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: ParselCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Extract data from the page.
        data = {
            'url': context.request.url,
            'title': context.selector.xpath('//title/text()').get(),
            'email_address_list': context.selector.re(EMAIL_REGEX),
        }

        # Push the extracted data to the default dataset.
        await context.push_data(data)

        # Enqueue all links found on the page.
        await context.enqueue_links()

    # Register pre navigation hook which will be called before each request.
    # This hook is optional and does not need to be defined at all.
    @crawler.pre_navigation_hook
    async def some_hook(context: BasicCrawlingContext) -> None:
        pass

    # Run the crawler with the initial list of URLs.
    await crawler.run(['https://github.com'])

    # Export the entire dataset to a JSON file.
    await crawler.export_data(path='results.json')


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/examples/parsel_crawler.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/examples/configure-json-logging.md)

[Сonfigure JSON logging](https://crawlee.dev/python/python/docs/examples/configure-json-logging.md)

[Next](https://crawlee.dev/python/python/docs/examples/playwright-crawler.md)

[Playwright crawler](https://crawlee.dev/python/python/docs/examples/playwright-crawler.md)


---

* [](https://crawlee.dev/python/python)
* [Examples](https://crawlee.dev/python/python/docs/examples.md)
* Playwright crawler

Version: 1.6

# Playwright crawler

This example demonstrates how to use [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) to recursively scrape the Hacker news website using headless Chromium and Playwright.

The [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) manages the browser and page instances, simplifying the process of interacting with web pages. In the request handler, Playwright's API is used to extract data from each post on the page. Specifically, it retrieves the title, rank, and URL of each post. Additionally, the handler enqueues links to the next pages to ensure continuous scraping. This setup is ideal for scraping dynamic web pages where JavaScript execution is required to render the content.

A **pre-navigation hook** can be used to perform actions before navigating to the URL. This hook provides further flexibility in controlling environment and preparing for navigation.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCAoXFxuICAgIFBsYXl3cmlnaHRDcmF3bGVyLFxcbiAgICBQbGF5d3JpZ2h0Q3Jhd2xpbmdDb250ZXh0LFxcbiAgICBQbGF5d3JpZ2h0UHJlTmF2Q3Jhd2xpbmdDb250ZXh0LFxcbilcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgIGNyYXdsZXIgPSBQbGF5d3JpZ2h0Q3Jhd2xlcihcXG4gICAgICAgICMgTGltaXQgdGhlIGNyYXdsIHRvIG1heCByZXF1ZXN0cy4gUmVtb3ZlIG9yIGluY3JlYXNlIGl0IGZvciBjcmF3bGluZyBhbGwgbGlua3MuXFxuICAgICAgICBtYXhfcmVxdWVzdHNfcGVyX2NyYXdsPTEwLFxcbiAgICAgICAgIyBIZWFkbGVzcyBtb2RlLCBzZXQgdG8gRmFsc2UgdG8gc2VlIHRoZSBicm93c2VyIGluIGFjdGlvbi5cXG4gICAgICAgIGhlYWRsZXNzPUZhbHNlLFxcbiAgICAgICAgIyBCcm93c2VyIHR5cGVzIHN1cHBvcnRlZCBieSBQbGF5d3JpZ2h0LlxcbiAgICAgICAgYnJvd3Nlcl90eXBlPSdjaHJvbWl1bScsXFxuICAgIClcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgIyBUaGUgaGFuZGxlciByZWNlaXZlcyBhIGNvbnRleHQgcGFyYW1ldGVyLCBwcm92aWRpbmcgdmFyaW91cyBwcm9wZXJ0aWVzIGFuZFxcbiAgICAjIGhlbHBlciBtZXRob2RzLiBIZXJlIGFyZSBhIGZldyBrZXkgb25lcyB3ZSB1c2UgZm9yIGRlbW9uc3RyYXRpb246XFxuICAgICMgLSByZXF1ZXN0OiBhbiBpbnN0YW5jZSBvZiB0aGUgUmVxdWVzdCBjbGFzcyBjb250YWluaW5nIGRldGFpbHMgc3VjaCBhcyB0aGUgVVJMXFxuICAgICMgICBiZWluZyBjcmF3bGVkIGFuZCB0aGUgSFRUUCBtZXRob2QgdXNlZC5cXG4gICAgIyAtIHBhZ2U6IFBsYXl3cmlnaHQncyBQYWdlIG9iamVjdCwgd2hpY2ggYWxsb3dzIGludGVyYWN0aW9uIHdpdGggdGhlIHdlYiBwYWdlXFxuICAgICMgICAoc2VlIGh0dHBzOi8vcGxheXdyaWdodC5kZXYvcHl0aG9uL2RvY3MvYXBpL2NsYXNzLXBhZ2UgZm9yIG1vcmUgZGV0YWlscykuXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIHJlcXVlc3RfaGFuZGxlcihjb250ZXh0OiBQbGF5d3JpZ2h0Q3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ1Byb2Nlc3Npbmcge2NvbnRleHQucmVxdWVzdC51cmx9IC4uLicpXFxuXFxuICAgICAgICAjIEV4dHJhY3QgZGF0YSBmcm9tIHRoZSBwYWdlIHVzaW5nIFBsYXl3cmlnaHQncyBBUEkuXFxuICAgICAgICBwb3N0cyA9IGF3YWl0IGNvbnRleHQucGFnZS5xdWVyeV9zZWxlY3Rvcl9hbGwoJy5hdGhpbmcnKVxcbiAgICAgICAgZGF0YSA9IFtdXFxuXFxuICAgICAgICBmb3IgcG9zdCBpbiBwb3N0czpcXG4gICAgICAgICAgICAjIEdldCB0aGUgSFRNTCBlbGVtZW50cyBmb3IgdGhlIHRpdGxlIGFuZCByYW5rIHdpdGhpbiBlYWNoIHBvc3QuXFxuICAgICAgICAgICAgdGl0bGVfZWxlbWVudCA9IGF3YWl0IHBvc3QucXVlcnlfc2VsZWN0b3IoJy50aXRsZSBhJylcXG4gICAgICAgICAgICByYW5rX2VsZW1lbnQgPSBhd2FpdCBwb3N0LnF1ZXJ5X3NlbGVjdG9yKCcucmFuaycpXFxuXFxuICAgICAgICAgICAgIyBFeHRyYWN0IHRoZSBkYXRhIHdlIHdhbnQgZnJvbSB0aGUgZWxlbWVudHMuXFxuICAgICAgICAgICAgdGl0bGUgPSBhd2FpdCB0aXRsZV9lbGVtZW50LmlubmVyX3RleHQoKSBpZiB0aXRsZV9lbGVtZW50IGVsc2UgTm9uZVxcbiAgICAgICAgICAgIHJhbmsgPSBhd2FpdCByYW5rX2VsZW1lbnQuaW5uZXJfdGV4dCgpIGlmIHJhbmtfZWxlbWVudCBlbHNlIE5vbmVcXG4gICAgICAgICAgICBocmVmID0gYXdhaXQgdGl0bGVfZWxlbWVudC5nZXRfYXR0cmlidXRlKCdocmVmJykgaWYgdGl0bGVfZWxlbWVudCBlbHNlIE5vbmVcXG5cXG4gICAgICAgICAgICBkYXRhLmFwcGVuZCh7J3RpdGxlJzogdGl0bGUsICdyYW5rJzogcmFuaywgJ2hyZWYnOiBocmVmfSlcXG5cXG4gICAgICAgICMgUHVzaCB0aGUgZXh0cmFjdGVkIGRhdGEgdG8gdGhlIGRlZmF1bHQgZGF0YXNldC4gSW4gbG9jYWwgY29uZmlndXJhdGlvbixcXG4gICAgICAgICMgdGhlIGRhdGEgd2lsbCBiZSBzdG9yZWQgYXMgSlNPTiBmaWxlcyBpbiAuL3N0b3JhZ2UvZGF0YXNldHMvZGVmYXVsdC5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQucHVzaF9kYXRhKGRhdGEpXFxuXFxuICAgICAgICAjIEZpbmQgYSBsaW5rIHRvIHRoZSBuZXh0IHBhZ2UgYW5kIGVucXVldWUgaXQgaWYgaXQgZXhpc3RzLlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5lbnF1ZXVlX2xpbmtzKHNlbGVjdG9yPScubW9yZWxpbmsnKVxcblxcbiAgICAjIERlZmluZSBhIGhvb2sgdGhhdCB3aWxsIGJlIGNhbGxlZCBlYWNoIHRpbWUgYmVmb3JlIG5hdmlnYXRpbmcgdG8gYSBuZXcgVVJMLlxcbiAgICAjIFRoZSBob29rIHJlY2VpdmVzIGEgY29udGV4dCBwYXJhbWV0ZXIsIHByb3ZpZGluZyBhY2Nlc3MgdG8gdGhlIHJlcXVlc3QgYW5kXFxuICAgICMgYnJvd3NlciBwYWdlIGFtb25nIG90aGVyIHRoaW5ncy4gSW4gdGhpcyBleGFtcGxlLCB3ZSBsb2cgdGhlIFVSTCBiZWluZ1xcbiAgICAjIG5hdmlnYXRlZCB0by5cXG4gICAgQGNyYXdsZXIucHJlX25hdmlnYXRpb25faG9va1xcbiAgICBhc3luYyBkZWYgbG9nX25hdmlnYXRpb25fdXJsKGNvbnRleHQ6IFBsYXl3cmlnaHRQcmVOYXZDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnTmF2aWdhdGluZyB0byB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgIyBSdW4gdGhlIGNyYXdsZXIgd2l0aCB0aGUgaW5pdGlhbCBsaXN0IG9mIFVSTHMuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9uZXdzLnljb21iaW5hdG9yLmNvbS8nXSlcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6NDA5NiwidGltZW91dCI6MTgwfX0.lhGS4WRFs0jNazacHZQbEFy60YyvtMSagdz9fiogohw\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import (
    PlaywrightCrawler,
    PlaywrightCrawlingContext,
    PlaywrightPreNavCrawlingContext,
)


async def main() -> None:
    crawler = PlaywrightCrawler(
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
        # Headless mode, set to False to see the browser in action.
        headless=False,
        # Browser types supported by Playwright.
        browser_type='chromium',
    )

    # Define the default request handler, which will be called for every request.
    # The handler receives a context parameter, providing various properties and
    # helper methods. Here are a few key ones we use for demonstration:
    # - request: an instance of the Request class containing details such as the URL
    #   being crawled and the HTTP method used.
    # - page: Playwright's Page object, which allows interaction with the web page
    #   (see https://playwright.dev/python/docs/api/class-page for more details).
    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Extract data from the page using Playwright's API.
        posts = await context.page.query_selector_all('.athing')
        data = []

        for post in posts:
            # Get the HTML elements for the title and rank within each post.
            title_element = await post.query_selector('.title a')
            rank_element = await post.query_selector('.rank')

            # Extract the data we want from the elements.
            title = await title_element.inner_text() if title_element else None
            rank = await rank_element.inner_text() if rank_element else None
            href = await title_element.get_attribute('href') if title_element else None

            data.append({'title': title, 'rank': rank, 'href': href})

        # Push the extracted data to the default dataset. In local configuration,
        # the data will be stored as JSON files in ./storage/datasets/default.
        await context.push_data(data)

        # Find a link to the next page and enqueue it if it exists.
        await context.enqueue_links(selector='.morelink')

    # Define a hook that will be called each time before navigating to a new URL.
    # The hook receives a context parameter, providing access to the request and
    # browser page among other things. In this example, we log the URL being
    # navigated to.
    @crawler.pre_navigation_hook
    async def log_navigation_url(context: PlaywrightPreNavCrawlingContext) -> None:
        context.log.info(f'Navigating to {context.request.url} ...')

    # Run the crawler with the initial list of URLs.
    await crawler.run(['https://news.ycombinator.com/'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/examples/playwright_crawler.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/examples/parsel-crawler.md)

[Parsel crawler](https://crawlee.dev/python/python/docs/examples/parsel-crawler.md)

[Next](https://crawlee.dev/python/python/docs/examples/adaptive-playwright-crawler.md)

[Adaptive Playwright crawler](https://crawlee.dev/python/python/docs/examples/adaptive-playwright-crawler.md)


---

* [](https://crawlee.dev/python/python)
* [Examples](https://crawlee.dev/python/python/docs/examples.md)
* Playwright crawler with block requests

Version: 1.6

# Playwright crawler with block requests

This example demonstrates how to optimize your [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) performance by blocking unnecessary network requests.

The primary use case is when you need to scrape or interact with web pages without loading non-essential resources like images, styles, or analytics scripts. This can significantly reduce bandwidth usage and improve crawling speed.

The [`block_requests`](https://crawlee.dev/python/python/api/class/BlockRequestsFunction.md) helper provides the most efficient way to block requests as it operates directly in the browser.

By default, [`block_requests`](https://crawlee.dev/python/python/api/class/BlockRequestsFunction.md) will block all URLs including the following patterns:

```
['.css', '.webp', '.jpg', '.jpeg', '.png', '.svg', '.gif', '.woff', '.pdf', '.zip']
```

You can also replace the default patterns list with your own by providing `url_patterns`, or extend it by passing additional patterns in `extra_url_patterns`.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCAoXFxuICAgIFBsYXl3cmlnaHRDcmF3bGVyLFxcbiAgICBQbGF5d3JpZ2h0Q3Jhd2xpbmdDb250ZXh0LFxcbiAgICBQbGF5d3JpZ2h0UHJlTmF2Q3Jhd2xpbmdDb250ZXh0LFxcbilcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgIGNyYXdsZXIgPSBQbGF5d3JpZ2h0Q3Jhd2xlcihcXG4gICAgICAgICMgTGltaXQgdGhlIGNyYXdsIHRvIG1heCByZXF1ZXN0cy4gUmVtb3ZlIG9yIGluY3JlYXNlIGl0IGZvciBjcmF3bGluZyBhbGwgbGlua3MuXFxuICAgICAgICBtYXhfcmVxdWVzdHNfcGVyX2NyYXdsPTEwLFxcbiAgICApXFxuXFxuICAgICMgRGVmaW5lIHRoZSBkZWZhdWx0IHJlcXVlc3QgaGFuZGxlciwgd2hpY2ggd2lsbCBiZSBjYWxsZWQgZm9yIGV2ZXJ5IHJlcXVlc3QuXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIHJlcXVlc3RfaGFuZGxlcihjb250ZXh0OiBQbGF5d3JpZ2h0Q3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ1Byb2Nlc3Npbmcge2NvbnRleHQucmVxdWVzdC51cmx9IC4uLicpXFxuXFxuICAgICAgICBhd2FpdCBjb250ZXh0LmVucXVldWVfbGlua3MoKVxcblxcbiAgICAjIERlZmluZSB0aGUgaG9vaywgd2hpY2ggd2lsbCBiZSBjYWxsZWQgYmVmb3JlIGV2ZXJ5IHJlcXVlc3QuXFxuICAgIEBjcmF3bGVyLnByZV9uYXZpZ2F0aW9uX2hvb2tcXG4gICAgYXN5bmMgZGVmIG5hdmlnYXRpb25faG9vayhjb250ZXh0OiBQbGF5d3JpZ2h0UHJlTmF2Q3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ05hdmlnYXRpbmcgdG8ge2NvbnRleHQucmVxdWVzdC51cmx9IC4uLicpXFxuXFxuICAgICAgICAjIEJsb2NrIGFsbCByZXF1ZXN0cyB0byBVUkxzIHRoYXQgaW5jbHVkZSBgYWRzYnlnb29nbGUuanNgIGFuZCBhbHNvIGFsbCBkZWZhdWx0cy5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQuYmxvY2tfcmVxdWVzdHMoZXh0cmFfdXJsX3BhdHRlcm5zPVsnYWRzYnlnb29nbGUuanMnXSlcXG5cXG4gICAgIyBSdW4gdGhlIGNyYXdsZXIgd2l0aCB0aGUgaW5pdGlhbCBsaXN0IG9mIFVSTHMuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9jcmF3bGVlLmRldi8nXSlcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6NDA5NiwidGltZW91dCI6MTgwfX0.CKsXQcCAlJOQ_ywpkTeMezjLqt8YuKUqMN5KIBgEHno\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import (
    PlaywrightCrawler,
    PlaywrightCrawlingContext,
    PlaywrightPreNavCrawlingContext,
)


async def main() -> None:
    crawler = PlaywrightCrawler(
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
    )

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        await context.enqueue_links()

    # Define the hook, which will be called before every request.
    @crawler.pre_navigation_hook
    async def navigation_hook(context: PlaywrightPreNavCrawlingContext) -> None:
        context.log.info(f'Navigating to {context.request.url} ...')

        # Block all requests to URLs that include `adsbygoogle.js` and also all defaults.
        await context.block_requests(extra_url_patterns=['adsbygoogle.js'])

    # Run the crawler with the initial list of URLs.
    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/examples/playwright_crawler_with_block_requests.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/examples/adaptive-playwright-crawler.md)

[Adaptive Playwright crawler](https://crawlee.dev/python/python/docs/examples/adaptive-playwright-crawler.md)

[Next](https://crawlee.dev/python/python/docs/examples/playwright-crawler-with-camoufox.md)

[Playwright crawler with Camoufox](https://crawlee.dev/python/python/docs/examples/playwright-crawler-with-camoufox.md)


---

* [](https://crawlee.dev/python/python)
* [Examples](https://crawlee.dev/python/python/docs/examples.md)
* Playwright crawler with Camoufox

Version: 1.6

# Playwright crawler with Camoufox

This example demonstrates how to integrate Camoufox into [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) using [`BrowserPool`](https://crawlee.dev/python/python/api/class/BrowserPool.md) with custom [`PlaywrightBrowserPlugin`](https://crawlee.dev/python/python/api/class/PlaywrightBrowserPlugin.md).

Camoufox is a stealthy minimalistic build of Firefox. For details please visit its homepage <https://camoufox.com/> . To be able to run this example you will need to install camoufox, as it is external tool, and it is not part of the crawlee. For installation please see <https://pypi.org/project/camoufox/>.

**Warning!** Camoufox is using custom build of firefox. This build can be hundreds of MB large. You can either pre-download this file using following command `python3 -m camoufox fetch` or camoufox will download it automatically once you try to run it, and it does not find existing binary. For more details please refer to: <https://github.com/daijro/camoufox/tree/main/pythonlib#camoufox-python-interface>

**Project template -** It is possible to generate project with Python code which includes Camoufox integration into crawlee through crawlee cli. Call `crawlee create` and pick `Playwright-camoufox` when asked for Crawler type.

The example code after PlayWrightCrawler instantiation is similar to example describing the use of Playwright Crawler. The main difference is that in this example Camoufox will be used as the browser through BrowserPool.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuIyAgQ2Ftb3Vmb3ggaXMgZXh0ZXJuYWwgcGFja2FnZSBhbmQgbmVlZHMgdG8gYmUgaW5zdGFsbGVkLiBJdCBpcyBub3QgaW5jbHVkZWQgaW4gY3Jhd2xlZS5cXG5mcm9tIGNhbW91Zm94IGltcG9ydCBBc3luY05ld0Jyb3dzZXJcXG5mcm9tIHR5cGluZ19leHRlbnNpb25zIGltcG9ydCBvdmVycmlkZVxcblxcbmZyb20gY3Jhd2xlZS5icm93c2VycyBpbXBvcnQgKFxcbiAgICBCcm93c2VyUG9vbCxcXG4gICAgUGxheXdyaWdodEJyb3dzZXJDb250cm9sbGVyLFxcbiAgICBQbGF5d3JpZ2h0QnJvd3NlclBsdWdpbixcXG4pXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQbGF5d3JpZ2h0Q3Jhd2xlciwgUGxheXdyaWdodENyYXdsaW5nQ29udGV4dFxcblxcblxcbmNsYXNzIENhbW91Zm94UGx1Z2luKFBsYXl3cmlnaHRCcm93c2VyUGx1Z2luKTpcXG4gICAgXFxcIlxcXCJcXFwiRXhhbXBsZSBicm93c2VyIHBsdWdpbiB0aGF0IHVzZXMgQ2Ftb3Vmb3ggYnJvd3NlcixcXG4gICAgYnV0IG90aGVyd2lzZSBrZWVwcyB0aGUgZnVuY3Rpb25hbGl0eSBvZiBQbGF5d3JpZ2h0QnJvd3NlclBsdWdpbi5cXG4gICAgXFxcIlxcXCJcXFwiXFxuXFxuICAgIEBvdmVycmlkZVxcbiAgICBhc3luYyBkZWYgbmV3X2Jyb3dzZXIoc2VsZikgLT4gUGxheXdyaWdodEJyb3dzZXJDb250cm9sbGVyOlxcbiAgICAgICAgaWYgbm90IHNlbGYuX3BsYXl3cmlnaHQ6XFxuICAgICAgICAgICAgcmFpc2UgUnVudGltZUVycm9yKCdQbGF5d3JpZ2h0IGJyb3dzZXIgcGx1Z2luIGlzIG5vdCBpbml0aWFsaXplZC4nKVxcblxcbiAgICAgICAgcmV0dXJuIFBsYXl3cmlnaHRCcm93c2VyQ29udHJvbGxlcihcXG4gICAgICAgICAgICBicm93c2VyPWF3YWl0IEFzeW5jTmV3QnJvd3NlcihcXG4gICAgICAgICAgICAgICAgc2VsZi5fcGxheXdyaWdodCwgKipzZWxmLl9icm93c2VyX2xhdW5jaF9vcHRpb25zXFxuICAgICAgICAgICAgKSxcXG4gICAgICAgICAgICAjIEluY3JlYXNlLCBpZiBjYW1vdWZveCBjYW4gaGFuZGxlIGl0IGluIHlvdXIgdXNlIGNhc2UuXFxuICAgICAgICAgICAgbWF4X29wZW5fcGFnZXNfcGVyX2Jyb3dzZXI9MSxcXG4gICAgICAgICAgICAjIFRoaXMgdHVybnMgb2ZmIHRoZSBjcmF3bGVlIGhlYWRlcl9nZW5lcmF0aW9uLiBDYW1vdWZveCBoYXMgaXRzIG93bi5cXG4gICAgICAgICAgICBoZWFkZXJfZ2VuZXJhdG9yPU5vbmUsXFxuICAgICAgICApXFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICBjcmF3bGVyID0gUGxheXdyaWdodENyYXdsZXIoXFxuICAgICAgICAjIExpbWl0IHRoZSBjcmF3bCB0byBtYXggcmVxdWVzdHMuIFJlbW92ZSBvciBpbmNyZWFzZSBpdCBmb3IgY3Jhd2xpbmcgYWxsIGxpbmtzLlxcbiAgICAgICAgbWF4X3JlcXVlc3RzX3Blcl9jcmF3bD0xMCxcXG4gICAgICAgICMgQ3VzdG9tIGJyb3dzZXIgcG9vbC4gR2l2ZXMgdXNlcnMgZnVsbCBjb250cm9sIG92ZXIgYnJvd3NlcnMgdXNlZCBieSB0aGUgY3Jhd2xlci5cXG4gICAgICAgIGJyb3dzZXJfcG9vbD1Ccm93c2VyUG9vbChwbHVnaW5zPVtDYW1vdWZveFBsdWdpbigpXSksXFxuICAgIClcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IFBsYXl3cmlnaHRDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgICAgICMgRXh0cmFjdCBzb21lIGRhdGEgZnJvbSB0aGUgcGFnZSB1c2luZyBQbGF5d3JpZ2h0J3MgQVBJLlxcbiAgICAgICAgcG9zdHMgPSBhd2FpdCBjb250ZXh0LnBhZ2UucXVlcnlfc2VsZWN0b3JfYWxsKCcuYXRoaW5nJylcXG4gICAgICAgIGZvciBwb3N0IGluIHBvc3RzOlxcbiAgICAgICAgICAgICMgR2V0IHRoZSBIVE1MIGVsZW1lbnRzIGZvciB0aGUgdGl0bGUgYW5kIHJhbmsgd2l0aGluIGVhY2ggcG9zdC5cXG4gICAgICAgICAgICB0aXRsZV9lbGVtZW50ID0gYXdhaXQgcG9zdC5xdWVyeV9zZWxlY3RvcignLnRpdGxlIGEnKVxcblxcbiAgICAgICAgICAgICMgRXh0cmFjdCB0aGUgZGF0YSB3ZSB3YW50IGZyb20gdGhlIGVsZW1lbnRzLlxcbiAgICAgICAgICAgIHRpdGxlID0gYXdhaXQgdGl0bGVfZWxlbWVudC5pbm5lcl90ZXh0KCkgaWYgdGl0bGVfZWxlbWVudCBlbHNlIE5vbmVcXG5cXG4gICAgICAgICMgUHVzaCB0aGUgZXh0cmFjdGVkIGRhdGEgdG8gdGhlIGRlZmF1bHQgZGF0YXNldC5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQucHVzaF9kYXRhKHsndGl0bGUnOiB0aXRsZX0pXFxuXFxuICAgICAgICAjIEZpbmQgYSBsaW5rIHRvIHRoZSBuZXh0IHBhZ2UgYW5kIGVucXVldWUgaXQgaWYgaXQgZXhpc3RzLlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5lbnF1ZXVlX2xpbmtzKHNlbGVjdG9yPScubW9yZWxpbmsnKVxcblxcbiAgICAjIFJ1biB0aGUgY3Jhd2xlciB3aXRoIHRoZSBpbml0aWFsIGxpc3Qgb2YgVVJMcy5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL25ld3MueWNvbWJpbmF0b3IuY29tLyddKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5Ijo0MDk2LCJ0aW1lb3V0IjoxODB9fQ.IpSt8pQLubDAKoVAkMIBaz6XzoSbWmH4j0qch-1QoVQ\&asrc=run_on_apify)

```
import asyncio

#  Camoufox is external package and needs to be installed. It is not included in crawlee.
from camoufox import AsyncNewBrowser
from typing_extensions import override

from crawlee.browsers import (
    BrowserPool,
    PlaywrightBrowserController,
    PlaywrightBrowserPlugin,
)
from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext


class CamoufoxPlugin(PlaywrightBrowserPlugin):
    """Example browser plugin that uses Camoufox browser,
    but otherwise keeps the functionality of PlaywrightBrowserPlugin.
    """

    @override
    async def new_browser(self) -> PlaywrightBrowserController:
        if not self._playwright:
            raise RuntimeError('Playwright browser plugin is not initialized.')

        return PlaywrightBrowserController(
            browser=await AsyncNewBrowser(
                self._playwright, **self._browser_launch_options
            ),
            # Increase, if camoufox can handle it in your use case.
            max_open_pages_per_browser=1,
            # This turns off the crawlee header_generation. Camoufox has its own.
            header_generator=None,
        )


async def main() -> None:
    crawler = PlaywrightCrawler(
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
        # Custom browser pool. Gives users full control over browsers used by the crawler.
        browser_pool=BrowserPool(plugins=[CamoufoxPlugin()]),
    )

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Extract some data from the page using Playwright's API.
        posts = await context.page.query_selector_all('.athing')
        for post in posts:
            # Get the HTML elements for the title and rank within each post.
            title_element = await post.query_selector('.title a')

            # Extract the data we want from the elements.
            title = await title_element.inner_text() if title_element else None

        # Push the extracted data to the default dataset.
        await context.push_data({'title': title})

        # Find a link to the next page and enqueue it if it exists.
        await context.enqueue_links(selector='.morelink')

    # Run the crawler with the initial list of URLs.
    await crawler.run(['https://news.ycombinator.com/'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/examples/playwright_crawler_with_camoufox.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/examples/playwright-crawler-with-block-requests.md)

[Playwright crawler with block requests](https://crawlee.dev/python/python/docs/examples/playwright-crawler-with-block-requests.md)

[Next](https://crawlee.dev/python/python/docs/examples/playwright-crawler-with-fingerprint-generator.md)

[Playwright crawler with fingerprint generator](https://crawlee.dev/python/python/docs/examples/playwright-crawler-with-fingerprint-generator.md)


---

* [](https://crawlee.dev/python/python)
* [Examples](https://crawlee.dev/python/python/docs/examples.md)
* Playwright crawler with fingerprint generator

Version: 1.6

# Playwright crawler with fingerprint generator

This example demonstrates how to use [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) together with [`FingerprintGenerator`](https://crawlee.dev/python/python/api/class/FingerprintGenerator.md) that will populate several browser attributes to mimic real browser fingerprint. To read more about fingerprints please see: <https://docs.apify.com/academy/anti-scraping/techniques/fingerprinting>.

You can implement your own fingerprint generator or use [`DefaultFingerprintGenerator`](https://crawlee.dev/python/python/api/class/BrowserforgeFingerprintGenerator.md). To use the generator initialize it with the desired fingerprint options. The generator will try to create fingerprint based on those options. Unspecified options will be automatically selected by the generator from the set of reasonable values. If some option is important for you, do not rely on the default and explicitly define it.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQbGF5d3JpZ2h0Q3Jhd2xlciwgUGxheXdyaWdodENyYXdsaW5nQ29udGV4dFxcbmZyb20gY3Jhd2xlZS5maW5nZXJwcmludF9zdWl0ZSBpbXBvcnQgKFxcbiAgICBEZWZhdWx0RmluZ2VycHJpbnRHZW5lcmF0b3IsXFxuICAgIEhlYWRlckdlbmVyYXRvck9wdGlvbnMsXFxuICAgIFNjcmVlbk9wdGlvbnMsXFxuKVxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBVc2UgZGVmYXVsdCBmaW5nZXJwcmludCBnZW5lcmF0b3Igd2l0aCBkZXNpcmVkIGZpbmdlcnByaW50IG9wdGlvbnMuXFxuICAgICMgR2VuZXJhdG9yIHdpbGwgZ2VuZXJhdGUgcmVhbCBsb29raW5nIGJyb3dzZXIgZmluZ2VycHJpbnQgYmFzZWQgb24gdGhlIG9wdGlvbnMuXFxuICAgICMgVW5zcGVjaWZpZWQgZmluZ2VycHJpbnQgb3B0aW9ucyB3aWxsIGJlIGF1dG9tYXRpY2FsbHkgc2VsZWN0ZWQgYnkgdGhlIGdlbmVyYXRvci5cXG4gICAgZmluZ2VycHJpbnRfZ2VuZXJhdG9yID0gRGVmYXVsdEZpbmdlcnByaW50R2VuZXJhdG9yKFxcbiAgICAgICAgaGVhZGVyX29wdGlvbnM9SGVhZGVyR2VuZXJhdG9yT3B0aW9ucyhicm93c2Vycz1bJ2Nocm9tZSddKSxcXG4gICAgICAgIHNjcmVlbl9vcHRpb25zPVNjcmVlbk9wdGlvbnMobWluX3dpZHRoPTQwMCksXFxuICAgIClcXG5cXG4gICAgY3Jhd2xlciA9IFBsYXl3cmlnaHRDcmF3bGVyKFxcbiAgICAgICAgIyBMaW1pdCB0aGUgY3Jhd2wgdG8gbWF4IHJlcXVlc3RzLiBSZW1vdmUgb3IgaW5jcmVhc2UgaXQgZm9yIGNyYXdsaW5nIGFsbCBsaW5rcy5cXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsXFxuICAgICAgICAjIEhlYWRsZXNzIG1vZGUsIHNldCB0byBGYWxzZSB0byBzZWUgdGhlIGJyb3dzZXIgaW4gYWN0aW9uLlxcbiAgICAgICAgaGVhZGxlc3M9RmFsc2UsXFxuICAgICAgICAjIEJyb3dzZXIgdHlwZXMgc3VwcG9ydGVkIGJ5IFBsYXl3cmlnaHQuXFxuICAgICAgICBicm93c2VyX3R5cGU9J2Nocm9taXVtJyxcXG4gICAgICAgICMgRmluZ2VycHJpbnQgZ2VuZXJhdG9yIHRvIGJlIHVzZWQuIEJ5IGRlZmF1bHQgbm8gZmluZ2VycHJpbnQgZ2VuZXJhdGlvbiBpcyBkb25lLlxcbiAgICAgICAgZmluZ2VycHJpbnRfZ2VuZXJhdG9yPWZpbmdlcnByaW50X2dlbmVyYXRvcixcXG4gICAgKVxcblxcbiAgICAjIERlZmluZSB0aGUgZGVmYXVsdCByZXF1ZXN0IGhhbmRsZXIsIHdoaWNoIHdpbGwgYmUgY2FsbGVkIGZvciBldmVyeSByZXF1ZXN0LlxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiByZXF1ZXN0X2hhbmRsZXIoY29udGV4dDogUGxheXdyaWdodENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm9jZXNzaW5nIHtjb250ZXh0LnJlcXVlc3QudXJsfSAuLi4nKVxcblxcbiAgICAgICAgIyBGaW5kIGEgbGluayB0byB0aGUgbmV4dCBwYWdlIGFuZCBlbnF1ZXVlIGl0IGlmIGl0IGV4aXN0cy5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQuZW5xdWV1ZV9saW5rcyhzZWxlY3Rvcj0nLm1vcmVsaW5rJylcXG5cXG4gICAgIyBSdW4gdGhlIGNyYXdsZXIgd2l0aCB0aGUgaW5pdGlhbCBsaXN0IG9mIFVSTHMuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9uZXdzLnljb21iaW5hdG9yLmNvbS8nXSlcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6NDA5NiwidGltZW91dCI6MTgwfX0.zJE_8Pww2ACjYwEywrwkU0p3QVafLSpjWeywiotNVfc\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext
from crawlee.fingerprint_suite import (
    DefaultFingerprintGenerator,
    HeaderGeneratorOptions,
    ScreenOptions,
)


async def main() -> None:
    # Use default fingerprint generator with desired fingerprint options.
    # Generator will generate real looking browser fingerprint based on the options.
    # Unspecified fingerprint options will be automatically selected by the generator.
    fingerprint_generator = DefaultFingerprintGenerator(
        header_options=HeaderGeneratorOptions(browsers=['chrome']),
        screen_options=ScreenOptions(min_width=400),
    )

    crawler = PlaywrightCrawler(
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
        # Headless mode, set to False to see the browser in action.
        headless=False,
        # Browser types supported by Playwright.
        browser_type='chromium',
        # Fingerprint generator to be used. By default no fingerprint generation is done.
        fingerprint_generator=fingerprint_generator,
    )

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Find a link to the next page and enqueue it if it exists.
        await context.enqueue_links(selector='.morelink')

    # Run the crawler with the initial list of URLs.
    await crawler.run(['https://news.ycombinator.com/'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/examples/playwright_crawler_with_fingerprint_generator.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/examples/playwright-crawler-with-camoufox.md)

[Playwright crawler with Camoufox](https://crawlee.dev/python/python/docs/examples/playwright-crawler-with-camoufox.md)

[Next](https://crawlee.dev/python/python/docs/examples/respect-robots-txt-file.md)

[Respect robots.txt file](https://crawlee.dev/python/python/docs/examples/respect-robots-txt-file.md)


---

* [](https://crawlee.dev/python/python)
* [Examples](https://crawlee.dev/python/python/docs/examples.md)
* Respect robots.txt file

Version: 1.6

On this page

# Respect robots.txt file

This example demonstrates how to configure your crawler to respect the rules established by websites for crawlers as described in the [robots.txt](https://www.robotstxt.org/robotstxt.html) file.

To configure `Crawlee` to follow the `robots.txt` file, set the parameter `respect_robots_txt_file=True` in [`BasicCrawlerOptions`](https://crawlee.dev/python/python/api/class/BasicCrawlerOptions.md). In this case, `Crawlee` will skip any URLs forbidden in the website's robots.txt file.

As an example, let's look at the website `https://news.ycombinator.com/` and its corresponding [robots.txt](https://news.ycombinator.com/robots.txt) file. Since the file has a rule `Disallow: /login`, the URL `https://news.ycombinator.com/login` will be automatically skipped.

The code below demonstrates this behavior using the [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md):

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCAoXFxuICAgIEJlYXV0aWZ1bFNvdXBDcmF3bGVyLFxcbiAgICBCZWF1dGlmdWxTb3VwQ3Jhd2xpbmdDb250ZXh0LFxcbilcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgICMgSW5pdGlhbGl6ZSB0aGUgY3Jhd2xlciB3aXRoIHJvYm90cy50eHQgY29tcGxpYW5jZSBlbmFibGVkXFxuICAgIGNyYXdsZXIgPSBCZWF1dGlmdWxTb3VwQ3Jhd2xlcihyZXNwZWN0X3JvYm90c190eHRfZmlsZT1UcnVlKVxcblxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiByZXF1ZXN0X2hhbmRsZXIoY29udGV4dDogQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm9jZXNzaW5nIHtjb250ZXh0LnJlcXVlc3QudXJsfSAuLi4nKVxcblxcbiAgICAjIFN0YXJ0IHRoZSBjcmF3bGVyIHdpdGggdGhlIHNwZWNpZmllZCBVUkxzXFxuICAgICMgVGhlIGNyYXdsZXIgd2lsbCBjaGVjayB0aGUgcm9ib3RzLnR4dCBmaWxlIGJlZm9yZSBtYWtpbmcgcmVxdWVzdHNcXG4gICAgIyBJbiB0aGlzIGV4YW1wbGUsICdodHRwczovL25ld3MueWNvbWJpbmF0b3IuY29tL2xvZ2luJyB3aWxsIGJlIHNraXBwZWRcXG4gICAgIyBiZWNhdXNlIGl0J3MgZGlzYWxsb3dlZCBpbiB0aGUgc2l0ZSdzIHJvYm90cy50eHQgZmlsZVxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihcXG4gICAgICAgIFsnaHR0cHM6Ly9uZXdzLnljb21iaW5hdG9yLmNvbS8nLCAnaHR0cHM6Ly9uZXdzLnljb21iaW5hdG9yLmNvbS9sb2dpbiddXFxuICAgIClcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6MTAyNCwidGltZW91dCI6MTgwfX0.1uePyGZCkXb73mkFKoMamjA1SNoN-OZd2J_klycLes4\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import (
    BeautifulSoupCrawler,
    BeautifulSoupCrawlingContext,
)


async def main() -> None:
    # Initialize the crawler with robots.txt compliance enabled
    crawler = BeautifulSoupCrawler(respect_robots_txt_file=True)

    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

    # Start the crawler with the specified URLs
    # The crawler will check the robots.txt file before making requests
    # In this example, 'https://news.ycombinator.com/login' will be skipped
    # because it's disallowed in the site's robots.txt file
    await crawler.run(
        ['https://news.ycombinator.com/', 'https://news.ycombinator.com/login']
    )


if __name__ == '__main__':
    asyncio.run(main())
```

## Handle with `on_skipped_request`[​](#handle-with-on_skipped_request "Direct link to handle-with-on_skipped_request")

If you want to process URLs skipped according to the `robots.txt` rules, for example for further analysis, you should use the `on_skipped_request` handler from [`BasicCrawler`](https://crawlee.dev/python/python/api/class/BasicCrawler.md#on_skipped_request).

Let's update the code by adding the `on_skipped_request` handler:

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBTa2lwcGVkUmVhc29uXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCAoXFxuICAgIEJlYXV0aWZ1bFNvdXBDcmF3bGVyLFxcbiAgICBCZWF1dGlmdWxTb3VwQ3Jhd2xpbmdDb250ZXh0LFxcbilcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgICMgSW5pdGlhbGl6ZSB0aGUgY3Jhd2xlciB3aXRoIHJvYm90cy50eHQgY29tcGxpYW5jZSBlbmFibGVkXFxuICAgIGNyYXdsZXIgPSBCZWF1dGlmdWxTb3VwQ3Jhd2xlcihyZXNwZWN0X3JvYm90c190eHRfZmlsZT1UcnVlKVxcblxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiByZXF1ZXN0X2hhbmRsZXIoY29udGV4dDogQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm9jZXNzaW5nIHtjb250ZXh0LnJlcXVlc3QudXJsfSAuLi4nKVxcblxcbiAgICAjIGhpZ2hsaWdodC1zdGFydFxcbiAgICAjIFRoaXMgaGFuZGxlciBpcyBjYWxsZWQgd2hlbiBhIHJlcXVlc3QgaXMgc2tpcHBlZFxcbiAgICBAY3Jhd2xlci5vbl9za2lwcGVkX3JlcXVlc3RcXG4gICAgYXN5bmMgZGVmIHNraXBwZWRfcmVxdWVzdF9oYW5kbGVyKHVybDogc3RyLCByZWFzb246IFNraXBwZWRSZWFzb24pIC0-IE5vbmU6XFxuICAgICAgICAjIENoZWNrIGlmIHRoZSByZXF1ZXN0IHdhcyBza2lwcGVkIGR1ZSB0byByb2JvdHMudHh0IHJ1bGVzXFxuICAgICAgICBpZiByZWFzb24gPT0gJ3JvYm90c190eHQnOlxcbiAgICAgICAgICAgIGNyYXdsZXIubG9nLmluZm8oZidTa2lwcGVkIHt1cmx9IGR1ZSB0byByb2JvdHMudHh0IHJ1bGVzLicpXFxuXFxuICAgICMgaGlnaGxpZ2h0LWVuZFxcblxcbiAgICAjIFN0YXJ0IHRoZSBjcmF3bGVyIHdpdGggdGhlIHNwZWNpZmllZCBVUkxzXFxuICAgICMgVGhlIGxvZ2luIFVSTCB3aWxsIGJlIHNraXBwZWQgYW5kIGhhbmRsZWQgYnkgdGhlIHNraXBwZWRfcmVxdWVzdF9oYW5kbGVyXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFxcbiAgICAgICAgWydodHRwczovL25ld3MueWNvbWJpbmF0b3IuY29tLycsICdodHRwczovL25ld3MueWNvbWJpbmF0b3IuY29tL2xvZ2luJ11cXG4gICAgKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.EugqJDmBmQMc4s9k8nFP43q_YBbWZjB2195iyoyosHA\&asrc=run_on_apify)

```
import asyncio

from crawlee import SkippedReason
from crawlee.crawlers import (
    BeautifulSoupCrawler,
    BeautifulSoupCrawlingContext,
)


async def main() -> None:
    # Initialize the crawler with robots.txt compliance enabled
    crawler = BeautifulSoupCrawler(respect_robots_txt_file=True)

    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

    # This handler is called when a request is skipped
    @crawler.on_skipped_request
    async def skipped_request_handler(url: str, reason: SkippedReason) -> None:
        # Check if the request was skipped due to robots.txt rules
        if reason == 'robots_txt':
            crawler.log.info(f'Skipped {url} due to robots.txt rules.')


    # Start the crawler with the specified URLs
    # The login URL will be skipped and handled by the skipped_request_handler
    await crawler.run(
        ['https://news.ycombinator.com/', 'https://news.ycombinator.com/login']
    )


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/examples/respect_robots_txt_file.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/examples/playwright-crawler-with-fingerprint-generator.md)

[Playwright crawler with fingerprint generator](https://crawlee.dev/python/python/docs/examples/playwright-crawler-with-fingerprint-generator.md)

[Next](https://crawlee.dev/python/python/docs/examples/resuming-paused-crawl.md)

[Resuming a paused crawl](https://crawlee.dev/python/python/docs/examples/resuming-paused-crawl.md)


---

* [](https://crawlee.dev/python/python)
* [Examples](https://crawlee.dev/python/python/docs/examples.md)
* Resuming a paused crawl

Version: 1.6

# Resuming a paused crawl

This example demonstrates how to resume crawling from its last state when running locally, if for some reason it was unexpectedly terminated.

If each run should continue crawling from the previous state, you can configure this using `purge_on_start` in [`Configuration`](https://crawlee.dev/python/python/api/class/Configuration.md).

Use the code below and perform 2 sequential runs. During the 1st run, stop the crawler by pressing `CTRL+C`, and the 2nd run will resume crawling from where it stopped.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBDb25jdXJyZW5jeVNldHRpbmdzLCBzZXJ2aWNlX2xvY2F0b3JcXG5mcm9tIGNyYXdsZWUuY3Jhd2xlcnMgaW1wb3J0IChcXG4gICAgQmVhdXRpZnVsU291cENyYXdsZXIsXFxuICAgIEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQsXFxuKVxcblxcbiMgRGlzYWJsZSBjbGVhcmluZyB0aGUgYFJlcXVlc3RRdWV1ZWAsIGBLZXlWYWx1ZVN0b3JlYCBhbmQgYERhdGFzZXRgIG9uIGVhY2ggcnVuLlxcbiMgVGhpcyBtYWtlcyB0aGUgc2NyYXBlciBjb250aW51ZSBmcm9tIHdoZXJlIGl0IGxlZnQgb2ZmIGluIHRoZSBwcmV2aW91cyBydW4uXFxuIyBUaGUgcmVjb21tZW5kZWQgd2F5IHRvIGFjaGlldmUgdGhpcyBiZWhhdmlvciBpcyBzZXR0aW5nIHRoZSBlbnZpcm9ubWVudCB2YXJpYWJsZVxcbiMgYENSQVdMRUVfUFVSR0VfT05fU1RBUlQ9MGBcXG5jb25maWd1cmF0aW9uID0gc2VydmljZV9sb2NhdG9yLmdldF9jb25maWd1cmF0aW9uKClcXG5jb25maWd1cmF0aW9uLnB1cmdlX29uX3N0YXJ0ID0gRmFsc2VcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgIGNyYXdsZXIgPSBCZWF1dGlmdWxTb3VwQ3Jhd2xlcihcXG4gICAgICAgICMgTGV0J3Mgc2xvdyBkb3duIHRoZSBjcmF3bGVyIGZvciBhIGRlbW9uc3RyYXRpb25cXG4gICAgICAgIGNvbmN1cnJlbmN5X3NldHRpbmdzPUNvbmN1cnJlbmN5U2V0dGluZ3MobWF4X3Rhc2tzX3Blcl9taW51dGU9MjApXFxuICAgIClcXG5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgIyBMaXN0IG9mIGxpbmtzIGZvciBjcmF3bFxcbiAgICByZXF1ZXN0cyA9IFtcXG4gICAgICAgICdodHRwczovL2NyYXdsZWUuZGV2JyxcXG4gICAgICAgICdodHRwczovL2NyYXdsZWUuZGV2L3B5dGhvbi9kb2NzJyxcXG4gICAgICAgICdodHRwczovL2NyYXdsZWUuZGV2L3B5dGhvbi9kb2NzL2V4YW1wbGVzJyxcXG4gICAgICAgICdodHRwczovL2NyYXdsZWUuZGV2L3B5dGhvbi9kb2NzL2d1aWRlcycsXFxuICAgICAgICAnaHR0cHM6Ly9jcmF3bGVlLmRldi9weXRob24vZG9jcy9xdWljay1zdGFydCcsXFxuICAgIF1cXG5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4ocmVxdWVzdHMpXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.qT0OyhtLbncYQurKrVjYo58aqxnRlmCLugt_FXT-uOM\&asrc=run_on_apify)

```
import asyncio

from crawlee import ConcurrencySettings, service_locator
from crawlee.crawlers import (
    BeautifulSoupCrawler,
    BeautifulSoupCrawlingContext,
)

# Disable clearing the `RequestQueue`, `KeyValueStore` and `Dataset` on each run.
# This makes the scraper continue from where it left off in the previous run.
# The recommended way to achieve this behavior is setting the environment variable
# `CRAWLEE_PURGE_ON_START=0`
configuration = service_locator.get_configuration()
configuration.purge_on_start = False


async def main() -> None:
    crawler = BeautifulSoupCrawler(
        # Let's slow down the crawler for a demonstration
        concurrency_settings=ConcurrencySettings(max_tasks_per_minute=20)
    )

    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

    # List of links for crawl
    requests = [
        'https://crawlee.dev',
        'https://crawlee.dev/python/docs',
        'https://crawlee.dev/python/docs/examples',
        'https://crawlee.dev/python/docs/guides',
        'https://crawlee.dev/python/docs/quick-start',
    ]

    await crawler.run(requests)


if __name__ == '__main__':
    asyncio.run(main())
```

Perform the 1st run, interrupting the crawler with `CTRL+C` after 2 links have been processed.

![Run with interruption](/python/assets/images/00-026ac2f973e1b772177cbab7c1b351e6.webp "Run with interruption.")

Now resume crawling after the pause to process the remaining 3 links.

![Resuming crawling](/python/assets/images/01-73269978a845fb83cf14febb18bfb531.webp "Resuming crawling.")

Alternatively, use the environment variable `CRAWLEE_PURGE_ON_START=0` instead of using `configuration.purge_on_start = False`.

For example, when running code:

```
CRAWLEE_PURGE_ON_START=0 python -m best_crawler
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/examples/resuming_paused_crawl.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/examples/respect-robots-txt-file.md)

[Respect robots.txt file](https://crawlee.dev/python/python/docs/examples/respect-robots-txt-file.md)

[Next](https://crawlee.dev/python/python/docs/examples/run-parallel-crawlers.md)

[Run parallel crawlers](https://crawlee.dev/python/python/docs/examples/run-parallel-crawlers.md)


---

* [](https://crawlee.dev/python/python)
* [Examples](https://crawlee.dev/python/python/docs/examples.md)
* Run parallel crawlers

Version: 1.6

# Run parallel crawlers

This example demonstrates how to run two parallel crawlers where one crawler processes links discovered by another crawler.

In some situations, you may need different approaches for scraping data from a website. For example, you might use [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) for navigating JavaScript-heavy pages and a faster, more lightweight [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md) for processing static pages. One way to solve this is to use [`AdaptivePlaywrightCrawler`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md), see the [Adaptive Playwright crawler example](https://crawlee.dev/python/python/docs/examples/adaptive-playwright-crawler.md) to learn more.

The code below demonstrates an alternative approach using two separate crawlers. Links are passed between crawlers via [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md) aliases. The `keep_alive` option allows the Playwright crawler to run in the background and wait for incoming links without stopping when its queue is empty. You can also use different storage clients for each crawler without losing the ability to pass links between queues. Learn more about available storage clients in this [guide](https://crawlee.dev/python/python/docs/guides/storage-clients.md).

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBDb25jdXJyZW5jeVNldHRpbmdzXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCAoXFxuICAgIFBhcnNlbENyYXdsZXIsXFxuICAgIFBhcnNlbENyYXdsaW5nQ29udGV4dCxcXG4gICAgUGxheXdyaWdodENyYXdsZXIsXFxuICAgIFBsYXl3cmlnaHRDcmF3bGluZ0NvbnRleHQsXFxuKVxcbmZyb20gY3Jhd2xlZS5zZXNzaW9ucyBpbXBvcnQgU2Vzc2lvblBvb2xcXG5mcm9tIGNyYXdsZWUuc3RvcmFnZXMgaW1wb3J0IFJlcXVlc3RRdWV1ZVxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBPcGVuIHJlcXVlc3QgcXVldWVzIGZvciBib3RoIGNyYXdsZXJzIHdpdGggZGlmZmVyZW50IGFsaWFzZXNcXG4gICAgcGxheXdyaWdodF9ycSA9IGF3YWl0IFJlcXVlc3RRdWV1ZS5vcGVuKGFsaWFzPSdwbGF5d3JpZ2h0LXJlcXVlc3RzJylcXG4gICAgcGFyc2VsX3JxID0gYXdhaXQgUmVxdWVzdFF1ZXVlLm9wZW4oYWxpYXM9J3BhcnNlbC1yZXF1ZXN0cycpXFxuXFxuICAgICMgVXNlIGEgc2hhcmVkIHNlc3Npb24gcG9vbCBiZXR3ZWVuIGJvdGggY3Jhd2xlcnNcXG4gICAgYXN5bmMgd2l0aCBTZXNzaW9uUG9vbCgpIGFzIHNlc3Npb25fcG9vbDpcXG4gICAgICAgIHBsYXl3cmlnaHRfY3Jhd2xlciA9IFBsYXl3cmlnaHRDcmF3bGVyKFxcbiAgICAgICAgICAgICMgU2V0IHRoZSByZXF1ZXN0IHF1ZXVlIGZvciBQbGF5d3JpZ2h0IGNyYXdsZXJcXG4gICAgICAgICAgICByZXF1ZXN0X21hbmFnZXI9cGxheXdyaWdodF9ycSxcXG4gICAgICAgICAgICBzZXNzaW9uX3Bvb2w9c2Vzc2lvbl9wb29sLFxcbiAgICAgICAgICAgICMgQ29uZmlndXJlIGNvbmN1cnJlbmN5IHNldHRpbmdzIGZvciBQbGF5d3JpZ2h0IGNyYXdsZXJcXG4gICAgICAgICAgICBjb25jdXJyZW5jeV9zZXR0aW5ncz1Db25jdXJyZW5jeVNldHRpbmdzKFxcbiAgICAgICAgICAgICAgICBtYXhfY29uY3VycmVuY3k9NSwgZGVzaXJlZF9jb25jdXJyZW5jeT01XFxuICAgICAgICAgICAgKSxcXG4gICAgICAgICAgICAjIFNldCBga2VlcF9hbGl2ZWBgIHNvIHRoYXQgdGhlIGNyYXdsZXIgZG9lcyBub3Qgc3RvcCB3b3JraW5nIHdoZW4gdGhlcmUgYXJlXFxuICAgICAgICAgICAgIyBubyByZXF1ZXN0cyBpbiB0aGUgcXVldWUuXFxuICAgICAgICAgICAga2VlcF9hbGl2ZT1UcnVlLFxcbiAgICAgICAgKVxcblxcbiAgICAgICAgcGFyc2VsX2NyYXdsZXIgPSBQYXJzZWxDcmF3bGVyKFxcbiAgICAgICAgICAgICMgU2V0IHRoZSByZXF1ZXN0IHF1ZXVlIGZvciBQYXJzZWwgY3Jhd2xlclxcbiAgICAgICAgICAgIHJlcXVlc3RfbWFuYWdlcj1wYXJzZWxfcnEsXFxuICAgICAgICAgICAgc2Vzc2lvbl9wb29sPXNlc3Npb25fcG9vbCxcXG4gICAgICAgICAgICAjIENvbmZpZ3VyZSBjb25jdXJyZW5jeSBzZXR0aW5ncyBmb3IgUGFyc2VsIGNyYXdsZXJcXG4gICAgICAgICAgICBjb25jdXJyZW5jeV9zZXR0aW5ncz1Db25jdXJyZW5jeVNldHRpbmdzKFxcbiAgICAgICAgICAgICAgICBtYXhfY29uY3VycmVuY3k9MTAsIGRlc2lyZWRfY29uY3VycmVuY3k9MTBcXG4gICAgICAgICAgICApLFxcbiAgICAgICAgICAgICMgU2V0IG1heGltdW0gcmVxdWVzdHMgcGVyIGNyYXdsIGZvciBQYXJzZWwgY3Jhd2xlclxcbiAgICAgICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9NTAsXFxuICAgICAgICApXFxuXFxuICAgICAgICBAcGxheXdyaWdodF9jcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgICAgIGFzeW5jIGRlZiBoYW5kbGVfcGxheXdyaWdodChjb250ZXh0OiBQbGF5d3JpZ2h0Q3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQbGF5d3JpZ2h0IFByb2Nlc3Npbmcge2NvbnRleHQucmVxdWVzdC51cmx9Li4uJylcXG5cXG4gICAgICAgICAgICB0aXRsZSA9IGF3YWl0IGNvbnRleHQucGFnZS50aXRsZSgpXFxuICAgICAgICAgICAgIyBQdXNoIHRoZSBleHRyYWN0ZWQgZGF0YSB0byB0aGUgZGF0YXNldCBmb3IgUGxheXdyaWdodCBjcmF3bGVyXFxuICAgICAgICAgICAgYXdhaXQgY29udGV4dC5wdXNoX2RhdGEoXFxuICAgICAgICAgICAgICAgIHsndGl0bGUnOiB0aXRsZSwgJ3VybCc6IGNvbnRleHQucmVxdWVzdC51cmwsICdzb3VyY2UnOiAncGxheXdyaWdodCd9LFxcbiAgICAgICAgICAgICAgICBkYXRhc2V0X25hbWU9J3BsYXl3cmlnaHQtZGF0YScsXFxuICAgICAgICAgICAgKVxcblxcbiAgICAgICAgQHBhcnNlbF9jcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgICAgIGFzeW5jIGRlZiBoYW5kbGVfcGFyc2VsKGNvbnRleHQ6IFBhcnNlbENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUGFyc2VsIFByb2Nlc3Npbmcge2NvbnRleHQucmVxdWVzdC51cmx9Li4uJylcXG5cXG4gICAgICAgICAgICB0aXRsZSA9IGNvbnRleHQucGFyc2VkX2NvbnRlbnQuY3NzKCd0aXRsZTo6dGV4dCcpLmdldCgpXFxuICAgICAgICAgICAgIyBQdXNoIHRoZSBleHRyYWN0ZWQgZGF0YSB0byB0aGUgZGF0YXNldCBmb3IgUGFyc2VsIGNyYXdsZXJcXG4gICAgICAgICAgICBhd2FpdCBjb250ZXh0LnB1c2hfZGF0YShcXG4gICAgICAgICAgICAgICAgeyd0aXRsZSc6IHRpdGxlLCAndXJsJzogY29udGV4dC5yZXF1ZXN0LnVybCwgJ3NvdXJjZSc6ICdwYXJzZWwnfSxcXG4gICAgICAgICAgICAgICAgZGF0YXNldF9uYW1lPSdwYXJzZWwtZGF0YScsXFxuICAgICAgICAgICAgKVxcblxcbiAgICAgICAgICAgICMgRW5xdWV1ZSBsaW5rcyB0byB0aGUgUGxheXdyaWdodCByZXF1ZXN0IHF1ZXVlIGZvciBibG9nIHBhZ2VzXFxuICAgICAgICAgICAgYXdhaXQgY29udGV4dC5lbnF1ZXVlX2xpbmtzKFxcbiAgICAgICAgICAgICAgICBzZWxlY3Rvcj0nYVtocmVmKj1cXFwiL2Jsb2cvXFxcIl0nLCBycV9hbGlhcz0ncGxheXdyaWdodC1yZXF1ZXN0cydcXG4gICAgICAgICAgICApXFxuICAgICAgICAgICAgIyBFbnF1ZXVlIG90aGVyIGxpbmtzIHRvIHRoZSBQYXJzZWwgcmVxdWVzdCBxdWV1ZVxcbiAgICAgICAgICAgIGF3YWl0IGNvbnRleHQuZW5xdWV1ZV9saW5rcyhzZWxlY3Rvcj0nYTpub3QoW2hyZWYqPVxcXCIvYmxvZy9cXFwiXSknKVxcblxcbiAgICAgICAgIyBTdGFydCB0aGUgUGxheXdyaWdodCBjcmF3bGVyIGluIHRoZSBiYWNrZ3JvdW5kXFxuICAgICAgICBiYWNrZ3JvdW5kX2NyYXdsZXJfdGFzayA9IGFzeW5jaW8uY3JlYXRlX3Rhc2socGxheXdyaWdodF9jcmF3bGVyLnJ1bihbXSkpXFxuXFxuICAgICAgICAjIFJ1biB0aGUgUGFyc2VsIGNyYXdsZXIgd2l0aCB0aGUgaW5pdGlhbCBVUkwgYW5kIHdhaXQgZm9yIGl0IHRvIGZpbmlzaFxcbiAgICAgICAgYXdhaXQgcGFyc2VsX2NyYXdsZXIucnVuKFsnaHR0cHM6Ly9jcmF3bGVlLmRldi9ibG9nJ10pXFxuXFxuICAgICAgICAjIFdhaXQgZm9yIHRoZSBQbGF5d3JpZ2h0IGNyYXdsZXIgdG8gZmluaXNoIHByb2Nlc3NpbmcgYWxsIHJlcXVlc3RzXFxuICAgICAgICB3aGlsZSBub3QgYXdhaXQgcGxheXdyaWdodF9ycS5pc19lbXB0eSgpOlxcbiAgICAgICAgICAgIHBsYXl3cmlnaHRfY3Jhd2xlci5sb2cuaW5mbygnV2FpdGluZyBmb3IgUGxheXdyaWdodCBjcmF3bGVyIHRvIGZpbmlzaC4uLicpXFxuICAgICAgICAgICAgYXdhaXQgYXN5bmNpby5zbGVlcCg1KVxcblxcbiAgICAgICAgIyBTdG9wIHRoZSBQbGF5d3JpZ2h0IGNyYXdsZXIgYWZ0ZXIgYWxsIHJlcXVlc3RzIGFyZSBwcm9jZXNzZWRcXG4gICAgICAgIHBsYXl3cmlnaHRfY3Jhd2xlci5zdG9wKClcXG5cXG4gICAgICAgICMgV2FpdCBmb3IgdGhlIGJhY2tncm91bmQgUGxheXdyaWdodCBjcmF3bGVyIHRhc2sgdG8gY29tcGxldGVcXG4gICAgICAgIGF3YWl0IGJhY2tncm91bmRfY3Jhd2xlcl90YXNrXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjQwOTYsInRpbWVvdXQiOjE4MH19.Uwn7tNUen2DEIGth8dOi9LphEXTnJDRLlRi-VyYIcfQ\&asrc=run_on_apify)

```
import asyncio

from crawlee import ConcurrencySettings
from crawlee.crawlers import (
    ParselCrawler,
    ParselCrawlingContext,
    PlaywrightCrawler,
    PlaywrightCrawlingContext,
)
from crawlee.sessions import SessionPool
from crawlee.storages import RequestQueue


async def main() -> None:
    # Open request queues for both crawlers with different aliases
    playwright_rq = await RequestQueue.open(alias='playwright-requests')
    parsel_rq = await RequestQueue.open(alias='parsel-requests')

    # Use a shared session pool between both crawlers
    async with SessionPool() as session_pool:
        playwright_crawler = PlaywrightCrawler(
            # Set the request queue for Playwright crawler
            request_manager=playwright_rq,
            session_pool=session_pool,
            # Configure concurrency settings for Playwright crawler
            concurrency_settings=ConcurrencySettings(
                max_concurrency=5, desired_concurrency=5
            ),
            # Set `keep_alive`` so that the crawler does not stop working when there are
            # no requests in the queue.
            keep_alive=True,
        )

        parsel_crawler = ParselCrawler(
            # Set the request queue for Parsel crawler
            request_manager=parsel_rq,
            session_pool=session_pool,
            # Configure concurrency settings for Parsel crawler
            concurrency_settings=ConcurrencySettings(
                max_concurrency=10, desired_concurrency=10
            ),
            # Set maximum requests per crawl for Parsel crawler
            max_requests_per_crawl=50,
        )

        @playwright_crawler.router.default_handler
        async def handle_playwright(context: PlaywrightCrawlingContext) -> None:
            context.log.info(f'Playwright Processing {context.request.url}...')

            title = await context.page.title()
            # Push the extracted data to the dataset for Playwright crawler
            await context.push_data(
                {'title': title, 'url': context.request.url, 'source': 'playwright'},
                dataset_name='playwright-data',
            )

        @parsel_crawler.router.default_handler
        async def handle_parsel(context: ParselCrawlingContext) -> None:
            context.log.info(f'Parsel Processing {context.request.url}...')

            title = context.parsed_content.css('title::text').get()
            # Push the extracted data to the dataset for Parsel crawler
            await context.push_data(
                {'title': title, 'url': context.request.url, 'source': 'parsel'},
                dataset_name='parsel-data',
            )

            # Enqueue links to the Playwright request queue for blog pages
            await context.enqueue_links(
                selector='a[href*="/blog/"]', rq_alias='playwright-requests'
            )
            # Enqueue other links to the Parsel request queue
            await context.enqueue_links(selector='a:not([href*="/blog/"])')

        # Start the Playwright crawler in the background
        background_crawler_task = asyncio.create_task(playwright_crawler.run([]))

        # Run the Parsel crawler with the initial URL and wait for it to finish
        await parsel_crawler.run(['https://crawlee.dev/blog'])

        # Wait for the Playwright crawler to finish processing all requests
        while not await playwright_rq.is_empty():
            playwright_crawler.log.info('Waiting for Playwright crawler to finish...')
            await asyncio.sleep(5)

        # Stop the Playwright crawler after all requests are processed
        playwright_crawler.stop()

        # Wait for the background Playwright crawler task to complete
        await background_crawler_task


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/examples/run_parallel_crawlers.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/examples/resuming-paused-crawl.md)

[Resuming a paused crawl](https://crawlee.dev/python/python/docs/examples/resuming-paused-crawl.md)

[Next](https://crawlee.dev/python/python/docs/examples/using_browser_profile.md)

[Using browser profile](https://crawlee.dev/python/python/docs/examples/using_browser_profile.md)


---

* [](https://crawlee.dev/python/python)
* [Examples](https://crawlee.dev/python/python/docs/examples.md)
* Using browser profile

Version: 1.6

On this page

# Using browser profile

This example demonstrates how to run [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) using your local browser profile from [Chrome](https://www.google.com/intl/us/chrome/) or [Firefox](https://www.firefox.com/).

Using browser profiles allows you to leverage existing login sessions, saved passwords, bookmarks, and other personalized browser data during crawling. This can be particularly useful for testing scenarios or when you need to access content that requires authentication.

## Chrome browser[​](#chrome-browser "Direct link to Chrome browser")

To run [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) with your Chrome profile, you need to know the path to your profile files. You can find this information by entering `chrome://version/` as a URL in your Chrome browser. If you have multiple profiles, pay attention to the profile name - if you only have one profile, it's always `Default`.

Profile access limitation

Due to [Chrome's security policies](https://developer.chrome.com/blog/remote-debugging-port), automation cannot use your main browsing profile directly. The example copies your profile to a temporary location as a workaround.

Make sure you don't have any running Chrome browser processes before running this code:

```
import asyncio
import shutil
from pathlib import Path
from tempfile import TemporaryDirectory

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext

# Profile name to use (usually 'Default' for single profile setups)
PROFILE_NAME = 'Default'

# Paths to Chrome profiles in your system (example for Windows)
# Use `chrome://version/` to find your profile path
PROFILE_PATH = Path(Path.home(), 'AppData', 'Local', 'Google', 'Chrome', 'User Data')


async def main() -> None:
    # Create a temporary folder to copy the profile to
    with TemporaryDirectory(prefix='crawlee-') as tmpdirname:
        tmp_profile_dir = Path(tmpdirname)

        # Copy the profile to a temporary folder
        shutil.copytree(
            PROFILE_PATH / PROFILE_NAME,
            tmp_profile_dir / PROFILE_NAME,
            dirs_exist_ok=True,
        )

        crawler = PlaywrightCrawler(
            headless=False,
            # Use the installed Chrome browser
            browser_type='chrome',
            # Disable fingerprints to preserve profile identity
            fingerprint_generator=None,
            # Set user data directory to temp folder
            user_data_dir=tmp_profile_dir,
            browser_launch_options={
                # Slow down actions to mimic human behavior
                'slow_mo': 200,
                'args': [
                    # Use the specified profile
                    f'--profile-directory={PROFILE_NAME}',
                ],
            },
        )

        @crawler.router.default_handler
        async def default_handler(context: PlaywrightCrawlingContext) -> None:
            context.log.info(f'Visiting {context.request.url}')

        await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

## Firefox browser[​](#firefox-browser "Direct link to Firefox browser")

To find the path to your Firefox profile, enter `about:profiles` as a URL in your Firefox browser. Unlike Chrome, you can use your standard profile path directly without copying it first.

Make sure you don't have any running Firefox browser processes before running this code:

```
import asyncio
from pathlib import Path

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext

# Replace this with your actual Firefox profile name
# Find it at about:profiles in Firefox
PROFILE_NAME = 'your-profile-name-here'

# Paths to Firefox profiles in your system (example for Windows)
# Use `about:profiles` to find your profile path
PROFILE_PATH = Path(
    Path.home(), 'AppData', 'Roaming', 'Mozilla', 'Firefox', 'Profiles', PROFILE_NAME
)


async def main() -> None:
    crawler = PlaywrightCrawler(
        # Use Firefox browser type
        browser_type='firefox',
        # Disable fingerprints to use the profile as is
        fingerprint_generator=None,
        headless=False,
        # Path to your Firefox profile
        user_data_dir=PROFILE_PATH,
        browser_launch_options={
            'args': [
                # Required to avoid version conflicts
                '--allow-downgrade'
            ]
        },
    )

    @crawler.router.default_handler
    async def default_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Visiting {context.request.url}')

    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/examples/using_browser_profile.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/examples/run-parallel-crawlers.md)

[Run parallel crawlers](https://crawlee.dev/python/python/docs/examples/run-parallel-crawlers.md)

[Next](https://crawlee.dev/python/python/docs/examples/using-sitemap-request-loader.md)

[Using sitemap request loader](https://crawlee.dev/python/python/docs/examples/using-sitemap-request-loader.md)


---

* [](https://crawlee.dev/python/python)
* [Examples](https://crawlee.dev/python/python/docs/examples.md)
* Using sitemap request loader

Version: 1.6

# Using sitemap request loader

This example demonstrates how to use [`SitemapRequestLoader`](https://crawlee.dev/python/python/api/class/SitemapRequestLoader.md) to crawl websites that provide `sitemap.xml` files following the [Sitemaps protocol](https://www.sitemaps.org/protocol.html). The [`SitemapRequestLoader`](https://crawlee.dev/python/python/api/class/SitemapRequestLoader.md) processes sitemaps in a streaming fashion without loading them entirely into memory, making it suitable for large sitemaps.

The example shows how to use the `transform_request_function` parameter to configure request options based on URL patterns. This allows you to modify request properties such as labels and user data based on the source URL, enabling different handling logic for different websites or sections.

The following code example implements processing of sitemaps from two different domains (Apify and Crawlee), with different labels assigned to requests based on their host. The `create_transform_request` function maps each host to the corresponding request configuration, while the crawler uses different handlers based on the assigned labels.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuZnJvbSBjb2xsZWN0aW9ucy5hYmMgaW1wb3J0IENhbGxhYmxlXFxuXFxuZnJvbSB5YXJsIGltcG9ydCBVUkxcXG5cXG5mcm9tIGNyYXdsZWUgaW1wb3J0IFJlcXVlc3RPcHRpb25zLCBSZXF1ZXN0VHJhbnNmb3JtQWN0aW9uXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcbmZyb20gY3Jhd2xlZS5odHRwX2NsaWVudHMgaW1wb3J0IEltcGl0SHR0cENsaWVudFxcbmZyb20gY3Jhd2xlZS5yZXF1ZXN0X2xvYWRlcnMgaW1wb3J0IFNpdGVtYXBSZXF1ZXN0TG9hZGVyXFxuXFxuXFxuIyBDcmVhdGUgYSB0cmFuc2Zvcm1fcmVxdWVzdF9mdW5jdGlvbiB0aGF0IG1hcHMgcmVxdWVzdCBvcHRpb25zIGJhc2VkIG9uIHRoZSBob3N0IGluXFxuIyB0aGUgVVJMXFxuZGVmIGNyZWF0ZV90cmFuc2Zvcm1fcmVxdWVzdChcXG4gICAgZGF0YV9tYXBwZXI6IGRpY3Rbc3RyLCBkaWN0XSxcXG4pIC0-IENhbGxhYmxlW1tSZXF1ZXN0T3B0aW9uc10sIFJlcXVlc3RPcHRpb25zIHwgUmVxdWVzdFRyYW5zZm9ybUFjdGlvbl06XFxuICAgIGRlZiB0cmFuc2Zvcm1fcmVxdWVzdChcXG4gICAgICAgIHJlcXVlc3Rfb3B0aW9uczogUmVxdWVzdE9wdGlvbnMsXFxuICAgICkgLT4gUmVxdWVzdE9wdGlvbnMgfCBSZXF1ZXN0VHJhbnNmb3JtQWN0aW9uOlxcbiAgICAgICAgIyBBY2NvcmRpbmcgdG8gdGhlIFNpdGVtYXAgcHJvdG9jb2wsIGFsbCBVUkxzIGluIGEgU2l0ZW1hcCBtdXN0IGJlIGZyb20gYSBzaW5nbGVcXG4gICAgICAgICMgaG9zdC5cXG4gICAgICAgIHJlcXVlc3RfaG9zdCA9IFVSTChyZXF1ZXN0X29wdGlvbnNbJ3VybCddKS5ob3N0XFxuXFxuICAgICAgICBpZiByZXF1ZXN0X2hvc3QgYW5kIChtYXBwaW5nX2RhdGEgOj0gZGF0YV9tYXBwZXIuZ2V0KHJlcXVlc3RfaG9zdCkpOlxcbiAgICAgICAgICAgICMgU2V0IHByb3BlcnRpZXMgZnJvbSB0aGUgbWFwcGluZyBkYXRhXFxuICAgICAgICAgICAgaWYgJ2xhYmVsJyBpbiBtYXBwaW5nX2RhdGE6XFxuICAgICAgICAgICAgICAgIHJlcXVlc3Rfb3B0aW9uc1snbGFiZWwnXSA9IG1hcHBpbmdfZGF0YVsnbGFiZWwnXVxcbiAgICAgICAgICAgIGlmICd1c2VyX2RhdGEnIGluIG1hcHBpbmdfZGF0YTpcXG4gICAgICAgICAgICAgICAgcmVxdWVzdF9vcHRpb25zWyd1c2VyX2RhdGEnXSA9IG1hcHBpbmdfZGF0YVsndXNlcl9kYXRhJ11cXG5cXG4gICAgICAgICAgICByZXR1cm4gcmVxdWVzdF9vcHRpb25zXFxuXFxuICAgICAgICByZXR1cm4gJ3VuY2hhbmdlZCdcXG5cXG4gICAgcmV0dXJuIHRyYW5zZm9ybV9yZXF1ZXN0XFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICAjIFByZXBhcmUgZGF0YSBtYXBwaW5nIGZvciBob3N0c1xcbiAgICBhcGlmeV9ob3N0ID0gVVJMKCdodHRwczovL2FwaWZ5LmNvbS9zaXRlbWFwLnhtbCcpLmhvc3RcXG4gICAgY3Jhd2xlZV9ob3N0ID0gVVJMKCdodHRwczovL2NyYXdsZWUuZGV2L3NpdGVtYXAueG1sJykuaG9zdFxcblxcbiAgICBpZiBub3QgYXBpZnlfaG9zdCBvciBub3QgY3Jhd2xlZV9ob3N0OlxcbiAgICAgICAgcmFpc2UgVmFsdWVFcnJvcignVW5hYmxlIHRvIGV4dHJhY3QgaG9zdCBmcm9tIFVSTHMnKVxcblxcbiAgICBkYXRhX21hcCA9IHtcXG4gICAgICAgIGFwaWZ5X2hvc3Q6IHtcXG4gICAgICAgICAgICAnbGFiZWwnOiAnYXBpZnknLFxcbiAgICAgICAgICAgICd1c2VyX2RhdGEnOiB7J3NvdXJjZSc6ICdhcGlmeSd9LFxcbiAgICAgICAgfSxcXG4gICAgICAgIGNyYXdsZWVfaG9zdDoge1xcbiAgICAgICAgICAgICdsYWJlbCc6ICdjcmF3bGVlJyxcXG4gICAgICAgICAgICAndXNlcl9kYXRhJzogeydzb3VyY2UnOiAnY3Jhd2xlZSd9LFxcbiAgICAgICAgfSxcXG4gICAgfVxcblxcbiAgICAjIEluaXRpYWxpemUgdGhlIFNpdGVtYXBSZXF1ZXN0TG9hZGVyIHdpdGggdGhlIHRyYW5zZm9ybSBmdW5jdGlvblxcbiAgICBhc3luYyB3aXRoIFNpdGVtYXBSZXF1ZXN0TG9hZGVyKFxcbiAgICAgICAgIyBTZXQgdGhlIHNpdGVtYXAgVVJMcyBhbmQgdGhlIEhUVFAgY2xpZW50XFxuICAgICAgICBzaXRlbWFwX3VybHM9WydodHRwczovL2NyYXdsZWUuZGV2L3NpdGVtYXAueG1sJywgJ2h0dHBzOi8vYXBpZnkuY29tL3NpdGVtYXAueG1sJ10sXFxuICAgICAgICBodHRwX2NsaWVudD1JbXBpdEh0dHBDbGllbnQoKSxcXG4gICAgICAgIHRyYW5zZm9ybV9yZXF1ZXN0X2Z1bmN0aW9uPWNyZWF0ZV90cmFuc2Zvcm1fcmVxdWVzdChkYXRhX21hcCksXFxuICAgICkgYXMgc2l0ZW1hcF9sb2FkZXI6XFxuICAgICAgICAjIENvbnZlcnQgdGhlIHNpdGVtYXAgbG9hZGVyIHRvIGEgcmVxdWVzdCBtYW5hZ2VyXFxuICAgICAgICByZXF1ZXN0X21hbmFnZXIgPSBhd2FpdCBzaXRlbWFwX2xvYWRlci50b190YW5kZW0oKVxcblxcbiAgICAgICAgIyBDcmVhdGUgYW5kIGNvbmZpZ3VyZSB0aGUgY3Jhd2xlclxcbiAgICAgICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKFxcbiAgICAgICAgICAgIHJlcXVlc3RfbWFuYWdlcj1yZXF1ZXN0X21hbmFnZXIsXFxuICAgICAgICAgICAgbWF4X3JlcXVlc3RzX3Blcl9jcmF3bD0xMCxcXG4gICAgICAgIClcXG5cXG4gICAgICAgICMgQ3JlYXRlIGRlZmF1bHQgaGFuZGxlciBmb3IgcmVxdWVzdHMgd2l0aG91dCBhIHNwZWNpZmljIGxhYmVsXFxuICAgICAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgICAgICBhc3luYyBkZWYgaGFuZGxlcihjb250ZXh0OiBCZWF1dGlmdWxTb3VwQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgICAgIHNvdXJjZSA9IGNvbnRleHQucmVxdWVzdC51c2VyX2RhdGEuZ2V0KCdzb3VyY2UnLCAndW5rbm93bicpXFxuICAgICAgICAgICAgY29udGV4dC5sb2cuaW5mbyhcXG4gICAgICAgICAgICAgICAgZidQcm9jZXNzaW5nIHJlcXVlc3Q6IHtjb250ZXh0LnJlcXVlc3QudXJsfSBmcm9tIHNvdXJjZToge3NvdXJjZX0nXFxuICAgICAgICAgICAgKVxcblxcbiAgICAgICAgIyBDcmVhdGUgaGFuZGxlciBmb3IgcmVxdWVzdHMgbGFiZWxlZCAnYXBpZnknXFxuICAgICAgICBAY3Jhd2xlci5yb3V0ZXIuaGFuZGxlcignYXBpZnknKVxcbiAgICAgICAgYXN5bmMgZGVmIGFwaWZ5X2hhbmRsZXIoY29udGV4dDogQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgICAgICBzb3VyY2UgPSBjb250ZXh0LnJlcXVlc3QudXNlcl9kYXRhLmdldCgnc291cmNlJywgJ3Vua25vd24nKVxcbiAgICAgICAgICAgIGNvbnRleHQubG9nLmluZm8oXFxuICAgICAgICAgICAgICAgIGYnQXBpZnkgaGFuZGxlciBwcm9jZXNzaW5nOiB7Y29udGV4dC5yZXF1ZXN0LnVybH0gZnJvbSBzb3VyY2U6IHtzb3VyY2V9J1xcbiAgICAgICAgICAgIClcXG5cXG4gICAgICAgICMgQ3JlYXRlIGhhbmRsZXIgZm9yIHJlcXVlc3RzIGxhYmVsZWQgJ2NyYXdsZWUnXFxuICAgICAgICBAY3Jhd2xlci5yb3V0ZXIuaGFuZGxlcignY3Jhd2xlZScpXFxuICAgICAgICBhc3luYyBkZWYgY3Jhd2xlZV9oYW5kbGVyKGNvbnRleHQ6IEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICAgICAgc291cmNlID0gY29udGV4dC5yZXF1ZXN0LnVzZXJfZGF0YS5nZXQoJ3NvdXJjZScsICd1bmtub3duJylcXG4gICAgICAgICAgICBjb250ZXh0LmxvZy5pbmZvKFxcbiAgICAgICAgICAgICAgICBmJ0NyYXdsZWUgaGFuZGxlciBwcm9jZXNzaW5nOiB7Y29udGV4dC5yZXF1ZXN0LnVybH0gZnJvbSBzb3VyY2U6IHtzb3VyY2V9J1xcbiAgICAgICAgICAgIClcXG5cXG4gICAgICAgIGF3YWl0IGNyYXdsZXIucnVuKClcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6MTAyNCwidGltZW91dCI6MTgwfX0.fd57eoRz5yIfUVlazTPgZwjQ5qvpngJkik1dtsCofyE\&asrc=run_on_apify)

```
import asyncio
from collections.abc import Callable

from yarl import URL

from crawlee import RequestOptions, RequestTransformAction
from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext
from crawlee.http_clients import ImpitHttpClient
from crawlee.request_loaders import SitemapRequestLoader


# Create a transform_request_function that maps request options based on the host in
# the URL
def create_transform_request(
    data_mapper: dict[str, dict],
) -> Callable[[RequestOptions], RequestOptions | RequestTransformAction]:
    def transform_request(
        request_options: RequestOptions,
    ) -> RequestOptions | RequestTransformAction:
        # According to the Sitemap protocol, all URLs in a Sitemap must be from a single
        # host.
        request_host = URL(request_options['url']).host

        if request_host and (mapping_data := data_mapper.get(request_host)):
            # Set properties from the mapping data
            if 'label' in mapping_data:
                request_options['label'] = mapping_data['label']
            if 'user_data' in mapping_data:
                request_options['user_data'] = mapping_data['user_data']

            return request_options

        return 'unchanged'

    return transform_request


async def main() -> None:
    # Prepare data mapping for hosts
    apify_host = URL('https://apify.com/sitemap.xml').host
    crawlee_host = URL('https://crawlee.dev/sitemap.xml').host

    if not apify_host or not crawlee_host:
        raise ValueError('Unable to extract host from URLs')

    data_map = {
        apify_host: {
            'label': 'apify',
            'user_data': {'source': 'apify'},
        },
        crawlee_host: {
            'label': 'crawlee',
            'user_data': {'source': 'crawlee'},
        },
    }

    # Initialize the SitemapRequestLoader with the transform function
    async with SitemapRequestLoader(
        # Set the sitemap URLs and the HTTP client
        sitemap_urls=['https://crawlee.dev/sitemap.xml', 'https://apify.com/sitemap.xml'],
        http_client=ImpitHttpClient(),
        transform_request_function=create_transform_request(data_map),
    ) as sitemap_loader:
        # Convert the sitemap loader to a request manager
        request_manager = await sitemap_loader.to_tandem()

        # Create and configure the crawler
        crawler = BeautifulSoupCrawler(
            request_manager=request_manager,
            max_requests_per_crawl=10,
        )

        # Create default handler for requests without a specific label
        @crawler.router.default_handler
        async def handler(context: BeautifulSoupCrawlingContext) -> None:
            source = context.request.user_data.get('source', 'unknown')
            context.log.info(
                f'Processing request: {context.request.url} from source: {source}'
            )

        # Create handler for requests labeled 'apify'
        @crawler.router.handler('apify')
        async def apify_handler(context: BeautifulSoupCrawlingContext) -> None:
            source = context.request.user_data.get('source', 'unknown')
            context.log.info(
                f'Apify handler processing: {context.request.url} from source: {source}'
            )

        # Create handler for requests labeled 'crawlee'
        @crawler.router.handler('crawlee')
        async def crawlee_handler(context: BeautifulSoupCrawlingContext) -> None:
            source = context.request.user_data.get('source', 'unknown')
            context.log.info(
                f'Crawlee handler processing: {context.request.url} from source: {source}'
            )

        await crawler.run()


if __name__ == '__main__':
    asyncio.run(main())
```

For more information about request loaders, see the [Request loaders guide](https://crawlee.dev/python/python/docs/guides/request-loaders.md).

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/examples/using_sitemap_request_loader.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/examples/using_browser_profile.md)

[Using browser profile](https://crawlee.dev/python/python/docs/examples/using_browser_profile.md)

[Next](https://crawlee.dev/python/python/docs/upgrading.md)

[Upgrading](https://crawlee.dev/python/python/docs/upgrading.md)


---

## [📄️<!-- --> <!-- -->Architecture overview](https://crawlee.dev/python/python/docs/guides/architecture-overview.md)

[An overview of the core components of the Crawlee library and its architecture.](https://crawlee.dev/python/python/docs/guides/architecture-overview.md)


---

* [](https://crawlee.dev/python/python)
* [Guides](https://crawlee.dev/python/python/docs/guides.md)
* Adaptive Playwright crawler

Version: 1.6

On this page

