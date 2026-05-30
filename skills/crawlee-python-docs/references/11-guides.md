# Adaptive Playwright crawler

An [`AdaptivePlaywrightCrawler`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md) is a combination of [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) and some implementation of HTTP-based crawler such as [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md) or [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md). It uses a more limited crawling context interface so that it is able to switch to HTTP-only crawling when it detects that it may bring a performance benefit.

Detection is done based on the [`RenderingTypePredictor`](https://crawlee.dev/python/python/api/class/RenderingTypePredictor.md) with default implementation [`DefaultRenderingTypePredictor`](https://crawlee.dev/python/python/api/class/DefaultRenderingTypePredictor.md). It predicts which crawling method should be used and learns from already crawled pages.

## When to use AdaptivePlaywrightCrawler[​](#when-to-use-adaptiveplaywrightcrawler "Direct link to When to use AdaptivePlaywrightCrawler")

Use [`AdaptivePlaywrightCrawler`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md) in scenarios where some target pages have to be crawled with [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md), but for others faster HTTP-based crawler is sufficient. This way, you can achieve lower costs when crawling multiple different websites.

Another use case is performing selector-based data extraction without prior knowledge of whether the selector exists in the static page or is dynamically added by a code executed in a browsing client.

## Request handler and adaptive context helpers[​](#request-handler-and-adaptive-context-helpers "Direct link to Request handler and adaptive context helpers")

Request handler for [`AdaptivePlaywrightCrawler`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md) works on special context type - [`AdaptivePlaywrightCrawlingContext`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md). This context is sometimes created by HTTP-based sub crawler and sometimes by playwright based sub crawler. Due to its dynamic nature, you can't always access [page](https://playwright.dev/python/docs/api/class-page) object. To overcome this limitation, there are three helper methods on this context that can be called regardless of how the context was created.

[`wait_for_selector`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#wait_for_selector) accepts `css` selector as first argument and timeout as second argument. The function will try to locate this selector a return once it is found(within timeout). In practice this means that if HTTP-based sub crawler was used, the function will find the selector only if it is part of the static content. If not, the adaptive crawler will fall back to the playwright sub crawler and will wait try to locate the selector within the timeout using playwright.

[`query_selector_one`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#query_selector_one) accepts `css` selector as first argument and timeout as second argument. This function acts similar to `wait_for_selector`, but it also returns one selector if any selector is found. Return value type is determined by used HTTP-based sub crawler. For example, it will be `Selector` for [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md) and `Tag` for [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md).

[`query_selector_all`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#query_selector_one) same as [`query_selector_one`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#query_selector_one), but returns all found selectors.

[`parse_with_static_parser`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#parse_with_static_parser) will re-parse the whole page. Return value type is determined by used HTTP-based sub crawler. It has optional arguments: `selector` and `timeout`. If those optional arguments are used then the function first calls [`wait_for_selector`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md#wait_for_selector) and then do the parsing. This can be used in scenario where some specific element can signal, that page is already complete.

See the following example about how to create request handler and use context helpers:

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuZnJvbSBkYXRldGltZSBpbXBvcnQgdGltZWRlbHRhXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBBZGFwdGl2ZVBsYXl3cmlnaHRDcmF3bGVyLCBBZGFwdGl2ZVBsYXl3cmlnaHRDcmF3bGluZ0NvbnRleHRcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgIGNyYXdsZXIgPSBBZGFwdGl2ZVBsYXl3cmlnaHRDcmF3bGVyLndpdGhfcGFyc2VsX3N0YXRpY19wYXJzZXIoKVxcblxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiByZXF1ZXN0X2hhbmRsZXIoY29udGV4dDogQWRhcHRpdmVQbGF5d3JpZ2h0Q3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgIyBMb2NhdGUgZWxlbWVudCBoMiB3aXRoaW4gNSBzZWNvbmRzXFxuICAgICAgICBoMiA9IGF3YWl0IGNvbnRleHQucXVlcnlfc2VsZWN0b3Jfb25lKCdoMicsIHRpbWVkZWx0YShtaWxsaXNlY29uZHM9NTAwMCkpXFxuICAgICAgICAjIERvIHN0dWZmIHdpdGggZWxlbWVudCBmb3VuZCBieSB0aGUgc2VsZWN0b3JcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oaDIpXFxuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9jcmF3bGVlLmRldi8nXSlcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6NDA5NiwidGltZW91dCI6MTgwfX0.pQ36ymKNrMVLfJbxTLIrpPyETkmHd0JQQf8oM10mu3s\&asrc=run_on_apify)

```
import asyncio
from datetime import timedelta

from crawlee.crawlers import AdaptivePlaywrightCrawler, AdaptivePlaywrightCrawlingContext


async def main() -> None:
    crawler = AdaptivePlaywrightCrawler.with_parsel_static_parser()

    @crawler.router.default_handler
    async def request_handler(context: AdaptivePlaywrightCrawlingContext) -> None:
        # Locate element h2 within 5 seconds
        h2 = await context.query_selector_one('h2', timedelta(milliseconds=5000))
        # Do stuff with element found by the selector
        context.log.info(h2)

    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

## Crawler configuration[​](#crawler-configuration "Direct link to Crawler configuration")

To use [`AdaptivePlaywrightCrawler`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md) it is recommended to use one of the prepared factory methods that will create the crawler with specific HTTP-based sub crawler variant: [`AdaptivePlaywrightCrawler.with_beautifulsoup_static_parser`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#with_beautifulsoup_static_parser) or [`AdaptivePlaywrightCrawler.with_parsel_static_parser`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#with_parsel_static_parser).

[`AdaptivePlaywrightCrawler`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md) is internally composed of two sub crawlers and you can do a detailed configuration of both of them. For detailed configuration options of the sub crawlers, please refer to their pages: [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md), [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md), [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md).

In the following example you can see how to create and configure [`AdaptivePlaywrightCrawler`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md) with two different HTTP-based sub crawlers:

* BeautifulSoupCrawler
* ParselCrawler

```
import asyncio

from crawlee.crawlers import AdaptivePlaywrightCrawler


async def main() -> None:
    crawler = AdaptivePlaywrightCrawler.with_beautifulsoup_static_parser(
        # Arguments relevant only for PlaywrightCrawler
        playwright_crawler_specific_kwargs={
            'headless': False,
            'browser_type': 'chromium',
        },
        # Common arguments relevant to all crawlers
        max_crawl_depth=5,
    )

    # ...


if __name__ == '__main__':
    asyncio.run(main())
```

```
import asyncio

from crawlee.crawlers import AdaptivePlaywrightCrawler


async def main() -> None:
    crawler = AdaptivePlaywrightCrawler.with_parsel_static_parser(
        # Arguments relevant only for PlaywrightCrawler
        playwright_crawler_specific_kwargs={
            'headless': False,
            'browser_type': 'chromium',
        },
        # Common arguments relevant to all crawlers
        max_crawl_depth=5,
    )

    # ...


if __name__ == '__main__':
    asyncio.run(main())
```

### Prediction related arguments[​](#prediction-related-arguments "Direct link to Prediction related arguments")

To control which pages are crawled by which method you can use following arguments:

[`RenderingTypePredictor`](https://crawlee.dev/python/python/api/class/RenderingTypePredictor.md) - Class that can give recommendations about which sub crawler should be used for specific url. Predictor will also recommend to use both sub crawlers for some page from time to time, to check that the given recommendation was correct. Predictor should be able to learn from previous results and gradually give more reliable recommendations.

`result_checker` - Is a function that checks result created from crawling a page. By default, it always returns `True`.

`result_comparator` - Is a function that compares two results (HTTP-based sub crawler result and playwright based sub crawler result) and returns `True` if they are considered the same. By default, this function compares calls of context helper `push_data` by each sub crawler. This function is used by `rendering_type_predictor` to evaluate whether HTTP-based crawler has the same results as playwright based sub crawler.

See the following example about how to pass prediction related arguments:

```
import asyncio

from crawlee import Request
from crawlee._types import RequestHandlerRunResult
from crawlee.crawlers import (
    AdaptivePlaywrightCrawler,
    RenderingType,
    RenderingTypePrediction,
    RenderingTypePredictor,
)


class CustomRenderingTypePredictor(RenderingTypePredictor):
    def __init__(self) -> None:
        super().__init__()

        self._learning_data = list[tuple[Request, RenderingType]]()

    def predict(self, request: Request) -> RenderingTypePrediction:
        # Some custom logic that produces some `RenderingTypePrediction`
        # based on the `request` input.
        rendering_type: RenderingType = (
            'static' if 'abc' in request.url else 'client only'
        )

        return RenderingTypePrediction(
            #  Recommends `static` rendering type -> HTTP-based sub crawler will be used.
            rendering_type=rendering_type,
            # Recommends that both sub crawlers should run with 20% chance. When both sub
            # crawlers are running, the predictor can compare results and learn.
            # High number means that predictor is not very confident about the
            # `rendering_type`, low number means that predictor is very confident.
            detection_probability_recommendation=0.2,
        )

    def store_result(self, request: Request, rendering_type: RenderingType) -> None:
        # This function allows predictor to store new learning data and retrain itself
        # if needed. `request` is input for prediction and `rendering_type` is the correct
        # prediction.
        self._learning_data.append((request, rendering_type))
        # retrain


def result_checker(result: RequestHandlerRunResult) -> bool:
    # Some function that inspects produced `result` and returns `True` if the result
    # is correct.
    return bool(result)  # Check something on result


def result_comparator(
    result_1: RequestHandlerRunResult, result_2: RequestHandlerRunResult
) -> bool:
    # Some function that inspects two results and returns `True` if they are
    # considered equivalent. It is used when comparing results produced by HTTP-based
    # sub crawler and playwright based sub crawler.
    return (
        result_1.push_data_calls == result_2.push_data_calls
    )  #  For example compare `push_data` calls.


async def main() -> None:
    crawler = AdaptivePlaywrightCrawler.with_parsel_static_parser(
        rendering_type_predictor=CustomRenderingTypePredictor(),
        result_checker=result_checker,
        result_comparator=result_comparator,
    )

    # ...


if __name__ == '__main__':
    asyncio.run(main())
```

## Page configuration with pre-navigation hooks[​](#page-configuration-with-pre-navigation-hooks "Direct link to Page configuration with pre-navigation hooks")

In some use cases, you may need to configure the [page](https://playwright.dev/python/docs/api/class-page) before it navigates to the target URL. For instance, you might set navigation timeouts or manipulate other page-level settings. For such cases you can use the [`pre_navigation_hook`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md#pre_navigation_hook) method of the [`AdaptivePlaywrightCrawler`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md). This method is called before the page navigates to the target URL and allows you to configure the page instance. Due to the dynamic nature of [`AdaptivePlaywrightCrawler`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md) it is possible that the hook will be executed for HTTP-based sub crawler or playwright-based sub crawler. Using [page](https://playwright.dev/python/docs/api/class-page) object for hook that will be executed on HTTP-based sub crawler will raise an exception. To overcome this you can use optional argument `playwright_only` = `True` when registering the hook.

See the following example about how to register the pre navigation hooks:

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBwbGF5d3JpZ2h0LmFzeW5jX2FwaSBpbXBvcnQgUm91dGVcXG5cXG5mcm9tIGNyYXdsZWUuY3Jhd2xlcnMgaW1wb3J0IChcXG4gICAgQWRhcHRpdmVQbGF5d3JpZ2h0Q3Jhd2xlcixcXG4gICAgQWRhcHRpdmVQbGF5d3JpZ2h0UHJlTmF2Q3Jhd2xpbmdDb250ZXh0LFxcbilcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgIGNyYXdsZXIgPSBBZGFwdGl2ZVBsYXl3cmlnaHRDcmF3bGVyLndpdGhfYmVhdXRpZnVsc291cF9zdGF0aWNfcGFyc2VyKClcXG5cXG4gICAgQGNyYXdsZXIucHJlX25hdmlnYXRpb25faG9va1xcbiAgICBhc3luYyBkZWYgaG9vayhjb250ZXh0OiBBZGFwdGl2ZVBsYXl3cmlnaHRQcmVOYXZDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBcXFwiXFxcIlxcXCJIb29rIGV4ZWN1dGVkIGJvdGggaW4gc3RhdGljIHN1YiBjcmF3bGVyIGFuZCBwbGF5d3JpZ2h0IHN1YiBjcmF3bGVyLlxcblxcbiAgICAgICAgVHJ5aW5nIHRvIGFjY2VzcyBgY29udGV4dC5wYWdlYCBpbiB0aGlzIGhvb2sgd291bGQgcmFpc2UgYEFkYXB0aXZlQ29udGV4dEVycm9yYFxcbiAgICAgICAgZm9yIHBhZ2VzIGNyYXdsZWQgd2l0aG91dCBwbGF5d3JpZ2h0LlxcbiAgICAgICAgXFxcIlxcXCJcXFwiXFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYncHJlIG5hdmlnYXRpb24gaG9vayBmb3I6IHtjb250ZXh0LnJlcXVlc3QudXJsfScpXFxuXFxuICAgIEBjcmF3bGVyLnByZV9uYXZpZ2F0aW9uX2hvb2socGxheXdyaWdodF9vbmx5PVRydWUpXFxuICAgIGFzeW5jIGRlZiBob29rX3BsYXl3cmlnaHQoY29udGV4dDogQWRhcHRpdmVQbGF5d3JpZ2h0UHJlTmF2Q3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgXFxcIlxcXCJcXFwiSG9vayBleGVjdXRlZCBvbmx5IGluIHBsYXl3cmlnaHQgc3ViIGNyYXdsZXIuXFxcIlxcXCJcXFwiXFxuXFxuICAgICAgICBhc3luYyBkZWYgc29tZV9yb3V0aW5nX2Z1bmN0aW9uKHJvdXRlOiBSb3V0ZSkgLT4gTm9uZTpcXG4gICAgICAgICAgICBhd2FpdCByb3V0ZS5jb250aW51ZV8oKVxcblxcbiAgICAgICAgYXdhaXQgY29udGV4dC5wYWdlLnJvdXRlKCcqLyoqJywgc29tZV9yb3V0aW5nX2Z1bmN0aW9uKVxcbiAgICAgICAgY29udGV4dC5sb2cuaW5mbyhcXG4gICAgICAgICAgICBmJ1BsYXl3cmlnaHQgb25seSBwcmUgbmF2aWdhdGlvbiBob29rIGZvcjoge2NvbnRleHQucmVxdWVzdC51cmx9J1xcbiAgICAgICAgKVxcblxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vY3Jhd2xlZS5kZXYvJ10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjQwOTYsInRpbWVvdXQiOjE4MH19.gu98k7zu2eDxVc8E5xpaqYNUkRzGkBvAfZB_fJrbKqc\&asrc=run_on_apify)

```
import asyncio

from playwright.async_api import Route

from crawlee.crawlers import (
    AdaptivePlaywrightCrawler,
    AdaptivePlaywrightPreNavCrawlingContext,
)


async def main() -> None:
    crawler = AdaptivePlaywrightCrawler.with_beautifulsoup_static_parser()

    @crawler.pre_navigation_hook
    async def hook(context: AdaptivePlaywrightPreNavCrawlingContext) -> None:
        """Hook executed both in static sub crawler and playwright sub crawler.

        Trying to access `context.page` in this hook would raise `AdaptiveContextError`
        for pages crawled without playwright.
        """
        context.log.info(f'pre navigation hook for: {context.request.url}')

    @crawler.pre_navigation_hook(playwright_only=True)
    async def hook_playwright(context: AdaptivePlaywrightPreNavCrawlingContext) -> None:
        """Hook executed only in playwright sub crawler."""

        async def some_routing_function(route: Route) -> None:
            await route.continue_()

        await context.page.route('*/**', some_routing_function)
        context.log.info(
            f'Playwright only pre navigation hook for: {context.request.url}'
        )

    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/guides/playwright_crawler_adaptive.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/guides/playwright-crawler.md)

[Playwright crawler](https://crawlee.dev/python/python/docs/guides/playwright-crawler.md)

[Next](https://crawlee.dev/python/python/docs/guides/playwright-crawler-stagehand.md)

[Playwright with Stagehand](https://crawlee.dev/python/python/docs/guides/playwright-crawler-stagehand.md)


---

* [](https://crawlee.dev/python/python)
* [Guides](https://crawlee.dev/python/python/docs/guides.md)
* Architecture overview

Version: 1.6

On this page

# Architecture overview

Crawlee is a modern and modular web scraping framework. It is designed for both HTTP-only and browser-based scraping. In this guide, we will provide a high-level overview of its architecture and the main components that make up the system.

## Crawler[​](#crawler "Direct link to Crawler")

The main user-facing component of Crawlee is the crawler, which orchestrates the crawling process and takes care of all other components. It manages storages, executes user-defined request handlers, handles retries, manages concurrency, and coordinates all other components. All crawlers inherit from the [`BasicCrawler`](https://crawlee.dev/python/python/api/class/BasicCrawler.md) class, which provides the basic functionality. There are two main groups of specialized crawlers: HTTP crawlers and browser crawlers.

info

You will learn more about the request handlers in the request router section.

<!-- -->

### HTTP crawlers[​](#http-crawlers "Direct link to HTTP crawlers")

HTTP crawlers use HTTP clients to fetch pages and parse them with HTML parsing libraries. They are fast and efficient for sites that do not require JavaScript rendering. HTTP clients are Crawlee components that wrap around HTTP libraries like [httpx](https://www.python-httpx.org/), [curl-impersonate](https://github.com/lwthiker/curl-impersonate) or [impit](https://apify.github.io/impit) and handle HTTP communication for requests and responses. You can learn more about them in the [HTTP clients guide](https://crawlee.dev/python/python/docs/guides/http-clients.md).

HTTP crawlers inherit from [`AbstractHttpCrawler`](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md) and there are three crawlers that belong to this category:

* [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md) utilizes the [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/) HTML parser.
* [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md) utilizes [Parsel](https://github.com/scrapy/parsel) for parsing HTML.
* [`HttpCrawler`](https://crawlee.dev/python/python/api/class/HttpCrawler.md) does not parse HTTP responses at all and is used when no content parsing is required.

You can learn more about HTTP crawlers in the [HTTP crawlers guide](https://crawlee.dev/python/python/docs/guides/http-crawlers.md).

### Browser crawlers[​](#browser-crawlers "Direct link to Browser crawlers")

Browser crawlers use a real browser to render pages, enabling scraping of sites that require JavaScript. They manage browser instances, pages, and context lifecycles. Currently, the only browser crawler is [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md), which utilizes the [Playwright](https://playwright.dev/) library. Playwright provides a high-level API for controlling and navigating browsers. You can learn more about [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md), its features, and how it internally manages browser instances in the [Playwright crawler guide](https://crawlee.dev/python/python/docs/guides/playwright-crawler.md).

### Adaptive crawler[​](#adaptive-crawler "Direct link to Adaptive crawler")

The [`AdaptivePlaywrightCrawler`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md) sits between HTTP and browser crawlers. It can automatically decide whether to use HTTP or browser crawling for each request based on heuristics or user configuration. This allows for optimal performance and compatibility. It also provides a uniform interface for both crawling types (modes). You can learn more about adaptive crawling in the [Adaptive Playwright crawler guide](https://crawlee.dev/python/python/docs/guides/adaptive-playwright-crawler.md).

## Crawling contexts[​](#crawling-contexts "Direct link to Crawling contexts")

Crawling contexts are objects that encapsulate the state and data for each request being processed by the crawler. They provide access to the request, response, session, and helper methods for handling the request. Crawling contexts are used to pass data between different parts of the crawler and to manage the lifecycle of each request. These contexts are provided to user-defined request handlers, which can then use them to access request data, response data, or use helper methods to interact with storages, and extract and enqueue new requests.

<!-- -->

They have a similar inheritance structure as the crawlers, with the base class being [`BasicCrawlingContext`](https://crawlee.dev/python/python/api/class/BasicCrawlingContext.md). The specific crawling contexts are:

* [`HttpCrawlingContext`](https://crawlee.dev/python/python/api/class/HttpCrawlingContext.md) for HTTP crawlers.
* [`ParsedHttpCrawlingContext`](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md) for HTTP crawlers with parsed responses.
* [`ParselCrawlingContext`](https://crawlee.dev/python/python/api/class/ParselCrawlingContext.md) for HTTP crawlers that use [Parsel](https://github.com/scrapy/parsel) for parsing.
* [`BeautifulSoupCrawlingContext`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawlingContext.md) for HTTP crawlers that use [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/) for parsing.
* [`PlaywrightPreNavCrawlingContext`](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md) for Playwright crawlers before the page is navigated.
* [`PlaywrightCrawlingContext`](https://crawlee.dev/python/python/api/class/PlaywrightCrawlingContext.md) for Playwright crawlers.
* [`AdaptivePlaywrightPreNavCrawlingContext`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightPreNavCrawlingContext.md) for Adaptive Playwright crawlers before the page is navigated.
* [`AdaptivePlaywrightCrawlingContext`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawlingContext.md) for Adaptive Playwright crawlers.

## Storages[​](#storages "Direct link to Storages")

Storages are the components that manage data in Crawlee. They provide a way to store and retrieve data during the crawling process. Crawlee's storage system consists of two main layers:

* **Storages**: High-level interfaces for interacting with different storage types
* **Storage clients**: Backend implementations that handle the actual data persistence and management (you will learn more about them in the next section)

Crawlee provides three built-in storage types for managing data:

* [`Dataset`](https://crawlee.dev/python/python/api/class/Dataset.md) - Append-only, tabular storage for structured data. It is ideal for storing scraping results.
* [`KeyValueStore`](https://crawlee.dev/python/python/api/class/KeyValueStore.md) - Storage for arbitrary data like JSON documents, images or configs. It supports get and set operations with key-value pairs; updates are only possible by replacement.
* [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md) - A managed queue for pending and completed requests, with automatic deduplication and dynamic addition of new items. It is used to track URLs for crawling.

See the [Storages guide](https://crawlee.dev/python/python/docs/guides/storages.md) for more details.

<!-- -->

## Storage clients[​](#storage-clients "Direct link to Storage clients")

Storage clients are the backend implementations for storages that handle interactions with different storage systems. They provide a unified interface for [`Dataset`](https://crawlee.dev/python/python/api/class/Dataset.md), [`KeyValueStore`](https://crawlee.dev/python/python/api/class/KeyValueStore.md), and [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md), regardless of the underlying storage implementation.

Crawlee provides several built-in storage client implementations:

* [`MemoryStorageClient`](https://crawlee.dev/python/python/api/class/MemoryStorageClient.md) - Stores data in memory with no persistence (ideal for testing and fast operations).
* [`FileSystemStorageClient`](https://crawlee.dev/python/python/api/class/FileSystemStorageClient.md) - Provides persistent file system storage with caching (default client).
* [`ApifyStorageClient`](https://docs.apify.com/sdk/python/reference/class/ApifyStorageClient) - Manages storage on the [Apify platform](https://apify.com/) (cloud-based). It is implemented in the [Apify SDK](https://github.com/apify/apify-sdk-python). You can find more information about it in the [Apify SDK documentation](https://docs.apify.com/sdk/python/docs/overview/introduction).

<!-- -->

Storage clients can be registered globally with the [`ServiceLocator`](https://crawlee.dev/python/python/api/class/ServiceLocator.md) (you will learn more about the [`ServiceLocator`](https://crawlee.dev/python/python/api/class/ServiceLocator.md) in the next section), passed directly to crawlers, or specified when opening individual storage instances. You can also create custom storage clients by implementing the [`StorageClient`](https://crawlee.dev/python/python/api/class/StorageClient.md) interface.

See the [Storage clients guide](https://crawlee.dev/python/python/docs/guides/storage-clients.md) for more details.

## Request router[​](#request-router "Direct link to Request router")

The request [`Router`](https://crawlee.dev/python/python/api/class/Router.md) is a central component that manages the flow of requests and responses in Crawlee. It is responsible for routing requests to the appropriate request handlers, managing the crawling context, and coordinating the execution of user-defined logic.

### Request handlers[​](#request-handlers "Direct link to Request handlers")

Request handlers are user-defined functions that process requests and responses in Crawlee. They are the core of the crawling logic and are responsible for handling data extraction, processing, and storage. Each request handler receives a crawling context as an argument, which provides access to request data, response data, and other information related to the request. Request handlers can be registered with the [`Router`](https://crawlee.dev/python/python/api/class/Router.md).

The request routing in Crawlee supports:

* Default handlers - Fallback handlers for requests without specific labels.
* Label-based routing - Handlers for specific request types based on labels.
* Error handlers - Handle errors during request processing.
* Failed request handlers - Handle requests that exceed retry limits.
* Pre-navigation hooks - Execute logic before navigating to URLs.

See the [Request router guide](https://crawlee.dev/python/python/docs/guides/request-router.md) for detailed information and examples.

## Service locator[​](#service-locator "Direct link to Service locator")

The [`ServiceLocator`](https://crawlee.dev/python/python/api/class/ServiceLocator.md) is a central registry for global services in Crawlee. It manages and provides access to core services throughout the framework, ensuring consistent configuration across all components. The service locator coordinates these three services:

* [`Configuration`](https://crawlee.dev/python/python/api/class/Configuration.md) - Application-wide settings and parameters that control various aspects of Crawlee behavior.
* [`StorageClient`](https://crawlee.dev/python/python/api/class/StorageClient.md) - Backend implementation for data storage across datasets, key-value stores, and request queues.
* [`EventManager`](https://crawlee.dev/python/python/api/class/EventManager.md) - Event coordination system for internal framework events and custom user hooks.

Services can be registered globally through the `service_locator` singleton instance, passed to crawler constructors, or provided when opening individual storage instances. The service locator includes conflict prevention mechanisms to ensure configuration consistency and prevent accidental service conflicts during runtime.

See the [Service locator guide](https://crawlee.dev/python/python/docs/guides/service-locator.md) for detailed information about service registration and configuration options.

## Request loaders[​](#request-loaders "Direct link to Request loaders")

Request loaders provide a subset of [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md) functionality, focusing specifically on reading and accessing streams of requests from various sources. They define how requests are fetched and processed, enabling use cases such as reading URLs from files, external APIs, sitemaps, or combining multiple sources together. Unlike request queues, they do not handle storage or persistence—they only provide request reading capabilities.

* [`RequestLoader`](https://crawlee.dev/python/python/api/class/RequestLoader.md) - Base interface for read-only access to a stream of requests, with capabilities like fetching the next request, marking as handled, and status checking.
* [`RequestList`](https://crawlee.dev/python/python/api/class/RequestList.md) - Lightweight in-memory implementation of `RequestLoader` for managing static lists of URLs.
* [`SitemapRequestLoader`](https://crawlee.dev/python/python/api/class/SitemapRequestLoader.md) - A specialized loader that reads URLs from XML and plain-text sitemaps following the [Sitemaps protocol](https://www.sitemaps.org/protocol.html) with filtering capabilities.

### Request managers[​](#request-managers "Direct link to Request managers")

[`RequestManager`](https://crawlee.dev/python/python/api/class/RequestManager.md) extends [`RequestLoader`](https://crawlee.dev/python/python/api/class/RequestLoader.md) with write capabilities for adding and reclaiming requests, providing full request management functionality. [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md) is the primary concrete implementation of [`RequestManager`](https://crawlee.dev/python/python/api/class/RequestManager.md).

[`RequestManagerTandem`](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md) combines a read-only `RequestLoader` with a writable [`RequestManager`](https://crawlee.dev/python/python/api/class/RequestManager.md), transferring requests from the loader to the manager for hybrid scenarios. This is useful when you want to start with a predefined set of URLs (from a file or sitemap) but also need to add new requests dynamically during crawling. The tandem first processes all requests from the loader, then handles any additional requests added to the manager.

Request loaders are useful when you need to start with a predefined set of URLs. The tandem approach allows processing requests from static sources (like files or sitemaps) while maintaining the ability to add new requests dynamically.

See the [Request loaders guide](https://crawlee.dev/python/python/docs/guides/request-loaders.md) for detailed information.

## Event manager[​](#event-manager "Direct link to Event manager")

The [`EventManager`](https://crawlee.dev/python/python/api/class/EventManager.md) is responsible for coordinating internal events throughout Crawlee and enabling custom hooks. It provides a system for registering event listeners, emitting events, and managing their execution lifecycle.

Crawlee provides several implementations of the event manager:

* [`EventManager`](https://crawlee.dev/python/python/api/class/EventManager.md) is the base class for event management in Crawlee.
* [`LocalEventManager`](https://crawlee.dev/python/python/api/class/LocalEventManager.md) extends the base event manager for local environments by automatically emitting `SYSTEM_INFO` events at regular intervals. This provides real-time system metrics including CPU usage and memory consumption, which are essential for internal components like the [`Snapshotter`](https://crawlee.dev/python/python/api/class/Snapshotter.md) and [`AutoscaledPool`](https://crawlee.dev/python/python/api/class/AutoscaledPool.md).
* [`ApifyEventManager`](https://docs.apify.com/sdk/python/reference/class/PlatformEventManager) - Manages events on the [Apify platform](https://apify.com/) (cloud-based). It is implemented in the [Apify SDK](https://docs.apify.com/sdk/python/).

info

You can learn more about [`Snapshotter`](https://crawlee.dev/python/python/api/class/Snapshotter.md) and [`AutoscaledPool`](https://crawlee.dev/python/python/api/class/AutoscaledPool.md) and their configuration in the [Scaling crawlers guide](https://crawlee.dev/python/python/docs/guides/scaling-crawlers.md).

Crawlee defines several built-in event types:

* `PERSIST_STATE` - Emitted periodically to trigger state persistence.
* `SYSTEM_INFO` - Contains CPU and memory usage information.
* `MIGRATING` - Signals that the crawler is migrating to a different environment.
* `ABORTING` - Indicates the crawler is aborting execution.
* `EXIT` - Emitted when the crawler is exiting.
* `CRAWLER_STATUS` - Provides status updates from crawlers.

Additional specialized events for browser and session management are also available.

The event manager operates as an async context manager, automatically starting periodic tasks when entered and ensuring all listeners complete before exiting. Event listeners can be either synchronous or asynchronous functions and are executed safely without blocking the main event loop.

<!-- -->

## Session management[​](#session-management "Direct link to Session management")

The core component of session management in Crawlee is [`SessionPool`](https://crawlee.dev/python/python/api/class/SessionPool.md). It manages a collection of sessions that simulate individual users with unique attributes like cookies, IP addresses (via proxies), and browser fingerprints. Sessions help avoid blocking by rotating user identities and maintaining realistic browsing patterns.

info

You can learn more about fingerprints and how to avoid getting blocked in the [Avoid blocking guide](https://crawlee.dev/python/python/docs/guides/avoid-blocking.md).

### Session[​](#session "Direct link to Session")

A session is represented as a [`Session`](https://crawlee.dev/python/python/api/class/Session.md) object, which contains components like cookies, error tracking, usage limits, and expiration handling. Sessions can be marked as good ([`Session.mark_good`](https://crawlee.dev/python/python/api/class/Session.md#mark_good)), bad ([`Session.mark_bad`](https://crawlee.dev/python/python/api/class/Session.md#mark_bad)), or retired ([`Session.retire`](https://crawlee.dev/python/python/api/class/Session.md#retire)) based on their performance, and they automatically become unusable when they exceed error thresholds or usage limits.

### Session pool[​](#session-pool "Direct link to Session pool")

The session pool provides automated session lifecycle management:

* Automatic rotation - Retrieves random sessions from the pool and creates new ones as needed.
* Pool maintenance - Removes retired sessions and maintains the pool at maximum capacity.
* State persistence - Persists session state to enable recovery across restarts.
* Configurable limits - Supports custom pool sizes, session settings, and creation functions.

The pool operates as an async context manager, automatically initializing with sessions and cleaning up on exit. It ensures proper session management by rotating sessions based on usage count, expiration time, and custom rules while maintaining optimal pool size.

See the [Session management guide](https://crawlee.dev/python/python/docs/guides/session-management.md) for more information.

## Statistics[​](#statistics "Direct link to Statistics")

The [`Statistics`](https://crawlee.dev/python/python/api/class/Statistics.md) class provides runtime monitoring for crawler operations, tracking performance metrics like request counts, processing times, retry attempts, and error patterns. It operates as an async context manager, automatically persisting data across crawler restarts and migrations using [`KeyValueStore`](https://crawlee.dev/python/python/api/class/KeyValueStore.md).

The system includes error tracking through the [`ErrorTracker`](https://crawlee.dev/python/python/api/class/ErrorTracker.md) class, which groups similar errors by type and message patterns using wildcard matching. It can capture HTML snapshots and screenshots for debugging and separately track retry-specific errors.

Statistics are logged at configurable intervals in both table and inline formats, with final summary data returned from the `crawler.run` method available through [`FinalStatistics`](https://crawlee.dev/python/python/api/class/FinalStatistics.md).

## Conclusion[​](#conclusion "Direct link to Conclusion")

In this guide, we provided a high-level overview of the core components of the Crawlee library and its architecture. We covered the main components like crawlers, crawling contexts, storages, request routers, service locator, request loaders, event manager, session management, and statistics. Check out other guides, the [API reference](https://crawlee.dev/python/python/api.md), and [Examples](https://crawlee.dev/python/python/docs/examples.md) for more details on how to use these components in your own projects.

If you have questions or need assistance, feel free to reach out on our [GitHub](https://github.com/apify/crawlee-python) or join our [Discord community](https://discord.com/invite/jyEM2PRvMU). Happy scraping!

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/guides/architecture_overview.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/guides.md)

[Guides](https://crawlee.dev/python/python/docs/guides.md)

[Next](https://crawlee.dev/python/python/docs/guides/avoid-blocking.md)

[Avoid getting blocked](https://crawlee.dev/python/python/docs/guides/avoid-blocking.md)


---

* [](https://crawlee.dev/python/python)
* [Guides](https://crawlee.dev/python/python/docs/guides.md)
* Avoid getting blocked

Version: 1.6

On this page

# Avoid getting blocked

A scraper might get blocked for numerous reasons. Let's narrow it down to the two main ones. The first is a bad or blocked IP address. You can learn about this topic in the [proxy management guide](https://crawlee.dev/python/python/docs/guides/proxy-management.md). The second reason is [browser fingerprints](https://pixelprivacy.com/resources/browser-fingerprinting/) (or signatures), which we will explore more in this guide. Check the [Apify Academy anti-scraping course](https://docs.apify.com/academy/anti-scraping) to gain a deeper theoretical understanding of blocking and learn a few tips and tricks.

Browser fingerprint is a collection of browser attributes and significant features that can show if our browser is a bot or a real user. Moreover, most browsers have these unique features that allow the website to track the browser even within different IP addresses. This is the main reason why scrapers should change browser fingerprints while doing browser-based scraping. In return, it should significantly reduce the blocking.

## Using browser fingerprints[​](#using-browser-fingerprints "Direct link to Using browser fingerprints")

Changing browser fingerprints can be a tedious job. Luckily, Crawlee provides this feature with minimal configuration necessary - the usage of fingerprints in [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) is enabled by default. You can customize the fingerprints by using the `fingerprint_generator` argument of the [`PlaywrightCrawler.__init__`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md#__init__), either pass your own implementation of [`FingerprintGenerator`](https://crawlee.dev/python/python/api/class/FingerprintGenerator.md) or use [`DefaultFingerprintGenerator`](https://crawlee.dev/python/python/api/class/BrowserforgeFingerprintGenerator.md).

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQbGF5d3JpZ2h0Q3Jhd2xlciwgUGxheXdyaWdodENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBGaW5nZXJwcmludCBnZW5lcmF0b3IgaXMgdXNlZCBieSBkZWZhdWx0LlxcbiAgICBjcmF3bGVyID0gUGxheXdyaWdodENyYXdsZXIoKVxcblxcbiAgICAjIERlZmluZSB0aGUgZGVmYXVsdCByZXF1ZXN0IGhhbmRsZXIsIHdoaWNoIHdpbGwgYmUgY2FsbGVkIGZvciBldmVyeSByZXF1ZXN0LlxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiByZXF1ZXN0X2hhbmRsZXIoY29udGV4dDogUGxheXdyaWdodENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm9jZXNzaW5nIHtjb250ZXh0LnJlcXVlc3QudXJsfSAuLi4nKVxcblxcbiAgICAgICAgIyBGaW5kIGEgbGluayB0byB0aGUgbmV4dCBwYWdlIGFuZCBlbnF1ZXVlIGl0IGlmIGl0IGV4aXN0cy5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQuZW5xdWV1ZV9saW5rcyhzZWxlY3Rvcj0nLm1vcmVsaW5rJylcXG5cXG4gICAgIyBSdW4gdGhlIGNyYXdsZXIgd2l0aCB0aGUgaW5pdGlhbCBsaXN0IG9mIFVSTHMuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9uZXdzLnljb21iaW5hdG9yLmNvbS8nXSlcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6NDA5NiwidGltZW91dCI6MTgwfX0.mXwRfslAeCXWPFntx9DgrgGZ5MFDwO9gggLKs_ZoD0k\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext


async def main() -> None:
    # Fingerprint generator is used by default.
    crawler = PlaywrightCrawler()

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

In certain cases we want to narrow down the fingerprints used - e.g. specify a certain operating system, locale or browser. This is also possible with Crawlee - the crawler can have the generation algorithm customized to reflect the particular browser version and many more. For description of fingerprint generation options please see [`HeaderGeneratorOptions`](https://crawlee.dev/python/python/api/class/HeaderGeneratorOptions.md), [`ScreenOptions`](https://crawlee.dev/python/python/api/class/ScreenOptions.md) and [`DefaultFingerprintGenerator.__init__`](https://crawlee.dev/python/python/api/class/BrowserforgeFingerprintGenerator.md#__init__) See the example below:

```
import asyncio

from crawlee.fingerprint_suite import (
    DefaultFingerprintGenerator,
    HeaderGeneratorOptions,
    ScreenOptions,
)


async def main() -> None:
    fingerprint_generator = DefaultFingerprintGenerator(
        header_options=HeaderGeneratorOptions(browsers=['chrome']),
        screen_options=ScreenOptions(min_width=400),
    )

    # ...


if __name__ == '__main__':
    asyncio.run(main())
```

If you do not want to use fingerprints, then pass `fingerprint_generator=None` argument to the [`PlaywrightCrawler.__init__`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md#__init__).

## Using Camoufox[​](#using-camoufox "Direct link to Using Camoufox")

In some cases even [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) with fingerprints is not enough. You can try using [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) together with [Camoufox](https://camoufox.com/). See the example integration below:

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

## Using CloakBrowser[​](#using-cloakbrowser "Direct link to Using CloakBrowser")

For sites with aggressive anti-bot protection, [CloakBrowser](https://github.com/CloakHQ/CloakBrowser) takes a different approach. Instead of overriding fingerprints at the JavaScript level (which anti-bot scripts can detect as tampering), CloakBrowser ships a custom Chromium binary with fingerprints modified directly in the C++ source code. It is also Chromium-based, which can matter when a target site behaves differently with Firefox than with Chrome. Install it separately with `pip install cloakbrowser` — the plugin calls `ensure_binary()` which automatically downloads and caches the Chromium binary on first run.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuIyBDbG9ha0Jyb3dzZXIgaXMgYW4gZXh0ZXJuYWwgcGFja2FnZS4gSW5zdGFsbCBpdCBzZXBhcmF0ZWx5LlxcbmZyb20gY2xvYWticm93c2VyLmNvbmZpZyBpbXBvcnQgSUdOT1JFX0RFRkFVTFRfQVJHUywgZ2V0X2RlZmF1bHRfc3RlYWx0aF9hcmdzXFxuZnJvbSBjbG9ha2Jyb3dzZXIuZG93bmxvYWQgaW1wb3J0IGVuc3VyZV9iaW5hcnlcXG5mcm9tIHR5cGluZ19leHRlbnNpb25zIGltcG9ydCBvdmVycmlkZVxcblxcbmZyb20gY3Jhd2xlZS5icm93c2VycyBpbXBvcnQgKFxcbiAgICBCcm93c2VyUG9vbCxcXG4gICAgUGxheXdyaWdodEJyb3dzZXJDb250cm9sbGVyLFxcbiAgICBQbGF5d3JpZ2h0QnJvd3NlclBsdWdpbixcXG4pXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQbGF5d3JpZ2h0Q3Jhd2xlciwgUGxheXdyaWdodENyYXdsaW5nQ29udGV4dFxcblxcblxcbmNsYXNzIENsb2FrQnJvd3NlclBsdWdpbihQbGF5d3JpZ2h0QnJvd3NlclBsdWdpbik6XFxuICAgIFxcXCJcXFwiXFxcIkV4YW1wbGUgYnJvd3NlciBwbHVnaW4gdGhhdCB1c2VzIENsb2FrQnJvd3NlcidzIHBhdGNoZWQgQ2hyb21pdW0sXFxuICAgIGJ1dCBvdGhlcndpc2Uga2VlcHMgdGhlIGZ1bmN0aW9uYWxpdHkgb2YgUGxheXdyaWdodEJyb3dzZXJQbHVnaW4uXFxuICAgIFxcXCJcXFwiXFxcIlxcblxcbiAgICBAb3ZlcnJpZGVcXG4gICAgYXN5bmMgZGVmIG5ld19icm93c2VyKHNlbGYpIC0-IFBsYXl3cmlnaHRCcm93c2VyQ29udHJvbGxlcjpcXG4gICAgICAgIGlmIG5vdCBzZWxmLl9wbGF5d3JpZ2h0OlxcbiAgICAgICAgICAgIHJhaXNlIFJ1bnRpbWVFcnJvcignUGxheXdyaWdodCBicm93c2VyIHBsdWdpbiBpcyBub3QgaW5pdGlhbGl6ZWQuJylcXG5cXG4gICAgICAgIGJpbmFyeV9wYXRoID0gZW5zdXJlX2JpbmFyeSgpXFxuICAgICAgICBzdGVhbHRoX2FyZ3MgPSBnZXRfZGVmYXVsdF9zdGVhbHRoX2FyZ3MoKVxcblxcbiAgICAgICAgIyBNZXJnZSBDbG9ha0Jyb3dzZXIgc3RlYWx0aCBhcmdzIHdpdGggYW55IHVzZXItcHJvdmlkZWQgbGF1bmNoIG9wdGlvbnMuXFxuICAgICAgICBsYXVuY2hfb3B0aW9ucyA9IGRpY3Qoc2VsZi5fYnJvd3Nlcl9sYXVuY2hfb3B0aW9ucylcXG4gICAgICAgIGxhdW5jaF9vcHRpb25zLnBvcCgnZXhlY3V0YWJsZV9wYXRoJywgTm9uZSlcXG4gICAgICAgIGxhdW5jaF9vcHRpb25zLnBvcCgnY2hyb21pdW1fc2FuZGJveCcsIE5vbmUpXFxuICAgICAgICBleGlzdGluZ19hcmdzID0gbGlzdChsYXVuY2hfb3B0aW9ucy5wb3AoJ2FyZ3MnLCBbXSkpXFxuICAgICAgICBsYXVuY2hfb3B0aW9uc1snYXJncyddID0gWypleGlzdGluZ19hcmdzLCAqc3RlYWx0aF9hcmdzXVxcblxcbiAgICAgICAgcmV0dXJuIFBsYXl3cmlnaHRCcm93c2VyQ29udHJvbGxlcihcXG4gICAgICAgICAgICBicm93c2VyPWF3YWl0IHNlbGYuX3BsYXl3cmlnaHQuY2hyb21pdW0ubGF1bmNoKFxcbiAgICAgICAgICAgICAgICBleGVjdXRhYmxlX3BhdGg9YmluYXJ5X3BhdGgsXFxuICAgICAgICAgICAgICAgIGlnbm9yZV9kZWZhdWx0X2FyZ3M9SUdOT1JFX0RFRkFVTFRfQVJHUyxcXG4gICAgICAgICAgICAgICAgKipsYXVuY2hfb3B0aW9ucyxcXG4gICAgICAgICAgICApLFxcbiAgICAgICAgICAgIG1heF9vcGVuX3BhZ2VzX3Blcl9icm93c2VyPTEsXFxuICAgICAgICAgICAgIyBDbG9ha0Jyb3dzZXIgaGFuZGxlcyBmaW5nZXJwcmludHMgYXQgdGhlIGJpbmFyeSBsZXZlbC5cXG4gICAgICAgICAgICBoZWFkZXJfZ2VuZXJhdG9yPU5vbmUsXFxuICAgICAgICApXFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICBjcmF3bGVyID0gUGxheXdyaWdodENyYXdsZXIoXFxuICAgICAgICAjIExpbWl0IHRoZSBjcmF3bCB0byBtYXggcmVxdWVzdHMuIFJlbW92ZSBvciBpbmNyZWFzZSBpdCBmb3IgY3Jhd2xpbmcgYWxsIGxpbmtzLlxcbiAgICAgICAgbWF4X3JlcXVlc3RzX3Blcl9jcmF3bD0xMCxcXG4gICAgICAgICMgQ3VzdG9tIGJyb3dzZXIgcG9vbC4gR2l2ZXMgdXNlcnMgZnVsbCBjb250cm9sIG92ZXIgYnJvd3NlcnMgdXNlZCBieSB0aGUgY3Jhd2xlci5cXG4gICAgICAgIGJyb3dzZXJfcG9vbD1Ccm93c2VyUG9vbChwbHVnaW5zPVtDbG9ha0Jyb3dzZXJQbHVnaW4oKV0pLFxcbiAgICApXFxuXFxuICAgICMgRGVmaW5lIHRoZSBkZWZhdWx0IHJlcXVlc3QgaGFuZGxlciwgd2hpY2ggd2lsbCBiZSBjYWxsZWQgZm9yIGV2ZXJ5IHJlcXVlc3QuXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIHJlcXVlc3RfaGFuZGxlcihjb250ZXh0OiBQbGF5d3JpZ2h0Q3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ1Byb2Nlc3Npbmcge2NvbnRleHQucmVxdWVzdC51cmx9IC4uLicpXFxuXFxuICAgICAgICAjIEV4dHJhY3Qgc29tZSBkYXRhIGZyb20gdGhlIHBhZ2UgdXNpbmcgUGxheXdyaWdodCdzIEFQSS5cXG4gICAgICAgIHBvc3RzID0gYXdhaXQgY29udGV4dC5wYWdlLnF1ZXJ5X3NlbGVjdG9yX2FsbCgnLmF0aGluZycpXFxuICAgICAgICBmb3IgcG9zdCBpbiBwb3N0czpcXG4gICAgICAgICAgICAjIEdldCB0aGUgSFRNTCBlbGVtZW50cyBmb3IgdGhlIHRpdGxlIGFuZCByYW5rIHdpdGhpbiBlYWNoIHBvc3QuXFxuICAgICAgICAgICAgdGl0bGVfZWxlbWVudCA9IGF3YWl0IHBvc3QucXVlcnlfc2VsZWN0b3IoJy50aXRsZSBhJylcXG5cXG4gICAgICAgICAgICAjIEV4dHJhY3QgdGhlIGRhdGEgd2Ugd2FudCBmcm9tIHRoZSBlbGVtZW50cy5cXG4gICAgICAgICAgICB0aXRsZSA9IGF3YWl0IHRpdGxlX2VsZW1lbnQuaW5uZXJfdGV4dCgpIGlmIHRpdGxlX2VsZW1lbnQgZWxzZSBOb25lXFxuXFxuICAgICAgICAjIFB1c2ggdGhlIGV4dHJhY3RlZCBkYXRhIHRvIHRoZSBkZWZhdWx0IGRhdGFzZXQuXFxuICAgICAgICBhd2FpdCBjb250ZXh0LnB1c2hfZGF0YSh7J3RpdGxlJzogdGl0bGV9KVxcblxcbiAgICAgICAgIyBGaW5kIGEgbGluayB0byB0aGUgbmV4dCBwYWdlIGFuZCBlbnF1ZXVlIGl0IGlmIGl0IGV4aXN0cy5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQuZW5xdWV1ZV9saW5rcyhzZWxlY3Rvcj0nLm1vcmVsaW5rJylcXG5cXG4gICAgIyBSdW4gdGhlIGNyYXdsZXIgd2l0aCB0aGUgaW5pdGlhbCBsaXN0IG9mIFVSTHMuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9uZXdzLnljb21iaW5hdG9yLmNvbS8nXSlcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6NDA5NiwidGltZW91dCI6MTgwfX0.aqmlorBMNr-JsoWS4_WC1-56dPls0a_qwmpbo_VCrFs\&asrc=run_on_apify)

```
import asyncio

# CloakBrowser is an external package. Install it separately.
from cloakbrowser.config import IGNORE_DEFAULT_ARGS, get_default_stealth_args
from cloakbrowser.download import ensure_binary
from typing_extensions import override

from crawlee.browsers import (
    BrowserPool,
    PlaywrightBrowserController,
    PlaywrightBrowserPlugin,
)
from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext


class CloakBrowserPlugin(PlaywrightBrowserPlugin):
    """Example browser plugin that uses CloakBrowser's patched Chromium,
    but otherwise keeps the functionality of PlaywrightBrowserPlugin.
    """

    @override
    async def new_browser(self) -> PlaywrightBrowserController:
        if not self._playwright:
            raise RuntimeError('Playwright browser plugin is not initialized.')

        binary_path = ensure_binary()
        stealth_args = get_default_stealth_args()

        # Merge CloakBrowser stealth args with any user-provided launch options.
        launch_options = dict(self._browser_launch_options)
        launch_options.pop('executable_path', None)
        launch_options.pop('chromium_sandbox', None)
        existing_args = list(launch_options.pop('args', []))
        launch_options['args'] = [*existing_args, *stealth_args]

        return PlaywrightBrowserController(
            browser=await self._playwright.chromium.launch(
                executable_path=binary_path,
                ignore_default_args=IGNORE_DEFAULT_ARGS,
                **launch_options,
            ),
            max_open_pages_per_browser=1,
            # CloakBrowser handles fingerprints at the binary level.
            header_generator=None,
        )


async def main() -> None:
    crawler = PlaywrightCrawler(
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
        # Custom browser pool. Gives users full control over browsers used by the crawler.
        browser_pool=BrowserPool(plugins=[CloakBrowserPlugin()]),
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

**Related links**

* [Fingerprint Suite Docs](https://github.com/apify/fingerprint-suite)
* [Apify Academy anti-scraping course](https://docs.apify.com/academy/anti-scraping)

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/guides/avoid_blocking.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/guides/architecture-overview.md)

[Architecture overview](https://crawlee.dev/python/python/docs/guides/architecture-overview.md)

[Next](https://crawlee.dev/python/python/docs/guides/logging-in-with-a-crawler.md)

[Logging in with a crawler](https://crawlee.dev/python/python/docs/guides/logging-in-with-a-crawler.md)


---

* [](https://crawlee.dev/python/python)
* [Guides](https://crawlee.dev/python/python/docs/guides.md)
* Creating web archive

Version: 1.6

On this page

# Creating web archive

Archiving webpages is one of the tasks that a web crawler can be used for. There are various use cases, such as archiving for future reference, speeding up web crawler development, creating top-level regression tests for web crawlers and so on.

There are various existing libraries of web archives with massive amount of data stored during their years of existence, for example [Wayback Machine](https://web.archive.org/) or [Common Crawl](https://commoncrawl.org/). There are also dedicated tools for archiving web pages, to name some: simple browser extensions such as [Archive Webpage](https://archiveweb.page/), open source tools such as [pywb](https://pypi.org/project/pywb/) or [warcio](https://pypi.org/project/warcio/), or even web crawlers specialized in archiving such as [Browsertrix](https://webrecorder.net/browsertrix/).

The common file format used for archiving is [WARC](https://www.iso.org/standard/68004.html). Crawlee does not offer any out-of-the-box functionality to create WARC files, but in this guide, we will show examples of approaches that can be easily used in your use case to create WARC files with Crawlee.

## Crawling through proxy recording server[​](#crawling-through-proxy-recording-server "Direct link to Crawling through proxy recording server")

This approach can be especially attractive as it does not require almost any code change to the crawler itself and the correct WARC creation is done by code from well maintained [pywb](https://pypi.org/project/pywb/) package. The trick is to run a properly configured [wayback proxy server](https://pywb.readthedocs.io/en/latest/manual/usage.html#using-pywb-recorder), use it as a proxy for the crawler and record any traffic. Another advantage of this approach is that it is language agnostic. This way, you can record both your Python-based crawler and your JavaScript-based crawler. This is very straightforward and a good place to start.

This approach expects that you have already created your crawler, and that you just want to archive all the pages it is visiting during its crawl.

Install [pywb](https://pypi.org/project/pywb/) which will allow you to use `wb-manager` and `wayback` commands. Create a new collection that will be used for this archiving session and start the wayback server:

```
wb-manager init example-collection
wayback --record --live -a --auto-interval 10 --proxy example-collection --proxy-record
```

Instead of passing many configuration arguments to `wayback` command, you can configure the server by adding configuration options to `config.yaml`. See the details in the [documentation](https://pywb.readthedocs.io/en/latest/manual/configuring.html#configuring-the-web-archive).

### Configure the crawler[​](#configure-the-crawler "Direct link to Configure the crawler")

Now you should use this locally hosted server as a proxy in your crawler. There are two more steps before starting the crawler:

* Make the crawler use the proxy server.
* Deal with the [pywb Certificate Authority](https://pywb.readthedocs.io/en/latest/manual/configuring.html#https-proxy-and-pywb-certificate-authority).

For example, in [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md), this is the simplest setup, which takes the shortcut and ignores the CA-related errors:

```
import asyncio

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext
from crawlee.proxy_configuration import ProxyConfiguration


async def main() -> None:
    crawler = PlaywrightCrawler(
        # Use the local wayback server as a proxy
        proxy_configuration=ProxyConfiguration(proxy_urls=['http://localhost:8080/']),
        # Ignore the HTTPS errors if you have not followed pywb CA setup instructions
        browser_launch_options={'ignore_https_errors': True},
        max_requests_per_crawl=10,
        headless=False,
    )

    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Archiving {context.request.url} ...')
        # For some sites, where the content loads dynamically,
        # it is needed to scroll the page to load all content.
        # It slows down the crawling, but ensures that all content is loaded.
        await context.infinite_scroll()
        await context.enqueue_links(strategy='same-domain')

    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

After you run the crawler you will be able to see the archived data in the wayback collection directory for example `.../collections/example-collection/archive`. You can then access the recorded pages directly in the proxy recording server or use it with any other WARC-compatible tool.

## Manual WARC creation[​](#manual-warc-creation "Direct link to Manual WARC creation")

A different approach is to create WARC files manually in the crawler, which gives you full control over the WARC files. This is way more complex and low-level approach as you have to ensure that all the relevant data is collected, and correctly stored and that the archiving functions are called at the right time. This is by no means a trivial task and the example archiving functions below are just the most simple examples that will be insufficient for many real-world use cases. You will need to extend and improve them to properly fit your specific needs.

### Simple crawlers[​](#simple-crawlers "Direct link to Simple crawlers")

With non-browser crawlers such as [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md) you will not be able to create high fidelity archive of the page as you will be missing all the JavaScript dynamic content. However, you can still create a WARC file with the HTML content of the page, which can be sufficient for some use cases. Let's take a look at the example below:

```
import asyncio
import io
from pathlib import Path

from warcio.statusandheaders import StatusAndHeaders
from warcio.warcwriter import WARCWriter

from crawlee.crawlers import ParselCrawler, ParselCrawlingContext


async def archive_response(context: ParselCrawlingContext, writer: WARCWriter) -> None:
    """Helper function for archiving response in WARC format."""
    # Create WARC records for response
    response_body = await context.http_response.read()
    response_payload_stream = io.BytesIO(response_body)

    response_headers = StatusAndHeaders(
        str(context.http_response.status_code),
        context.http_response.headers,
        protocol='HTTP/1.1',
    )
    response_record = writer.create_warc_record(
        context.request.url,
        'response',
        payload=response_payload_stream,
        length=len(response_body),
        http_headers=response_headers,
    )
    writer.write_record(response_record)


async def main() -> None:
    crawler = ParselCrawler(
        max_requests_per_crawl=10,
    )

    # Create a WARC archive file a prepare the writer.
    archive = Path('example.warc.gz')
    with archive.open('wb') as output:
        writer = WARCWriter(output, gzip=True)

        # Create a WARC info record to store metadata about the archive.
        warcinfo_payload = {
            'software': 'Crawlee',
            'format': 'WARC/1.1',
            'description': 'Example archive created with ParselCrawler',
        }
        writer.write_record(writer.create_warcinfo_record(archive.name, warcinfo_payload))

        # Define the default request handler, which will be called for every request.
        @crawler.router.default_handler
        async def request_handler(context: ParselCrawlingContext) -> None:
            context.log.info(f'Archiving {context.request.url} ...')
            await archive_response(context=context, writer=writer)
            await context.enqueue_links(strategy='same-domain')

        await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

The example above is calling an archiving function on each request using the `request_handler`.

### Browser-based crawlers[​](#browser-based-crawlers "Direct link to Browser-based crawlers")

With browser crawlers such as [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) you should be able to create high fidelity archive of a web page. Let's take a look at the example below:

```
import asyncio
import io
import logging
from functools import partial
from pathlib import Path

from playwright.async_api import Request
from warcio.statusandheaders import StatusAndHeaders
from warcio.warcwriter import WARCWriter

from crawlee.crawlers import (
    PlaywrightCrawler,
    PlaywrightCrawlingContext,
    PlaywrightPreNavCrawlingContext,
)


async def archive_response(
    request: Request, writer: WARCWriter, logger: logging.Logger
) -> None:
    """Helper function for archiving response in WARC format."""
    response = await request.response()
    if not response:
        logger.warning(f'Could not get response {request.url}')
        return
    try:
        response_body = await response.body()
    except Exception as e:
        logger.warning(f'Could not get response body for {response.url}: {e}')
        return
    logger.info(f'Archiving resource {response.url}')
    response_payload_stream = io.BytesIO(response_body)
    response_headers = StatusAndHeaders(
        str(response.status), response.headers, protocol='HTTP/1.1'
    )
    response_record = writer.create_warc_record(
        response.url,
        'response',
        payload=response_payload_stream,
        length=len(response_body),
        http_headers=response_headers,
    )
    writer.write_record(response_record)


async def main() -> None:
    crawler = PlaywrightCrawler(
        max_requests_per_crawl=1,
        headless=False,
    )

    # Create a WARC archive file a prepare the writer.
    archive = Path('example.warc.gz')
    with archive.open('wb') as output:
        writer = WARCWriter(output, gzip=True)

        # Create a WARC info record to store metadata about the archive.
        warcinfo_payload = {
            'software': 'Crawlee',
            'format': 'WARC/1.1',
            'description': 'Example archive created with PlaywrightCrawler',
        }
        writer.write_record(writer.create_warcinfo_record(archive.name, warcinfo_payload))

        @crawler.pre_navigation_hook
        async def archiving_hook(context: PlaywrightPreNavCrawlingContext) -> None:
            # Ensure that all responses with additional resources are archived
            context.page.on(
                'requestfinished',
                partial(archive_response, logger=context.log, writer=writer),
            )

        @crawler.router.default_handler
        async def request_handler(context: PlaywrightCrawlingContext) -> None:
            # For some sites, where the content loads dynamically,
            # it is needed to scroll the page to load all content.
            # It slows down the crawling, but ensures that all content is loaded.
            await context.infinite_scroll()
            await context.enqueue_links(strategy='same-domain')

        await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

The example above is adding an archiving callback on each response in the pre\_navigation `archiving_hook`. This ensures that additional resources requested by the browser are also archived.

## Using the archived data[​](#using-the-archived-data "Direct link to Using the archived data")

In the following section, we will describe an example use case how you can use the recorded WARC files to speed up the development of your web crawler. The idea is to use the archived data as a source of responses for your crawler so that you can test it against the real data without having to crawl the web again.

It is assumed that you already have the WARC files. If not, please read the previous sections on how to create them first.

Let's use pywb again. This time we will not use it as a recording server, but as a proxy server that will serve the previously archived pages to your crawler in development.

```
wb-manager init example-collection
wb-manager add example-collection /your_path_to_warc_file/example.warc.gz
wayback --proxy example-collection
```

Previous commands start the wayback server that allows crawler requests to be served from the archived pages in the `example-collection` instead of sending requests to the real website. This is again [proxy mode of the wayback server](https://pywb.readthedocs.io/en/latest/manual/usage.html#http-s-proxy-mode-access), but without recording capability. Now you need to [configure your crawler](#configure-the-crawler) to use this proxy server, which was already described above. Once everything is finished, you can just run your crawler, and it will crawl the offline archived version of the website from your WARC file.

You can also manually browse the archived pages in the wayback server by going to the locally hosted server and entering the collection and URL of the archived page, for example: `http://localhost:8080/example-collection/https:/crawlee.dev/`. The wayback server will serve the page from the WARC file if it exists, or it will return a 404 error if it does not. For more detail about the server please refer to the [pywb documentation](https://pywb.readthedocs.io/en/latest/manual/usage.html#getting-started).

If you have questions or need assistance, feel free to reach out on our [GitHub](https://github.com/apify/crawlee-python) or join our [Discord](https://discord.com/invite/jyEM2PRvMU) community.

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/guides/creating_web_archive.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/guides/logging-in-with-a-crawler.md)

[Logging in with a crawler](https://crawlee.dev/python/python/docs/guides/logging-in-with-a-crawler.md)

[Next](https://crawlee.dev/python/python/docs/guides/error-handling.md)

[Error handling](https://crawlee.dev/python/python/docs/guides/error-handling.md)


---

* [](https://crawlee.dev/python/python)
* [Guides](https://crawlee.dev/python/python/docs/guides.md)
* Error handling

Version: 1.6

On this page

# Error handling

This guide demonstrates techniques for handling common errors encountered during web crawling operations.

## Handling proxy errors[​](#handling-proxy-errors "Direct link to Handling proxy errors")

Low-quality proxies can cause problems even with high settings for `max_request_retries` and `max_session_rotations` in [`BasicCrawlerOptions`](https://crawlee.dev/python/python/api/class/BasicCrawlerOptions.md). If you can't get data because of proxy errors, you might want to try again. You can do this using [`failed_request_handler`](https://crawlee.dev/python/python/api/class/BasicCrawler.md#failed_request_handler):

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBSZXF1ZXN0XFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCYXNpY0NyYXdsaW5nQ29udGV4dCwgSHR0cENyYXdsZXIsIEh0dHBDcmF3bGluZ0NvbnRleHRcXG5mcm9tIGNyYXdsZWUuZXJyb3JzIGltcG9ydCBQcm94eUVycm9yXFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICAjIFNldCBob3cgbWFueSBzZXNzaW9uIHJvdGF0aW9ucyB3aWxsIGhhcHBlbiBiZWZvcmUgY2FsbGluZyB0aGUgZXJyb3IgaGFuZGxlclxcbiAgICAjIHdoZW4gUHJveHlFcnJvciBvY2N1cnNcXG4gICAgY3Jhd2xlciA9IEh0dHBDcmF3bGVyKG1heF9zZXNzaW9uX3JvdGF0aW9ucz01LCBtYXhfcmVxdWVzdF9yZXRyaWVzPTYpXFxuXFxuICAgICMgRm9yIHRoaXMgZXhhbXBsZSwgd2UnbGwgY3JlYXRlIGEgcHJveHkgZXJyb3IgaW4gb3VyIGhhbmRsZXJcXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgZGVmYXVsdF9oYW5kbGVyKGNvbnRleHQ6IEh0dHBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG4gICAgICAgIHJhaXNlIFByb3h5RXJyb3IoJ1NpbXVsYXRlZCBwcm94eSBlcnJvcicpXFxuXFxuICAgICMgVGhpcyBoYW5kbGVyIHJ1bnMgYWZ0ZXIgYWxsIHJldHJ5IGF0dGVtcHRzIGFyZSBleGhhdXN0ZWRcXG4gICAgQGNyYXdsZXIuZmFpbGVkX3JlcXVlc3RfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgZmFpbGVkX2hhbmRsZXIoY29udGV4dDogQmFzaWNDcmF3bGluZ0NvbnRleHQsIGVycm9yOiBFeGNlcHRpb24pIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5lcnJvcihmJ0ZhaWxlZCByZXF1ZXN0IHtjb250ZXh0LnJlcXVlc3QudXJsfSwgYWZ0ZXIgNSByb3RhdGlvbnMnKVxcbiAgICAgICAgcmVxdWVzdCA9IGNvbnRleHQucmVxdWVzdFxcbiAgICAgICAgIyBGb3IgcHJveHkgZXJyb3JzLCB3ZSBjYW4gYWRkIGEgbmV3IGBSZXF1ZXN0YCB0byB0cnkgYWdhaW5cXG4gICAgICAgIGlmIGlzaW5zdGFuY2UoZXJyb3IsIFByb3h5RXJyb3IpIGFuZCBub3QgcmVxdWVzdC51bmlxdWVfa2V5LnN0YXJ0c3dpdGgoJ3JldHJ5Jyk6XFxuICAgICAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ1JldHJ5aW5nIHtyZXF1ZXN0LnVybH0gLi4uJylcXG4gICAgICAgICAgICAjIENyZWF0ZSBhIG5ldyBgUmVxdWVzdGAgd2l0aCBhIG1vZGlmaWVkIGtleSB0byBhdm9pZCBkZWR1cGxpY2F0aW9uXFxuICAgICAgICAgICAgbmV3X3JlcXVlc3QgPSBSZXF1ZXN0LmZyb21fdXJsKFxcbiAgICAgICAgICAgICAgICByZXF1ZXN0LnVybCwgdW5pcXVlX2tleT1mJ3JldHJ5e3JlcXVlc3QudW5pcXVlX2tleX0nXFxuICAgICAgICAgICAgKVxcblxcbiAgICAgICAgICAgICMgQWRkIHRoZSBuZXcgYFJlcXVlc3RgIHRvIHRoZSBgUXVldWVgXFxuICAgICAgICAgICAgcnEgPSBhd2FpdCBjcmF3bGVyLmdldF9yZXF1ZXN0X21hbmFnZXIoKVxcbiAgICAgICAgICAgIGF3YWl0IHJxLmFkZF9yZXF1ZXN0KG5ld19yZXF1ZXN0KVxcblxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vY3Jhd2xlZS5kZXYvJ10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.SDxP0k7b-d309vC1F2mCNkS2YXNZWybeoEAXBOnq2cY\&asrc=run_on_apify)

```
import asyncio

from crawlee import Request
from crawlee.crawlers import BasicCrawlingContext, HttpCrawler, HttpCrawlingContext
from crawlee.errors import ProxyError


async def main() -> None:
    # Set how many session rotations will happen before calling the error handler
    # when ProxyError occurs
    crawler = HttpCrawler(max_session_rotations=5, max_request_retries=6)

    # For this example, we'll create a proxy error in our handler
    @crawler.router.default_handler
    async def default_handler(context: HttpCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')
        raise ProxyError('Simulated proxy error')

    # This handler runs after all retry attempts are exhausted
    @crawler.failed_request_handler
    async def failed_handler(context: BasicCrawlingContext, error: Exception) -> None:
        context.log.error(f'Failed request {context.request.url}, after 5 rotations')
        request = context.request
        # For proxy errors, we can add a new `Request` to try again
        if isinstance(error, ProxyError) and not request.unique_key.startswith('retry'):
            context.log.info(f'Retrying {request.url} ...')
            # Create a new `Request` with a modified key to avoid deduplication
            new_request = Request.from_url(
                request.url, unique_key=f'retry{request.unique_key}'
            )

            # Add the new `Request` to the `Queue`
            rq = await crawler.get_request_manager()
            await rq.add_request(new_request)

    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

You can use this same approach when testing different proxy providers. To better manage this process, you can count proxy errors and [stop the crawler](https://crawlee.dev/python/python/docs/examples/crawler-stop.md) if you get too many.

## Changing how error status codes are handled[​](#changing-how-error-status-codes-are-handled "Direct link to Changing how error status codes are handled")

By default, when [`Sessions`](https://crawlee.dev/python/python/api/class/Session.md) get status codes like [401](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/401), [403](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/403), or [429](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/429), Crawlee marks the [`Session`](https://crawlee.dev/python/python/api/class/Session.md) as `retire` and switches to a new one. This might not be what you want, especially when working with [authentication](https://crawlee.dev/python/python/docs/guides/logging-in-with-a-crawler.md). You can learn more in the [Session management guide](https://crawlee.dev/python/python/docs/guides/session-management.md).

Here's an example of how to change this behavior:

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuaW1wb3J0IGpzb25cXG5cXG5mcm9tIGNyYXdsZWUgaW1wb3J0IEh0dHBIZWFkZXJzXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBIdHRwQ3Jhd2xlciwgSHR0cENyYXdsaW5nQ29udGV4dFxcbmZyb20gY3Jhd2xlZS5lcnJvcnMgaW1wb3J0IEh0dHBTdGF0dXNDb2RlRXJyb3JcXG5mcm9tIGNyYXdsZWUuc2Vzc2lvbnMgaW1wb3J0IFNlc3Npb25Qb29sXFxuXFxuIyBVc2luZyBhIHBsYWNlaG9sZGVyIHJlZnJlc2ggdG9rZW4gZm9yIHRoaXMgZXhhbXBsZVxcblJFRlJFU0hfVE9LRU4gPSAnUExBQ0VIT0xERVInXFxuVU5BVVRIT1JJWkVEX0NPREUgPSA0MDFcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgIGNyYXdsZXIgPSBIdHRwQ3Jhd2xlcihcXG4gICAgICAgIG1heF9yZXF1ZXN0X3JldHJpZXM9MixcXG4gICAgICAgICMgT25seSB0cmVhdCA0MDMgYXMgYSBibG9ja2luZyBzdGF0dXMgY29kZSwgbm90IDQwMVxcbiAgICAgICAgc2Vzc2lvbl9wb29sPVNlc3Npb25Qb29sKGNyZWF0ZV9zZXNzaW9uX3NldHRpbmdzPXsnYmxvY2tlZF9zdGF0dXNfY29kZXMnOiBbNDAzXX0pLFxcbiAgICAgICAgIyBEb24ndCB0cmVhdCA0MDEgcmVzcG9uc2VzIGFzIGVycm9yc1xcbiAgICAgICAgaWdub3JlX2h0dHBfZXJyb3Jfc3RhdHVzX2NvZGVzPVtVTkFVVEhPUklaRURfQ09ERV0sXFxuICAgIClcXG5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgZGVmYXVsdF9oYW5kbGVyKGNvbnRleHQ6IEh0dHBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG4gICAgICAgICMgTm93IHdlIGNhbiBoYW5kbGUgNDAxIHJlc3BvbnNlcyBvdXJzZWx2ZXNcXG4gICAgICAgIGlmIGNvbnRleHQuaHR0cF9yZXNwb25zZS5zdGF0dXNfY29kZSA9PSBVTkFVVEhPUklaRURfQ09ERTpcXG4gICAgICAgICAgICAjIEdldCBhIGZyZXNoIGFjY2VzcyB0b2tlblxcbiAgICAgICAgICAgIGhlYWRlcnMgPSB7J2F1dGhvcml6YXRpb24nOiBmJ0JlYXJlciB7UkVGUkVTSF9UT0tFTn0nfVxcbiAgICAgICAgICAgIHJlc3BvbnNlID0gYXdhaXQgY29udGV4dC5zZW5kX3JlcXVlc3QoXFxuICAgICAgICAgICAgICAgICdodHRwczovL3BsYWNlaG9sZGVyLm9yZy9yZWZyZXNoJywgaGVhZGVycz1oZWFkZXJzXFxuICAgICAgICAgICAgKVxcbiAgICAgICAgICAgIGRhdGEgPSBqc29uLmxvYWRzKGF3YWl0IHJlc3BvbnNlLnJlYWQoKSlcXG4gICAgICAgICAgICAjIEFkZCB0aGUgbmV3IHRva2VuIHRvIG91ciBgUmVxdWVzdGAgaGVhZGVyc1xcbiAgICAgICAgICAgIGNvbnRleHQucmVxdWVzdC5oZWFkZXJzIHw9IEh0dHBIZWFkZXJzKFxcbiAgICAgICAgICAgICAgICB7J2F1dGhvcml6YXRpb24nOiBmJ0JlYXJlciB7ZGF0YVtcXFwiYWNjZXNzX3Rva2VuXFxcIl19J30sXFxuICAgICAgICAgICAgKVxcbiAgICAgICAgICAgICMgVHJpZ2dlciBhIHJldHJ5IHdpdGggb3VyIHVwZGF0ZWQgaGVhZGVyc1xcbiAgICAgICAgICAgIHJhaXNlIEh0dHBTdGF0dXNDb2RlRXJyb3IoJ1VuYXV0aG9yaXplZCcsIHN0YXR1c19jb2RlPVVOQVVUSE9SSVpFRF9DT0RFKVxcblxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHA6Ly9odHRwYmluZ28ub3JnL3N0YXR1cy80MDEnXSlcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6MTAyNCwidGltZW91dCI6MTgwfX0.wpBMTQmPDq-a5XlbK-0JcBNcwfR0HaXuHlowld7s1Gw\&asrc=run_on_apify)

```
import asyncio
import json

from crawlee import HttpHeaders
from crawlee.crawlers import HttpCrawler, HttpCrawlingContext
from crawlee.errors import HttpStatusCodeError
from crawlee.sessions import SessionPool

# Using a placeholder refresh token for this example
REFRESH_TOKEN = 'PLACEHOLDER'
UNAUTHORIZED_CODE = 401


async def main() -> None:
    crawler = HttpCrawler(
        max_request_retries=2,
        # Only treat 403 as a blocking status code, not 401
        session_pool=SessionPool(create_session_settings={'blocked_status_codes': [403]}),
        # Don't treat 401 responses as errors
        ignore_http_error_status_codes=[UNAUTHORIZED_CODE],
    )

    @crawler.router.default_handler
    async def default_handler(context: HttpCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')
        # Now we can handle 401 responses ourselves
        if context.http_response.status_code == UNAUTHORIZED_CODE:
            # Get a fresh access token
            headers = {'authorization': f'Bearer {REFRESH_TOKEN}'}
            response = await context.send_request(
                'https://placeholder.org/refresh', headers=headers
            )
            data = json.loads(await response.read())
            # Add the new token to our `Request` headers
            context.request.headers |= HttpHeaders(
                {'authorization': f'Bearer {data["access_token"]}'},
            )
            # Trigger a retry with our updated headers
            raise HttpStatusCodeError('Unauthorized', status_code=UNAUTHORIZED_CODE)

    await crawler.run(['http://httpbingo.org/status/401'])


if __name__ == '__main__':
    asyncio.run(main())
```

## Turning off retries for non-network errors[​](#turning-off-retries-for-non-network-errors "Direct link to Turning off retries for non-network errors")

Sometimes you might get unexpected errors when parsing data, like when a website has an unusual structure. Crawlee normally tries again based on your `max_request_retries` setting, but sometimes you don't want that.

Here's how to turn off retries for non-network errors using [`error_handler`](https://crawlee.dev/python/python/api/class/BasicCrawler.md#error_handler), which runs before Crawlee tries again:

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCYXNpY0NyYXdsaW5nQ29udGV4dCwgSHR0cENyYXdsZXIsIEh0dHBDcmF3bGluZ0NvbnRleHRcXG5mcm9tIGNyYXdsZWUuZXJyb3JzIGltcG9ydCBIdHRwU3RhdHVzQ29kZUVycm9yLCBTZXNzaW9uRXJyb3JcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgIGNyYXdsZXIgPSBIdHRwQ3Jhd2xlcihtYXhfcmVxdWVzdF9yZXRyaWVzPTUpXFxuXFxuICAgICMgQ3JlYXRlIGEgcGFyc2luZyBlcnJvciBmb3IgZGVtb25zdHJhdGlvblxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiBkZWZhdWx0X2hhbmRsZXIoY29udGV4dDogSHR0cENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm9jZXNzaW5nIHtjb250ZXh0LnJlcXVlc3QudXJsfSAuLi4nKVxcbiAgICAgICAgcmFpc2UgVmFsdWVFcnJvcignU2ltdWxhdGVkIHBhcnNpbmcgZXJyb3InKVxcblxcbiAgICAjIFRoaXMgaGFuZGxlciBydW5zIGJlZm9yZSBhbnkgcmV0cnkgYXR0ZW1wdHNcXG4gICAgQGNyYXdsZXIuZXJyb3JfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmV0cnlfaGFuZGxlcihjb250ZXh0OiBCYXNpY0NyYXdsaW5nQ29udGV4dCwgZXJyb3I6IEV4Y2VwdGlvbikgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmVycm9yKGYnRmFpbGVkIHJlcXVlc3Qge2NvbnRleHQucmVxdWVzdC51cmx9JylcXG4gICAgICAgICMgT25seSBhbGxvdyByZXRyaWVzIGZvciBuZXR3b3JrLXJlbGF0ZWQgZXJyb3JzXFxuICAgICAgICBpZiBub3QgaXNpbnN0YW5jZShlcnJvciwgKFNlc3Npb25FcnJvciwgSHR0cFN0YXR1c0NvZGVFcnJvcikpOlxcbiAgICAgICAgICAgIGNvbnRleHQubG9nLmVycm9yKCdOb24tbmV0d29yayBlcnJvciBkZXRlY3RlZCcpXFxuICAgICAgICAgICAgIyBTdG9wIGZ1cnRoZXIgcmV0cnkgYXR0ZW1wdHMgZm9yIHRoaXMgYFJlcXVlc3RgXFxuICAgICAgICAgICAgY29udGV4dC5yZXF1ZXN0Lm5vX3JldHJ5ID0gVHJ1ZVxcblxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vY3Jhd2xlZS5kZXYvJ10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.tpTb6RbC-rTLn6MaogtURkN0YgWsc6iCZfSpQNwNDSE\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BasicCrawlingContext, HttpCrawler, HttpCrawlingContext
from crawlee.errors import HttpStatusCodeError, SessionError


async def main() -> None:
    crawler = HttpCrawler(max_request_retries=5)

    # Create a parsing error for demonstration
    @crawler.router.default_handler
    async def default_handler(context: HttpCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')
        raise ValueError('Simulated parsing error')

    # This handler runs before any retry attempts
    @crawler.error_handler
    async def retry_handler(context: BasicCrawlingContext, error: Exception) -> None:
        context.log.error(f'Failed request {context.request.url}')
        # Only allow retries for network-related errors
        if not isinstance(error, (SessionError, HttpStatusCodeError)):
            context.log.error('Non-network error detected')
            # Stop further retry attempts for this `Request`
            context.request.no_retry = True

    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/guides/error_handling.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/guides/creating-web-archive.md)

[Creating web archive](https://crawlee.dev/python/python/docs/guides/creating-web-archive.md)

[Next](https://crawlee.dev/python/python/docs/guides/http-clients.md)

[HTTP clients](https://crawlee.dev/python/python/docs/guides/http-clients.md)


---

* [](https://crawlee.dev/python/python)
* [Guides](https://crawlee.dev/python/python/docs/guides.md)
* HTTP clients

Version: 1.6

On this page

# HTTP clients

HTTP clients are utilized by HTTP-based crawlers (e.g., [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md) and [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md)) to communicate with web servers. They use external HTTP libraries for communication rather than a browser. Examples of such libraries include [httpx](https://pypi.org/project/httpx/), [aiohttp](https://pypi.org/project/aiohttp/), [curl-cffi](https://pypi.org/project/curl-cffi/), and [impit](https://apify.github.io/impit/). After retrieving page content, an HTML parsing library is typically used to facilitate data extraction. Examples of such libraries include [beautifulsoup](https://pypi.org/project/beautifulsoup4/), [parsel](https://pypi.org/project/parsel/), [selectolax](https://pypi.org/project/selectolax/), and [pyquery](https://pypi.org/project/pyquery/). These crawlers are faster than browser-based crawlers but cannot execute client-side JavaScript.

<!-- -->

## Switching between HTTP clients[​](#switching-between-http-clients "Direct link to Switching between HTTP clients")

Crawlee currently provides three main HTTP clients: [`ImpitHttpClient`](https://crawlee.dev/python/python/api/class/ImpitHttpClient.md), which uses the `impit` library, [`HttpxHttpClient`](https://crawlee.dev/python/python/api/class/HttpxHttpClient.md), which uses the `httpx` library with `browserforge` for custom HTTP headers and fingerprints, and [`CurlImpersonateHttpClient`](https://crawlee.dev/python/python/api/class/CurlImpersonateHttpClient.md), which uses the `curl-cffi` library. You can switch between them by setting the `http_client` parameter when initializing a crawler class. The default HTTP client is [`ImpitHttpClient`](https://crawlee.dev/python/python/api/class/ImpitHttpClient.md). For more details on anti-blocking features, see our [avoid getting blocked guide](https://crawlee.dev/python/python/docs/guides/avoid-blocking.md).

Below are examples of how to configure the HTTP client for the [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md):

* ParselCrawler with HTTPX
* ParselCrawler with curl-cffi
* ParselCrawler with impit

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQYXJzZWxDcmF3bGVyLCBQYXJzZWxDcmF3bGluZ0NvbnRleHRcXG5mcm9tIGNyYXdsZWUuaHR0cF9jbGllbnRzIGltcG9ydCBIdHRweEh0dHBDbGllbnRcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgIGh0dHBfY2xpZW50ID0gSHR0cHhIdHRwQ2xpZW50KFxcbiAgICAgICAgIyBPcHRpb25hbCBhZGRpdGlvbmFsIGtleXdvcmQgYXJndW1lbnRzIGZvciBgaHR0cHguQXN5bmNDbGllbnRgLlxcbiAgICAgICAgdGltZW91dD0xMCxcXG4gICAgICAgIGZvbGxvd19yZWRpcmVjdHM9VHJ1ZSxcXG4gICAgKVxcblxcbiAgICBjcmF3bGVyID0gUGFyc2VsQ3Jhd2xlcihcXG4gICAgICAgIGh0dHBfY2xpZW50PWh0dHBfY2xpZW50LFxcbiAgICAgICAgIyBMaW1pdCB0aGUgY3Jhd2wgdG8gbWF4IHJlcXVlc3RzLiBSZW1vdmUgb3IgaW5jcmVhc2UgaXQgZm9yIGNyYXdsaW5nIGFsbCBsaW5rcy5cXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsXFxuICAgIClcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IFBhcnNlbENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm9jZXNzaW5nIHtjb250ZXh0LnJlcXVlc3QudXJsfSAuLi4nKVxcblxcbiAgICAgICAgIyBFbnF1ZXVlIGFsbCBsaW5rcyBmcm9tIHRoZSBwYWdlLlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5lbnF1ZXVlX2xpbmtzKClcXG5cXG4gICAgICAgICMgRXh0cmFjdCBkYXRhIGZyb20gdGhlIHBhZ2UuXFxuICAgICAgICBkYXRhID0ge1xcbiAgICAgICAgICAgICd1cmwnOiBjb250ZXh0LnJlcXVlc3QudXJsLFxcbiAgICAgICAgICAgICd0aXRsZSc6IGNvbnRleHQuc2VsZWN0b3IuY3NzKCd0aXRsZTo6dGV4dCcpLmdldCgpLFxcbiAgICAgICAgfVxcblxcbiAgICAgICAgIyBQdXNoIHRoZSBleHRyYWN0ZWQgZGF0YSB0byB0aGUgZGVmYXVsdCBkYXRhc2V0LlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5wdXNoX2RhdGEoZGF0YSlcXG5cXG4gICAgIyBSdW4gdGhlIGNyYXdsZXIgd2l0aCB0aGUgaW5pdGlhbCBsaXN0IG9mIFVSTHMuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9jcmF3bGVlLmRldiddKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.quxMsAoacnrYzU23C0E3NpYJWPpQQCg_pnRSV24_zuI\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import ParselCrawler, ParselCrawlingContext
from crawlee.http_clients import HttpxHttpClient


async def main() -> None:
    http_client = HttpxHttpClient(
        # Optional additional keyword arguments for `httpx.AsyncClient`.
        timeout=10,
        follow_redirects=True,
    )

    crawler = ParselCrawler(
        http_client=http_client,
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
    )

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: ParselCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Enqueue all links from the page.
        await context.enqueue_links()

        # Extract data from the page.
        data = {
            'url': context.request.url,
            'title': context.selector.css('title::text').get(),
        }

        # Push the extracted data to the default dataset.
        await context.push_data(data)

    # Run the crawler with the initial list of URLs.
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQYXJzZWxDcmF3bGVyLCBQYXJzZWxDcmF3bGluZ0NvbnRleHRcXG5mcm9tIGNyYXdsZWUuaHR0cF9jbGllbnRzIGltcG9ydCBDdXJsSW1wZXJzb25hdGVIdHRwQ2xpZW50XFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICBodHRwX2NsaWVudCA9IEN1cmxJbXBlcnNvbmF0ZUh0dHBDbGllbnQoXFxuICAgICAgICAjIE9wdGlvbmFsIGFkZGl0aW9uYWwga2V5d29yZCBhcmd1bWVudHMgZm9yIGBjdXJsX2NmZmkucmVxdWVzdHMuQXN5bmNTZXNzaW9uYC5cXG4gICAgICAgIHRpbWVvdXQ9MTAsXFxuICAgICAgICBpbXBlcnNvbmF0ZT0nY2hyb21lMTMxJyxcXG4gICAgKVxcblxcbiAgICBjcmF3bGVyID0gUGFyc2VsQ3Jhd2xlcihcXG4gICAgICAgIGh0dHBfY2xpZW50PWh0dHBfY2xpZW50LFxcbiAgICAgICAgIyBMaW1pdCB0aGUgY3Jhd2wgdG8gbWF4IHJlcXVlc3RzLiBSZW1vdmUgb3IgaW5jcmVhc2UgaXQgZm9yIGNyYXdsaW5nIGFsbCBsaW5rcy5cXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsXFxuICAgIClcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IFBhcnNlbENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm9jZXNzaW5nIHtjb250ZXh0LnJlcXVlc3QudXJsfSAuLi4nKVxcblxcbiAgICAgICAgIyBFbnF1ZXVlIGFsbCBsaW5rcyBmcm9tIHRoZSBwYWdlLlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5lbnF1ZXVlX2xpbmtzKClcXG5cXG4gICAgICAgICMgRXh0cmFjdCBkYXRhIGZyb20gdGhlIHBhZ2UuXFxuICAgICAgICBkYXRhID0ge1xcbiAgICAgICAgICAgICd1cmwnOiBjb250ZXh0LnJlcXVlc3QudXJsLFxcbiAgICAgICAgICAgICd0aXRsZSc6IGNvbnRleHQuc2VsZWN0b3IuY3NzKCd0aXRsZTo6dGV4dCcpLmdldCgpLFxcbiAgICAgICAgfVxcblxcbiAgICAgICAgIyBQdXNoIHRoZSBleHRyYWN0ZWQgZGF0YSB0byB0aGUgZGVmYXVsdCBkYXRhc2V0LlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5wdXNoX2RhdGEoZGF0YSlcXG5cXG4gICAgIyBSdW4gdGhlIGNyYXdsZXIgd2l0aCB0aGUgaW5pdGlhbCBsaXN0IG9mIFVSTHMuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9jcmF3bGVlLmRldiddKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.xGfUoZvDFliQspV4LkJoE3RLkSxRjhvvFB581gBnEIA\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import ParselCrawler, ParselCrawlingContext
from crawlee.http_clients import CurlImpersonateHttpClient


async def main() -> None:
    http_client = CurlImpersonateHttpClient(
        # Optional additional keyword arguments for `curl_cffi.requests.AsyncSession`.
        timeout=10,
        impersonate='chrome131',
    )

    crawler = ParselCrawler(
        http_client=http_client,
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
    )

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: ParselCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Enqueue all links from the page.
        await context.enqueue_links()

        # Extract data from the page.
        data = {
            'url': context.request.url,
            'title': context.selector.css('title::text').get(),
        }

        # Push the extracted data to the default dataset.
        await context.push_data(data)

    # Run the crawler with the initial list of URLs.
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQYXJzZWxDcmF3bGVyLCBQYXJzZWxDcmF3bGluZ0NvbnRleHRcXG5mcm9tIGNyYXdsZWUuaHR0cF9jbGllbnRzIGltcG9ydCBJbXBpdEh0dHBDbGllbnRcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgIGh0dHBfY2xpZW50ID0gSW1waXRIdHRwQ2xpZW50KFxcbiAgICAgICAgIyBPcHRpb25hbCBhZGRpdGlvbmFsIGtleXdvcmQgYXJndW1lbnRzIGZvciBgaW1waXQuQXN5bmNDbGllbnRgLlxcbiAgICAgICAgaHR0cDM9VHJ1ZSxcXG4gICAgICAgIGJyb3dzZXI9J2ZpcmVmb3gnLFxcbiAgICAgICAgdmVyaWZ5PVRydWUsXFxuICAgIClcXG5cXG4gICAgY3Jhd2xlciA9IFBhcnNlbENyYXdsZXIoXFxuICAgICAgICBodHRwX2NsaWVudD1odHRwX2NsaWVudCxcXG4gICAgICAgICMgTGltaXQgdGhlIGNyYXdsIHRvIG1heCByZXF1ZXN0cy4gUmVtb3ZlIG9yIGluY3JlYXNlIGl0IGZvciBjcmF3bGluZyBhbGwgbGlua3MuXFxuICAgICAgICBtYXhfcmVxdWVzdHNfcGVyX2NyYXdsPTEwLFxcbiAgICApXFxuXFxuICAgICMgRGVmaW5lIHRoZSBkZWZhdWx0IHJlcXVlc3QgaGFuZGxlciwgd2hpY2ggd2lsbCBiZSBjYWxsZWQgZm9yIGV2ZXJ5IHJlcXVlc3QuXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIHJlcXVlc3RfaGFuZGxlcihjb250ZXh0OiBQYXJzZWxDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgICAgICMgRW5xdWV1ZSBhbGwgbGlua3MgZnJvbSB0aGUgcGFnZS5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQuZW5xdWV1ZV9saW5rcygpXFxuXFxuICAgICAgICAjIEV4dHJhY3QgZGF0YSBmcm9tIHRoZSBwYWdlLlxcbiAgICAgICAgZGF0YSA9IHtcXG4gICAgICAgICAgICAndXJsJzogY29udGV4dC5yZXF1ZXN0LnVybCxcXG4gICAgICAgICAgICAndGl0bGUnOiBjb250ZXh0LnNlbGVjdG9yLmNzcygndGl0bGU6OnRleHQnKS5nZXQoKSxcXG4gICAgICAgIH1cXG5cXG4gICAgICAgICMgUHVzaCB0aGUgZXh0cmFjdGVkIGRhdGEgdG8gdGhlIGRlZmF1bHQgZGF0YXNldC5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQucHVzaF9kYXRhKGRhdGEpXFxuXFxuICAgICMgUnVuIHRoZSBjcmF3bGVyIHdpdGggdGhlIGluaXRpYWwgbGlzdCBvZiBVUkxzLlxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vY3Jhd2xlZS5kZXYnXSlcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6MTAyNCwidGltZW91dCI6MTgwfX0.AWZhtbHdvXd9ijyjFLp0PmvfdM1OcFIVjWrTjCJOFSA\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import ParselCrawler, ParselCrawlingContext
from crawlee.http_clients import ImpitHttpClient


async def main() -> None:
    http_client = ImpitHttpClient(
        # Optional additional keyword arguments for `impit.AsyncClient`.
        http3=True,
        browser='firefox',
        verify=True,
    )

    crawler = ParselCrawler(
        http_client=http_client,
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
    )

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: ParselCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Enqueue all links from the page.
        await context.enqueue_links()

        # Extract data from the page.
        data = {
            'url': context.request.url,
            'title': context.selector.css('title::text').get(),
        }

        # Push the extracted data to the default dataset.
        await context.push_data(data)

    # Run the crawler with the initial list of URLs.
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

## Installation requirements[​](#installation-requirements "Direct link to Installation requirements")

Since [`ImpitHttpClient`](https://crawlee.dev/python/python/api/class/ImpitHttpClient.md) is the default HTTP client, it's included with the base Crawlee installation and requires no additional packages.

For [`CurlImpersonateHttpClient`](https://crawlee.dev/python/python/api/class/CurlImpersonateHttpClient.md), you need to install Crawlee with the `curl-impersonate` extra:

```
python -m pip install 'crawlee[curl-impersonate]'
```

For [`HttpxHttpClient`](https://crawlee.dev/python/python/api/class/HttpxHttpClient.md), you need to install Crawlee with the `httpx` extra:

```
python -m pip install 'crawlee[httpx]'
```

Alternatively, you can install all available extras to get access to all HTTP clients and features:

```
python -m pip install 'crawlee[all]'
```

## Creating custom HTTP clients[​](#creating-custom-http-clients "Direct link to Creating custom HTTP clients")

Crawlee provides an abstract base class, [`HttpClient`](https://crawlee.dev/python/python/api/class/HttpClient.md), which defines the interface that all HTTP clients must implement. This allows you to create custom HTTP clients tailored to your specific requirements.

HTTP clients are responsible for several key operations:

* sending HTTP requests and receiving responses,
* managing cookies and sessions,
* handling headers and authentication,
* managing proxy configurations,
* connection pooling with timeout management.

To create a custom HTTP client, you need to inherit from the [`HttpClient`](https://crawlee.dev/python/python/api/class/HttpClient.md) base class and implement all required abstract methods. Your implementation must be async-compatible and include proper cleanup and resource management to work seamlessly with Crawlee's concurrent processing model.

## Conclusion[​](#conclusion "Direct link to Conclusion")

This guide introduced you to the HTTP clients available in Crawlee and demonstrated how to switch between them, including their installation requirements and usage examples. You also learned about the responsibilities of HTTP clients and how to implement your own custom HTTP client by inheriting from the [`HttpClient`](https://crawlee.dev/python/python/api/class/HttpClient.md) base class.

If you have questions or need assistance, feel free to reach out on our [GitHub](https://github.com/apify/crawlee-python) or join our [Discord community](https://discord.com/invite/jyEM2PRvMU). Happy scraping!

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/guides/http_clients.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/guides/error-handling.md)

[Error handling](https://crawlee.dev/python/python/docs/guides/error-handling.md)

[Next](https://crawlee.dev/python/python/docs/guides/http-crawlers.md)

[HTTP crawlers](https://crawlee.dev/python/python/docs/guides/http-crawlers.md)


---

* [](https://crawlee.dev/python/python)
* [Guides](https://crawlee.dev/python/python/docs/guides.md)
* HTTP crawlers

Version: 1.6

On this page

# HTTP crawlers

HTTP crawlers are ideal for extracting data from server-rendered websites that don't require JavaScript execution. These crawlers make requests via HTTP clients to fetch HTML content and then parse it using various parsing libraries. For client-side rendered content, where you need to execute JavaScript consider using [Playwright crawler](https://crawlee.dev/python/python/docs/guides/playwright-crawler.md) instead.

## Overview[​](#overview "Direct link to Overview")

All HTTP crawlers share a common architecture built around the [`AbstractHttpCrawler`](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md) base class. The main differences lie in the parsing strategy and the context provided to request handlers. There are [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md), [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md), and [`HttpCrawler`](https://crawlee.dev/python/python/api/class/HttpCrawler.md). It can also be extended to create custom crawlers with specialized parsing requirements. They use HTTP clients to fetch page content and parsing libraries to extract data from the HTML, check out the [HTTP clients guide](https://crawlee.dev/python/python/docs/guides/http-clients.md) to learn about the HTTP clients used by these crawlers, how to switch between them, and how to create custom HTTP clients tailored to your specific requirements.

<!-- -->

## BeautifulSoupCrawler[​](#beautifulsoupcrawler "Direct link to BeautifulSoupCrawler")

The [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md) uses the [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/) library for HTML parsing. It provides fault-tolerant parsing that handles malformed HTML, automatic character encoding detection, and supports CSS selectors, tag navigation, and custom search functions. Use this crawler when working with imperfect HTML structures, when you prefer BeautifulSoup's intuitive API, or when prototyping web scraping solutions.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBDcmVhdGUgYSBCZWF1dGlmdWxTb3VwQ3Jhd2xlciBpbnN0YW5jZVxcbiAgICBjcmF3bGVyID0gQmVhdXRpZnVsU291cENyYXdsZXIoXFxuICAgICAgICAjIExpbWl0IHRoZSBjcmF3bCB0byAxMCByZXF1ZXN0c1xcbiAgICAgICAgbWF4X3JlcXVlc3RzX3Blcl9jcmF3bD0xMCxcXG4gICAgKVxcblxcbiAgICAjIERlZmluZSB0aGUgZGVmYXVsdCByZXF1ZXN0IGhhbmRsZXJcXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0nKVxcblxcbiAgICAgICAgIyBFeHRyYWN0IGRhdGEgdXNpbmcgQmVhdXRpZnVsU291cFxcbiAgICAgICAgZGF0YSA9IHtcXG4gICAgICAgICAgICAndXJsJzogY29udGV4dC5yZXF1ZXN0LnVybCxcXG4gICAgICAgICAgICAndGl0bGUnOiBjb250ZXh0LnNvdXAudGl0bGUuc3RyaW5nIGlmIGNvbnRleHQuc291cC50aXRsZSBlbHNlIE5vbmUsXFxuICAgICAgICB9XFxuXFxuICAgICAgICAjIFB1c2ggZXh0cmFjdGVkIGRhdGEgdG8gdGhlIGRhdGFzZXRcXG4gICAgICAgIGF3YWl0IGNvbnRleHQucHVzaF9kYXRhKGRhdGEpXFxuXFxuICAgICAgICAjIEVucXVldWUgbGlua3MgZm91bmQgb24gdGhlIHBhZ2UgZm9yIGZ1cnRoZXIgY3Jhd2xpbmdcXG4gICAgICAgIGF3YWl0IGNvbnRleHQuZW5xdWV1ZV9saW5rcygpXFxuXFxuICAgICMgUnVuIHRoZSBjcmF3bGVyXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9jcmF3bGVlLmRldiddKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.qAMYVdW9wPVErdMU9sTZA89XCv6QZmj-vd2_mPjfFU4\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


async def main() -> None:
    # Create a BeautifulSoupCrawler instance
    crawler = BeautifulSoupCrawler(
        # Limit the crawl to 10 requests
        max_requests_per_crawl=10,
    )

    # Define the default request handler
    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url}')

        # Extract data using BeautifulSoup
        data = {
            'url': context.request.url,
            'title': context.soup.title.string if context.soup.title else None,
        }

        # Push extracted data to the dataset
        await context.push_data(data)

        # Enqueue links found on the page for further crawling
        await context.enqueue_links()

    # Run the crawler
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

## ParselCrawler[​](#parselcrawler "Direct link to ParselCrawler")

The [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md) uses the [Parsel](https://parsel.readthedocs.io/) library, which provides XPath 1.0 and CSS selector support built on `lxml` for high performance. It includes built-in regex support for pattern matching, proper XML namespace handling, and offers better performance than BeautifulSoup while maintaining a clean API. Use this crawler when you need XPath functionality, require high-performance parsing, or need to extract data using regular expressions.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQYXJzZWxDcmF3bGVyLCBQYXJzZWxDcmF3bGluZ0NvbnRleHRcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgICMgQ3JlYXRlIGEgUGFyc2VsQ3Jhd2xlciBpbnN0YW5jZVxcbiAgICBjcmF3bGVyID0gUGFyc2VsQ3Jhd2xlcihcXG4gICAgICAgICMgTGltaXQgdGhlIGNyYXdsIHRvIDEwIHJlcXVlc3RzXFxuICAgICAgICBtYXhfcmVxdWVzdHNfcGVyX2NyYXdsPTEwLFxcbiAgICApXFxuXFxuICAgICMgRGVmaW5lIHRoZSBkZWZhdWx0IHJlcXVlc3QgaGFuZGxlclxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiByZXF1ZXN0X2hhbmRsZXIoY29udGV4dDogUGFyc2VsQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ1Byb2Nlc3Npbmcge2NvbnRleHQucmVxdWVzdC51cmx9JylcXG5cXG4gICAgICAgICMgRXh0cmFjdCBkYXRhIHVzaW5nIFBhcnNlbCdzIFhQYXRoIGFuZCBDU1Mgc2VsZWN0b3JzXFxuICAgICAgICBkYXRhID0ge1xcbiAgICAgICAgICAgICd1cmwnOiBjb250ZXh0LnJlcXVlc3QudXJsLFxcbiAgICAgICAgICAgICd0aXRsZSc6IGNvbnRleHQuc2VsZWN0b3IueHBhdGgoJy8vdGl0bGUvdGV4dCgpJykuZ2V0KCksXFxuICAgICAgICB9XFxuXFxuICAgICAgICAjIFB1c2ggZXh0cmFjdGVkIGRhdGEgdG8gdGhlIGRhdGFzZXRcXG4gICAgICAgIGF3YWl0IGNvbnRleHQucHVzaF9kYXRhKGRhdGEpXFxuXFxuICAgICAgICAjIEVucXVldWUgbGlua3MgZm91bmQgb24gdGhlIHBhZ2UgZm9yIGZ1cnRoZXIgY3Jhd2xpbmdcXG4gICAgICAgIGF3YWl0IGNvbnRleHQuZW5xdWV1ZV9saW5rcygpXFxuXFxuICAgICMgUnVuIHRoZSBjcmF3bGVyXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9jcmF3bGVlLmRldiddKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.rO-CUHkR6UqBNdmGMcEZ8cBkBEHjNdfYG9VRbF1ZNCc\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import ParselCrawler, ParselCrawlingContext


async def main() -> None:
    # Create a ParselCrawler instance
    crawler = ParselCrawler(
        # Limit the crawl to 10 requests
        max_requests_per_crawl=10,
    )

    # Define the default request handler
    @crawler.router.default_handler
    async def request_handler(context: ParselCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url}')

        # Extract data using Parsel's XPath and CSS selectors
        data = {
            'url': context.request.url,
            'title': context.selector.xpath('//title/text()').get(),
        }

        # Push extracted data to the dataset
        await context.push_data(data)

        # Enqueue links found on the page for further crawling
        await context.enqueue_links()

    # Run the crawler
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

## HttpCrawler[​](#httpcrawler "Direct link to HttpCrawler")

The [`HttpCrawler`](https://crawlee.dev/python/python/api/class/HttpCrawler.md) provides direct access to HTTP response body and headers without automatic parsing, offering maximum performance with no parsing overhead. It supports any content type (JSON, XML, binary) and allows complete control over response processing, including memory-efficient handling of large responses. Use this crawler when working with non-HTML content, requiring maximum performance, implementing custom parsing logic, or needing access to raw response data.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuaW1wb3J0IHJlXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBIdHRwQ3Jhd2xlciwgSHR0cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBDcmVhdGUgYW4gSHR0cENyYXdsZXIgaW5zdGFuY2UgLSBubyBhdXRvbWF0aWMgcGFyc2luZ1xcbiAgICBjcmF3bGVyID0gSHR0cENyYXdsZXIoXFxuICAgICAgICAjIExpbWl0IHRoZSBjcmF3bCB0byAxMCByZXF1ZXN0c1xcbiAgICAgICAgbWF4X3JlcXVlc3RzX3Blcl9jcmF3bD0xMCxcXG4gICAgKVxcblxcbiAgICAjIERlZmluZSB0aGUgZGVmYXVsdCByZXF1ZXN0IGhhbmRsZXJcXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IEh0dHBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0nKVxcblxcbiAgICAgICAgIyBHZXQgdGhlIHJhdyByZXNwb25zZSBjb250ZW50XFxuICAgICAgICByZXNwb25zZV9ib2R5ID0gYXdhaXQgY29udGV4dC5odHRwX3Jlc3BvbnNlLnJlYWQoKVxcbiAgICAgICAgcmVzcG9uc2VfdGV4dCA9IHJlc3BvbnNlX2JvZHkuZGVjb2RlKCd1dGYtOCcpXFxuXFxuICAgICAgICAjIEV4dHJhY3QgdGl0bGUgbWFudWFsbHkgdXNpbmcgcmVnZXggKHNpbmNlIHdlIGRvbid0IGhhdmUgYSBwYXJzZXIpXFxuICAgICAgICB0aXRsZV9tYXRjaCA9IHJlLnNlYXJjaChcXG4gICAgICAgICAgICByJzx0aXRsZVtePl0qPihbXjxdKyk8L3RpdGxlPicsIHJlc3BvbnNlX3RleHQsIHJlLklHTk9SRUNBU0VcXG4gICAgICAgIClcXG4gICAgICAgIHRpdGxlID0gdGl0bGVfbWF0Y2guZ3JvdXAoMSkuc3RyaXAoKSBpZiB0aXRsZV9tYXRjaCBlbHNlIE5vbmVcXG5cXG4gICAgICAgICMgRXh0cmFjdCBiYXNpYyBpbmZvcm1hdGlvblxcbiAgICAgICAgZGF0YSA9IHtcXG4gICAgICAgICAgICAndXJsJzogY29udGV4dC5yZXF1ZXN0LnVybCxcXG4gICAgICAgICAgICAndGl0bGUnOiB0aXRsZSxcXG4gICAgICAgIH1cXG5cXG4gICAgICAgICMgUHVzaCBleHRyYWN0ZWQgZGF0YSB0byB0aGUgZGF0YXNldFxcbiAgICAgICAgYXdhaXQgY29udGV4dC5wdXNoX2RhdGEoZGF0YSlcXG5cXG4gICAgICAgICMgU2ltcGxlIGxpbmsgZXh0cmFjdGlvbiBmb3IgZnVydGhlciBjcmF3bGluZ1xcbiAgICAgICAgaHJlZl9wYXR0ZXJuID0gcidocmVmPVtcXFwiXFxcXCddKFteXFxcIlxcXFwnXSspW1xcXCJcXFxcJ10nXFxuICAgICAgICBtYXRjaGVzID0gcmUuZmluZGFsbChocmVmX3BhdHRlcm4sIHJlc3BvbnNlX3RleHQsIHJlLklHTk9SRUNBU0UpXFxuXFxuICAgICAgICAjIEVucXVldWUgZmlyc3QgZmV3IGxpbmtzIGZvdW5kIChsaW1pdCB0byBhdm9pZCB0b28gbWFueSByZXF1ZXN0cylcXG4gICAgICAgIGZvciBocmVmIGluIG1hdGNoZXNbOjNdOlxcbiAgICAgICAgICAgIGlmIGhyZWYuc3RhcnRzd2l0aCgnaHR0cCcpIGFuZCAnY3Jhd2xlZS5kZXYnIGluIGhyZWY6XFxuICAgICAgICAgICAgICAgIGF3YWl0IGNvbnRleHQuYWRkX3JlcXVlc3RzKFtocmVmXSlcXG5cXG4gICAgIyBSdW4gdGhlIGNyYXdsZXJcXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2NyYXdsZWUuZGV2J10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.q1ejL-3xTUHHOTt6_aYK8di7CreyzV0stFUCVZEwfVI\&asrc=run_on_apify)

```
import asyncio
import re

from crawlee.crawlers import HttpCrawler, HttpCrawlingContext


async def main() -> None:
    # Create an HttpCrawler instance - no automatic parsing
    crawler = HttpCrawler(
        # Limit the crawl to 10 requests
        max_requests_per_crawl=10,
    )

    # Define the default request handler
    @crawler.router.default_handler
    async def request_handler(context: HttpCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url}')

        # Get the raw response content
        response_body = await context.http_response.read()
        response_text = response_body.decode('utf-8')

        # Extract title manually using regex (since we don't have a parser)
        title_match = re.search(
            r'<title[^>]*>([^<]+)</title>', response_text, re.IGNORECASE
        )
        title = title_match.group(1).strip() if title_match else None

        # Extract basic information
        data = {
            'url': context.request.url,
            'title': title,
        }

        # Push extracted data to the dataset
        await context.push_data(data)

        # Simple link extraction for further crawling
        href_pattern = r'href=["\']([^"\']+)["\']'
        matches = re.findall(href_pattern, response_text, re.IGNORECASE)

        # Enqueue first few links found (limit to avoid too many requests)
        for href in matches[:3]:
            if href.startswith('http') and 'crawlee.dev' in href:
                await context.add_requests([href])

    # Run the crawler
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

### Using custom parsers[​](#using-custom-parsers "Direct link to Using custom parsers")

Since [`HttpCrawler`](https://crawlee.dev/python/python/api/class/HttpCrawler.md) provides raw HTTP responses, you can integrate any parsing library. Note that helpers like [`enqueue_links`](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md) and [`extract_links`](https://crawlee.dev/python/python/api/class/ExtractLinksFunction.md) are not available with this approach.

The following examples demonstrate how to integrate with several popular parsing libraries, including [lxml](https://lxml.de/) (high-performance parsing with XPath 1.0), [lxml with SaxonC-HE](https://pypi.org/project/saxonche/) (XPath 3.1 support), [selectolax](https://github.com/rushter/selectolax) (high-speed CSS selectors), [PyQuery](https://pyquery.readthedocs.io/) (jQuery-like syntax), and [scrapling](https://github.com/D4Vinci/Scrapling) (a Scrapy/Parsel-style API offering BeautifulSoup-like methods).

* lxml
* lxml with SaxonC-HE
* selectolax
* PyQuery
* Scrapling

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBseG1sIGltcG9ydCBodG1sXFxuZnJvbSBweWRhbnRpYyBpbXBvcnQgVmFsaWRhdGlvbkVycm9yXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBSZXF1ZXN0XFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBIdHRwQ3Jhd2xlciwgSHR0cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IEh0dHBDcmF3bGVyKFxcbiAgICAgICAgbWF4X3JlcXVlc3RfcmV0cmllcz0xLFxcbiAgICAgICAgbWF4X3JlcXVlc3RzX3Blcl9jcmF3bD0xMCxcXG4gICAgKVxcblxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiByZXF1ZXN0X2hhbmRsZXIoY29udGV4dDogSHR0cENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm9jZXNzaW5nIHtjb250ZXh0LnJlcXVlc3QudXJsfSAuLi4nKVxcblxcbiAgICAgICAgIyBQYXJzZSB0aGUgSFRNTCBjb250ZW50IHVzaW5nIGx4bWwuXFxuICAgICAgICBwYXJzZWRfaHRtbCA9IGh0bWwuZnJvbXN0cmluZyhhd2FpdCBjb250ZXh0Lmh0dHBfcmVzcG9uc2UucmVhZCgpKVxcblxcbiAgICAgICAgIyBFeHRyYWN0IGRhdGEgZnJvbSB0aGUgcGFnZS5cXG4gICAgICAgIGRhdGEgPSB7XFxuICAgICAgICAgICAgJ3VybCc6IGNvbnRleHQucmVxdWVzdC51cmwsXFxuICAgICAgICAgICAgJ3RpdGxlJzogcGFyc2VkX2h0bWwuZmluZHRleHQoJy4vL3RpdGxlJyksXFxuICAgICAgICAgICAgJ2gxcyc6IFtoMS50ZXh0X2NvbnRlbnQoKSBmb3IgaDEgaW4gcGFyc2VkX2h0bWwuZmluZGFsbCgnLi8vaDEnKV0sXFxuICAgICAgICAgICAgJ2gycyc6IFtoMi50ZXh0X2NvbnRlbnQoKSBmb3IgaDIgaW4gcGFyc2VkX2h0bWwuZmluZGFsbCgnLi8vaDInKV0sXFxuICAgICAgICAgICAgJ2gzcyc6IFtoMy50ZXh0X2NvbnRlbnQoKSBmb3IgaDMgaW4gcGFyc2VkX2h0bWwuZmluZGFsbCgnLi8vaDMnKV0sXFxuICAgICAgICB9XFxuICAgICAgICBhd2FpdCBjb250ZXh0LnB1c2hfZGF0YShkYXRhKVxcblxcbiAgICAgICAgIyBDb252ZXJ0IHJlbGF0aXZlIFVSTHMgdG8gYWJzb2x1dGUgYmVmb3JlIGV4dHJhY3RpbmcgbGlua3MuXFxuICAgICAgICBwYXJzZWRfaHRtbC5tYWtlX2xpbmtzX2Fic29sdXRlKGNvbnRleHQucmVxdWVzdC51cmwsIHJlc29sdmVfYmFzZV9ocmVmPVRydWUpXFxuXFxuICAgICAgICAjIFhwYXRoIDEuMCBzZWxlY3RvciBmb3IgZXh0cmFjdGluZyB2YWxpZCBocmVmIGF0dHJpYnV0ZXMuXFxuICAgICAgICBsaW5rc194cGF0aCA9IChcXG4gICAgICAgICAgICAnLy9hL0BocmVmW25vdChzdGFydHMtd2l0aCguLCBcXFwiI1xcXCIpKSAnXFxuICAgICAgICAgICAgJ2FuZCBub3Qoc3RhcnRzLXdpdGgoLiwgXFxcImphdmFzY3JpcHQ6XFxcIikpICdcXG4gICAgICAgICAgICAnYW5kIG5vdChzdGFydHMtd2l0aCguLCBcXFwibWFpbHRvOlxcXCIpKV0nXFxuICAgICAgICApXFxuXFxuICAgICAgICBleHRyYWN0ZWRfcmVxdWVzdHMgPSBbXVxcblxcbiAgICAgICAgIyBFeHRyYWN0IGxpbmtzLlxcbiAgICAgICAgZm9yIHVybCBpbiBwYXJzZWRfaHRtbC54cGF0aChsaW5rc194cGF0aCk6XFxuICAgICAgICAgICAgdHJ5OlxcbiAgICAgICAgICAgICAgICByZXF1ZXN0ID0gUmVxdWVzdC5mcm9tX3VybCh1cmwpXFxuICAgICAgICAgICAgZXhjZXB0IFZhbGlkYXRpb25FcnJvciBhcyBleGM6XFxuICAgICAgICAgICAgICAgIGNvbnRleHQubG9nLndhcm5pbmcoZidTa2lwcGluZyBpbnZhbGlkIFVSTCBcXFwie3VybH1cXFwiOiB7ZXhjfScpXFxuICAgICAgICAgICAgICAgIGNvbnRpbnVlXFxuICAgICAgICAgICAgZXh0cmFjdGVkX3JlcXVlc3RzLmFwcGVuZChyZXF1ZXN0KVxcblxcbiAgICAgICAgIyBBZGQgZXh0cmFjdGVkIHJlcXVlc3RzIHRvIHRoZSBxdWV1ZSB3aXRoIHRoZSBzYW1lLWRvbWFpbiBzdHJhdGVneS5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQuYWRkX3JlcXVlc3RzKGV4dHJhY3RlZF9yZXF1ZXN0cywgc3RyYXRlZ3k9J3NhbWUtZG9tYWluJylcXG5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2NyYXdsZWUuZGV2J10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.F0mTlHpK3XR5JjB6no2nuCuYuDbrk7SBPrDCWB4hgUc\&asrc=run_on_apify)

```
import asyncio

from lxml import html
from pydantic import ValidationError

from crawlee import Request
from crawlee.crawlers import HttpCrawler, HttpCrawlingContext


async def main() -> None:
    crawler = HttpCrawler(
        max_request_retries=1,
        max_requests_per_crawl=10,
    )

    @crawler.router.default_handler
    async def request_handler(context: HttpCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Parse the HTML content using lxml.
        parsed_html = html.fromstring(await context.http_response.read())

        # Extract data from the page.
        data = {
            'url': context.request.url,
            'title': parsed_html.findtext('.//title'),
            'h1s': [h1.text_content() for h1 in parsed_html.findall('.//h1')],
            'h2s': [h2.text_content() for h2 in parsed_html.findall('.//h2')],
            'h3s': [h3.text_content() for h3 in parsed_html.findall('.//h3')],
        }
        await context.push_data(data)

        # Convert relative URLs to absolute before extracting links.
        parsed_html.make_links_absolute(context.request.url, resolve_base_href=True)

        # Xpath 1.0 selector for extracting valid href attributes.
        links_xpath = (
            '//a/@href[not(starts-with(., "#")) '
            'and not(starts-with(., "javascript:")) '
            'and not(starts-with(., "mailto:"))]'
        )

        extracted_requests = []

        # Extract links.
        for url in parsed_html.xpath(links_xpath):
            try:
                request = Request.from_url(url)
            except ValidationError as exc:
                context.log.warning(f'Skipping invalid URL "{url}": {exc}')
                continue
            extracted_requests.append(request)

        # Add extracted requests to the queue with the same-domain strategy.
        await context.add_requests(extracted_requests, strategy='same-domain')

    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBseG1sIGltcG9ydCBodG1sXFxuZnJvbSBweWRhbnRpYyBpbXBvcnQgVmFsaWRhdGlvbkVycm9yXFxuZnJvbSBzYXhvbmNoZSBpbXBvcnQgUHlTYXhvblByb2Nlc3NvclxcblxcbmZyb20gY3Jhd2xlZSBpbXBvcnQgUmVxdWVzdFxcbmZyb20gY3Jhd2xlZS5jcmF3bGVycyBpbXBvcnQgSHR0cENyYXdsZXIsIEh0dHBDcmF3bGluZ0NvbnRleHRcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgIGNyYXdsZXIgPSBIdHRwQ3Jhd2xlcihcXG4gICAgICAgIG1heF9yZXF1ZXN0X3JldHJpZXM9MSxcXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsXFxuICAgIClcXG5cXG4gICAgIyBDcmVhdGUgU2F4b24gcHJvY2Vzc29yIG9uY2UgYW5kIHJldXNlIGFjcm9zcyByZXF1ZXN0cy5cXG4gICAgc2F4b25fcHJvYyA9IFB5U2F4b25Qcm9jZXNzb3IobGljZW5zZT1GYWxzZSlcXG4gICAgeHBhdGhfcHJvYyA9IHNheG9uX3Byb2MubmV3X3hwYXRoX3Byb2Nlc3NvcigpXFxuXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIHJlcXVlc3RfaGFuZGxlcihjb250ZXh0OiBIdHRwQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ1Byb2Nlc3Npbmcge2NvbnRleHQucmVxdWVzdC51cmx9IC4uLicpXFxuXFxuICAgICAgICAjIFBhcnNlIEhUTUwgd2l0aCBseG1sLlxcbiAgICAgICAgcGFyc2VkX2h0bWwgPSBodG1sLmZyb21zdHJpbmcoYXdhaXQgY29udGV4dC5odHRwX3Jlc3BvbnNlLnJlYWQoKSlcXG4gICAgICAgICMgQ29udmVydCByZWxhdGl2ZSBVUkxzIHRvIGFic29sdXRlIGJlZm9yZSBleHRyYWN0aW5nIGxpbmtzLlxcbiAgICAgICAgcGFyc2VkX2h0bWwubWFrZV9saW5rc19hYnNvbHV0ZShjb250ZXh0LnJlcXVlc3QudXJsLCByZXNvbHZlX2Jhc2VfaHJlZj1UcnVlKVxcbiAgICAgICAgIyBDb252ZXJ0IHBhcnNlZCBIVE1MIHRvIFhNTCBmb3IgU2F4b24gcHJvY2Vzc2luZy5cXG4gICAgICAgIHhtbCA9IGh0bWwudG9zdHJpbmcocGFyc2VkX2h0bWwsIGVuY29kaW5nPSd1bmljb2RlJywgbWV0aG9kPSd4bWwnKVxcbiAgICAgICAgIyBQYXJzZSBYTUwgd2l0aCBTYXhvbi5cXG4gICAgICAgIHBhcnNlZF94bWwgPSBzYXhvbl9wcm9jLnBhcnNlX3htbCh4bWxfdGV4dD14bWwpXFxuICAgICAgICAjIFNldCB0aGUgcGFyc2VkIGNvbnRleHQgZm9yIFhQYXRoIGV2YWx1YXRpb24uXFxuICAgICAgICB4cGF0aF9wcm9jLnNldF9jb250ZXh0KHhkbV9pdGVtPXBhcnNlZF94bWwpXFxuXFxuICAgICAgICAjIEV4dHJhY3QgZGF0YSB1c2luZyBYUGF0aCAyLjAgc3RyaW5nKCkgZnVuY3Rpb24uXFxuICAgICAgICBkYXRhID0ge1xcbiAgICAgICAgICAgICd1cmwnOiBjb250ZXh0LnJlcXVlc3QudXJsLFxcbiAgICAgICAgICAgICd0aXRsZSc6IHhwYXRoX3Byb2MuZXZhbHVhdGVfc2luZ2xlKCcuLy90aXRsZS9zdHJpbmcoKScpLFxcbiAgICAgICAgICAgICdoMXMnOiBbc3RyKGgpIGZvciBoIGluICh4cGF0aF9wcm9jLmV2YWx1YXRlKCcvL2gxL3N0cmluZygpJykgb3IgW10pXSxcXG4gICAgICAgICAgICAnaDJzJzogW3N0cihoKSBmb3IgaCBpbiAoeHBhdGhfcHJvYy5ldmFsdWF0ZSgnLy9oMi9zdHJpbmcoKScpIG9yIFtdKV0sXFxuICAgICAgICAgICAgJ2gzcyc6IFtzdHIoaCkgZm9yIGggaW4gKHhwYXRoX3Byb2MuZXZhbHVhdGUoJy8vaDMvc3RyaW5nKCknKSBvciBbXSldLFxcbiAgICAgICAgfVxcbiAgICAgICAgYXdhaXQgY29udGV4dC5wdXNoX2RhdGEoZGF0YSlcXG5cXG4gICAgICAgICMgWFBhdGggMi4wIHdpdGggZGlzdGluY3QtdmFsdWVzKCkgdG8gZ2V0IHVuaXF1ZSBsaW5rcyBhbmQgcmVtb3ZlIGZyYWdtZW50cy5cXG4gICAgICAgIGxpbmtzX3hwYXRoID0gXFxcIlxcXCJcXFwiXFxuICAgICAgICAgICAgZGlzdGluY3QtdmFsdWVzKFxcbiAgICAgICAgICAgICAgICBmb3IgJGhyZWYgaW4gLy9hL0BocmVmW1xcbiAgICAgICAgICAgICAgICAgICAgbm90KHN0YXJ0cy13aXRoKC4sIFxcXCIjXFxcIikpXFxuICAgICAgICAgICAgICAgICAgICBhbmQgbm90KHN0YXJ0cy13aXRoKC4sIFxcXCJqYXZhc2NyaXB0OlxcXCIpKVxcbiAgICAgICAgICAgICAgICAgICAgYW5kIG5vdChzdGFydHMtd2l0aCguLCBcXFwibWFpbHRvOlxcXCIpKVxcbiAgICAgICAgICAgICAgICBdXFxuICAgICAgICAgICAgICAgIHJldHVybiByZXBsYWNlKCRocmVmLCBcXFwiIy4qJFxcXCIsIFxcXCJcXFwiKVxcbiAgICAgICAgICAgIClcXG4gICAgICAgIFxcXCJcXFwiXFxcIlxcblxcbiAgICAgICAgZXh0cmFjdGVkX3JlcXVlc3RzID0gW11cXG5cXG4gICAgICAgICMgRXh0cmFjdCBsaW5rcy5cXG4gICAgICAgIGZvciBpdGVtIGluIHhwYXRoX3Byb2MuZXZhbHVhdGUobGlua3NfeHBhdGgpIG9yIFtdOlxcbiAgICAgICAgICAgIHVybCA9IGl0ZW0uc3RyaW5nX3ZhbHVlXFxuICAgICAgICAgICAgdHJ5OlxcbiAgICAgICAgICAgICAgICByZXF1ZXN0ID0gUmVxdWVzdC5mcm9tX3VybCh1cmwpXFxuICAgICAgICAgICAgZXhjZXB0IFZhbGlkYXRpb25FcnJvciBhcyBleGM6XFxuICAgICAgICAgICAgICAgIGNvbnRleHQubG9nLndhcm5pbmcoZidTa2lwcGluZyBpbnZhbGlkIFVSTCBcXFwie3VybH1cXFwiOiB7ZXhjfScpXFxuICAgICAgICAgICAgICAgIGNvbnRpbnVlXFxuICAgICAgICAgICAgZXh0cmFjdGVkX3JlcXVlc3RzLmFwcGVuZChyZXF1ZXN0KVxcblxcbiAgICAgICAgIyBBZGQgZXh0cmFjdGVkIHJlcXVlc3RzIHRvIHRoZSBxdWV1ZSB3aXRoIHRoZSBzYW1lLWRvbWFpbiBzdHJhdGVneS5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQuYWRkX3JlcXVlc3RzKGV4dHJhY3RlZF9yZXF1ZXN0cywgc3RyYXRlZ3k9J3NhbWUtZG9tYWluJylcXG5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2NyYXdsZWUuZGV2J10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.UwrjVfCuCOBwNSREHrA90Jz91W_8CUc34yB44z8WXFI\&asrc=run_on_apify)

```
import asyncio

from lxml import html
from pydantic import ValidationError
from saxonche import PySaxonProcessor

from crawlee import Request
from crawlee.crawlers import HttpCrawler, HttpCrawlingContext


async def main() -> None:
    crawler = HttpCrawler(
        max_request_retries=1,
        max_requests_per_crawl=10,
    )

    # Create Saxon processor once and reuse across requests.
    saxon_proc = PySaxonProcessor(license=False)
    xpath_proc = saxon_proc.new_xpath_processor()

    @crawler.router.default_handler
    async def request_handler(context: HttpCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Parse HTML with lxml.
        parsed_html = html.fromstring(await context.http_response.read())
        # Convert relative URLs to absolute before extracting links.
        parsed_html.make_links_absolute(context.request.url, resolve_base_href=True)
        # Convert parsed HTML to XML for Saxon processing.
        xml = html.tostring(parsed_html, encoding='unicode', method='xml')
        # Parse XML with Saxon.
        parsed_xml = saxon_proc.parse_xml(xml_text=xml)
        # Set the parsed context for XPath evaluation.
        xpath_proc.set_context(xdm_item=parsed_xml)

        # Extract data using XPath 2.0 string() function.
        data = {
            'url': context.request.url,
            'title': xpath_proc.evaluate_single('.//title/string()'),
            'h1s': [str(h) for h in (xpath_proc.evaluate('//h1/string()') or [])],
            'h2s': [str(h) for h in (xpath_proc.evaluate('//h2/string()') or [])],
            'h3s': [str(h) for h in (xpath_proc.evaluate('//h3/string()') or [])],
        }
        await context.push_data(data)

        # XPath 2.0 with distinct-values() to get unique links and remove fragments.
        links_xpath = """
            distinct-values(
                for $href in //a/@href[
                    not(starts-with(., "#"))
                    and not(starts-with(., "javascript:"))
                    and not(starts-with(., "mailto:"))
                ]
                return replace($href, "#.*$", "")
            )
        """

        extracted_requests = []

        # Extract links.
        for item in xpath_proc.evaluate(links_xpath) or []:
            url = item.string_value
            try:
                request = Request.from_url(url)
            except ValidationError as exc:
                context.log.warning(f'Skipping invalid URL "{url}": {exc}')
                continue
            extracted_requests.append(request)

        # Add extracted requests to the queue with the same-domain strategy.
        await context.add_requests(extracted_requests, strategy='same-domain')

    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBweWRhbnRpYyBpbXBvcnQgVmFsaWRhdGlvbkVycm9yXFxuZnJvbSBzZWxlY3RvbGF4LmxleGJvciBpbXBvcnQgTGV4Ym9ySFRNTFBhcnNlclxcbmZyb20geWFybCBpbXBvcnQgVVJMXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBSZXF1ZXN0XFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBIdHRwQ3Jhd2xlciwgSHR0cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IEh0dHBDcmF3bGVyKFxcbiAgICAgICAgbWF4X3JlcXVlc3RfcmV0cmllcz0xLFxcbiAgICAgICAgbWF4X3JlcXVlc3RzX3Blcl9jcmF3bD0xMCxcXG4gICAgKVxcblxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiByZXF1ZXN0X2hhbmRsZXIoY29udGV4dDogSHR0cENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm9jZXNzaW5nIHtjb250ZXh0LnJlcXVlc3QudXJsfSAuLi4nKVxcblxcbiAgICAgICAgIyBQYXJzZSB0aGUgSFRNTCBjb250ZW50IHVzaW5nIFNlbGVjdG9sYXggd2l0aCBMZXhib3IgYmFja2VuZC5cXG4gICAgICAgIHBhcnNlZF9odG1sID0gTGV4Ym9ySFRNTFBhcnNlcihhd2FpdCBjb250ZXh0Lmh0dHBfcmVzcG9uc2UucmVhZCgpKVxcblxcbiAgICAgICAgIyBFeHRyYWN0IGRhdGEgZnJvbSB0aGUgcGFnZS5cXG4gICAgICAgIGRhdGEgPSB7XFxuICAgICAgICAgICAgJ3VybCc6IGNvbnRleHQucmVxdWVzdC51cmwsXFxuICAgICAgICAgICAgJ3RpdGxlJzogcGFyc2VkX2h0bWwuY3NzX2ZpcnN0KCd0aXRsZScpLnRleHQoKSxcXG4gICAgICAgICAgICAnaDFzJzogW2gxLnRleHQoKSBmb3IgaDEgaW4gcGFyc2VkX2h0bWwuY3NzKCdoMScpXSxcXG4gICAgICAgICAgICAnaDJzJzogW2gyLnRleHQoKSBmb3IgaDIgaW4gcGFyc2VkX2h0bWwuY3NzKCdoMicpXSxcXG4gICAgICAgICAgICAnaDNzJzogW2gzLnRleHQoKSBmb3IgaDMgaW4gcGFyc2VkX2h0bWwuY3NzKCdoMycpXSxcXG4gICAgICAgIH1cXG4gICAgICAgIGF3YWl0IGNvbnRleHQucHVzaF9kYXRhKGRhdGEpXFxuXFxuICAgICAgICAjIENzcyBzZWxlY3RvciB0byBleHRyYWN0IHZhbGlkIGhyZWYgYXR0cmlidXRlcy5cXG4gICAgICAgIGxpbmtzX3NlbGVjdG9yID0gKFxcbiAgICAgICAgICAgICdhW2hyZWZdOm5vdChbaHJlZl49XFxcIiNcXFwiXSk6bm90KFtocmVmXj1cXFwiamF2YXNjcmlwdDpcXFwiXSk6bm90KFtocmVmXj1cXFwibWFpbHRvOlxcXCJdKSdcXG4gICAgICAgIClcXG4gICAgICAgIGJhc2VfdXJsID0gVVJMKGNvbnRleHQucmVxdWVzdC51cmwpXFxuICAgICAgICBleHRyYWN0ZWRfcmVxdWVzdHMgPSBbXVxcblxcbiAgICAgICAgIyBFeHRyYWN0IGxpbmtzLlxcbiAgICAgICAgZm9yIGl0ZW0gaW4gcGFyc2VkX2h0bWwuY3NzKGxpbmtzX3NlbGVjdG9yKTpcXG4gICAgICAgICAgICBocmVmID0gaXRlbS5hdHRyaWJ1dGVzLmdldCgnaHJlZicpXFxuICAgICAgICAgICAgaWYgbm90IGhyZWY6XFxuICAgICAgICAgICAgICAgIGNvbnRpbnVlXFxuXFxuICAgICAgICAgICAgIyBDb252ZXJ0IHJlbGF0aXZlIFVSTHMgdG8gYWJzb2x1dGUgaWYgbmVlZGVkLlxcbiAgICAgICAgICAgIHVybCA9IHN0cihiYXNlX3VybC5qb2luKFVSTChocmVmKSkpXFxuICAgICAgICAgICAgdHJ5OlxcbiAgICAgICAgICAgICAgICByZXF1ZXN0ID0gUmVxdWVzdC5mcm9tX3VybCh1cmwpXFxuICAgICAgICAgICAgZXhjZXB0IFZhbGlkYXRpb25FcnJvciBhcyBleGM6XFxuICAgICAgICAgICAgICAgIGNvbnRleHQubG9nLndhcm5pbmcoZidTa2lwcGluZyBpbnZhbGlkIFVSTCBcXFwie3VybH1cXFwiOiB7ZXhjfScpXFxuICAgICAgICAgICAgICAgIGNvbnRpbnVlXFxuICAgICAgICAgICAgZXh0cmFjdGVkX3JlcXVlc3RzLmFwcGVuZChyZXF1ZXN0KVxcblxcbiAgICAgICAgIyBBZGQgZXh0cmFjdGVkIHJlcXVlc3RzIHRvIHRoZSBxdWV1ZSB3aXRoIHRoZSBzYW1lLWRvbWFpbiBzdHJhdGVneS5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQuYWRkX3JlcXVlc3RzKGV4dHJhY3RlZF9yZXF1ZXN0cywgc3RyYXRlZ3k9J3NhbWUtZG9tYWluJylcXG5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2NyYXdsZWUuZGV2J10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.vccoyBSbYPEP9O3wqtA96J5pqt2VqbQs1POBjVXT7rY\&asrc=run_on_apify)

```
import asyncio

from pydantic import ValidationError
from selectolax.lexbor import LexborHTMLParser
from yarl import URL

from crawlee import Request
from crawlee.crawlers import HttpCrawler, HttpCrawlingContext


async def main() -> None:
    crawler = HttpCrawler(
        max_request_retries=1,
        max_requests_per_crawl=10,
    )

    @crawler.router.default_handler
    async def request_handler(context: HttpCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Parse the HTML content using Selectolax with Lexbor backend.
        parsed_html = LexborHTMLParser(await context.http_response.read())

        # Extract data from the page.
        data = {
            'url': context.request.url,
            'title': parsed_html.css_first('title').text(),
            'h1s': [h1.text() for h1 in parsed_html.css('h1')],
            'h2s': [h2.text() for h2 in parsed_html.css('h2')],
            'h3s': [h3.text() for h3 in parsed_html.css('h3')],
        }
        await context.push_data(data)

        # Css selector to extract valid href attributes.
        links_selector = (
            'a[href]:not([href^="#"]):not([href^="javascript:"]):not([href^="mailto:"])'
        )
        base_url = URL(context.request.url)
        extracted_requests = []

        # Extract links.
        for item in parsed_html.css(links_selector):
            href = item.attributes.get('href')
            if not href:
                continue

            # Convert relative URLs to absolute if needed.
            url = str(base_url.join(URL(href)))
            try:
                request = Request.from_url(url)
            except ValidationError as exc:
                context.log.warning(f'Skipping invalid URL "{url}": {exc}')
                continue
            extracted_requests.append(request)

        # Add extracted requests to the queue with the same-domain strategy.
        await context.add_requests(extracted_requests, strategy='same-domain')

    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBweWRhbnRpYyBpbXBvcnQgVmFsaWRhdGlvbkVycm9yXFxuZnJvbSBweXF1ZXJ5IGltcG9ydCBQeVF1ZXJ5XFxuZnJvbSB5YXJsIGltcG9ydCBVUkxcXG5cXG5mcm9tIGNyYXdsZWUgaW1wb3J0IFJlcXVlc3RcXG5mcm9tIGNyYXdsZWUuY3Jhd2xlcnMgaW1wb3J0IEh0dHBDcmF3bGVyLCBIdHRwQ3Jhd2xpbmdDb250ZXh0XFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICBjcmF3bGVyID0gSHR0cENyYXdsZXIoXFxuICAgICAgICBtYXhfcmVxdWVzdF9yZXRyaWVzPTEsXFxuICAgICAgICBtYXhfcmVxdWVzdHNfcGVyX2NyYXdsPTEwLFxcbiAgICApXFxuXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIHJlcXVlc3RfaGFuZGxlcihjb250ZXh0OiBIdHRwQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ1Byb2Nlc3Npbmcge2NvbnRleHQucmVxdWVzdC51cmx9IC4uLicpXFxuXFxuICAgICAgICAjIFBhcnNlIHRoZSBIVE1MIGNvbnRlbnQgdXNpbmcgUHlRdWVyeS5cXG4gICAgICAgIHBhcnNlZF9odG1sID0gUHlRdWVyeShhd2FpdCBjb250ZXh0Lmh0dHBfcmVzcG9uc2UucmVhZCgpKVxcblxcbiAgICAgICAgIyBFeHRyYWN0IGRhdGEgdXNpbmcgalF1ZXJ5LXN0eWxlIHNlbGVjdG9ycy5cXG4gICAgICAgIGRhdGEgPSB7XFxuICAgICAgICAgICAgJ3VybCc6IGNvbnRleHQucmVxdWVzdC51cmwsXFxuICAgICAgICAgICAgJ3RpdGxlJzogcGFyc2VkX2h0bWwoJ3RpdGxlJykudGV4dCgpLFxcbiAgICAgICAgICAgICdoMXMnOiBbaDEudGV4dCgpIGZvciBoMSBpbiBwYXJzZWRfaHRtbCgnaDEnKS5pdGVtcygpXSxcXG4gICAgICAgICAgICAnaDJzJzogW2gyLnRleHQoKSBmb3IgaDIgaW4gcGFyc2VkX2h0bWwoJ2gyJykuaXRlbXMoKV0sXFxuICAgICAgICAgICAgJ2gzcyc6IFtoMy50ZXh0KCkgZm9yIGgzIGluIHBhcnNlZF9odG1sKCdoMycpLml0ZW1zKCldLFxcbiAgICAgICAgfVxcbiAgICAgICAgYXdhaXQgY29udGV4dC5wdXNoX2RhdGEoZGF0YSlcXG5cXG4gICAgICAgICMgQ3NzIHNlbGVjdG9yIHRvIGV4dHJhY3QgdmFsaWQgaHJlZiBhdHRyaWJ1dGVzLlxcbiAgICAgICAgbGlua3Nfc2VsZWN0b3IgPSAoXFxuICAgICAgICAgICAgJ2FbaHJlZl06bm90KFtocmVmXj1cXFwiI1xcXCJdKTpub3QoW2hyZWZePVxcXCJqYXZhc2NyaXB0OlxcXCJdKTpub3QoW2hyZWZePVxcXCJtYWlsdG86XFxcIl0pJ1xcbiAgICAgICAgKVxcbiAgICAgICAgYmFzZV91cmwgPSBVUkwoY29udGV4dC5yZXF1ZXN0LnVybClcXG5cXG4gICAgICAgIGV4dHJhY3RlZF9yZXF1ZXN0cyA9IFtdXFxuXFxuICAgICAgICAjIEV4dHJhY3QgbGlua3MuXFxuICAgICAgICBmb3IgaXRlbSBpbiBwYXJzZWRfaHRtbChsaW5rc19zZWxlY3RvcikuaXRlbXMoKTpcXG4gICAgICAgICAgICBocmVmID0gaXRlbS5hdHRyKCdocmVmJylcXG4gICAgICAgICAgICBpZiBub3QgaHJlZjpcXG4gICAgICAgICAgICAgICAgY29udGludWVcXG5cXG4gICAgICAgICAgICAjIENvbnZlcnQgcmVsYXRpdmUgVVJMcyB0byBhYnNvbHV0ZSBpZiBuZWVkZWQuXFxuICAgICAgICAgICAgdXJsID0gc3RyKGJhc2VfdXJsLmpvaW4oVVJMKHN0cihocmVmKSkpKVxcbiAgICAgICAgICAgIHRyeTpcXG4gICAgICAgICAgICAgICAgcmVxdWVzdCA9IFJlcXVlc3QuZnJvbV91cmwodXJsKVxcbiAgICAgICAgICAgIGV4Y2VwdCBWYWxpZGF0aW9uRXJyb3IgYXMgZXhjOlxcbiAgICAgICAgICAgICAgICBjb250ZXh0LmxvZy53YXJuaW5nKGYnU2tpcHBpbmcgaW52YWxpZCBVUkwgXFxcInt1cmx9XFxcIjoge2V4Y30nKVxcbiAgICAgICAgICAgICAgICBjb250aW51ZVxcbiAgICAgICAgICAgIGV4dHJhY3RlZF9yZXF1ZXN0cy5hcHBlbmQocmVxdWVzdClcXG5cXG4gICAgICAgICMgQWRkIGV4dHJhY3RlZCByZXF1ZXN0cyB0byB0aGUgcXVldWUgd2l0aCB0aGUgc2FtZS1kb21haW4gc3RyYXRlZ3kuXFxuICAgICAgICBhd2FpdCBjb250ZXh0LmFkZF9yZXF1ZXN0cyhleHRyYWN0ZWRfcmVxdWVzdHMsIHN0cmF0ZWd5PSdzYW1lLWRvbWFpbicpXFxuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9jcmF3bGVlLmRldiddKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.qJE5FSido7yGTg5je1T2xBWM-_AGPnDjqDRa9KEI_N4\&asrc=run_on_apify)

```
import asyncio

from pydantic import ValidationError
from pyquery import PyQuery
from yarl import URL

from crawlee import Request
from crawlee.crawlers import HttpCrawler, HttpCrawlingContext


async def main() -> None:
    crawler = HttpCrawler(
        max_request_retries=1,
        max_requests_per_crawl=10,
    )

    @crawler.router.default_handler
    async def request_handler(context: HttpCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Parse the HTML content using PyQuery.
        parsed_html = PyQuery(await context.http_response.read())

        # Extract data using jQuery-style selectors.
        data = {
            'url': context.request.url,
            'title': parsed_html('title').text(),
            'h1s': [h1.text() for h1 in parsed_html('h1').items()],
            'h2s': [h2.text() for h2 in parsed_html('h2').items()],
            'h3s': [h3.text() for h3 in parsed_html('h3').items()],
        }
        await context.push_data(data)

        # Css selector to extract valid href attributes.
        links_selector = (
            'a[href]:not([href^="#"]):not([href^="javascript:"]):not([href^="mailto:"])'
        )
        base_url = URL(context.request.url)

        extracted_requests = []

        # Extract links.
        for item in parsed_html(links_selector).items():
            href = item.attr('href')
            if not href:
                continue

            # Convert relative URLs to absolute if needed.
            url = str(base_url.join(URL(str(href))))
            try:
                request = Request.from_url(url)
            except ValidationError as exc:
                context.log.warning(f'Skipping invalid URL "{url}": {exc}')
                continue
            extracted_requests.append(request)

        # Add extracted requests to the queue with the same-domain strategy.
        await context.add_requests(extracted_requests, strategy='same-domain')

    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBweWRhbnRpYyBpbXBvcnQgVmFsaWRhdGlvbkVycm9yXFxuZnJvbSBzY3JhcGxpbmcucGFyc2VyIGltcG9ydCBTZWxlY3RvclxcbmZyb20geWFybCBpbXBvcnQgVVJMXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBSZXF1ZXN0XFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBIdHRwQ3Jhd2xlciwgSHR0cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IEh0dHBDcmF3bGVyKFxcbiAgICAgICAgbWF4X3JlcXVlc3RfcmV0cmllcz0xLFxcbiAgICAgICAgbWF4X3JlcXVlc3RzX3Blcl9jcmF3bD0xMCxcXG4gICAgKVxcblxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiByZXF1ZXN0X2hhbmRsZXIoY29udGV4dDogSHR0cENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm9jZXNzaW5nIHtjb250ZXh0LnJlcXVlc3QudXJsfSAuLi4nKVxcblxcbiAgICAgICAgIyBQYXJzZSB0aGUgSFRNTCBjb250ZW50IHVzaW5nIFNjcmFwbGluZy5cXG4gICAgICAgIHBhZ2UgPSBTZWxlY3Rvcihhd2FpdCBjb250ZXh0Lmh0dHBfcmVzcG9uc2UucmVhZCgpLCB1cmw9Y29udGV4dC5yZXF1ZXN0LnVybClcXG5cXG4gICAgICAgICMgRXh0cmFjdCBkYXRhIHVzaW5nIFhwYXRoIHNlbGVjdG9ycyB3aXRoIC5nZXRfYWxsX3RleHQgbWV0aG9kIGZvciBmdWxsIHRleHRcXG4gICAgICAgICMgY29udGVudC5cXG4gICAgICAgIHRpdGxlX2VsID0gcGFnZS54cGF0aF9maXJzdCgnLy90aXRsZScpXFxuICAgICAgICBkYXRhID0ge1xcbiAgICAgICAgICAgICd1cmwnOiBjb250ZXh0LnJlcXVlc3QudXJsLFxcbiAgICAgICAgICAgICd0aXRsZSc6IHRpdGxlX2VsLnRleHQgaWYgaXNpbnN0YW5jZSh0aXRsZV9lbCwgU2VsZWN0b3IpIGVsc2UgdGl0bGVfZWwsXFxuICAgICAgICAgICAgJ2gxcyc6IFtcXG4gICAgICAgICAgICAgICAgaDEuZ2V0X2FsbF90ZXh0KCkgaWYgaXNpbnN0YW5jZShoMSwgU2VsZWN0b3IpIGVsc2UgaDFcXG4gICAgICAgICAgICAgICAgZm9yIGgxIGluIHBhZ2UueHBhdGgoJy8vaDEnKVxcbiAgICAgICAgICAgIF0sXFxuICAgICAgICAgICAgJ2gycyc6IFtcXG4gICAgICAgICAgICAgICAgaDIuZ2V0X2FsbF90ZXh0KCkgaWYgaXNpbnN0YW5jZShoMiwgU2VsZWN0b3IpIGVsc2UgaDJcXG4gICAgICAgICAgICAgICAgZm9yIGgyIGluIHBhZ2UueHBhdGgoJy8vaDInKVxcbiAgICAgICAgICAgIF0sXFxuICAgICAgICAgICAgJ2gzcyc6IFtcXG4gICAgICAgICAgICAgICAgaDMuZ2V0X2FsbF90ZXh0KCkgaWYgaXNpbnN0YW5jZShoMywgU2VsZWN0b3IpIGVsc2UgaDNcXG4gICAgICAgICAgICAgICAgZm9yIGgzIGluIHBhZ2UueHBhdGgoJy8vaDMnKVxcbiAgICAgICAgICAgIF0sXFxuICAgICAgICB9XFxuICAgICAgICBhd2FpdCBjb250ZXh0LnB1c2hfZGF0YShkYXRhKVxcblxcbiAgICAgICAgIyBDc3Mgc2VsZWN0b3IgdG8gZXh0cmFjdCB2YWxpZCBocmVmIGF0dHJpYnV0ZXMuXFxuICAgICAgICBsaW5rc19zZWxlY3RvciA9IChcXG4gICAgICAgICAgICAnYVtocmVmXTpub3QoW2hyZWZePVxcXCIjXFxcIl0pOm5vdChbaHJlZl49XFxcImphdmFzY3JpcHQ6XFxcIl0pOm5vdChbaHJlZl49XFxcIm1haWx0bzpcXFwiXSknXFxuICAgICAgICApXFxuICAgICAgICBiYXNlX3VybCA9IFVSTChjb250ZXh0LnJlcXVlc3QudXJsKVxcbiAgICAgICAgZXh0cmFjdGVkX3JlcXVlc3RzID0gW11cXG5cXG4gICAgICAgICMgRXh0cmFjdCBsaW5rcy5cXG4gICAgICAgIGZvciBpdGVtIGluIHBhZ2UuY3NzKGxpbmtzX3NlbGVjdG9yKTpcXG4gICAgICAgICAgICBocmVmID0gaXRlbS5hdHRyaWIuZ2V0KCdocmVmJykgaWYgaXNpbnN0YW5jZShpdGVtLCBTZWxlY3RvcikgZWxzZSBOb25lXFxuICAgICAgICAgICAgaWYgbm90IGhyZWY6XFxuICAgICAgICAgICAgICAgIGNvbnRpbnVlXFxuXFxuICAgICAgICAgICAgIyBDb252ZXJ0IHJlbGF0aXZlIFVSTHMgdG8gYWJzb2x1dGUgaWYgbmVlZGVkLlxcbiAgICAgICAgICAgIHVybCA9IHN0cihiYXNlX3VybC5qb2luKFVSTChocmVmKSkpXFxuICAgICAgICAgICAgdHJ5OlxcbiAgICAgICAgICAgICAgICByZXF1ZXN0ID0gUmVxdWVzdC5mcm9tX3VybCh1cmwpXFxuICAgICAgICAgICAgZXhjZXB0IFZhbGlkYXRpb25FcnJvciBhcyBleGM6XFxuICAgICAgICAgICAgICAgIGNvbnRleHQubG9nLndhcm5pbmcoZidTa2lwcGluZyBpbnZhbGlkIFVSTCBcXFwie3VybH1cXFwiOiB7ZXhjfScpXFxuICAgICAgICAgICAgICAgIGNvbnRpbnVlXFxuICAgICAgICAgICAgZXh0cmFjdGVkX3JlcXVlc3RzLmFwcGVuZChyZXF1ZXN0KVxcblxcbiAgICAgICAgIyBBZGQgZXh0cmFjdGVkIHJlcXVlc3RzIHRvIHRoZSBxdWV1ZSB3aXRoIHRoZSBzYW1lLWRvbWFpbiBzdHJhdGVneS5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQuYWRkX3JlcXVlc3RzKGV4dHJhY3RlZF9yZXF1ZXN0cywgc3RyYXRlZ3k9J3NhbWUtZG9tYWluJylcXG5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2NyYXdsZWUuZGV2J10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.cDVjDeVxU7XhHNqvYVvh5vb3dBrsoJnyU6Aas0Ur7bY\&asrc=run_on_apify)

```
import asyncio

from pydantic import ValidationError
from scrapling.parser import Selector
from yarl import URL

from crawlee import Request
from crawlee.crawlers import HttpCrawler, HttpCrawlingContext


async def main() -> None:
    crawler = HttpCrawler(
        max_request_retries=1,
        max_requests_per_crawl=10,
    )

    @crawler.router.default_handler
    async def request_handler(context: HttpCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Parse the HTML content using Scrapling.
        page = Selector(await context.http_response.read(), url=context.request.url)

        # Extract data using Xpath selectors with .get_all_text method for full text
        # content.
        title_el = page.xpath_first('//title')
        data = {
            'url': context.request.url,
            'title': title_el.text if isinstance(title_el, Selector) else title_el,
            'h1s': [
                h1.get_all_text() if isinstance(h1, Selector) else h1
                for h1 in page.xpath('//h1')
            ],
            'h2s': [
                h2.get_all_text() if isinstance(h2, Selector) else h2
                for h2 in page.xpath('//h2')
            ],
            'h3s': [
                h3.get_all_text() if isinstance(h3, Selector) else h3
                for h3 in page.xpath('//h3')
            ],
        }
        await context.push_data(data)

        # Css selector to extract valid href attributes.
        links_selector = (
            'a[href]:not([href^="#"]):not([href^="javascript:"]):not([href^="mailto:"])'
        )
        base_url = URL(context.request.url)
        extracted_requests = []

        # Extract links.
        for item in page.css(links_selector):
            href = item.attrib.get('href') if isinstance(item, Selector) else None
            if not href:
                continue

            # Convert relative URLs to absolute if needed.
            url = str(base_url.join(URL(href)))
            try:
                request = Request.from_url(url)
            except ValidationError as exc:
                context.log.warning(f'Skipping invalid URL "{url}": {exc}')
                continue
            extracted_requests.append(request)

        # Add extracted requests to the queue with the same-domain strategy.
        await context.add_requests(extracted_requests, strategy='same-domain')

    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

## Custom HTTP crawler[​](#custom-http-crawler "Direct link to Custom HTTP crawler")

While the built-in crawlers cover most use cases, you might need a custom HTTP crawler for specialized parsing requirements. To create a custom HTTP crawler, inherit directly from [`AbstractHttpCrawler`](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md). This approach requires implementing:

1. **Custom parser class**: Inherit from [`AbstractHttpParser`](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md).
2. **Custom context class**: Define what data and helpers are available to handlers.
3. **Custom crawler class**: Tie everything together.

This approach is recommended when you need tight integration between parsing and the crawling context, or when you're building a reusable crawler for a specific technology or format.

The following example demonstrates how to create a custom crawler using `selectolax` with the `Lexbor` engine.

### Parser implementation[​](#parser-implementation "Direct link to Parser implementation")

The parser converts HTTP responses into a parsed document and provides methods for element selection. Implement [`AbstractHttpParser`](https://crawlee.dev/python/python/api/class/AbstractHttpParser.md) using `selectolax` with required methods for parsing and querying:

selectolax\_parser.py

```
from __future__ import annotations

import asyncio
from typing import TYPE_CHECKING

from selectolax.lexbor import LexborHTMLParser, LexborNode
from typing_extensions import override

from crawlee.crawlers._abstract_http import AbstractHttpParser

if TYPE_CHECKING:
    from collections.abc import Iterable, Sequence

    from crawlee.http_clients import HttpResponse


class SelectolaxLexborParser(AbstractHttpParser[LexborHTMLParser, LexborNode]):
    """Parser for parsing HTTP response using Selectolax Lexbor."""

    @override
    async def parse(self, response: HttpResponse) -> LexborHTMLParser:
        """Parse HTTP response body into a document object."""
        response_body = await response.read()
        # Run parsing in a thread to avoid blocking the event loop.
        return await asyncio.to_thread(LexborHTMLParser, response_body)

    @override
    async def parse_text(self, text: str) -> LexborHTMLParser:
        """Parse raw HTML string into a document object."""
        return LexborHTMLParser(text)

    @override
    async def select(
        self, parsed_content: LexborHTMLParser, selector: str
    ) -> Sequence[LexborNode]:
        """Select elements matching a CSS selector."""
        return tuple(item for item in parsed_content.css(selector))

    @override
    def is_matching_selector(
        self, parsed_content: LexborHTMLParser, selector: str
    ) -> bool:
        """Check if any element matches the selector."""
        return parsed_content.css_first(selector) is not None

    @override
    def find_links(
        self, parsed_content: LexborHTMLParser, selector: str, attribute: str
    ) -> Iterable[str]:
        """Extract href attributes from elements matching the selector.

        Used by `enqueue_links` helper to discover URLs.
        """
        link: LexborNode
        urls: list[str] = []
        for link in parsed_content.css(selector):
            url = link.attributes.get(attribute)
            if url:
                urls.append(url.strip())
        return urls
```

This is enough to use your parser with `AbstractHttpCrawler.create_parsed_http_crawler_class` factory method. For more control, continue with custom context and crawler classes below.

### Crawling context definition (optional)[​](#crawling-context-definition-optional "Direct link to Crawling context definition (optional)")

The crawling context is passed to request handlers and provides access to the parsed content. Extend [`ParsedHttpCrawlingContext`](https://crawlee.dev/python/python/api/class/ParsedHttpCrawlingContext.md) to define the interface your handlers will work with. Here you can implement additional helpers for the crawler context.

selectolax\_context.py

```
from dataclasses import dataclass, fields

from selectolax.lexbor import LexborHTMLParser
from typing_extensions import Self

from crawlee.crawlers._abstract_http import ParsedHttpCrawlingContext


# Custom context for Selectolax parser, you can add your own methods here
# to facilitate working with the parsed document.
@dataclass(frozen=True)
class SelectolaxLexborContext(ParsedHttpCrawlingContext[LexborHTMLParser]):
    """Crawling context providing access to the parsed page.

    This context is passed to request handlers and includes all standard
    context methods (push_data, enqueue_links, etc.) plus custom helpers.
    """

    @property
    def parser(self) -> LexborHTMLParser:
        """Convenient alias for accessing the parsed document."""
        return self.parsed_content

    @classmethod
    def from_parsed_http_crawling_context(
        cls, context: ParsedHttpCrawlingContext[LexborHTMLParser]
    ) -> Self:
        """Create custom context from the base context.

        Copies all fields from the base context to preserve framework
        functionality while adding custom interface.
        """
        return cls(
            **{field.name: getattr(context, field.name) for field in fields(context)}
        )
```

### Crawler composition[​](#crawler-composition "Direct link to Crawler composition")

The crawler class connects the parser and context. Extend [`AbstractHttpCrawler`](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md) and configure the context pipeline to use your custom components:

selectolax\_crawler.py

```
from __future__ import annotations

from typing import TYPE_CHECKING

from selectolax.lexbor import LexborHTMLParser, LexborNode

from crawlee.crawlers import AbstractHttpCrawler, HttpCrawlerOptions

from .selectolax_context import SelectolaxLexborContext
from .selectolax_parser import SelectolaxLexborParser

if TYPE_CHECKING:
    from collections.abc import AsyncGenerator

    from typing_extensions import Unpack

    from crawlee.crawlers._abstract_http import ParsedHttpCrawlingContext


# Custom crawler using custom context, It is optional and you can use
# AbstractHttpCrawler directly with SelectolaxLexborParser if you don't need
# any custom context methods.
class SelectolaxLexborCrawler(
    AbstractHttpCrawler[SelectolaxLexborContext, LexborHTMLParser, LexborNode]
):
    """Custom crawler using Selectolax Lexbor for HTML parsing."""

    def __init__(
        self,
        **kwargs: Unpack[HttpCrawlerOptions[SelectolaxLexborContext]],
    ) -> None:
        # Final step converts the base context to custom context type.
        async def final_step(
            context: ParsedHttpCrawlingContext[LexborHTMLParser],
        ) -> AsyncGenerator[SelectolaxLexborContext, None]:
            # Yield custom context wrapping with additional functionality around the base
            # context.
            yield SelectolaxLexborContext.from_parsed_http_crawling_context(context)

        # Build context pipeline: HTTP request -> parsing -> custom context.
        kwargs['_context_pipeline'] = (
            self._create_static_content_crawler_pipeline().compose(final_step)
        )
        super().__init__(
            parser=SelectolaxLexborParser(),
            **kwargs,
        )
```

### Crawler usage[​](#crawler-usage "Direct link to Crawler usage")

The custom crawler works like any built-in crawler. Request handlers receive your custom context with full access to framework helpers like [`enqueue_links`](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md). Additionally, the custom parser can be used with [`AdaptivePlaywrightCrawler`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md) for adaptive crawling:

* SelectolaxCrawler
* AdaptivePlaywrightCrawler with SelectolaxParser

```
import asyncio

from .selectolax_crawler import SelectolaxLexborContext, SelectolaxLexborCrawler


async def main() -> None:
    crawler = SelectolaxLexborCrawler(
        max_requests_per_crawl=10,
    )

    @crawler.router.default_handler
    async def handle_request(context: SelectolaxLexborContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        data = {
            'url': context.request.url,
            'title': context.parser.css_first('title').text(),
        }

        await context.push_data(data)
        await context.enqueue_links()

    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

```
import asyncio

from crawlee.crawlers import (
    AdaptivePlaywrightCrawler,
    AdaptivePlaywrightCrawlingContext,
)

from .selectolax_parser import SelectolaxLexborParser


async def main() -> None:
    crawler: AdaptivePlaywrightCrawler = AdaptivePlaywrightCrawler(
        max_requests_per_crawl=10,
        # Use custom Selectolax parser for static content parsing.
        static_parser=SelectolaxLexborParser(),
    )

    @crawler.router.default_handler
    async def handle_request(context: AdaptivePlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')
        data = {
            'url': context.request.url,
            'title': await context.query_selector_one('title'),
        }

        await context.push_data(data)

        await context.enqueue_links()

    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

## Conclusion[​](#conclusion "Direct link to Conclusion")

This guide provided a comprehensive overview of HTTP crawlers in Crawlee. You learned about the three main crawler types - [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md) for fault-tolerant HTML parsing, [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md) for high-performance extraction with XPath and CSS selectors, and [`HttpCrawler`](https://crawlee.dev/python/python/api/class/HttpCrawler.md) for raw response processing. You also discovered how to integrate third-party parsing libraries with [`HttpCrawler`](https://crawlee.dev/python/python/api/class/HttpCrawler.md) and how to create fully custom crawlers using [`AbstractHttpCrawler`](https://crawlee.dev/python/python/api/class/AbstractHttpCrawler.md) for specialized parsing requirements.

If you have questions or need assistance, feel free to reach out on our [GitHub](https://github.com/apify/crawlee-python) or join our [Discord community](https://discord.com/invite/jyEM2PRvMU). Happy scraping!

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/guides/http_crawlers.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/guides/http-clients.md)

[HTTP clients](https://crawlee.dev/python/python/docs/guides/http-clients.md)

[Next](https://crawlee.dev/python/python/docs/guides/playwright-crawler.md)

[Playwright crawler](https://crawlee.dev/python/python/docs/guides/playwright-crawler.md)


---

* [](https://crawlee.dev/python/python)
* [Guides](https://crawlee.dev/python/python/docs/guides.md)
* Logging in with a crawler

Version: 1.6

On this page

# Logging in with a crawler

Many websites require authentication to access their content. This guide demonstrates how to implement login functionality using both [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) and [`HttpCrawler`](https://crawlee.dev/python/python/api/class/HttpCrawler.md).

## Session management for authentication[​](#session-management-for-authentication "Direct link to Session management for authentication")

When implementing authentication, you'll typically want to maintain the same [`Session`](https://crawlee.dev/python/python/api/class/Session.md) throughout your crawl to preserve login state. This requires proper configuration of the [`SessionPool`](https://crawlee.dev/python/python/api/class/SessionPool.md). For more details, see our [session management guide](https://crawlee.dev/python/python/docs/guides/session-management.md).

If your use case requires multiple authenticated sessions with different credentials, you can:

* Use the `new_session_function` parameter in [`SessionPool`](https://crawlee.dev/python/python/api/class/SessionPool.md#__init__) to customize session creation.
* Specify the `session_id` parameter in [`Request`](https://crawlee.dev/python/python/api/class/Request.md#from_url) to bind specific requests to particular sessions.

For this guide, we'll use [demoqa.com](https://demoqa.com/login), a testing site designed for automation practice that provides a login form and protected content.

## Login with Playwright crawler[​](#login-with-playwright-crawler "Direct link to Login with Playwright crawler")

The following example demonstrates how to authenticate on a website using [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md), which provides browser automation capabilities for filling out logging forms.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuZnJvbSBkYXRldGltZSBpbXBvcnQgdGltZWRlbHRhXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBDb25jdXJyZW5jeVNldHRpbmdzLCBSZXF1ZXN0XFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCAoXFxuICAgIFBsYXl3cmlnaHRDcmF3bGVyLFxcbiAgICBQbGF5d3JpZ2h0Q3Jhd2xpbmdDb250ZXh0LFxcbilcXG5mcm9tIGNyYXdsZWUuc2Vzc2lvbnMgaW1wb3J0IFNlc3Npb25Qb29sXFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICBjcmF3bGVyID0gUGxheXdyaWdodENyYXdsZXIoXFxuICAgICAgICBtYXhfcmVxdWVzdHNfcGVyX2NyYXdsPTEwLFxcbiAgICAgICAgaGVhZGxlc3M9VHJ1ZSxcXG4gICAgICAgIGJyb3dzZXJfdHlwZT0nY2hyb21pdW0nLFxcbiAgICAgICAgIyBXZSBvbmx5IGhhdmUgb25lIHNlc3Npb24gYW5kIGl0IHNob3VsZG4ndCByb3RhdGVcXG4gICAgICAgIG1heF9zZXNzaW9uX3JvdGF0aW9ucz0wLFxcbiAgICAgICAgIyBMaW1pdCBjcmF3bGluZyBpbnRlbnNpdHkgdG8gYXZvaWQgYmxvY2tpbmdcXG4gICAgICAgIGNvbmN1cnJlbmN5X3NldHRpbmdzPUNvbmN1cnJlbmN5U2V0dGluZ3MobWF4X3Rhc2tzX3Blcl9taW51dGU9MzApLFxcbiAgICAgICAgc2Vzc2lvbl9wb29sPVNlc3Npb25Qb29sKFxcbiAgICAgICAgICAgICMgTGltaXQgdGhlIHBvb2wgdG8gb25lIHNlc3Npb25cXG4gICAgICAgICAgICBtYXhfcG9vbF9zaXplPTEsXFxuICAgICAgICAgICAgY3JlYXRlX3Nlc3Npb25fc2V0dGluZ3M9e1xcbiAgICAgICAgICAgICAgICAjIEhpZ2ggdmFsdWUgZm9yIHNlc3Npb24gdXNhZ2UgbGltaXRcXG4gICAgICAgICAgICAgICAgJ21heF91c2FnZV9jb3VudCc6IDk5OV85OTksXFxuICAgICAgICAgICAgICAgICMgSGlnaCB2YWx1ZSBmb3Igc2Vzc2lvbiBsaWZldGltZVxcbiAgICAgICAgICAgICAgICAnbWF4X2FnZSc6IHRpbWVkZWx0YShob3Vycz05OTlfOTk5KSxcXG4gICAgICAgICAgICAgICAgIyBIaWdoIHNjb3JlIGFsbG93cyB0aGUgc2Vzc2lvbiB0byBlbmNvdW50ZXIgbW9yZSBlcnJvcnNcXG4gICAgICAgICAgICAgICAgIyBiZWZvcmUgY3Jhd2xlZSBkZWNpZGVzIHRoZSBzZXNzaW9uIGlzIGJsb2NrZWRcXG4gICAgICAgICAgICAgICAgIyBNYWtlIHN1cmUgeW91IGtub3cgaG93IHRvIGhhbmRsZSB0aGVzZSBlcnJvcnNcXG4gICAgICAgICAgICAgICAgJ21heF9lcnJvcl9zY29yZSc6IDEwMCxcXG4gICAgICAgICAgICB9LFxcbiAgICAgICAgKSxcXG4gICAgKVxcblxcbiAgICAjIFRoZSBtYWluIGhhbmRsZXIgZm9yIHByb2Nlc3NpbmcgcmVxdWVzdHNcXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IFBsYXl3cmlnaHRDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgIyBBIGhhbmRsZXIgZm9yIHRoZSBsb2dpbiBwYWdlXFxuICAgIEBjcmF3bGVyLnJvdXRlci5oYW5kbGVyKCdsb2dpbicpXFxuICAgIGFzeW5jIGRlZiBsb2dpbl9oYW5kbGVyKGNvbnRleHQ6IFBsYXl3cmlnaHRDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyBsb2dpbiB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgICAgICMgQ2hlY2sgaWYgdGhlIHNlc3Npb24gaXMgYXZhaWxhYmxlXFxuICAgICAgICBpZiBub3QgY29udGV4dC5zZXNzaW9uOlxcbiAgICAgICAgICAgIHJhaXNlIFJ1bnRpbWVFcnJvcignU2Vzc2lvbiBub3QgZm91bmQnKVxcblxcbiAgICAgICAgIyBFbnRlcmluZyBkYXRhIGludG8gdGhlIGZvcm0sIGBkZWxheWAgdG8gc2ltdWxhdGUgaHVtYW4gdHlwaW5nXFxuICAgICAgICAjIFdpdGhvdXQgdGhpcywgdGhlIGRhdGEgd2lsbCBiZSBlbnRlcmVkIGluc3RhbnRseVxcbiAgICAgICAgYXdhaXQgY29udGV4dC5wYWdlLnR5cGUoJyN1c2VyTmFtZScsICdjcmF3bGVlX3Rlc3QnLCBkZWxheT0xMDApXFxuICAgICAgICBhd2FpdCBjb250ZXh0LnBhZ2UudHlwZSgnI3Bhc3N3b3JkJywgJ1Rlc3QxMjM0IScsIGRlbGF5PTEwMClcXG4gICAgICAgIGF3YWl0IGNvbnRleHQucGFnZS5jbGljaygnI2xvZ2luJywgZGVsYXk9MTAwKVxcblxcbiAgICAgICAgIyBXYWl0IGZvciBhbiBlbGVtZW50IGNvbmZpcm1pbmcgdGhhdCB3ZSBoYXZlIHN1Y2Nlc3NmdWxseVxcbiAgICAgICAgIyBsb2dnZWQgaW4gdG8gdGhlIHNpdGVcXG4gICAgICAgIGF3YWl0IGNvbnRleHQucGFnZS5sb2NhdG9yKCcjdXNlck5hbWUtdmFsdWUnKS5maXJzdC53YWl0X2ZvcihzdGF0ZT0ndmlzaWJsZScpXFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKCdMb2dpbiBzdWNjZXNzZnVsIScpXFxuXFxuICAgICAgICAjIE1vdmluZyBvbiB0byB0aGUgYmFzaWMgZmxvdyBvZiBjcmF3bGluZ1xcbiAgICAgICAgYXdhaXQgY29udGV4dC5hZGRfcmVxdWVzdHMoWydodHRwczovL2RlbW9xYS5jb20vYm9va3MnXSlcXG5cXG4gICAgIyBXZSBzdGFydCBjcmF3bGluZyB3aXRoIGxvZ2luLiBUaGlzIGlzIG5lY2Vzc2FyeSB0byBhY2Nlc3MgdGhlIHJlc3Qgb2YgdGhlIHBhZ2VzXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFtSZXF1ZXN0LmZyb21fdXJsKCdodHRwczovL2RlbW9xYS5jb20vbG9naW4nLCBsYWJlbD0nbG9naW4nKV0pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjQwOTYsInRpbWVvdXQiOjE4MH19.DICS1ZRcx0-xUchIzF8FsFTRXQ1b61ZvfyIyha_VG-Q\&asrc=run_on_apify)

```
import asyncio
from datetime import timedelta

from crawlee import ConcurrencySettings, Request
from crawlee.crawlers import (
    PlaywrightCrawler,
    PlaywrightCrawlingContext,
)
from crawlee.sessions import SessionPool


async def main() -> None:
    crawler = PlaywrightCrawler(
        max_requests_per_crawl=10,
        headless=True,
        browser_type='chromium',
        # We only have one session and it shouldn't rotate
        max_session_rotations=0,
        # Limit crawling intensity to avoid blocking
        concurrency_settings=ConcurrencySettings(max_tasks_per_minute=30),
        session_pool=SessionPool(
            # Limit the pool to one session
            max_pool_size=1,
            create_session_settings={
                # High value for session usage limit
                'max_usage_count': 999_999,
                # High value for session lifetime
                'max_age': timedelta(hours=999_999),
                # High score allows the session to encounter more errors
                # before crawlee decides the session is blocked
                # Make sure you know how to handle these errors
                'max_error_score': 100,
            },
        ),
    )

    # The main handler for processing requests
    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

    # A handler for the login page
    @crawler.router.handler('login')
    async def login_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing login {context.request.url} ...')

        # Check if the session is available
        if not context.session:
            raise RuntimeError('Session not found')

        # Entering data into the form, `delay` to simulate human typing
        # Without this, the data will be entered instantly
        await context.page.type('#userName', 'crawlee_test', delay=100)
        await context.page.type('#password', 'Test1234!', delay=100)
        await context.page.click('#login', delay=100)

        # Wait for an element confirming that we have successfully
        # logged in to the site
        await context.page.locator('#userName-value').first.wait_for(state='visible')
        context.log.info('Login successful!')

        # Moving on to the basic flow of crawling
        await context.add_requests(['https://demoqa.com/books'])

    # We start crawling with login. This is necessary to access the rest of the pages
    await crawler.run([Request.from_url('https://demoqa.com/login', label='login')])


if __name__ == '__main__':
    asyncio.run(main())
```

## Login with HTTP crawler[​](#login-with-http-crawler "Direct link to Login with HTTP crawler")

You can also use [`HttpCrawler`](https://crawlee.dev/python/python/api/class/HttpCrawler.md) (or its more specific variants like [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md) or [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md)) to authenticate by sending a POST [`Request`](https://crawlee.dev/python/python/api/class/Request.md) with your credentials directly to the authentication endpoint.

HTTP-based authentication often varies significantly between websites. Using browser [DevTools](https://developer.chrome.com/docs/devtools/overview) to analyze the `Network` tab during manual login can help you understand the specific authentication flow, required headers, and body parameters for your target website.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuaW1wb3J0IGpzb25cXG5mcm9tIGRhdGV0aW1lIGltcG9ydCBkYXRldGltZSwgdGltZWRlbHRhXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBDb25jdXJyZW5jeVNldHRpbmdzLCBSZXF1ZXN0XFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCAoXFxuICAgIEh0dHBDcmF3bGVyLFxcbiAgICBIdHRwQ3Jhd2xpbmdDb250ZXh0LFxcbilcXG5mcm9tIGNyYXdsZWUuc2Vzc2lvbnMgaW1wb3J0IFNlc3Npb25Qb29sXFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICBjcmF3bGVyID0gSHR0cENyYXdsZXIoXFxuICAgICAgICBtYXhfcmVxdWVzdHNfcGVyX2NyYXdsPTEwLFxcbiAgICAgICAgIyBDb25maWd1cmUgdG8gdXNlIGEgc2luZ2xlIHBlcnNpc3RlbnQgc2Vzc2lvbiB0aHJvdWdob3V0IHRoZSBjcmF3bFxcbiAgICAgICAgbWF4X3Nlc3Npb25fcm90YXRpb25zPTAsXFxuICAgICAgICAjIExpbWl0IHJlcXVlc3QgcmF0ZSB0byBhdm9pZCB0cmlnZ2VyaW5nIGFudGktc2NyYXBpbmcgbWVhc3VyZXNcXG4gICAgICAgIGNvbmN1cnJlbmN5X3NldHRpbmdzPUNvbmN1cnJlbmN5U2V0dGluZ3MobWF4X3Rhc2tzX3Blcl9taW51dGU9MzApLFxcbiAgICAgICAgc2Vzc2lvbl9wb29sPVNlc3Npb25Qb29sKFxcbiAgICAgICAgICAgIG1heF9wb29sX3NpemU9MSxcXG4gICAgICAgICAgICBjcmVhdGVfc2Vzc2lvbl9zZXR0aW5ncz17XFxuICAgICAgICAgICAgICAgICMgU2V0IGhpZ2ggdmFsdWUgdG8gZW5zdXJlIHRoZSBzZXNzaW9uIGlzbid0IHJlcGxhY2VkIGR1cmluZyBjcmF3bGluZ1xcbiAgICAgICAgICAgICAgICAnbWF4X3VzYWdlX2NvdW50JzogOTk5Xzk5OSxcXG4gICAgICAgICAgICAgICAgIyBTZXQgaGlnaCB2YWx1ZSB0byBwcmV2ZW50IHNlc3Npb24gZXhwaXJhdGlvbiBkdXJpbmcgY3Jhd2xpbmdcXG4gICAgICAgICAgICAgICAgJ21heF9hZ2UnOiB0aW1lZGVsdGEoaG91cnM9OTk5Xzk5OSksXFxuICAgICAgICAgICAgICAgICMgSGlnaGVyIGVycm9yIHRvbGVyYW5jZSBiZWZvcmUgdGhlIHNlc3Npb24gaXMgY29uc2lkZXJlZCBibG9ja2VkXFxuICAgICAgICAgICAgICAgICMgTWFrZSBzdXJlIHlvdSBpbXBsZW1lbnQgcHJvcGVyIGVycm9yIGhhbmRsaW5nIGluIHlvdXIgY29kZVxcbiAgICAgICAgICAgICAgICAnbWF4X2Vycm9yX3Njb3JlJzogMTAwLFxcbiAgICAgICAgICAgIH0sXFxuICAgICAgICApLFxcbiAgICApXFxuXFxuICAgICMgRGVmYXVsdCByZXF1ZXN0IGhhbmRsZXIgZm9yIG5vcm1hbCBwYWdlIHByb2Nlc3NpbmdcXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IEh0dHBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgIyBTcGVjaWFsaXplZCBoYW5kbGVyIGZvciB0aGUgbG9naW4gQVBJIHJlcXVlc3RcXG4gICAgQGNyYXdsZXIucm91dGVyLmhhbmRsZXIoJ2xvZ2luJylcXG4gICAgYXN5bmMgZGVmIGxvZ2luX2hhbmRsZXIoY29udGV4dDogSHR0cENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm9jZXNzaW5nIGxvZ2luIGF0IHtjb250ZXh0LnJlcXVlc3QudXJsfSAuLi4nKVxcblxcbiAgICAgICAgIyBWZXJpZnkgdGhhdCBhIHNlc3Npb24gaXMgYXZhaWxhYmxlIGJlZm9yZSBwcm9jZWVkaW5nXFxuICAgICAgICBpZiBub3QgY29udGV4dC5zZXNzaW9uOlxcbiAgICAgICAgICAgIHJhaXNlIFJ1bnRpbWVFcnJvcignU2Vzc2lvbiBub3QgZm91bmQnKVxcblxcbiAgICAgICAgIyBQYXJzZSB0aGUgQVBJIHJlc3BvbnNlIGNvbnRhaW5pbmcgYXV0aGVudGljYXRpb24gdG9rZW5zIGFuZCB1c2VyIGRhdGFcXG4gICAgICAgIGRhdGEgPSBqc29uLmxvYWRzKGF3YWl0IGNvbnRleHQuaHR0cF9yZXNwb25zZS5yZWFkKCkpXFxuXFxuICAgICAgICAjIEV4dHJhY3QgYXV0aGVudGljYXRpb24gZGF0YSBmcm9tIHRoZSByZXNwb25zZVxcbiAgICAgICAgdG9rZW4gPSBkYXRhWyd0b2tlbiddXFxuICAgICAgICBleHBpcmVzID0gZGF0YVsnZXhwaXJlcyddLnJlcGxhY2UoJ1onLCAnKzAwOjAwJylcXG4gICAgICAgIGV4cGlyZXNfaW50ID0gaW50KGRhdGV0aW1lLmZyb21pc29mb3JtYXQoZXhwaXJlcykudGltZXN0YW1wKCkpXFxuICAgICAgICB1c2VyX2lkID0gZGF0YVsndXNlcklkJ11cXG4gICAgICAgIHVzZXJuYW1lID0gZGF0YVsndXNlcm5hbWUnXVxcblxcbiAgICAgICAgIyBTZXQgYXV0aGVudGljYXRpb24gY29va2llcyBpbiB0aGUgc2Vzc2lvbiB0aGF0IHdpbGwgYmUgdXNlZFxcbiAgICAgICAgIyBmb3Igc3Vic2VxdWVudCByZXF1ZXN0c1xcbiAgICAgICAgY29udGV4dC5zZXNzaW9uLmNvb2tpZXMuc2V0KG5hbWU9J3Rva2VuJywgdmFsdWU9dG9rZW4sIGV4cGlyZXM9ZXhwaXJlc19pbnQpXFxuICAgICAgICBjb250ZXh0LnNlc3Npb24uY29va2llcy5zZXQobmFtZT0ndXNlcklEJywgdmFsdWU9dXNlcl9pZClcXG4gICAgICAgIGNvbnRleHQuc2Vzc2lvbi5jb29raWVzLnNldChuYW1lPSd1c2VyTmFtZScsIHZhbHVlPXVzZXJuYW1lKVxcblxcbiAgICAgICAgIyBBZnRlciBzdWNjZXNzZnVsIGF1dGhlbnRpY2F0aW9uLCBjb250aW51ZSBjcmF3bGluZyB3aXRoIHRoZVxcbiAgICAgICAgIyBhdXRoZW50aWNhdGVkIHNlc3Npb25cXG4gICAgICAgIGF3YWl0IGNvbnRleHQuYWRkX3JlcXVlc3RzKFsnaHR0cHM6Ly9kZW1vcWEuY29tL0Jvb2tTdG9yZS92MS9Cb29rcyddKVxcblxcbiAgICAjIENyZWF0ZSBhIFBPU1QgcmVxdWVzdCB0byB0aGUgYXV0aGVudGljYXRpb24gQVBJIGVuZHBvaW50XFxuICAgICMgVGhpcyB3aWxsIHRyaWdnZXIgdGhlIGxvZ2luX2hhbmRsZXIgd2hlbiBleGVjdXRlZFxcbiAgICByZXF1ZXN0ID0gUmVxdWVzdC5mcm9tX3VybChcXG4gICAgICAgICdodHRwczovL2RlbW9xYS5jb20vQWNjb3VudC92MS9Mb2dpbicsXFxuICAgICAgICBsYWJlbD0nbG9naW4nLFxcbiAgICAgICAgbWV0aG9kPSdQT1NUJyxcXG4gICAgICAgIHBheWxvYWQ9anNvbi5kdW1wcyhcXG4gICAgICAgICAgICB7J3VzZXJOYW1lJzogJ2NyYXdsZWVfdGVzdCcsICdwYXNzd29yZCc6ICdUZXN0MTIzNCEnfVxcbiAgICAgICAgKS5lbmNvZGUoKSxcXG4gICAgICAgIGhlYWRlcnM9eydDb250ZW50LVR5cGUnOiAnYXBwbGljYXRpb24vanNvbid9LFxcbiAgICApXFxuXFxuICAgICMgU3RhcnQgdGhlIGNyYXdsaW5nIHByb2Nlc3Mgd2l0aCB0aGUgbG9naW4gcmVxdWVzdFxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbcmVxdWVzdF0pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.tOfZt_zsw3qs5VpmPLQCk160mAgyHxK0dhyFIN3Jrcs\&asrc=run_on_apify)

```
import asyncio
import json
from datetime import datetime, timedelta

from crawlee import ConcurrencySettings, Request
from crawlee.crawlers import (
    HttpCrawler,
    HttpCrawlingContext,
)
from crawlee.sessions import SessionPool


async def main() -> None:
    crawler = HttpCrawler(
        max_requests_per_crawl=10,
        # Configure to use a single persistent session throughout the crawl
        max_session_rotations=0,
        # Limit request rate to avoid triggering anti-scraping measures
        concurrency_settings=ConcurrencySettings(max_tasks_per_minute=30),
        session_pool=SessionPool(
            max_pool_size=1,
            create_session_settings={
                # Set high value to ensure the session isn't replaced during crawling
                'max_usage_count': 999_999,
                # Set high value to prevent session expiration during crawling
                'max_age': timedelta(hours=999_999),
                # Higher error tolerance before the session is considered blocked
                # Make sure you implement proper error handling in your code
                'max_error_score': 100,
            },
        ),
    )

    # Default request handler for normal page processing
    @crawler.router.default_handler
    async def request_handler(context: HttpCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

    # Specialized handler for the login API request
    @crawler.router.handler('login')
    async def login_handler(context: HttpCrawlingContext) -> None:
        context.log.info(f'Processing login at {context.request.url} ...')

        # Verify that a session is available before proceeding
        if not context.session:
            raise RuntimeError('Session not found')

        # Parse the API response containing authentication tokens and user data
        data = json.loads(await context.http_response.read())

        # Extract authentication data from the response
        token = data['token']
        expires = data['expires'].replace('Z', '+00:00')
        expires_int = int(datetime.fromisoformat(expires).timestamp())
        user_id = data['userId']
        username = data['username']

        # Set authentication cookies in the session that will be used
        # for subsequent requests
        context.session.cookies.set(name='token', value=token, expires=expires_int)
        context.session.cookies.set(name='userID', value=user_id)
        context.session.cookies.set(name='userName', value=username)

        # After successful authentication, continue crawling with the
        # authenticated session
        await context.add_requests(['https://demoqa.com/BookStore/v1/Books'])

    # Create a POST request to the authentication API endpoint
    # This will trigger the login_handler when executed
    request = Request.from_url(
        'https://demoqa.com/Account/v1/Login',
        label='login',
        method='POST',
        payload=json.dumps(
            {'userName': 'crawlee_test', 'password': 'Test1234!'}
        ).encode(),
        headers={'Content-Type': 'application/json'},
    )

    # Start the crawling process with the login request
    await crawler.run([request])


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/guides/crawler_login.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/guides/avoid-blocking.md)

[Avoid getting blocked](https://crawlee.dev/python/python/docs/guides/avoid-blocking.md)

[Next](https://crawlee.dev/python/python/docs/guides/creating-web-archive.md)

[Creating web archive](https://crawlee.dev/python/python/docs/guides/creating-web-archive.md)


---

* [](https://crawlee.dev/python/python)
* [Guides](https://crawlee.dev/python/python/docs/guides.md)
* Playwright crawler

Version: 1.6

On this page

# Playwright crawler

A [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) is a browser-based crawler. In contrast to HTTP-based crawlers like [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md) or [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md), it uses a real browser to render pages and extract data. It is built on top of the [Playwright](https://playwright.dev/python/) browser automation library. While browser-based crawlers are typically slower and less efficient than HTTP-based crawlers, they can handle dynamic, client-side rendered sites that standard HTTP-based crawlers cannot manage.

## When to use Playwright crawler[​](#when-to-use-playwright-crawler "Direct link to When to use Playwright crawler")

Use [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) in scenarios that require full browser capabilities, such as:

* **Dynamic content rendering**: Required when pages rely on heavy JavaScript to load or modify content in the browser.
* **Anti-scraping protection**: Helpful for sites using JavaScript-based security or advanced anti-automation measures.
* **Complex cookie management**: Necessary for sites with session or cookie requirements that standard HTTP-based crawlers cannot handle easily.

If [HTTP-based crawlers](https://crawlee.dev/python/python/docs/guides/http-crawlers.md) are insufficient, [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) can address these challenges. See a [basic example](https://crawlee.dev/python/python/docs/examples/playwright-crawler.md) for a typical usage demonstration.

## Advanced configuration[​](#advanced-configuration "Direct link to Advanced configuration")

The [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) uses other Crawlee components under the hood, notably [`BrowserPool`](https://crawlee.dev/python/python/api/class/BrowserPool.md) and [`PlaywrightBrowserPlugin`](https://crawlee.dev/python/python/api/class/PlaywrightBrowserPlugin.md). These components let you to configure the browser and context settings, launch multiple browsers, and apply pre-navigation hooks. You can create your own instances of these components and pass them to the [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) constructor.

* The [`PlaywrightBrowserPlugin`](https://crawlee.dev/python/python/api/class/PlaywrightBrowserPlugin.md) manages how browsers are launched and how browser contexts are created. It accepts [browser launch](https://playwright.dev/python/docs/api/class-browsertype#browser-type-launch) and [new context](https://playwright.dev/python/docs/api/class-browser#browser-new-context) options.
* The [`BrowserPool`](https://crawlee.dev/python/python/api/class/BrowserPool.md) manages the lifecycle of browser instances (launching, recycling, etc.). You can customize its behavior to suit your needs.

## Managing multiple browsers[​](#managing-multiple-browsers "Direct link to Managing multiple browsers")

The [`BrowserPool`](https://crawlee.dev/python/python/api/class/BrowserPool.md) allows you to manage multiple browsers. Each browser instance is managed by a separate [`PlaywrightBrowserPlugin`](https://crawlee.dev/python/python/api/class/PlaywrightBrowserPlugin.md) and can be configured independently. This is useful for scenarios like testing multiple configurations or implementing browser rotation to help avoid blocks or detect different site behaviors.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmJyb3dzZXJzIGltcG9ydCBCcm93c2VyUG9vbCwgUGxheXdyaWdodEJyb3dzZXJQbHVnaW5cXG5mcm9tIGNyYXdsZWUuY3Jhd2xlcnMgaW1wb3J0IFBsYXl3cmlnaHRDcmF3bGVyLCBQbGF5d3JpZ2h0Q3Jhd2xpbmdDb250ZXh0XFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICAjIENyZWF0ZSBhIHBsdWdpbiBmb3IgZWFjaCByZXF1aXJlZCBicm93c2VyLlxcbiAgICBwbHVnaW5fY2hyb21pdW0gPSBQbGF5d3JpZ2h0QnJvd3NlclBsdWdpbihcXG4gICAgICAgIGJyb3dzZXJfdHlwZT0nY2hyb21pdW0nLCBtYXhfb3Blbl9wYWdlc19wZXJfYnJvd3Nlcj0xXFxuICAgIClcXG4gICAgcGx1Z2luX2ZpcmVmb3ggPSBQbGF5d3JpZ2h0QnJvd3NlclBsdWdpbihcXG4gICAgICAgIGJyb3dzZXJfdHlwZT0nZmlyZWZveCcsIG1heF9vcGVuX3BhZ2VzX3Blcl9icm93c2VyPTFcXG4gICAgKVxcblxcbiAgICBjcmF3bGVyID0gUGxheXdyaWdodENyYXdsZXIoXFxuICAgICAgICBicm93c2VyX3Bvb2w9QnJvd3NlclBvb2wocGx1Z2lucz1bcGx1Z2luX2Nocm9taXVtLCBwbHVnaW5fZmlyZWZveF0pLFxcbiAgICAgICAgIyBMaW1pdCB0aGUgY3Jhd2wgdG8gbWF4IHJlcXVlc3RzLiBSZW1vdmUgb3IgaW5jcmVhc2UgaXQgZm9yIGNyYXdsaW5nIGFsbCBsaW5rcy5cXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsXFxuICAgIClcXG5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IFBsYXl3cmlnaHRDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBicm93c2VyX25hbWUgPSAoXFxuICAgICAgICAgICAgY29udGV4dC5wYWdlLmNvbnRleHQuYnJvd3Nlci5icm93c2VyX3R5cGUubmFtZVxcbiAgICAgICAgICAgIGlmIGNvbnRleHQucGFnZS5jb250ZXh0LmJyb3dzZXJcXG4gICAgICAgICAgICBlbHNlICd1bmRlZmluZWQnXFxuICAgICAgICApXFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gd2l0aCB7YnJvd3Nlcl9uYW1lfSAuLi4nKVxcblxcbiAgICAgICAgYXdhaXQgY29udGV4dC5lbnF1ZXVlX2xpbmtzKClcXG5cXG4gICAgIyBSdW4gdGhlIGNyYXdsZXIgd2l0aCB0aGUgaW5pdGlhbCBsaXN0IG9mIFVSTHMuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9jcmF3bGVlLmRldicsICdodHRwczovL2FwaWZ5LmNvbS8nXSlcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6NDA5NiwidGltZW91dCI6MTgwfX0.TTnx-_vAt3I7VKgVoteaTkQuYimBdwOjZCt5BFJQKo8\&asrc=run_on_apify)

```
import asyncio

from crawlee.browsers import BrowserPool, PlaywrightBrowserPlugin
from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext


async def main() -> None:
    # Create a plugin for each required browser.
    plugin_chromium = PlaywrightBrowserPlugin(
        browser_type='chromium', max_open_pages_per_browser=1
    )
    plugin_firefox = PlaywrightBrowserPlugin(
        browser_type='firefox', max_open_pages_per_browser=1
    )

    crawler = PlaywrightCrawler(
        browser_pool=BrowserPool(plugins=[plugin_chromium, plugin_firefox]),
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
    )

    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        browser_name = (
            context.page.context.browser.browser_type.name
            if context.page.context.browser
            else 'undefined'
        )
        context.log.info(f'Processing {context.request.url} with {browser_name} ...')

        await context.enqueue_links()

    # Run the crawler with the initial list of URLs.
    await crawler.run(['https://crawlee.dev', 'https://apify.com/'])


if __name__ == '__main__':
    asyncio.run(main())
```

## Browser launch and context configuration[​](#browser-launch-and-context-configuration "Direct link to Browser launch and context configuration")

The [`PlaywrightBrowserPlugin`](https://crawlee.dev/python/python/api/class/PlaywrightBrowserPlugin.md) provides access to all relevant Playwright configuration options for both [browser launches](https://playwright.dev/python/docs/api/class-browsertype#browser-type-launch) and [new browser contexts](https://playwright.dev/python/docs/api/class-browser#browser-new-context). You can specify these options in the constructor of [`PlaywrightBrowserPlugin`](https://crawlee.dev/python/python/api/class/PlaywrightBrowserPlugin.md) or [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md):

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQbGF5d3JpZ2h0Q3Jhd2xlciwgUGxheXdyaWdodENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IFBsYXl3cmlnaHRDcmF3bGVyKFxcbiAgICAgICAgaGVhZGxlc3M9RmFsc2UsXFxuICAgICAgICBicm93c2VyX3R5cGU9J2Nocm9taXVtJyxcXG4gICAgICAgICMgQnJvd3NlciBsYXVuY2ggb3B0aW9uc1xcbiAgICAgICAgYnJvd3Nlcl9sYXVuY2hfb3B0aW9ucz17XFxuICAgICAgICAgICAgIyBGb3Igc3VwcG9ydCBgbXNlZGdlYCBjaGFubmVsIHlvdSBuZWVkIHRvIGluc3RhbGwgaXRcXG4gICAgICAgICAgICAjIGBwbGF5d3JpZ2h0IGluc3RhbGwgbXNlZGdlYFxcbiAgICAgICAgICAgICdjaGFubmVsJzogJ21zZWRnZScsXFxuICAgICAgICAgICAgJ3Nsb3dfbW8nOiAyMDAsXFxuICAgICAgICB9LFxcbiAgICAgICAgIyBDb250ZXh0IGxhdW5jaCBvcHRpb25zLCBhcHBsaWVkIHRvIGVhY2ggcGFnZSBhcyBpdCBpcyBjcmVhdGVkXFxuICAgICAgICBicm93c2VyX25ld19jb250ZXh0X29wdGlvbnM9e1xcbiAgICAgICAgICAgICdjb2xvcl9zY2hlbWUnOiAnZGFyaycsXFxuICAgICAgICAgICAgIyBTZXQgaGVhZGVyc1xcbiAgICAgICAgICAgICdleHRyYV9odHRwX2hlYWRlcnMnOiB7XFxuICAgICAgICAgICAgICAgICdDdXN0b20tSGVhZGVyJzogJ215LWhlYWRlcicsXFxuICAgICAgICAgICAgICAgICdBY2NlcHQtTGFuZ3VhZ2UnOiAnZW4nLFxcbiAgICAgICAgICAgIH0sXFxuICAgICAgICAgICAgIyBTZXQgb25seSBVc2VyIEFnZW50XFxuICAgICAgICAgICAgJ3VzZXJfYWdlbnQnOiAnTXktVXNlci1BZ2VudCcsXFxuICAgICAgICB9LFxcbiAgICAgICAgIyBMaW1pdCB0aGUgY3Jhd2wgdG8gbWF4IHJlcXVlc3RzLiBSZW1vdmUgb3IgaW5jcmVhc2UgaXQgZm9yIGNyYXdsaW5nIGFsbCBsaW5rcy5cXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsXFxuICAgIClcXG5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IFBsYXl3cmlnaHRDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQuZW5xdWV1ZV9saW5rcygpXFxuXFxuICAgICMgUnVuIHRoZSBjcmF3bGVyIHdpdGggdGhlIGluaXRpYWwgbGlzdCBvZiBVUkxzLlxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vY3Jhd2xlZS5kZXYnXSlcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6NDA5NiwidGltZW91dCI6MTgwfX0.eRN5TXwq2OilyOetMfZIdmqkPW2IeDdUf76bpd6r5fw\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext


async def main() -> None:
    crawler = PlaywrightCrawler(
        headless=False,
        browser_type='chromium',
        # Browser launch options
        browser_launch_options={
            # For support `msedge` channel you need to install it
            # `playwright install msedge`
            'channel': 'msedge',
            'slow_mo': 200,
        },
        # Context launch options, applied to each page as it is created
        browser_new_context_options={
            'color_scheme': 'dark',
            # Set headers
            'extra_http_headers': {
                'Custom-Header': 'my-header',
                'Accept-Language': 'en',
            },
            # Set only User Agent
            'user_agent': 'My-User-Agent',
        },
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
    )

    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        await context.enqueue_links()

    # Run the crawler with the initial list of URLs.
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

You can also configure each plugin used by [`BrowserPool`](https://crawlee.dev/python/python/api/class/BrowserPool.md):

```
import asyncio

from crawlee.browsers import BrowserPool, PlaywrightBrowserPlugin
from crawlee.crawlers import PlaywrightCrawler


async def main() -> None:
    crawler = PlaywrightCrawler(
        browser_pool=BrowserPool(
            plugins=[
                PlaywrightBrowserPlugin(
                    browser_type='chromium',
                    browser_launch_options={
                        'headless': False,
                        'channel': 'msedge',
                        'slow_mo': 200,
                    },
                    browser_new_context_options={
                        'color_scheme': 'dark',
                        'extra_http_headers': {
                            'Custom-Header': 'my-header',
                            'Accept-Language': 'en',
                        },
                        'user_agent': 'My-User-Agent',
                    },
                )
            ]
        )
    )

    # ...


if __name__ == '__main__':
    asyncio.run(main())
```

For an example of how to implement a custom browser plugin, see the [Camoufox example](https://crawlee.dev/python/python/docs/examples/playwright-crawler-with-camoufox.md). [Camoufox](https://camoufox.com/) is a stealth browser plugin designed to reduce detection by anti-scraping measures and is fully compatible with [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md).

## Page configuration with lifecycle page hooks[​](#page-configuration-with-lifecycle-page-hooks "Direct link to Page configuration with lifecycle page hooks")

For additional setup or event-driven actions around page creation and closure, the [`BrowserPool`](https://crawlee.dev/python/python/api/class/BrowserPool.md) exposes four lifecycle hooks: [`pre_page_create_hook`](https://crawlee.dev/python/python/api/class/BrowserPool.md#pre_page_create_hook), [`post_page_create_hook`](https://crawlee.dev/python/python/api/class/BrowserPool.md#post_page_create_hook), [`pre_page_close_hook`](https://crawlee.dev/python/python/api/class/BrowserPool.md#pre_page_close_hook), and [`post_page_close_hook`](https://crawlee.dev/python/python/api/class/BrowserPool.md#post_page_close_hook). To use them, create a `BrowserPool` instance and pass it to [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) via the `browser_pool` argument.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImZyb20gX19mdXR1cmVfXyBpbXBvcnQgYW5ub3RhdGlvbnNcXG5cXG5pbXBvcnQgYXN5bmNpb1xcbmltcG9ydCBsb2dnaW5nXFxuZnJvbSB0eXBpbmcgaW1wb3J0IFRZUEVfQ0hFQ0tJTkcsIEFueVxcblxcbmZyb20gY3Jhd2xlZS5icm93c2VycyBpbXBvcnQgQnJvd3NlclBvb2xcXG5mcm9tIGNyYXdsZWUuY3Jhd2xlcnMgaW1wb3J0IFBsYXl3cmlnaHRDcmF3bGVyLCBQbGF5d3JpZ2h0Q3Jhd2xpbmdDb250ZXh0XFxuZnJvbSBjcmF3bGVlLnN0b3JhZ2VzIGltcG9ydCBLZXlWYWx1ZVN0b3JlXFxuXFxuaWYgVFlQRV9DSEVDS0lORzpcXG4gICAgZnJvbSBjcmF3bGVlLmJyb3dzZXJzLl9icm93c2VyX2NvbnRyb2xsZXIgaW1wb3J0IEJyb3dzZXJDb250cm9sbGVyXFxuICAgIGZyb20gY3Jhd2xlZS5icm93c2Vycy5fdHlwZXMgaW1wb3J0IENyYXdsZWVQYWdlXFxuICAgIGZyb20gY3Jhd2xlZS5wcm94eV9jb25maWd1cmF0aW9uIGltcG9ydCBQcm94eUluZm9cXG5cXG5sb2dnZXIgPSBsb2dnaW5nLmdldExvZ2dlcihfX25hbWVfXylcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgIGFzeW5jIHdpdGggQnJvd3NlclBvb2woKSBhcyBicm93c2VyX3Bvb2w6XFxuXFxuICAgICAgICBAYnJvd3Nlcl9wb29sLnByZV9wYWdlX2NyZWF0ZV9ob29rXFxuICAgICAgICBhc3luYyBkZWYgbG9nX3BhZ2VfaW5pdChcXG4gICAgICAgICAgICBwYWdlX2lkOiBzdHIsXFxuICAgICAgICAgICAgX2Jyb3dzZXJfY29udHJvbGxlcjogQnJvd3NlckNvbnRyb2xsZXIsXFxuICAgICAgICAgICAgX2Jyb3dzZXJfbmV3X2NvbnRleHRfb3B0aW9uczogZGljdFtzdHIsIEFueV0sXFxuICAgICAgICAgICAgX3Byb3h5X2luZm86IFByb3h5SW5mbyB8IE5vbmUsXFxuICAgICAgICApIC0-IE5vbmU6XFxuICAgICAgICAgICAgXFxcIlxcXCJcXFwiTG9nIHdoZW4gYSBuZXcgcGFnZSBpcyBhYm91dCB0byBiZSBjcmVhdGVkLlxcXCJcXFwiXFxcIlxcbiAgICAgICAgICAgIGxvZ2dlci5pbmZvKGYnQ3JlYXRpbmcgcGFnZSB7cGFnZV9pZH0uLi4nKVxcblxcbiAgICAgICAgQGJyb3dzZXJfcG9vbC5wb3N0X3BhZ2VfY3JlYXRlX2hvb2tcXG4gICAgICAgIGFzeW5jIGRlZiBzZXRfdmlld3BvcnQoXFxuICAgICAgICAgICAgY3Jhd2xlZV9wYWdlOiBDcmF3bGVlUGFnZSwgX2Jyb3dzZXJfY29udHJvbGxlcjogQnJvd3NlckNvbnRyb2xsZXJcXG4gICAgICAgICkgLT4gTm9uZTpcXG4gICAgICAgICAgICBcXFwiXFxcIlxcXCJTZXQgYSBmaXhlZCB2aWV3cG9ydCBzaXplIG9uIGVhY2ggbmV3bHkgY3JlYXRlZCBwYWdlLlxcXCJcXFwiXFxcIlxcbiAgICAgICAgICAgIGF3YWl0IGNyYXdsZWVfcGFnZS5wYWdlLnNldF92aWV3cG9ydF9zaXplKHsnd2lkdGgnOiAxMjgwLCAnaGVpZ2h0JzogMTAyNH0pXFxuXFxuICAgICAgICBAYnJvd3Nlcl9wb29sLnByZV9wYWdlX2Nsb3NlX2hvb2tcXG4gICAgICAgIGFzeW5jIGRlZiBzYXZlX3NjcmVlbnNob3QoXFxuICAgICAgICAgICAgY3Jhd2xlZV9wYWdlOiBDcmF3bGVlUGFnZSwgX2Jyb3dzZXJfY29udHJvbGxlcjogQnJvd3NlckNvbnRyb2xsZXJcXG4gICAgICAgICkgLT4gTm9uZTpcXG4gICAgICAgICAgICBcXFwiXFxcIlxcXCJTYXZlIGEgc2NyZWVuc2hvdCB0byBLZXlWYWx1ZVN0b3JlIGJlZm9yZSBlYWNoIHBhZ2UgaXMgY2xvc2VkLlxcXCJcXFwiXFxcIlxcbiAgICAgICAgICAgIGt2cyA9IGF3YWl0IEtleVZhbHVlU3RvcmUub3BlbigpXFxuXFxuICAgICAgICAgICAgc2NyZWVuc2hvdCA9IGF3YWl0IGNyYXdsZWVfcGFnZS5wYWdlLnNjcmVlbnNob3QoKVxcbiAgICAgICAgICAgIGF3YWl0IGt2cy5zZXRfdmFsdWUoXFxuICAgICAgICAgICAgICAgIGtleT1mJ3NjcmVlbnNob3Qte2NyYXdsZWVfcGFnZS5pZH0nLFxcbiAgICAgICAgICAgICAgICB2YWx1ZT1zY3JlZW5zaG90LFxcbiAgICAgICAgICAgICAgICBjb250ZW50X3R5cGU9J2ltYWdlL3BuZycsXFxuICAgICAgICAgICAgKVxcbiAgICAgICAgICAgIGxvZ2dlci5pbmZvKGYnU2F2ZWQgc2NyZWVuc2hvdCBmb3IgcGFnZSB7Y3Jhd2xlZV9wYWdlLmlkfS4nKVxcblxcbiAgICAgICAgQGJyb3dzZXJfcG9vbC5wb3N0X3BhZ2VfY2xvc2VfaG9va1xcbiAgICAgICAgYXN5bmMgZGVmIGxvZ19wYWdlX2Nsb3NlZChcXG4gICAgICAgICAgICBwYWdlX2lkOiBzdHIsIF9icm93c2VyX2NvbnRyb2xsZXI6IEJyb3dzZXJDb250cm9sbGVyXFxuICAgICAgICApIC0-IE5vbmU6XFxuICAgICAgICAgICAgXFxcIlxcXCJcXFwiTG9nIGFmdGVyIGVhY2ggcGFnZSBpcyBjbG9zZWQuXFxcIlxcXCJcXFwiXFxuICAgICAgICAgICAgbG9nZ2VyLmluZm8oZidQYWdlIHtwYWdlX2lkfSBjbG9zZWQgc3VjY2Vzc2Z1bGx5LicpXFxuXFxuICAgICAgICBjcmF3bGVyID0gUGxheXdyaWdodENyYXdsZXIoXFxuICAgICAgICAgICAgYnJvd3Nlcl9wb29sPWJyb3dzZXJfcG9vbCxcXG4gICAgICAgICAgICBtYXhfcmVxdWVzdHNfcGVyX2NyYXdsPTUsXFxuICAgICAgICApXFxuXFxuICAgICAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgICAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IFBsYXl3cmlnaHRDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ1Byb2Nlc3Npbmcge2NvbnRleHQucmVxdWVzdC51cmx9IC4uLicpXFxuXFxuICAgICAgICAgICAgYXdhaXQgY29udGV4dC5lbnF1ZXVlX2xpbmtzKClcXG5cXG4gICAgICAgICMgUnVuIHRoZSBjcmF3bGVyIHdpdGggdGhlIGluaXRpYWwgbGlzdCBvZiBVUkxzLlxcbiAgICAgICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2NyYXdsZWUuZGV2J10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjQwOTYsInRpbWVvdXQiOjE4MH19.qDHlCadgSYS-JLfhNHh7c_dX8dIk7uIz6iMNQts9ZWo\&asrc=run_on_apify)

```
from __future__ import annotations

import asyncio
import logging
from typing import TYPE_CHECKING, Any

from crawlee.browsers import BrowserPool
from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext
from crawlee.storages import KeyValueStore

if TYPE_CHECKING:
    from crawlee.browsers._browser_controller import BrowserController
    from crawlee.browsers._types import CrawleePage
    from crawlee.proxy_configuration import ProxyInfo

logger = logging.getLogger(__name__)


async def main() -> None:
    async with BrowserPool() as browser_pool:

        @browser_pool.pre_page_create_hook
        async def log_page_init(
            page_id: str,
            _browser_controller: BrowserController,
            _browser_new_context_options: dict[str, Any],
            _proxy_info: ProxyInfo | None,
        ) -> None:
            """Log when a new page is about to be created."""
            logger.info(f'Creating page {page_id}...')

        @browser_pool.post_page_create_hook
        async def set_viewport(
            crawlee_page: CrawleePage, _browser_controller: BrowserController
        ) -> None:
            """Set a fixed viewport size on each newly created page."""
            await crawlee_page.page.set_viewport_size({'width': 1280, 'height': 1024})

        @browser_pool.pre_page_close_hook
        async def save_screenshot(
            crawlee_page: CrawleePage, _browser_controller: BrowserController
        ) -> None:
            """Save a screenshot to KeyValueStore before each page is closed."""
            kvs = await KeyValueStore.open()

            screenshot = await crawlee_page.page.screenshot()
            await kvs.set_value(
                key=f'screenshot-{crawlee_page.id}',
                value=screenshot,
                content_type='image/png',
            )
            logger.info(f'Saved screenshot for page {crawlee_page.id}.')

        @browser_pool.post_page_close_hook
        async def log_page_closed(
            page_id: str, _browser_controller: BrowserController
        ) -> None:
            """Log after each page is closed."""
            logger.info(f'Page {page_id} closed successfully.')

        crawler = PlaywrightCrawler(
            browser_pool=browser_pool,
            max_requests_per_crawl=5,
        )

        @crawler.router.default_handler
        async def request_handler(context: PlaywrightCrawlingContext) -> None:
            context.log.info(f'Processing {context.request.url} ...')

            await context.enqueue_links()

        # Run the crawler with the initial list of URLs.
        await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

## Navigation hooks[​](#navigation-hooks "Direct link to Navigation hooks")

Navigation hooks allow for additional configuration at specific points during page navigation. The [`pre_navigation_hook`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md#pre_navigation_hook) is called before each navigation and provides [`PlaywrightPreNavCrawlingContext`](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md) - including the [page](https://playwright.dev/python/docs/api/class-page) instance and a [`block_requests`](https://crawlee.dev/python/python/api/class/PlaywrightPreNavCrawlingContext.md#block_requests) helper for filtering unwanted resource types and URL patterns. See the [block requests example](https://crawlee.dev/python/python/docs/examples/playwright-crawler-with-block-requests.md) for a dedicated walkthrough. Similarly, the [`post_navigation_hook`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md#post_navigation_hook) is called after each navigation and provides [`PlaywrightPostNavCrawlingContext`](https://crawlee.dev/python/python/api/class/PlaywrightPostNavCrawlingContext.md) - useful for post-load checks such as detecting CAPTCHAs or verifying page state.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCAoXFxuICAgIFBsYXl3cmlnaHRDcmF3bGVyLFxcbiAgICBQbGF5d3JpZ2h0Q3Jhd2xpbmdDb250ZXh0LFxcbiAgICBQbGF5d3JpZ2h0UG9zdE5hdkNyYXdsaW5nQ29udGV4dCxcXG4gICAgUGxheXdyaWdodFByZU5hdkNyYXdsaW5nQ29udGV4dCxcXG4pXFxuZnJvbSBjcmF3bGVlLmVycm9ycyBpbXBvcnQgU2Vzc2lvbkVycm9yXFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICBjcmF3bGVyID0gUGxheXdyaWdodENyYXdsZXIobWF4X3JlcXVlc3RzX3Blcl9jcmF3bD0xMClcXG5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IFBsYXl3cmlnaHRDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQuZW5xdWV1ZV9saW5rcygpXFxuXFxuICAgIEBjcmF3bGVyLnByZV9uYXZpZ2F0aW9uX2hvb2tcXG4gICAgYXN5bmMgZGVmIGNvbmZpZ3VyZV9wYWdlKGNvbnRleHQ6IFBsYXl3cmlnaHRQcmVOYXZDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnTmF2aWdhdGluZyB0byB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgICAgICMgYmxvY2sgc3R5bGVzaGVldHMsIGltYWdlcywgZm9udHMgYW5kIG90aGVyIHN0YXRpYyBhc3NldHNcXG4gICAgICAgICMgdG8gc3BlZWQgdXAgcGFnZSBsb2FkaW5nXFxuICAgICAgICBhd2FpdCBjb250ZXh0LmJsb2NrX3JlcXVlc3RzKClcXG5cXG4gICAgQGNyYXdsZXIucG9zdF9uYXZpZ2F0aW9uX2hvb2tcXG4gICAgYXN5bmMgZGVmIGN1c3RvbV9jYXB0Y2hhX2NoZWNrKGNvbnRleHQ6IFBsYXl3cmlnaHRQb3N0TmF2Q3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgIyBjaGVjayBpZiB0aGUgcGFnZSBjb250YWlucyBhIGNhcHRjaGFcXG4gICAgICAgIGNhcHRjaGFfZWxlbWVudCA9IGNvbnRleHQucGFnZS5sb2NhdG9yKCdpbnB1dFtuYW1lPVxcXCJjYXB0Y2hhXFxcIl0nKS5maXJzdFxcbiAgICAgICAgaWYgYXdhaXQgY2FwdGNoYV9lbGVtZW50LmlzX3Zpc2libGUoKTpcXG4gICAgICAgICAgICBjb250ZXh0LmxvZy53YXJuaW5nKCdDYXB0Y2hhIGRldGVjdGVkISBTa2lwcGluZyB0aGUgcGFnZS4nKVxcbiAgICAgICAgICAgIHJhaXNlIFNlc3Npb25FcnJvcignQ2FwdGNoYSBkZXRlY3RlZCcpXFxuXFxuICAgICMgUnVuIHRoZSBjcmF3bGVyIHdpdGggdGhlIGluaXRpYWwgbGlzdCBvZiBVUkxzLlxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vY3Jhd2xlZS5kZXYnXSlcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6NDA5NiwidGltZW91dCI6MTgwfX0.-5xAfA9ds6yeAT1C8WDu_NTCyL7apB8yWQrbOAzzMkQ\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import (
    PlaywrightCrawler,
    PlaywrightCrawlingContext,
    PlaywrightPostNavCrawlingContext,
    PlaywrightPreNavCrawlingContext,
)
from crawlee.errors import SessionError


async def main() -> None:
    crawler = PlaywrightCrawler(max_requests_per_crawl=10)

    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        await context.enqueue_links()

    @crawler.pre_navigation_hook
    async def configure_page(context: PlaywrightPreNavCrawlingContext) -> None:
        context.log.info(f'Navigating to {context.request.url} ...')

        # block stylesheets, images, fonts and other static assets
        # to speed up page loading
        await context.block_requests()

    @crawler.post_navigation_hook
    async def custom_captcha_check(context: PlaywrightPostNavCrawlingContext) -> None:
        # check if the page contains a captcha
        captcha_element = context.page.locator('input[name="captcha"]').first
        if await captcha_element.is_visible():
            context.log.warning('Captcha detected! Skipping the page.')
            raise SessionError('Captcha detected')

    # Run the crawler with the initial list of URLs.
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

## Conclusion[​](#conclusion "Direct link to Conclusion")

This guide introduced the [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) and explained how to configure it using [`BrowserPool`](https://crawlee.dev/python/python/api/class/BrowserPool.md) and [`PlaywrightBrowserPlugin`](https://crawlee.dev/python/python/api/class/PlaywrightBrowserPlugin.md). You learned how to launch multiple browsers, configure browser and context settings, use [`BrowserPool`](https://crawlee.dev/python/python/api/class/BrowserPool.md) lifecycle page hooks, and apply navigation hooks. If you have questions or need assistance, feel free to reach out on our [GitHub](https://github.com/apify/crawlee-python) or join our [Discord community](https://discord.com/invite/jyEM2PRvMU). Happy scraping!

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/guides/playwright_crawler.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/guides/http-crawlers.md)

[HTTP crawlers](https://crawlee.dev/python/python/docs/guides/http-crawlers.md)

[Next](https://crawlee.dev/python/python/docs/guides/adaptive-playwright-crawler.md)

[Adaptive Playwright crawler](https://crawlee.dev/python/python/docs/guides/adaptive-playwright-crawler.md)


---

* [](https://crawlee.dev/python/python)
* [Guides](https://crawlee.dev/python/python/docs/guides.md)
* Playwright with Stagehand

Version: 1.6

On this page

# Playwright with Stagehand

[Stagehand](https://docs.stagehand.dev/) is a framework that combines [Playwright](https://playwright.dev/python/) with AI-driven natural language understanding and decision-making capabilities. With Stagehand, you can use natural language instructions to interact with web pages instead of writing complex selectors and automation logic.

Stagehand supports multiple AI models through [`LiteLLM`](https://docs.litellm.ai/docs/). This guide demonstrates how to integrate Stagehand with [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) using [Gemini](https://ai.google.dev/gemini-api/docs) as the AI model provider.

info

This guide is based on stagehand-python v0.4.0 with local configuration settings and may not be compatible with newer versions.

## Get Gemini API key[​](#get-gemini-api-key "Direct link to Get Gemini API key")

You need to register with [Google AI Studio](https://aistudio.google.com/) and navigate to [Get API key](https://aistudio.google.com/app/apikey) to obtain your API key.

## Create support classes for Stagehand[​](#create-support-classes-for-stagehand "Direct link to Create support classes for Stagehand")

To integrate Stagehand with Crawlee, you need to create wrapper classes that allow [`PlaywrightBrowserPlugin`](https://crawlee.dev/python/python/api/class/PlaywrightBrowserPlugin.md) to manage the Playwright lifecycle.

Create `CrawleeStagehand` - a custom Stagehand subclass that overrides the `init` method to prevent Stagehand from launching its own Playwright instance.

Create `CrawleeStagehandPage` - a wrapper class for `StagehandPage` that implements the [Playwright Page](https://playwright.dev/python/docs/next/api/class-page) behavior expected by [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md).

support\_classes.py

```
from __future__ import annotations

from typing import TYPE_CHECKING, Any

from stagehand import Stagehand, StagehandPage

if TYPE_CHECKING:
    from types import TracebackType


class CrawleeStagehandPage:
    """StagehandPage wrapper for Crawlee."""

    def __init__(self, page: StagehandPage) -> None:
        self._page = page

    async def goto(
        self,
        url: str,
        *,
        referer: str | None = None,
        timeout: int | None = None,
        wait_until: str | None = None,
    ) -> Any:
        """Navigate to the specified URL."""
        # Override goto to return navigation result that `PlaywrightCrawler` expects
        return await self._page._page.goto(  # noqa: SLF001
            url,
            referer=referer,
            timeout=timeout,
            wait_until=wait_until,
        )

    def __getattr__(self, name: str) -> Any:
        """Delegate all other methods to the underlying StagehandPage."""
        return getattr(self._page, name)

    async def __aenter__(self) -> CrawleeStagehandPage:
        """Enter the context manager."""
        return self

    async def __aexit__(
        self,
        exc_type: type[BaseException] | None,
        exc_value: BaseException | None,
        exc_traceback: TracebackType | None,
    ) -> None:
        await self._page.close()


class CrawleeStagehand(Stagehand):
    """Stagehand wrapper for Crawlee to disable the launch of Playwright."""

    async def init(self) -> None:
        # Skip Stagehand's own Playwright initialization
        # Let Crawlee's PlaywrightBrowserPlugin manage the browser lifecycle
        self._initialized = True
```

## Create browser integration classes[​](#create-browser-integration-classes "Direct link to Create browser integration classes")

You need to create a custom browser plugin and controller that properly initialize Stagehand and obtain browser pages from `StagehandContext`.

Create `StagehandPlugin` - a subclass of [`PlaywrightBrowserPlugin`](https://crawlee.dev/python/python/api/class/PlaywrightBrowserPlugin.md) that holds the Stagehand instance and creates `PlaywrightPersistentBrowser` instances.

Create `StagehandBrowserController` - a subclass of [`PlaywrightBrowserController`](https://crawlee.dev/python/python/api/class/PlaywrightBrowserController.md) that lazily initializes `StagehandContext` and creates new pages with AI capabilities on demand.

browser\_classes.py

```
from __future__ import annotations

from datetime import datetime, timezone
from typing import TYPE_CHECKING, Any, cast

from stagehand.context import StagehandContext
from typing_extensions import override

from crawlee.browsers import (
    PlaywrightBrowserController,
    PlaywrightBrowserPlugin,
    PlaywrightPersistentBrowser,
)

from .support_classes import CrawleeStagehandPage

if TYPE_CHECKING:
    from collections.abc import Mapping

    from playwright.async_api import Page
    from stagehand import Stagehand

    from crawlee.proxy_configuration import ProxyInfo


class StagehandBrowserController(PlaywrightBrowserController):
    @override
    def __init__(
        self, browser: PlaywrightPersistentBrowser, stagehand: Stagehand, **kwargs: Any
    ) -> None:
        # Initialize with browser context instead of browser instance
        super().__init__(browser, **kwargs)

        self._stagehand = stagehand
        self._stagehand_context: StagehandContext | None = None

    @override
    async def new_page(
        self,
        browser_new_context_options: Mapping[str, Any] | None = None,
        proxy_info: ProxyInfo | None = None,
    ) -> Page:
        # Initialize browser context if not already done
        if not self._browser_context:
            self._browser_context = await self._create_browser_context(
                browser_new_context_options=browser_new_context_options,
                proxy_info=proxy_info,
            )

        # Initialize Stagehand context if not already done
        if not self._stagehand_context:
            self._stagehand_context = await StagehandContext.init(
                self._browser_context, self._stagehand
            )

        # Create a new page using Stagehand context
        page = await self._stagehand_context.new_page()

        pw_page = page._page  # noqa: SLF001

        # Handle page close event
        pw_page.on(event='close', f=self._on_page_close)

        # Update internal state
        self._pages.append(pw_page)
        self._last_page_opened_at = datetime.now(timezone.utc)

        self._total_opened_pages += 1

        # Wrap StagehandPage to provide Playwright Page interface
        return cast('Page', CrawleeStagehandPage(page))


class StagehandPlugin(PlaywrightBrowserPlugin):
    """Browser plugin that integrates Stagehand with Crawlee's browser management."""

    @override
    def __init__(self, stagehand: Stagehand, **kwargs: Any) -> None:
        super().__init__(**kwargs)

        self._stagehand = stagehand

    @override
    async def new_browser(self) -> StagehandBrowserController:
        if not self._playwright:
            raise RuntimeError('Playwright browser plugin is not initialized.')

        browser = PlaywrightPersistentBrowser(
            # Stagehand can run only on a Chromium-based browser.
            self._playwright.chromium,
            self._user_data_dir,
            self._browser_launch_options,
        )

        # Return custom controller with Stagehand
        return StagehandBrowserController(
            browser=browser,
            stagehand=self._stagehand,
            header_generator=None,
            fingerprint_generator=None,
        )
```

## Create a crawler[​](#create-a-crawler "Direct link to Create a crawler")

Now you can create a [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) that uses Stagehand's AI capabilities to interact with web pages using natural language commands:

stagehand\_run.py

```
from __future__ import annotations

import asyncio
import os
from typing import cast

from stagehand import StagehandConfig, StagehandPage

from crawlee import ConcurrencySettings
from crawlee.browsers import BrowserPool
from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext

from .browser_classes import StagehandPlugin
from .support_classes import CrawleeStagehand


async def main() -> None:
    # Configure local Stagehand with Gemini model
    config = StagehandConfig(
        env='LOCAL',
        model_name='google/gemini-2.5-flash-preview-05-20',
        model_api_key=os.getenv('GEMINI_API_KEY'),
    )

    # Create Stagehand instance
    stagehand = CrawleeStagehand(config)

    # Create crawler with custom browser pool using Stagehand
    crawler = PlaywrightCrawler(
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
        # Custom browser pool. Gives users full control over browsers used by the crawler.
        concurrency_settings=ConcurrencySettings(max_tasks_per_minute=10),
        browser_pool=BrowserPool(
            plugins=[
                StagehandPlugin(stagehand, browser_launch_options={'headless': True})
            ],
        ),
    )

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Cast to StagehandPage for proper type hints in IDE
        page = cast('StagehandPage', context.page)

        # Use regular Playwright method
        playwright_title = await page.title()
        context.log.info(f'Playwright page title: {playwright_title}')

        # Use AI-powered extraction with natural language
        gemini_title = await page.extract('Extract page title')
        context.log.info(f'Gemini page title: {gemini_title}')

        await context.enqueue_links()

    # Run the crawler with the initial list of URLs.
    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

The integration works through several key components:

* `CrawleeStagehand` prevents Stagehand from launching its own Playwright instance, allowing Crawlee to manage the browser lifecycle
* `StagehandPlugin` extends the Playwright browser plugin to create Stagehand-enabled browser instances
* `StagehandBrowserController` uses `StagehandContext` to create pages with AI capabilities
* `CrawleeStagehandPage` provides interface compatibility between Stagehand pages and Crawlee's expectations

In the request handler, you can use natural language commands like `page.extract('Extract title page')` to perform intelligent data extraction without writing complex selectors.

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/guides/playwright_crawler_stagehand.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/guides/adaptive-playwright-crawler.md)

[Adaptive Playwright crawler](https://crawlee.dev/python/python/docs/guides/adaptive-playwright-crawler.md)

[Next](https://crawlee.dev/python/python/docs/guides/proxy-management.md)

[Proxy management](https://crawlee.dev/python/python/docs/guides/proxy-management.md)


---

* [](https://crawlee.dev/python/python)
* [Guides](https://crawlee.dev/python/python/docs/guides.md)
* Proxy management

Version: 1.6

On this page

# Proxy management

[IP address blocking](https://en.wikipedia.org/wiki/IP_address_blocking) is one of the oldest and most effective ways of preventing access to a website. It is therefore paramount for a good web scraping library to provide easy to use but powerful tools which can work around IP blocking. The most powerful weapon in our anti IP blocking arsenal is a [proxy server](https://en.wikipedia.org/wiki/Proxy_server).

With Crawlee we can use our own proxy servers or proxy servers acquired from third-party providers.

## Quick start[​](#quick-start "Direct link to Quick start")

If you already have proxy URLs of your own, you can start using them immediately in only a few lines of code.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLnByb3h5X2NvbmZpZ3VyYXRpb24gaW1wb3J0IFByb3h5Q29uZmlndXJhdGlvblxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgcHJveHlfY29uZmlndXJhdGlvbiA9IFByb3h5Q29uZmlndXJhdGlvbihcXG4gICAgICAgIHByb3h5X3VybHM9W1xcbiAgICAgICAgICAgICdodHRwOi8vcHJveHktMS5jb20vJyxcXG4gICAgICAgICAgICAnaHR0cDovL3Byb3h5LTIuY29tLycsXFxuICAgICAgICBdXFxuICAgIClcXG5cXG4gICAgIyBUaGUgcHJveHkgVVJMcyBhcmUgcm90YXRlZCBpbiBhIHJvdW5kLXJvYmluLlxcbiAgICBwcm94eV91cmxfMSA9IGF3YWl0IHByb3h5X2NvbmZpZ3VyYXRpb24ubmV3X3VybCgpICAjIGh0dHA6Ly9wcm94eS0xLmNvbS9cXG4gICAgcHJveHlfdXJsXzIgPSBhd2FpdCBwcm94eV9jb25maWd1cmF0aW9uLm5ld191cmwoKSAgIyBodHRwOi8vcHJveHktMi5jb20vXFxuICAgIHByb3h5X3VybF8zID0gYXdhaXQgcHJveHlfY29uZmlndXJhdGlvbi5uZXdfdXJsKCkgICMgaHR0cDovL3Byb3h5LTEuY29tL1xcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ._SFIM1r9O3bHkyasnhAYnhQtIqFEp44jkuizacw7DZM\&asrc=run_on_apify)

```
import asyncio

from crawlee.proxy_configuration import ProxyConfiguration


async def main() -> None:
    proxy_configuration = ProxyConfiguration(
        proxy_urls=[
            'http://proxy-1.com/',
            'http://proxy-2.com/',
        ]
    )

    # The proxy URLs are rotated in a round-robin.
    proxy_url_1 = await proxy_configuration.new_url()  # http://proxy-1.com/
    proxy_url_2 = await proxy_configuration.new_url()  # http://proxy-2.com/
    proxy_url_3 = await proxy_configuration.new_url()  # http://proxy-1.com/


if __name__ == '__main__':
    asyncio.run(main())
```

Examples of how to use our proxy URLs with crawlers are shown below in [Crawler integration](#crawler-integration) section.

## Proxy configuration[​](#proxy-configuration "Direct link to Proxy configuration")

All our proxy needs are managed by the [`ProxyConfiguration`](https://crawlee.dev/python/python/api/class/ProxyConfiguration.md) class. We create an instance using the [`ProxyConfiguration`](https://crawlee.dev/python/python/api/class/ProxyConfiguration.md) constructor function based on the provided options.

### Crawler integration[​](#crawler-integration "Direct link to Crawler integration")

`ProxyConfiguration` integrates seamlessly into [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md) and [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md).

* BeautifulSoupCrawler
* PlaywrightCrawler

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcbmZyb20gY3Jhd2xlZS5wcm94eV9jb25maWd1cmF0aW9uIGltcG9ydCBQcm94eUNvbmZpZ3VyYXRpb25cXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgICMgQ3JlYXRlIGEgUHJveHlDb25maWd1cmF0aW9uIG9iamVjdCBhbmQgcGFzcyBpdCB0byB0aGUgY3Jhd2xlci5cXG4gICAgcHJveHlfY29uZmlndXJhdGlvbiA9IFByb3h5Q29uZmlndXJhdGlvbihcXG4gICAgICAgIHByb3h5X3VybHM9W1xcbiAgICAgICAgICAgICdodHRwOi8vcHJveHktMS5jb20vJyxcXG4gICAgICAgICAgICAnaHR0cDovL3Byb3h5LTIuY29tLycsXFxuICAgICAgICBdXFxuICAgIClcXG4gICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKHByb3h5X2NvbmZpZ3VyYXRpb249cHJveHlfY29uZmlndXJhdGlvbilcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgZGVmYXVsdF9oYW5kbGVyKGNvbnRleHQ6IEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICAjIEV4dHJhY3QgZGF0YSBmcm9tIHRoZSBwYWdlLlxcbiAgICAgICAgZGF0YSA9IHtcXG4gICAgICAgICAgICAndXJsJzogY29udGV4dC5yZXF1ZXN0LnVybCxcXG4gICAgICAgICAgICAndGl0bGUnOiBjb250ZXh0LnNvdXAudGl0bGUuc3RyaW5nIGlmIGNvbnRleHQuc291cC50aXRsZSBlbHNlIE5vbmUsXFxuICAgICAgICB9XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnRXh0cmFjdGVkIGRhdGE6IHtkYXRhfScpXFxuXFxuICAgICMgUnVuIHRoZSBjcmF3bGVyIHdpdGggdGhlIGluaXRpYWwgbGlzdCBvZiByZXF1ZXN0cy5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2NyYXdsZWUuZGV2LyddKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.MHaJGzuPVy5TiiKzipM9Q90xNWvA83O3vY0oCAsr82w\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext
from crawlee.proxy_configuration import ProxyConfiguration


async def main() -> None:
    # Create a ProxyConfiguration object and pass it to the crawler.
    proxy_configuration = ProxyConfiguration(
        proxy_urls=[
            'http://proxy-1.com/',
            'http://proxy-2.com/',
        ]
    )
    crawler = BeautifulSoupCrawler(proxy_configuration=proxy_configuration)

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def default_handler(context: BeautifulSoupCrawlingContext) -> None:
        # Extract data from the page.
        data = {
            'url': context.request.url,
            'title': context.soup.title.string if context.soup.title else None,
        }
        context.log.info(f'Extracted data: {data}')

    # Run the crawler with the initial list of requests.
    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQbGF5d3JpZ2h0Q3Jhd2xlciwgUGxheXdyaWdodENyYXdsaW5nQ29udGV4dFxcbmZyb20gY3Jhd2xlZS5wcm94eV9jb25maWd1cmF0aW9uIGltcG9ydCBQcm94eUNvbmZpZ3VyYXRpb25cXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgICMgQ3JlYXRlIGEgUHJveHlDb25maWd1cmF0aW9uIG9iamVjdCBhbmQgcGFzcyBpdCB0byB0aGUgY3Jhd2xlci5cXG4gICAgcHJveHlfY29uZmlndXJhdGlvbiA9IFByb3h5Q29uZmlndXJhdGlvbihcXG4gICAgICAgIHByb3h5X3VybHM9W1xcbiAgICAgICAgICAgICdodHRwOi8vcHJveHktMS5jb20vJyxcXG4gICAgICAgICAgICAnaHR0cDovL3Byb3h5LTIuY29tLycsXFxuICAgICAgICBdXFxuICAgIClcXG4gICAgY3Jhd2xlciA9IFBsYXl3cmlnaHRDcmF3bGVyKHByb3h5X2NvbmZpZ3VyYXRpb249cHJveHlfY29uZmlndXJhdGlvbilcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgZGVmYXVsdF9oYW5kbGVyKGNvbnRleHQ6IFBsYXl3cmlnaHRDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICAjIEV4dHJhY3QgZGF0YSBmcm9tIHRoZSBwYWdlLlxcbiAgICAgICAgZGF0YSA9IHtcXG4gICAgICAgICAgICAndXJsJzogY29udGV4dC5yZXF1ZXN0LnVybCxcXG4gICAgICAgICAgICAndGl0bGUnOiBhd2FpdCBjb250ZXh0LnBhZ2UudGl0bGUoKSxcXG4gICAgICAgIH1cXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidFeHRyYWN0ZWQgZGF0YToge2RhdGF9JylcXG5cXG4gICAgIyBSdW4gdGhlIGNyYXdsZXIgd2l0aCB0aGUgaW5pdGlhbCBsaXN0IG9mIHJlcXVlc3RzLlxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vY3Jhd2xlZS5kZXYvJ10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjQwOTYsInRpbWVvdXQiOjE4MH19.lUH_DLNR7zcBf84Bg4iG1Gt1HnH2EKDeZ8hFRgjjYjE\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext
from crawlee.proxy_configuration import ProxyConfiguration


async def main() -> None:
    # Create a ProxyConfiguration object and pass it to the crawler.
    proxy_configuration = ProxyConfiguration(
        proxy_urls=[
            'http://proxy-1.com/',
            'http://proxy-2.com/',
        ]
    )
    crawler = PlaywrightCrawler(proxy_configuration=proxy_configuration)

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def default_handler(context: PlaywrightCrawlingContext) -> None:
        # Extract data from the page.
        data = {
            'url': context.request.url,
            'title': await context.page.title(),
        }
        context.log.info(f'Extracted data: {data}')

    # Run the crawler with the initial list of requests.
    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

Our crawlers will now use the selected proxies for all connections.

### IP Rotation and session management[​](#ip-rotation-and-session-management "Direct link to IP Rotation and session management")

The [`proxy_configuration.new_url()`](https://crawlee.dev/python/python/api/class/ProxyConfiguration.md#new_url) method allows us to pass a `session_id` parameter. This creates a `session_id`-`proxy_url` pair, ensuring that subsequent `new_url()` calls with the same `session_id` return the same `proxy_url`. This is extremely useful in scraping, because we want to create the impression of a real user. See the [`SessionPool`](https://crawlee.dev/python/python/api/class/SessionPool.md) class for more information on how maintaining a real session helps avoid blocking.

For more details on session management, check out the [Session management](https://crawlee.dev/python/python/docs/guides/session-management.md) guide.

When no `session_id` is provided, our proxy URLs are rotated round-robin.

* BeautifulSoupCrawler
* PlaywrightCrawler

```
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler
from crawlee.proxy_configuration import ProxyConfiguration


async def main() -> None:
    # Create a ProxyConfiguration object and pass it to the crawler.
    proxy_configuration = ProxyConfiguration(
        proxy_urls=[
            'http://proxy-1.com/',
            'http://proxy-2.com/',
        ]
    )
    crawler = BeautifulSoupCrawler(
        proxy_configuration=proxy_configuration,
        use_session_pool=True,
    )

    # ...


if __name__ == '__main__':
    asyncio.run(main())
```

```
import asyncio

from crawlee.crawlers import PlaywrightCrawler
from crawlee.proxy_configuration import ProxyConfiguration


async def main() -> None:
    # Create a ProxyConfiguration object and pass it to the crawler.
    proxy_configuration = ProxyConfiguration(
        proxy_urls=[
            'http://proxy-1.com/',
            'http://proxy-2.com/',
        ]
    )
    crawler = PlaywrightCrawler(
        proxy_configuration=proxy_configuration,
        use_session_pool=True,
    )

    # ...


if __name__ == '__main__':
    asyncio.run(main())
```

### Tiered proxies[​](#tiered-proxies "Direct link to Tiered proxies")

When you use HTTP proxies in real world crawling scenarios, you have to decide which type of proxy to use to reach the sweet spot between cost efficiency and reliably avoiding blocking. Some websites may allow crawling with no proxy, on some you may get away with using datacenter proxies, which are cheap but easily detected, and sometimes you need to use expensive residential proxies.

To take the guesswork out of this process, Crawlee allows you to configure multiple tiers of proxy URLs. When crawling, it will automatically pick the lowest tier (smallest index) where it doesn't encounter blocking. If you organize your proxy server URLs in tiers so that the lowest tier contains the cheapest, least reliable ones and each higher tier contains more expensive, more reliable ones, you will get an optimal anti-blocking performance.

In an active tier, Crawlee will alternate between proxies in a round-robin fashion, just like it would with `proxy_urls`.

* BeautifulSoupCrawler
* PlaywrightCrawler

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcbmZyb20gY3Jhd2xlZS5wcm94eV9jb25maWd1cmF0aW9uIGltcG9ydCBQcm94eUNvbmZpZ3VyYXRpb25cXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgICMgQ3JlYXRlIGEgUHJveHlDb25maWd1cmF0aW9uIG9iamVjdCBhbmQgcGFzcyBpdCB0byB0aGUgY3Jhd2xlci5cXG4gICAgcHJveHlfY29uZmlndXJhdGlvbiA9IFByb3h5Q29uZmlndXJhdGlvbihcXG4gICAgICAgIHRpZXJlZF9wcm94eV91cmxzPVtcXG4gICAgICAgICAgICAjIE5vIHByb3h5IHRpZXIuXFxuICAgICAgICAgICAgIyBPcHRpb25hbCBpbiBjYXNlIHlvdSBkbyBub3Qgd2FudCB0byB1c2UgYW55IHByb3h5IG9uIGxvd2VzdCB0aWVyLlxcbiAgICAgICAgICAgIFtOb25lXSxcXG4gICAgICAgICAgICAjIGxvd2VyIHRpZXIsIGNoZWFwZXIsIHByZWZlcnJlZCBhcyBsb25nIGFzIHRoZXkgd29ya1xcbiAgICAgICAgICAgIFtcXG4gICAgICAgICAgICAgICAgJ2h0dHA6Ly9jaGVhcC1kYXRhY2VudGVyLXByb3h5LTEuY29tLycsXFxuICAgICAgICAgICAgICAgICdodHRwOi8vY2hlYXAtZGF0YWNlbnRlci1wcm94eS0yLmNvbS8nLFxcbiAgICAgICAgICAgIF0sXFxuICAgICAgICAgICAgIyBoaWdoZXIgdGllciwgbW9yZSBleHBlbnNpdmUsIHVzZWQgYXMgYSBmYWxsYmFja1xcbiAgICAgICAgICAgIFtcXG4gICAgICAgICAgICAgICAgJ2h0dHA6Ly9leHBlbnNpdmUtcmVzaWRlbnRpYWwtcHJveHktMS5jb20vJyxcXG4gICAgICAgICAgICAgICAgJ2h0dHA6Ly9leHBlbnNpdmUtcmVzaWRlbnRpYWwtcHJveHktMi5jb20vJyxcXG4gICAgICAgICAgICBdLFxcbiAgICAgICAgXVxcbiAgICApXFxuICAgIGNyYXdsZXIgPSBCZWF1dGlmdWxTb3VwQ3Jhd2xlcihwcm94eV9jb25maWd1cmF0aW9uPXByb3h5X2NvbmZpZ3VyYXRpb24pXFxuXFxuICAgICMgRGVmaW5lIHRoZSBkZWZhdWx0IHJlcXVlc3QgaGFuZGxlciwgd2hpY2ggd2lsbCBiZSBjYWxsZWQgZm9yIGV2ZXJ5IHJlcXVlc3QuXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIGRlZmF1bHRfaGFuZGxlcihjb250ZXh0OiBCZWF1dGlmdWxTb3VwQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgIyBMb2cgdGhlIHByb3h5IHVzZWQgZm9yIHRoZSBjdXJyZW50IHJlcXVlc3QuXFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJveHkgZm9yIHRoZSBjdXJyZW50IHJlcXVlc3Q6IHtjb250ZXh0LnByb3h5X2luZm99JylcXG5cXG4gICAgIyBSdW4gdGhlIGNyYXdsZXIgd2l0aCB0aGUgaW5pdGlhbCBsaXN0IG9mIHJlcXVlc3RzLlxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vY3Jhd2xlZS5kZXYvJ10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.Xzxh0B5ZcBIHyu1PrQH9FqoE589UmEqfvOb9OvK60FA\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext
from crawlee.proxy_configuration import ProxyConfiguration


async def main() -> None:
    # Create a ProxyConfiguration object and pass it to the crawler.
    proxy_configuration = ProxyConfiguration(
        tiered_proxy_urls=[
            # No proxy tier.
            # Optional in case you do not want to use any proxy on lowest tier.
            [None],
            # lower tier, cheaper, preferred as long as they work
            [
                'http://cheap-datacenter-proxy-1.com/',
                'http://cheap-datacenter-proxy-2.com/',
            ],
            # higher tier, more expensive, used as a fallback
            [
                'http://expensive-residential-proxy-1.com/',
                'http://expensive-residential-proxy-2.com/',
            ],
        ]
    )
    crawler = BeautifulSoupCrawler(proxy_configuration=proxy_configuration)

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def default_handler(context: BeautifulSoupCrawlingContext) -> None:
        # Log the proxy used for the current request.
        context.log.info(f'Proxy for the current request: {context.proxy_info}')

    # Run the crawler with the initial list of requests.
    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQbGF5d3JpZ2h0Q3Jhd2xlciwgUGxheXdyaWdodENyYXdsaW5nQ29udGV4dFxcbmZyb20gY3Jhd2xlZS5wcm94eV9jb25maWd1cmF0aW9uIGltcG9ydCBQcm94eUNvbmZpZ3VyYXRpb25cXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgICMgQ3JlYXRlIGEgUHJveHlDb25maWd1cmF0aW9uIG9iamVjdCBhbmQgcGFzcyBpdCB0byB0aGUgY3Jhd2xlci5cXG4gICAgcHJveHlfY29uZmlndXJhdGlvbiA9IFByb3h5Q29uZmlndXJhdGlvbihcXG4gICAgICAgIHRpZXJlZF9wcm94eV91cmxzPVtcXG4gICAgICAgICAgICAjIE5vIHByb3h5IHRpZXIuXFxuICAgICAgICAgICAgIyBPcHRpb25hbCBpbiBjYXNlIHlvdSBkbyBub3Qgd2FudCB0byB1c2UgYW55IHByb3h5IG9uIGxvd2VzdCB0aWVyLlxcbiAgICAgICAgICAgIFtOb25lXSxcXG4gICAgICAgICAgICAjIGxvd2VyIHRpZXIsIGNoZWFwZXIsIHByZWZlcnJlZCBhcyBsb25nIGFzIHRoZXkgd29ya1xcbiAgICAgICAgICAgIFtcXG4gICAgICAgICAgICAgICAgJ2h0dHA6Ly9jaGVhcC1kYXRhY2VudGVyLXByb3h5LTEuY29tLycsXFxuICAgICAgICAgICAgICAgICdodHRwOi8vY2hlYXAtZGF0YWNlbnRlci1wcm94eS0yLmNvbS8nLFxcbiAgICAgICAgICAgIF0sXFxuICAgICAgICAgICAgIyBoaWdoZXIgdGllciwgbW9yZSBleHBlbnNpdmUsIHVzZWQgYXMgYSBmYWxsYmFja1xcbiAgICAgICAgICAgIFtcXG4gICAgICAgICAgICAgICAgJ2h0dHA6Ly9leHBlbnNpdmUtcmVzaWRlbnRpYWwtcHJveHktMS5jb20vJyxcXG4gICAgICAgICAgICAgICAgJ2h0dHA6Ly9leHBlbnNpdmUtcmVzaWRlbnRpYWwtcHJveHktMi5jb20vJyxcXG4gICAgICAgICAgICBdLFxcbiAgICAgICAgXVxcbiAgICApXFxuICAgIGNyYXdsZXIgPSBQbGF5d3JpZ2h0Q3Jhd2xlcihwcm94eV9jb25maWd1cmF0aW9uPXByb3h5X2NvbmZpZ3VyYXRpb24pXFxuXFxuICAgICMgRGVmaW5lIHRoZSBkZWZhdWx0IHJlcXVlc3QgaGFuZGxlciwgd2hpY2ggd2lsbCBiZSBjYWxsZWQgZm9yIGV2ZXJ5IHJlcXVlc3QuXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIGRlZmF1bHRfaGFuZGxlcihjb250ZXh0OiBQbGF5d3JpZ2h0Q3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgIyBMb2cgdGhlIHByb3h5IHVzZWQgZm9yIHRoZSBjdXJyZW50IHJlcXVlc3QuXFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJveHkgZm9yIHRoZSBjdXJyZW50IHJlcXVlc3Q6IHtjb250ZXh0LnByb3h5X2luZm99JylcXG5cXG4gICAgIyBSdW4gdGhlIGNyYXdsZXIgd2l0aCB0aGUgaW5pdGlhbCBsaXN0IG9mIHJlcXVlc3RzLlxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vY3Jhd2xlZS5kZXYvJ10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjQwOTYsInRpbWVvdXQiOjE4MH19.PVqSGurJn0CtD1V6PVcutWRbCMSa4rZtnNja0R8ybSI\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext
from crawlee.proxy_configuration import ProxyConfiguration


async def main() -> None:
    # Create a ProxyConfiguration object and pass it to the crawler.
    proxy_configuration = ProxyConfiguration(
        tiered_proxy_urls=[
            # No proxy tier.
            # Optional in case you do not want to use any proxy on lowest tier.
            [None],
            # lower tier, cheaper, preferred as long as they work
            [
                'http://cheap-datacenter-proxy-1.com/',
                'http://cheap-datacenter-proxy-2.com/',
            ],
            # higher tier, more expensive, used as a fallback
            [
                'http://expensive-residential-proxy-1.com/',
                'http://expensive-residential-proxy-2.com/',
            ],
        ]
    )
    crawler = PlaywrightCrawler(proxy_configuration=proxy_configuration)

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def default_handler(context: PlaywrightCrawlingContext) -> None:
        # Log the proxy used for the current request.
        context.log.info(f'Proxy for the current request: {context.proxy_info}')

    # Run the crawler with the initial list of requests.
    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

## Inspecting current proxy in crawlers[​](#inspecting-current-proxy-in-crawlers "Direct link to Inspecting current proxy in crawlers")

The [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md) and [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md) provide access to information about the currently used proxy via the request handler using a [`proxy_info`](https://crawlee.dev/python/python/api/class/ProxyInfo.md) object. This object allows easy access to the proxy URL.

* BeautifulSoupCrawler
* PlaywrightCrawler

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcbmZyb20gY3Jhd2xlZS5wcm94eV9jb25maWd1cmF0aW9uIGltcG9ydCBQcm94eUNvbmZpZ3VyYXRpb25cXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgICMgQ3JlYXRlIGEgUHJveHlDb25maWd1cmF0aW9uIG9iamVjdCBhbmQgcGFzcyBpdCB0byB0aGUgY3Jhd2xlci5cXG4gICAgcHJveHlfY29uZmlndXJhdGlvbiA9IFByb3h5Q29uZmlndXJhdGlvbihcXG4gICAgICAgIHByb3h5X3VybHM9W1xcbiAgICAgICAgICAgICdodHRwOi8vcHJveHktMS5jb20vJyxcXG4gICAgICAgICAgICAnaHR0cDovL3Byb3h5LTIuY29tLycsXFxuICAgICAgICBdXFxuICAgIClcXG4gICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKHByb3h5X2NvbmZpZ3VyYXRpb249cHJveHlfY29uZmlndXJhdGlvbilcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgZGVmYXVsdF9oYW5kbGVyKGNvbnRleHQ6IEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICAjIExvZyB0aGUgcHJveHkgdXNlZCBmb3IgdGhlIGN1cnJlbnQgcmVxdWVzdC5cXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm94eSBmb3IgdGhlIGN1cnJlbnQgcmVxdWVzdDoge2NvbnRleHQucHJveHlfaW5mb30nKVxcblxcbiAgICAjIFJ1biB0aGUgY3Jhd2xlciB3aXRoIHRoZSBpbml0aWFsIGxpc3Qgb2YgcmVxdWVzdHMuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9jcmF3bGVlLmRldi8nXSlcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6MTAyNCwidGltZW91dCI6MTgwfX0.sZh0_U1qkgWXm9ol_O8AhdWKX3a3yCUFydvjMfohP_0\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext
from crawlee.proxy_configuration import ProxyConfiguration


async def main() -> None:
    # Create a ProxyConfiguration object and pass it to the crawler.
    proxy_configuration = ProxyConfiguration(
        proxy_urls=[
            'http://proxy-1.com/',
            'http://proxy-2.com/',
        ]
    )
    crawler = BeautifulSoupCrawler(proxy_configuration=proxy_configuration)

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def default_handler(context: BeautifulSoupCrawlingContext) -> None:
        # Log the proxy used for the current request.
        context.log.info(f'Proxy for the current request: {context.proxy_info}')

    # Run the crawler with the initial list of requests.
    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQbGF5d3JpZ2h0Q3Jhd2xlciwgUGxheXdyaWdodENyYXdsaW5nQ29udGV4dFxcbmZyb20gY3Jhd2xlZS5wcm94eV9jb25maWd1cmF0aW9uIGltcG9ydCBQcm94eUNvbmZpZ3VyYXRpb25cXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgICMgQ3JlYXRlIGEgUHJveHlDb25maWd1cmF0aW9uIG9iamVjdCBhbmQgcGFzcyBpdCB0byB0aGUgY3Jhd2xlci5cXG4gICAgcHJveHlfY29uZmlndXJhdGlvbiA9IFByb3h5Q29uZmlndXJhdGlvbihcXG4gICAgICAgIHByb3h5X3VybHM9W1xcbiAgICAgICAgICAgICdodHRwOi8vcHJveHktMS5jb20vJyxcXG4gICAgICAgICAgICAnaHR0cDovL3Byb3h5LTIuY29tLycsXFxuICAgICAgICBdXFxuICAgIClcXG4gICAgY3Jhd2xlciA9IFBsYXl3cmlnaHRDcmF3bGVyKHByb3h5X2NvbmZpZ3VyYXRpb249cHJveHlfY29uZmlndXJhdGlvbilcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgZGVmYXVsdF9oYW5kbGVyKGNvbnRleHQ6IFBsYXl3cmlnaHRDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICAjIExvZyB0aGUgcHJveHkgdXNlZCBmb3IgdGhlIGN1cnJlbnQgcmVxdWVzdC5cXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm94eSBmb3IgdGhlIGN1cnJlbnQgcmVxdWVzdDoge2NvbnRleHQucHJveHlfaW5mb30nKVxcblxcbiAgICAjIFJ1biB0aGUgY3Jhd2xlciB3aXRoIHRoZSBpbml0aWFsIGxpc3Qgb2YgcmVxdWVzdHMuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9jcmF3bGVlLmRldi8nXSlcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6NDA5NiwidGltZW91dCI6MTgwfX0.CZkU8QCVY0TfZjeekwfNg0Srjj8hQIdWcTqvCJygy74\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext
from crawlee.proxy_configuration import ProxyConfiguration


async def main() -> None:
    # Create a ProxyConfiguration object and pass it to the crawler.
    proxy_configuration = ProxyConfiguration(
        proxy_urls=[
            'http://proxy-1.com/',
            'http://proxy-2.com/',
        ]
    )
    crawler = PlaywrightCrawler(proxy_configuration=proxy_configuration)

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def default_handler(context: PlaywrightCrawlingContext) -> None:
        # Log the proxy used for the current request.
        context.log.info(f'Proxy for the current request: {context.proxy_info}')

    # Run the crawler with the initial list of requests.
    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/guides/proxy_management.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/guides/playwright-crawler-stagehand.md)

[Playwright with Stagehand](https://crawlee.dev/python/python/docs/guides/playwright-crawler-stagehand.md)

[Next](https://crawlee.dev/python/python/docs/guides/request-loaders.md)

[Request loaders](https://crawlee.dev/python/python/docs/guides/request-loaders.md)


---

* [](https://crawlee.dev/python/python)
* [Guides](https://crawlee.dev/python/python/docs/guides.md)
* Request loaders

Version: 1.6

On this page

# Request loaders

The [`request_loaders`](https://github.com/apify/crawlee-python/tree/master/src/crawlee/request_loaders) sub-package extends the functionality of the [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md), providing additional tools for managing URLs and requests. If you are new to Crawlee and unfamiliar with the [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md), consider starting with the [Storages](https://crawlee.dev/python/python/docs/guides/storages.md) guide first. Request loaders define how requests are fetched and stored, enabling various use cases such as reading URLs from files, external APIs, or combining multiple sources together.

## Overview[​](#overview "Direct link to Overview")

The [`request_loaders`](https://github.com/apify/crawlee-python/tree/master/src/crawlee/request_loaders) sub-package introduces the following abstract classes:

* [`RequestLoader`](https://crawlee.dev/python/python/api/class/RequestLoader.md): The base interface for reading requests in a crawl.
* [`RequestManager`](https://crawlee.dev/python/python/api/class/RequestManager.md): Extends `RequestLoader` with write capabilities.
* [`RequestManagerTandem`](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md): Combines a read-only `RequestLoader` with a writable `RequestManager`.

And specific request loader implementations:

* [`RequestList`](https://crawlee.dev/python/python/api/class/RequestList.md): A lightweight implementation for managing a static list of URLs.
* [`SitemapRequestLoader`](https://crawlee.dev/python/python/api/class/SitemapRequestLoader.md): A specialized loader that reads URLs from XML and plain-text sitemaps following the [Sitemaps protocol](https://www.sitemaps.org/protocol.html) with filtering capabilities.

Below is a class diagram that illustrates the relationships between these components and the [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md):

<!-- -->

## Request loaders[​](#request-loaders "Direct link to Request loaders")

The [`RequestLoader`](https://crawlee.dev/python/python/api/class/RequestLoader.md) interface defines the foundation for fetching requests during a crawl. It provides abstract methods for basic operations like retrieving, marking, and checking the status of requests. Concrete implementations, such as [`RequestList`](https://crawlee.dev/python/python/api/class/RequestList.md), build on this interface to handle specific scenarios. You can create your own custom loader that reads from an external file, web endpoint, database, or any other specific data source. For more details, refer to the [`RequestLoader`](https://crawlee.dev/python/python/api/class/RequestLoader.md) API reference.

NOTE

To learn how to use request loaders in your crawlers, see the [Request manager tandem](#request-manager-tandem) section below.

### Request list[​](#request-list "Direct link to Request list")

The [`RequestList`](https://crawlee.dev/python/python/api/class/RequestList.md) can accept an asynchronous generator as input, allowing requests to be streamed rather than loading them all into memory at once. This can significantly reduce memory usage, especially when working with large sets of URLs.

Here is a basic example of working with the [`RequestList`](https://crawlee.dev/python/python/api/class/RequestList.md):

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLnJlcXVlc3RfbG9hZGVycyBpbXBvcnQgUmVxdWVzdExpc3RcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgICMgT3BlbiB0aGUgcmVxdWVzdCBsaXN0LCBpZiBpdCBkb2VzIG5vdCBleGlzdCwgaXQgd2lsbCBiZSBjcmVhdGVkLlxcbiAgICAjIExlYXZlIG5hbWUgZW1wdHkgdG8gdXNlIHRoZSBkZWZhdWx0IHJlcXVlc3QgbGlzdC5cXG4gICAgcmVxdWVzdF9saXN0ID0gUmVxdWVzdExpc3QoXFxuICAgICAgICBuYW1lPSdteS1yZXF1ZXN0LWxpc3QnLFxcbiAgICAgICAgcmVxdWVzdHM9W1xcbiAgICAgICAgICAgICdodHRwczovL2FwaWZ5LmNvbS8nLFxcbiAgICAgICAgICAgICdodHRwczovL2NyYXdsZWUuZGV2LycsXFxuICAgICAgICAgICAgJ2h0dHBzOi8vY3Jhd2xlZS5kZXYvcHl0aG9uLycsXFxuICAgICAgICBdLFxcbiAgICApXFxuXFxuICAgICMgRmV0Y2ggYW5kIHByb2Nlc3MgcmVxdWVzdHMgZnJvbSB0aGUgcXVldWUuXFxuICAgIHdoaWxlIHJlcXVlc3QgOj0gYXdhaXQgcmVxdWVzdF9saXN0LmZldGNoX25leHRfcmVxdWVzdCgpOlxcbiAgICAgICAgIyBEbyBzb21ldGhpbmcgd2l0aCBpdC4uLlxcbiAgICAgICAgcHJpbnQoZidQcm9jZXNzaW5nIHtyZXF1ZXN0LnVybH0nKVxcblxcbiAgICAgICAgIyBBbmQgbWFyayBpdCBhcyBoYW5kbGVkLlxcbiAgICAgICAgYXdhaXQgcmVxdWVzdF9saXN0Lm1hcmtfcmVxdWVzdF9hc19oYW5kbGVkKHJlcXVlc3QpXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.qhezd-3n1Jcyk7dglGnx7h1j_ETgdwC9SYEFrfdW3ts\&asrc=run_on_apify)

```
import asyncio

from crawlee.request_loaders import RequestList


async def main() -> None:
    # Open the request list, if it does not exist, it will be created.
    # Leave name empty to use the default request list.
    request_list = RequestList(
        name='my-request-list',
        requests=[
            'https://apify.com/',
            'https://crawlee.dev/',
            'https://crawlee.dev/python/',
        ],
    )

    # Fetch and process requests from the queue.
    while request := await request_list.fetch_next_request():
        # Do something with it...
        print(f'Processing {request.url}')

        # And mark it as handled.
        await request_list.mark_request_as_handled(request)


if __name__ == '__main__':
    asyncio.run(main())
```

### Request list with persistence[​](#request-list-with-persistence "Direct link to Request list with persistence")

The [`RequestList`](https://crawlee.dev/python/python/api/class/RequestList.md) supports state persistence, allowing it to resume from where it left off after interruption. This is particularly useful for long-running crawls or when you need to pause and resume crawling later.

To enable persistence, provide `persist_state_key` and optionally `persist_requests_key` parameters, and disable automatic cleanup by setting `purge_on_start = False` in the configuration. The `persist_state_key` saves the loader's progress, while `persist_requests_key` ensures that the request data doesn't change between runs. For more details on resuming interrupted crawls, see the [Resuming a paused crawl](https://crawlee.dev/python/python/docs/examples/resuming-paused-crawl.md) example.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuaW1wb3J0IGxvZ2dpbmdcXG5cXG5mcm9tIGNyYXdsZWUgaW1wb3J0IHNlcnZpY2VfbG9jYXRvclxcbmZyb20gY3Jhd2xlZS5yZXF1ZXN0X2xvYWRlcnMgaW1wb3J0IFJlcXVlc3RMaXN0XFxuXFxubG9nZ2luZy5iYXNpY0NvbmZpZyhsZXZlbD1sb2dnaW5nLklORk8sIGZvcm1hdD0nJShhc2N0aW1lKXMtJShsZXZlbG5hbWUpcy0lKG1lc3NhZ2UpcycpXFxubG9nZ2VyID0gbG9nZ2luZy5nZXRMb2dnZXIoX19uYW1lX18pXFxuXFxuXFxuIyBEaXNhYmxlIGNsZWFyaW5nIHRoZSBgS2V5VmFsdWVTdG9yZWAgb24gZWFjaCBydW4uXFxuIyBUaGlzIGlzIG5lY2Vzc2FyeSBzbyB0aGF0IHRoZSBzdGF0ZSBrZXlzIGFyZSBub3QgY2xlYXJlZCBhdCBzdGFydHVwLlxcbiMgVGhlIHJlY29tbWVuZGVkIHdheSB0byBhY2hpZXZlIHRoaXMgYmVoYXZpb3IgaXMgc2V0dGluZyB0aGUgZW52aXJvbm1lbnQgdmFyaWFibGVcXG4jIGBDUkFXTEVFX1BVUkdFX09OX1NUQVJUPTBgXFxuY29uZmlndXJhdGlvbiA9IHNlcnZpY2VfbG9jYXRvci5nZXRfY29uZmlndXJhdGlvbigpXFxuY29uZmlndXJhdGlvbi5wdXJnZV9vbl9zdGFydCA9IEZhbHNlXFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICAjIE9wZW4gdGhlIHJlcXVlc3QgbGlzdCwgaWYgaXQgZG9lcyBub3QgZXhpc3QsIGl0IHdpbGwgYmUgY3JlYXRlZC5cXG4gICAgIyBMZWF2ZSBuYW1lIGVtcHR5IHRvIHVzZSB0aGUgZGVmYXVsdCByZXF1ZXN0IGxpc3QuXFxuICAgIHJlcXVlc3RfbGlzdCA9IFJlcXVlc3RMaXN0KFxcbiAgICAgICAgbmFtZT0nbXktcmVxdWVzdC1saXN0JyxcXG4gICAgICAgIHJlcXVlc3RzPVtcXG4gICAgICAgICAgICAnaHR0cHM6Ly9hcGlmeS5jb20vJyxcXG4gICAgICAgICAgICAnaHR0cHM6Ly9jcmF3bGVlLmRldi8nLFxcbiAgICAgICAgICAgICdodHRwczovL2NyYXdsZWUuZGV2L3B5dGhvbi8nLFxcbiAgICAgICAgXSxcXG4gICAgICAgICMgRW5hYmxlIHBlcnNpc3RlbmNlXFxuICAgICAgICBwZXJzaXN0X3N0YXRlX2tleT0nbXktcGVyc2lzdC1zdGF0ZScsXFxuICAgICAgICBwZXJzaXN0X3JlcXVlc3RzX2tleT0nbXktcGVyc2lzdC1yZXF1ZXN0cycsXFxuICAgIClcXG5cXG4gICAgIyBXZSByZWNlaXZlIG9ubHkgb25lIHJlcXVlc3QuXFxuICAgICMgRWFjaCB0aW1lIHlvdSBydW4gaXQsIGl0IHdpbGwgYmUgYSBuZXcgcmVxdWVzdCB1bnRpbCB5b3UgZXhoYXVzdCB0aGUgYFJlcXVlc3RMaXN0YC5cXG4gICAgcmVxdWVzdCA9IGF3YWl0IHJlcXVlc3RfbGlzdC5mZXRjaF9uZXh0X3JlcXVlc3QoKVxcbiAgICBpZiByZXF1ZXN0OlxcbiAgICAgICAgbG9nZ2VyLmluZm8oZidQcm9jZXNzaW5nIHJlcXVlc3Q6IHtyZXF1ZXN0LnVybH0nKVxcbiAgICAgICAgIyBEbyBzb21ldGhpbmcgd2l0aCBpdC4uLlxcblxcbiAgICAgICAgIyBBbmQgbWFyayBpdCBhcyBoYW5kbGVkLlxcbiAgICAgICAgYXdhaXQgcmVxdWVzdF9saXN0Lm1hcmtfcmVxdWVzdF9hc19oYW5kbGVkKHJlcXVlc3QpXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.tBkyjj0kJ6vGZM4C6HKsK5oYOfYVwTyx4W617fK6dgE\&asrc=run_on_apify)

```
import asyncio
import logging

from crawlee import service_locator
from crawlee.request_loaders import RequestList

logging.basicConfig(level=logging.INFO, format='%(asctime)s-%(levelname)s-%(message)s')
logger = logging.getLogger(__name__)


# Disable clearing the `KeyValueStore` on each run.
# This is necessary so that the state keys are not cleared at startup.
# The recommended way to achieve this behavior is setting the environment variable
# `CRAWLEE_PURGE_ON_START=0`
configuration = service_locator.get_configuration()
configuration.purge_on_start = False


async def main() -> None:
    # Open the request list, if it does not exist, it will be created.
    # Leave name empty to use the default request list.
    request_list = RequestList(
        name='my-request-list',
        requests=[
            'https://apify.com/',
            'https://crawlee.dev/',
            'https://crawlee.dev/python/',
        ],
        # Enable persistence
        persist_state_key='my-persist-state',
        persist_requests_key='my-persist-requests',
    )

    # We receive only one request.
    # Each time you run it, it will be a new request until you exhaust the `RequestList`.
    request = await request_list.fetch_next_request()
    if request:
        logger.info(f'Processing request: {request.url}')
        # Do something with it...

        # And mark it as handled.
        await request_list.mark_request_as_handled(request)


if __name__ == '__main__':
    asyncio.run(main())
```

### Sitemap request loader[​](#sitemap-request-loader "Direct link to Sitemap request loader")

The [`SitemapRequestLoader`](https://crawlee.dev/python/python/api/class/SitemapRequestLoader.md) is a specialized request loader that reads URLs from sitemaps following the [Sitemaps protocol](https://www.sitemaps.org/protocol.html). It supports both XML and plain text sitemap formats. It's particularly useful when you want to crawl a website systematically by following its sitemap structure.

note

The `SitemapRequestLoader` is designed specifically for sitemaps that follow the standard Sitemaps protocol. HTML pages containing links are not supported by this loader - those should be handled by regular crawlers using the `enqueue_links` functionality.

The loader supports filtering URLs using glob patterns and regular expressions, allowing you to include or exclude specific types of URLs. The [`SitemapRequestLoader`](https://crawlee.dev/python/python/api/class/SitemapRequestLoader.md) provides streaming processing of sitemaps, ensuring efficient memory usage without loading the entire sitemap into memory.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuaW1wb3J0IHJlXFxuXFxuZnJvbSBjcmF3bGVlLmh0dHBfY2xpZW50cyBpbXBvcnQgSW1waXRIdHRwQ2xpZW50XFxuZnJvbSBjcmF3bGVlLnJlcXVlc3RfbG9hZGVycyBpbXBvcnQgU2l0ZW1hcFJlcXVlc3RMb2FkZXJcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgICMgQ3JlYXRlIGFuIEhUVFAgY2xpZW50IGZvciBmZXRjaGluZyB0aGUgc2l0ZW1hcC5cXG4gICAgaHR0cF9jbGllbnQgPSBJbXBpdEh0dHBDbGllbnQoKVxcblxcbiAgICAjIENyZWF0ZSBhIHNpdGVtYXAgcmVxdWVzdCBsb2FkZXIgd2l0aCBmaWx0ZXJpbmcgcnVsZXMuXFxuICAgIHNpdGVtYXBfbG9hZGVyID0gU2l0ZW1hcFJlcXVlc3RMb2FkZXIoXFxuICAgICAgICBzaXRlbWFwX3VybHM9WydodHRwczovL2NyYXdsZWUuZGV2L3NpdGVtYXAueG1sJ10sXFxuICAgICAgICBodHRwX2NsaWVudD1odHRwX2NsaWVudCxcXG4gICAgICAgIGluY2x1ZGU9W3JlLmNvbXBpbGUocicuKmRvY3MuKicpXSwgICMgT25seSBpbmNsdWRlIFVSTHMgY29udGFpbmluZyAnZG9jcycuXFxuICAgICAgICBtYXhfYnVmZmVyX3NpemU9NTAwLCAgIyBLZWVwIHVwIHRvIDUwMCBVUkxzIGluIG1lbW9yeSBiZWZvcmUgcHJvY2Vzc2luZy5cXG4gICAgKVxcblxcbiAgICAjIFdlIHdvcmsgd2l0aCB0aGUgbG9hZGVyIHVudGlsIHdlIHByb2Nlc3MgYWxsIHJlbGV2YW50IGxpbmtzIGZyb20gdGhlIHNpdGVtYXAuXFxuICAgIHdoaWxlIHJlcXVlc3QgOj0gYXdhaXQgc2l0ZW1hcF9sb2FkZXIuZmV0Y2hfbmV4dF9yZXF1ZXN0KCk6XFxuICAgICAgICAjIERvIHNvbWV0aGluZyB3aXRoIGl0Li4uXFxuICAgICAgICBwcmludChmJ1Byb2Nlc3Npbmcge3JlcXVlc3QudXJsfScpXFxuXFxuICAgICAgICAjIEFuZCBtYXJrIGl0IGFzIGhhbmRsZWQuXFxuICAgICAgICBhd2FpdCBzaXRlbWFwX2xvYWRlci5tYXJrX3JlcXVlc3RfYXNfaGFuZGxlZChyZXF1ZXN0KVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.vMkvAAsmDkBDHEQnSvLZjf_nySlyGBgd1Uhl3cBBGRw\&asrc=run_on_apify)

```
import asyncio
import re

from crawlee.http_clients import ImpitHttpClient
from crawlee.request_loaders import SitemapRequestLoader


async def main() -> None:
    # Create an HTTP client for fetching the sitemap.
    http_client = ImpitHttpClient()

    # Create a sitemap request loader with filtering rules.
    sitemap_loader = SitemapRequestLoader(
        sitemap_urls=['https://crawlee.dev/sitemap.xml'],
        http_client=http_client,
        include=[re.compile(r'.*docs.*')],  # Only include URLs containing 'docs'.
        max_buffer_size=500,  # Keep up to 500 URLs in memory before processing.
    )

    # We work with the loader until we process all relevant links from the sitemap.
    while request := await sitemap_loader.fetch_next_request():
        # Do something with it...
        print(f'Processing {request.url}')

        # And mark it as handled.
        await sitemap_loader.mark_request_as_handled(request)


if __name__ == '__main__':
    asyncio.run(main())
```

### Sitemap request loader with persistence[​](#sitemap-request-loader-with-persistence "Direct link to Sitemap request loader with persistence")

Similarly, the [`SitemapRequestLoader`](https://crawlee.dev/python/python/api/class/SitemapRequestLoader.md) supports state persistence to resume processing from where it left off. This is especially valuable when processing large sitemaps that may take considerable time to complete.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuaW1wb3J0IGxvZ2dpbmdcXG5cXG5mcm9tIGNyYXdsZWUgaW1wb3J0IHNlcnZpY2VfbG9jYXRvclxcbmZyb20gY3Jhd2xlZS5odHRwX2NsaWVudHMgaW1wb3J0IEltcGl0SHR0cENsaWVudFxcbmZyb20gY3Jhd2xlZS5yZXF1ZXN0X2xvYWRlcnMgaW1wb3J0IFNpdGVtYXBSZXF1ZXN0TG9hZGVyXFxuXFxubG9nZ2luZy5iYXNpY0NvbmZpZyhsZXZlbD1sb2dnaW5nLklORk8sIGZvcm1hdD0nJShhc2N0aW1lKXMtJShsZXZlbG5hbWUpcy0lKG1lc3NhZ2UpcycpXFxubG9nZ2VyID0gbG9nZ2luZy5nZXRMb2dnZXIoX19uYW1lX18pXFxuXFxuXFxuIyBEaXNhYmxlIGNsZWFyaW5nIHRoZSBgS2V5VmFsdWVTdG9yZWAgb24gZWFjaCBydW4uXFxuIyBUaGlzIGlzIG5lY2Vzc2FyeSBzbyB0aGF0IHRoZSBzdGF0ZSBrZXlzIGFyZSBub3QgY2xlYXJlZCBhdCBzdGFydHVwLlxcbiMgVGhlIHJlY29tbWVuZGVkIHdheSB0byBhY2hpZXZlIHRoaXMgYmVoYXZpb3IgaXMgc2V0dGluZyB0aGUgZW52aXJvbm1lbnQgdmFyaWFibGVcXG4jIGBDUkFXTEVFX1BVUkdFX09OX1NUQVJUPTBgXFxuY29uZmlndXJhdGlvbiA9IHNlcnZpY2VfbG9jYXRvci5nZXRfY29uZmlndXJhdGlvbigpXFxuY29uZmlndXJhdGlvbi5wdXJnZV9vbl9zdGFydCA9IEZhbHNlXFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICAjIENyZWF0ZSBhbiBIVFRQIGNsaWVudCBmb3IgZmV0Y2hpbmcgc2l0ZW1hcHNcXG4gICAgIyBVc2UgdGhlIGNvbnRleHQgbWFuYWdlciBmb3IgYFNpdGVtYXBSZXF1ZXN0TG9hZGVyYCB0byBjb3JyZWN0bHkgc2F2ZSB0aGUgc3RhdGUgd2hlblxcbiAgICAjIHRoZSB3b3JrIGlzIGNvbXBsZXRlZC5cXG4gICAgYXN5bmMgd2l0aCAoXFxuICAgICAgICBJbXBpdEh0dHBDbGllbnQoKSBhcyBodHRwX2NsaWVudCxcXG4gICAgICAgIFNpdGVtYXBSZXF1ZXN0TG9hZGVyKFxcbiAgICAgICAgICAgIHNpdGVtYXBfdXJscz1bJ2h0dHBzOi8vY3Jhd2xlZS5kZXYvc2l0ZW1hcC54bWwnXSxcXG4gICAgICAgICAgICBodHRwX2NsaWVudD1odHRwX2NsaWVudCxcXG4gICAgICAgICAgICAjIEVuYWJsZSBwZXJzaXN0ZW5jZVxcbiAgICAgICAgICAgIHBlcnNpc3Rfc3RhdGVfa2V5PSdteS1wZXJzaXN0LXN0YXRlJyxcXG4gICAgICAgICkgYXMgc2l0ZW1hcF9sb2FkZXIsXFxuICAgICk6XFxuICAgICAgICAjIFdlIHJlY2VpdmUgb25seSBvbmUgcmVxdWVzdC5cXG4gICAgICAgICMgRWFjaCB0aW1lIHlvdSBydW4gaXQsIGl0IHdpbGwgYmUgYSBuZXcgcmVxdWVzdCB1bnRpbCB5b3UgZXhoYXVzdCB0aGUgc2l0ZW1hcC5cXG4gICAgICAgIHJlcXVlc3QgPSBhd2FpdCBzaXRlbWFwX2xvYWRlci5mZXRjaF9uZXh0X3JlcXVlc3QoKVxcbiAgICAgICAgaWYgcmVxdWVzdDpcXG4gICAgICAgICAgICBsb2dnZXIuaW5mbyhmJ1Byb2Nlc3NpbmcgcmVxdWVzdDoge3JlcXVlc3QudXJsfScpXFxuICAgICAgICAgICAgIyBEbyBzb21ldGhpbmcgd2l0aCBpdC4uLlxcblxcbiAgICAgICAgICAgICMgQW5kIG1hcmsgaXQgYXMgaGFuZGxlZC5cXG4gICAgICAgICAgICBhd2FpdCBzaXRlbWFwX2xvYWRlci5tYXJrX3JlcXVlc3RfYXNfaGFuZGxlZChyZXF1ZXN0KVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.qENS0rYVbNwAMfiWRjIoX9mcXhqnrOVfjos9r8Zn6m0\&asrc=run_on_apify)

```
import asyncio
import logging

from crawlee import service_locator
from crawlee.http_clients import ImpitHttpClient
from crawlee.request_loaders import SitemapRequestLoader

logging.basicConfig(level=logging.INFO, format='%(asctime)s-%(levelname)s-%(message)s')
logger = logging.getLogger(__name__)


# Disable clearing the `KeyValueStore` on each run.
# This is necessary so that the state keys are not cleared at startup.
# The recommended way to achieve this behavior is setting the environment variable
# `CRAWLEE_PURGE_ON_START=0`
configuration = service_locator.get_configuration()
configuration.purge_on_start = False


async def main() -> None:
    # Create an HTTP client for fetching sitemaps
    # Use the context manager for `SitemapRequestLoader` to correctly save the state when
    # the work is completed.
    async with (
        ImpitHttpClient() as http_client,
        SitemapRequestLoader(
            sitemap_urls=['https://crawlee.dev/sitemap.xml'],
            http_client=http_client,
            # Enable persistence
            persist_state_key='my-persist-state',
        ) as sitemap_loader,
    ):
        # We receive only one request.
        # Each time you run it, it will be a new request until you exhaust the sitemap.
        request = await sitemap_loader.fetch_next_request()
        if request:
            logger.info(f'Processing request: {request.url}')
            # Do something with it...

            # And mark it as handled.
            await sitemap_loader.mark_request_as_handled(request)


if __name__ == '__main__':
    asyncio.run(main())
```

When using persistence with `SitemapRequestLoader`, make sure to use the context manager (`async with`) to properly save the state when the work is completed.

## Request managers[​](#request-managers "Direct link to Request managers")

The [`RequestManager`](https://crawlee.dev/python/python/api/class/RequestManager.md) extends `RequestLoader` with write capabilities. In addition to reading requests, a request manager can add and reclaim them. This is essential for dynamic crawling projects where new URLs may emerge during the crawl process, or when certain requests fail and need to be retried. For more details, refer to the [`RequestManager`](https://crawlee.dev/python/python/api/class/RequestManager.md) API reference.

## Request manager tandem[​](#request-manager-tandem "Direct link to Request manager tandem")

The [`RequestManagerTandem`](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md) class allows you to combine the read-only capabilities of a `RequestLoader` (like [`RequestList`](https://crawlee.dev/python/python/api/class/RequestList.md)) with the read-write capabilities of a `RequestManager` (like [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md)). This is useful for scenarios where you need to load initial requests from a static source (such as a file or database) and dynamically add or retry requests during the crawl. Additionally, it provides deduplication capabilities, ensuring that requests are not processed multiple times.

Under the hood, [`RequestManagerTandem`](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md) checks whether the read-only loader still has pending requests. If so, each new request from the loader is transferred to the manager. Any newly added or reclaimed requests go directly to the manager side.

### Request list with request queue[​](#request-list-with-request-queue "Direct link to Request list with request queue")

This section describes the combination of the [`RequestList`](https://crawlee.dev/python/python/api/class/RequestList.md) and [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md) classes. This setup is particularly useful when you have a static list of URLs that you want to crawl, but also need to handle dynamic requests discovered during the crawl process. The [`RequestManagerTandem`](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md) class facilitates this combination, with the [`RequestLoader.to_tandem`](https://crawlee.dev/python/python/api/class/RequestLoader.md#to_tandem) method available as a convenient shortcut. Requests from the [`RequestList`](https://crawlee.dev/python/python/api/class/RequestList.md) are processed first by being enqueued into the default [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md), which handles persistence and retries for failed requests.

* Explicit usage
* Using to\_tandem helper

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQYXJzZWxDcmF3bGVyLCBQYXJzZWxDcmF3bGluZ0NvbnRleHRcXG5mcm9tIGNyYXdsZWUucmVxdWVzdF9sb2FkZXJzIGltcG9ydCBSZXF1ZXN0TGlzdCwgUmVxdWVzdE1hbmFnZXJUYW5kZW1cXG5mcm9tIGNyYXdsZWUuc3RvcmFnZXMgaW1wb3J0IFJlcXVlc3RRdWV1ZVxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBDcmVhdGUgYSBzdGF0aWMgcmVxdWVzdCBsaXN0LlxcbiAgICByZXF1ZXN0X2xpc3QgPSBSZXF1ZXN0TGlzdChbJ2h0dHBzOi8vY3Jhd2xlZS5kZXYnLCAnaHR0cHM6Ly9hcGlmeS5jb20nXSlcXG5cXG4gICAgIyBPcGVuIHRoZSBkZWZhdWx0IHJlcXVlc3QgcXVldWUuXFxuICAgIHJlcXVlc3RfcXVldWUgPSBhd2FpdCBSZXF1ZXN0UXVldWUub3BlbigpXFxuXFxuICAgICMgQW5kIGNvbWJpbmUgdGhlbSB0b2dldGhlciB0byBhIHNpbmdsZSByZXF1ZXN0IG1hbmFnZXIuXFxuICAgIHJlcXVlc3RfbWFuYWdlciA9IFJlcXVlc3RNYW5hZ2VyVGFuZGVtKHJlcXVlc3RfbGlzdCwgcmVxdWVzdF9xdWV1ZSlcXG5cXG4gICAgIyBDcmVhdGUgYSBjcmF3bGVyIGFuZCBwYXNzIHRoZSByZXF1ZXN0IG1hbmFnZXIgdG8gaXQuXFxuICAgIGNyYXdsZXIgPSBQYXJzZWxDcmF3bGVyKFxcbiAgICAgICAgcmVxdWVzdF9tYW5hZ2VyPXJlcXVlc3RfbWFuYWdlcixcXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsICAjIExpbWl0IHRoZSBtYXggcmVxdWVzdHMgcGVyIGNyYXdsLlxcbiAgICApXFxuXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIGhhbmRsZXIoY29udGV4dDogUGFyc2VsQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ1Byb2Nlc3Npbmcge2NvbnRleHQucmVxdWVzdC51cmx9JylcXG5cXG4gICAgICAgICMgTmV3IGxpbmtzIHdpbGwgYmUgZW5xdWV1ZWQgZGlyZWN0bHkgdG8gdGhlIHF1ZXVlLlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5lbnF1ZXVlX2xpbmtzKClcXG5cXG4gICAgICAgICMgRXh0cmFjdCBkYXRhIHVzaW5nIFBhcnNlbCdzIFhQYXRoIGFuZCBDU1Mgc2VsZWN0b3JzLlxcbiAgICAgICAgZGF0YSA9IHtcXG4gICAgICAgICAgICAndXJsJzogY29udGV4dC5yZXF1ZXN0LnVybCxcXG4gICAgICAgICAgICAndGl0bGUnOiBjb250ZXh0LnNlbGVjdG9yLnhwYXRoKCcvL3RpdGxlL3RleHQoKScpLmdldCgpLFxcbiAgICAgICAgfVxcblxcbiAgICAgICAgIyBQdXNoIGV4dHJhY3RlZCBkYXRhIHRvIHRoZSBkYXRhc2V0LlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5wdXNoX2RhdGEoZGF0YSlcXG5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.bhGLKImCsyaO1pHENuPHCG4q5F63hwJPkfmV4Cx80_c\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import ParselCrawler, ParselCrawlingContext
from crawlee.request_loaders import RequestList, RequestManagerTandem
from crawlee.storages import RequestQueue


async def main() -> None:
    # Create a static request list.
    request_list = RequestList(['https://crawlee.dev', 'https://apify.com'])

    # Open the default request queue.
    request_queue = await RequestQueue.open()

    # And combine them together to a single request manager.
    request_manager = RequestManagerTandem(request_list, request_queue)

    # Create a crawler and pass the request manager to it.
    crawler = ParselCrawler(
        request_manager=request_manager,
        max_requests_per_crawl=10,  # Limit the max requests per crawl.
    )

    @crawler.router.default_handler
    async def handler(context: ParselCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url}')

        # New links will be enqueued directly to the queue.
        await context.enqueue_links()

        # Extract data using Parsel's XPath and CSS selectors.
        data = {
            'url': context.request.url,
            'title': context.selector.xpath('//title/text()').get(),
        }

        # Push extracted data to the dataset.
        await context.push_data(data)

    await crawler.run()


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQYXJzZWxDcmF3bGVyLCBQYXJzZWxDcmF3bGluZ0NvbnRleHRcXG5mcm9tIGNyYXdsZWUucmVxdWVzdF9sb2FkZXJzIGltcG9ydCBSZXF1ZXN0TGlzdFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBDcmVhdGUgYSBzdGF0aWMgcmVxdWVzdCBsaXN0LlxcbiAgICByZXF1ZXN0X2xpc3QgPSBSZXF1ZXN0TGlzdChbJ2h0dHBzOi8vY3Jhd2xlZS5kZXYnLCAnaHR0cHM6Ly9hcGlmeS5jb20nXSlcXG5cXG4gICAgIyBoaWdobGlnaHQtc3RhcnRcXG4gICAgIyBDb252ZXJ0IHRoZSByZXF1ZXN0IGxpc3QgdG8gYSByZXF1ZXN0IG1hbmFnZXIgdXNpbmcgdGhlIHRvX3RhbmRlbSBtZXRob2QuXFxuICAgICMgSXQgaXMgYSB0YW5kZW0gd2l0aCB0aGUgZGVmYXVsdCByZXF1ZXN0IHF1ZXVlLlxcbiAgICByZXF1ZXN0X21hbmFnZXIgPSBhd2FpdCByZXF1ZXN0X2xpc3QudG9fdGFuZGVtKClcXG4gICAgIyBoaWdobGlnaHQtZW5kXFxuXFxuICAgICMgQ3JlYXRlIGEgY3Jhd2xlciBhbmQgcGFzcyB0aGUgcmVxdWVzdCBtYW5hZ2VyIHRvIGl0LlxcbiAgICBjcmF3bGVyID0gUGFyc2VsQ3Jhd2xlcihcXG4gICAgICAgIHJlcXVlc3RfbWFuYWdlcj1yZXF1ZXN0X21hbmFnZXIsXFxuICAgICAgICBtYXhfcmVxdWVzdHNfcGVyX2NyYXdsPTEwLCAgIyBMaW1pdCB0aGUgbWF4IHJlcXVlc3RzIHBlciBjcmF3bC5cXG4gICAgKVxcblxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiBoYW5kbGVyKGNvbnRleHQ6IFBhcnNlbENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm9jZXNzaW5nIHtjb250ZXh0LnJlcXVlc3QudXJsfScpXFxuXFxuICAgICAgICAjIE5ldyBsaW5rcyB3aWxsIGJlIGVucXVldWVkIGRpcmVjdGx5IHRvIHRoZSBxdWV1ZS5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQuZW5xdWV1ZV9saW5rcygpXFxuXFxuICAgICAgICAjIEV4dHJhY3QgZGF0YSB1c2luZyBQYXJzZWwncyBYUGF0aCBhbmQgQ1NTIHNlbGVjdG9ycy5cXG4gICAgICAgIGRhdGEgPSB7XFxuICAgICAgICAgICAgJ3VybCc6IGNvbnRleHQucmVxdWVzdC51cmwsXFxuICAgICAgICAgICAgJ3RpdGxlJzogY29udGV4dC5zZWxlY3Rvci54cGF0aCgnLy90aXRsZS90ZXh0KCknKS5nZXQoKSxcXG4gICAgICAgIH1cXG5cXG4gICAgICAgICMgUHVzaCBleHRyYWN0ZWQgZGF0YSB0byB0aGUgZGF0YXNldC5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQucHVzaF9kYXRhKGRhdGEpXFxuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKClcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6MTAyNCwidGltZW91dCI6MTgwfX0.S40KyKGuRCFqrCtkeESiqYXo_RQ-f9RnKF1cojIPFE4\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import ParselCrawler, ParselCrawlingContext
from crawlee.request_loaders import RequestList


async def main() -> None:
    # Create a static request list.
    request_list = RequestList(['https://crawlee.dev', 'https://apify.com'])

    # Convert the request list to a request manager using the to_tandem method.
    # It is a tandem with the default request queue.
    request_manager = await request_list.to_tandem()

    # Create a crawler and pass the request manager to it.
    crawler = ParselCrawler(
        request_manager=request_manager,
        max_requests_per_crawl=10,  # Limit the max requests per crawl.
    )

    @crawler.router.default_handler
    async def handler(context: ParselCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url}')

        # New links will be enqueued directly to the queue.
        await context.enqueue_links()

        # Extract data using Parsel's XPath and CSS selectors.
        data = {
            'url': context.request.url,
            'title': context.selector.xpath('//title/text()').get(),
        }

        # Push extracted data to the dataset.
        await context.push_data(data)

    await crawler.run()


if __name__ == '__main__':
    asyncio.run(main())
```

### Sitemap request loader with request queue[​](#sitemap-request-loader-with-request-queue "Direct link to Sitemap request loader with request queue")

Similar to the [`RequestList`](https://crawlee.dev/python/python/api/class/RequestList.md) example above, you can combine a [`SitemapRequestLoader`](https://crawlee.dev/python/python/api/class/SitemapRequestLoader.md) with a [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md) using the [`RequestManagerTandem`](https://crawlee.dev/python/python/api/class/RequestManagerTandem.md) class. This setup is particularly useful when you want to crawl URLs from a sitemap while also handling dynamic requests discovered during the crawl process. URLs from the sitemap are processed first by being enqueued into the default [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md), which handles persistence and retries for failed requests.

* Explicit usage
* Using to\_tandem helper

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuaW1wb3J0IHJlXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQYXJzZWxDcmF3bGVyLCBQYXJzZWxDcmF3bGluZ0NvbnRleHRcXG5mcm9tIGNyYXdsZWUuaHR0cF9jbGllbnRzIGltcG9ydCBJbXBpdEh0dHBDbGllbnRcXG5mcm9tIGNyYXdsZWUucmVxdWVzdF9sb2FkZXJzIGltcG9ydCBSZXF1ZXN0TWFuYWdlclRhbmRlbSwgU2l0ZW1hcFJlcXVlc3RMb2FkZXJcXG5mcm9tIGNyYXdsZWUuc3RvcmFnZXMgaW1wb3J0IFJlcXVlc3RRdWV1ZVxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBDcmVhdGUgYW4gSFRUUCBjbGllbnQgZm9yIGZldGNoaW5nIHRoZSBzaXRlbWFwLlxcbiAgICBodHRwX2NsaWVudCA9IEltcGl0SHR0cENsaWVudCgpXFxuXFxuICAgICMgQ3JlYXRlIGEgc2l0ZW1hcCByZXF1ZXN0IGxvYWRlciB3aXRoIGZpbHRlcmluZyBydWxlcy5cXG4gICAgc2l0ZW1hcF9sb2FkZXIgPSBTaXRlbWFwUmVxdWVzdExvYWRlcihcXG4gICAgICAgIHNpdGVtYXBfdXJscz1bJ2h0dHBzOi8vY3Jhd2xlZS5kZXYvc2l0ZW1hcC54bWwnXSxcXG4gICAgICAgIGh0dHBfY2xpZW50PWh0dHBfY2xpZW50LFxcbiAgICAgICAgaW5jbHVkZT1bcmUuY29tcGlsZShyJy4qZG9jcy4qJyldLCAgIyBPbmx5IGluY2x1ZGUgVVJMcyBjb250YWluaW5nICdkb2NzJy5cXG4gICAgICAgIG1heF9idWZmZXJfc2l6ZT01MDAsICAjIEtlZXAgdXAgdG8gNTAwIFVSTHMgaW4gbWVtb3J5IGJlZm9yZSBwcm9jZXNzaW5nLlxcbiAgICApXFxuXFxuICAgICMgT3BlbiB0aGUgZGVmYXVsdCByZXF1ZXN0IHF1ZXVlLlxcbiAgICByZXF1ZXN0X3F1ZXVlID0gYXdhaXQgUmVxdWVzdFF1ZXVlLm9wZW4oKVxcblxcbiAgICAjIEFuZCBjb21iaW5lIHRoZW0gdG9nZXRoZXIgdG8gYSBzaW5nbGUgcmVxdWVzdCBtYW5hZ2VyLlxcbiAgICByZXF1ZXN0X21hbmFnZXIgPSBSZXF1ZXN0TWFuYWdlclRhbmRlbShzaXRlbWFwX2xvYWRlciwgcmVxdWVzdF9xdWV1ZSlcXG5cXG4gICAgIyBDcmVhdGUgYSBjcmF3bGVyIGFuZCBwYXNzIHRoZSByZXF1ZXN0IG1hbmFnZXIgdG8gaXQuXFxuICAgIGNyYXdsZXIgPSBQYXJzZWxDcmF3bGVyKFxcbiAgICAgICAgcmVxdWVzdF9tYW5hZ2VyPXJlcXVlc3RfbWFuYWdlcixcXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsICAjIExpbWl0IHRoZSBtYXggcmVxdWVzdHMgcGVyIGNyYXdsLlxcbiAgICApXFxuXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIGhhbmRsZXIoY29udGV4dDogUGFyc2VsQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ1Byb2Nlc3Npbmcge2NvbnRleHQucmVxdWVzdC51cmx9JylcXG5cXG4gICAgICAgICMgTmV3IGxpbmtzIHdpbGwgYmUgZW5xdWV1ZWQgZGlyZWN0bHkgdG8gdGhlIHF1ZXVlLlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5lbnF1ZXVlX2xpbmtzKClcXG5cXG4gICAgICAgICMgRXh0cmFjdCBkYXRhIHVzaW5nIFBhcnNlbCdzIFhQYXRoIGFuZCBDU1Mgc2VsZWN0b3JzLlxcbiAgICAgICAgZGF0YSA9IHtcXG4gICAgICAgICAgICAndXJsJzogY29udGV4dC5yZXF1ZXN0LnVybCxcXG4gICAgICAgICAgICAndGl0bGUnOiBjb250ZXh0LnNlbGVjdG9yLnhwYXRoKCcvL3RpdGxlL3RleHQoKScpLmdldCgpLFxcbiAgICAgICAgfVxcblxcbiAgICAgICAgIyBQdXNoIGV4dHJhY3RlZCBkYXRhIHRvIHRoZSBkYXRhc2V0LlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5wdXNoX2RhdGEoZGF0YSlcXG5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.TmGxZAQ0dhmZ0dfhEPttSN21qHHBIVm3v8D-6YHz4w8\&asrc=run_on_apify)

```
import asyncio
import re

from crawlee.crawlers import ParselCrawler, ParselCrawlingContext
from crawlee.http_clients import ImpitHttpClient
from crawlee.request_loaders import RequestManagerTandem, SitemapRequestLoader
from crawlee.storages import RequestQueue


async def main() -> None:
    # Create an HTTP client for fetching the sitemap.
    http_client = ImpitHttpClient()

    # Create a sitemap request loader with filtering rules.
    sitemap_loader = SitemapRequestLoader(
        sitemap_urls=['https://crawlee.dev/sitemap.xml'],
        http_client=http_client,
        include=[re.compile(r'.*docs.*')],  # Only include URLs containing 'docs'.
        max_buffer_size=500,  # Keep up to 500 URLs in memory before processing.
    )

    # Open the default request queue.
    request_queue = await RequestQueue.open()

    # And combine them together to a single request manager.
    request_manager = RequestManagerTandem(sitemap_loader, request_queue)

    # Create a crawler and pass the request manager to it.
    crawler = ParselCrawler(
        request_manager=request_manager,
        max_requests_per_crawl=10,  # Limit the max requests per crawl.
    )

    @crawler.router.default_handler
    async def handler(context: ParselCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url}')

        # New links will be enqueued directly to the queue.
        await context.enqueue_links()

        # Extract data using Parsel's XPath and CSS selectors.
        data = {
            'url': context.request.url,
            'title': context.selector.xpath('//title/text()').get(),
        }

        # Push extracted data to the dataset.
        await context.push_data(data)

    await crawler.run()


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuaW1wb3J0IHJlXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQYXJzZWxDcmF3bGVyLCBQYXJzZWxDcmF3bGluZ0NvbnRleHRcXG5mcm9tIGNyYXdsZWUuaHR0cF9jbGllbnRzIGltcG9ydCBJbXBpdEh0dHBDbGllbnRcXG5mcm9tIGNyYXdsZWUucmVxdWVzdF9sb2FkZXJzIGltcG9ydCBTaXRlbWFwUmVxdWVzdExvYWRlclxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBDcmVhdGUgYW4gSFRUUCBjbGllbnQgZm9yIGZldGNoaW5nIHRoZSBzaXRlbWFwLlxcbiAgICBodHRwX2NsaWVudCA9IEltcGl0SHR0cENsaWVudCgpXFxuXFxuICAgICMgQ3JlYXRlIGEgc2l0ZW1hcCByZXF1ZXN0IGxvYWRlciB3aXRoIGZpbHRlcmluZyBydWxlcy5cXG4gICAgc2l0ZW1hcF9sb2FkZXIgPSBTaXRlbWFwUmVxdWVzdExvYWRlcihcXG4gICAgICAgIHNpdGVtYXBfdXJscz1bJ2h0dHBzOi8vY3Jhd2xlZS5kZXYvc2l0ZW1hcC54bWwnXSxcXG4gICAgICAgIGh0dHBfY2xpZW50PWh0dHBfY2xpZW50LFxcbiAgICAgICAgaW5jbHVkZT1bcmUuY29tcGlsZShyJy4qZG9jcy4qJyldLCAgIyBPbmx5IGluY2x1ZGUgVVJMcyBjb250YWluaW5nICdkb2NzJy5cXG4gICAgICAgIG1heF9idWZmZXJfc2l6ZT01MDAsICAjIEtlZXAgdXAgdG8gNTAwIFVSTHMgaW4gbWVtb3J5IGJlZm9yZSBwcm9jZXNzaW5nLlxcbiAgICApXFxuXFxuICAgICMgaGlnaGxpZ2h0LXN0YXJ0XFxuICAgICMgQ29udmVydCB0aGUgc2l0ZW1hcCBsb2FkZXIgaW50byBhIHJlcXVlc3QgbWFuYWdlciBsaW5rZWRcXG4gICAgIyB0byB0aGUgZGVmYXVsdCByZXF1ZXN0IHF1ZXVlLlxcbiAgICByZXF1ZXN0X21hbmFnZXIgPSBhd2FpdCBzaXRlbWFwX2xvYWRlci50b190YW5kZW0oKVxcbiAgICAjIGhpZ2hsaWdodC1lbmRcXG5cXG4gICAgIyBDcmVhdGUgYSBjcmF3bGVyIGFuZCBwYXNzIHRoZSByZXF1ZXN0IG1hbmFnZXIgdG8gaXQuXFxuICAgIGNyYXdsZXIgPSBQYXJzZWxDcmF3bGVyKFxcbiAgICAgICAgcmVxdWVzdF9tYW5hZ2VyPXJlcXVlc3RfbWFuYWdlcixcXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsICAjIExpbWl0IHRoZSBtYXggcmVxdWVzdHMgcGVyIGNyYXdsLlxcbiAgICApXFxuXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIGhhbmRsZXIoY29udGV4dDogUGFyc2VsQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ1Byb2Nlc3Npbmcge2NvbnRleHQucmVxdWVzdC51cmx9JylcXG5cXG4gICAgICAgICMgTmV3IGxpbmtzIHdpbGwgYmUgZW5xdWV1ZWQgZGlyZWN0bHkgdG8gdGhlIHF1ZXVlLlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5lbnF1ZXVlX2xpbmtzKClcXG5cXG4gICAgICAgICMgRXh0cmFjdCBkYXRhIHVzaW5nIFBhcnNlbCdzIFhQYXRoIGFuZCBDU1Mgc2VsZWN0b3JzLlxcbiAgICAgICAgZGF0YSA9IHtcXG4gICAgICAgICAgICAndXJsJzogY29udGV4dC5yZXF1ZXN0LnVybCxcXG4gICAgICAgICAgICAndGl0bGUnOiBjb250ZXh0LnNlbGVjdG9yLnhwYXRoKCcvL3RpdGxlL3RleHQoKScpLmdldCgpLFxcbiAgICAgICAgfVxcblxcbiAgICAgICAgIyBQdXNoIGV4dHJhY3RlZCBkYXRhIHRvIHRoZSBkYXRhc2V0LlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5wdXNoX2RhdGEoZGF0YSlcXG5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.fguglk0Me86sRsZ22d_6kcBzxL7qTz2aHLJP65r1DJE\&asrc=run_on_apify)

```
import asyncio
import re

from crawlee.crawlers import ParselCrawler, ParselCrawlingContext
from crawlee.http_clients import ImpitHttpClient
from crawlee.request_loaders import SitemapRequestLoader


async def main() -> None:
    # Create an HTTP client for fetching the sitemap.
    http_client = ImpitHttpClient()

    # Create a sitemap request loader with filtering rules.
    sitemap_loader = SitemapRequestLoader(
        sitemap_urls=['https://crawlee.dev/sitemap.xml'],
        http_client=http_client,
        include=[re.compile(r'.*docs.*')],  # Only include URLs containing 'docs'.
        max_buffer_size=500,  # Keep up to 500 URLs in memory before processing.
    )

    # Convert the sitemap loader into a request manager linked
    # to the default request queue.
    request_manager = await sitemap_loader.to_tandem()

    # Create a crawler and pass the request manager to it.
    crawler = ParselCrawler(
        request_manager=request_manager,
        max_requests_per_crawl=10,  # Limit the max requests per crawl.
    )

    @crawler.router.default_handler
    async def handler(context: ParselCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url}')

        # New links will be enqueued directly to the queue.
        await context.enqueue_links()

        # Extract data using Parsel's XPath and CSS selectors.
        data = {
            'url': context.request.url,
            'title': context.selector.xpath('//title/text()').get(),
        }

        # Push extracted data to the dataset.
        await context.push_data(data)

    await crawler.run()


if __name__ == '__main__':
    asyncio.run(main())
```

## Conclusion[​](#conclusion "Direct link to Conclusion")

This guide explained the `request_loaders` sub-package, which extends the functionality of the `RequestQueue` with additional tools for managing URLs and requests. You learned about the `RequestLoader`, `RequestManager`, and `RequestManagerTandem` classes, as well as the `RequestList` and `SitemapRequestLoader` implementations. You also saw practical examples of how to work with these classes to handle various crawling scenarios.

If you have questions or need assistance, feel free to reach out on our [GitHub](https://github.com/apify/crawlee-python) or join our [Discord community](https://discord.com/invite/jyEM2PRvMU). Happy scraping!

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/guides/request_loaders.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/guides/proxy-management.md)

[Proxy management](https://crawlee.dev/python/python/docs/guides/proxy-management.md)

[Next](https://crawlee.dev/python/python/docs/guides/request-router.md)

[Request router](https://crawlee.dev/python/python/docs/guides/request-router.md)


---

* [](https://crawlee.dev/python/python)
* [Guides](https://crawlee.dev/python/python/docs/guides.md)
* Request router

Version: 1.6

On this page

# Request router

The [`Router`](https://crawlee.dev/python/python/api/class/Router.md) class manages request flow and coordinates the execution of user-defined logic in Crawlee projects. It routes incoming requests to appropriate user-defined handlers based on labels, manages error scenarios, and provides hooks for pre-navigation execution. The [`Router`](https://crawlee.dev/python/python/api/class/Router.md) serves as the orchestrator for all crawling operations, ensuring that each request is processed by the correct handler according to its type and label.

## Request handlers[​](#request-handlers "Direct link to Request handlers")

Request handlers are user-defined functions that process individual requests and their corresponding responses. Each handler receives a crawling context as its primary argument, which provides access to the current request, response data, and utility methods for data extraction, link enqueuing, and storage operations. Handlers determine how different types of pages are processed and how data is extracted and stored.

note

The code examples in this guide use [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md) for demonstration, but the [`Router`](https://crawlee.dev/python/python/api/class/Router.md) works with all crawler types.

### Built-in router[​](#built-in-router "Direct link to Built-in router")

Every crawler instance includes a built-in [`Router`](https://crawlee.dev/python/python/api/class/Router.md) accessible through the `crawler.router` property. This approach simplifies initial setup and covers basic use cases where request routing requirements are straightforward.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQYXJzZWxDcmF3bGVyLCBQYXJzZWxDcmF3bGluZ0NvbnRleHRcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgICMgQ3JlYXRlIGEgY3Jhd2xlciBpbnN0YW5jZVxcbiAgICBjcmF3bGVyID0gUGFyc2VsQ3Jhd2xlcihcXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsICAjIExpbWl0IHRoZSBtYXggcmVxdWVzdHMgcGVyIGNyYXdsLlxcbiAgICApXFxuXFxuICAgICMgVXNlIHRoZSBjcmF3bGVyJ3MgYnVpbHQtaW4gcm91dGVyIHRvIGRlZmluZSBhIGRlZmF1bHQgaGFuZGxlclxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiBkZWZhdWx0X2hhbmRsZXIoY29udGV4dDogUGFyc2VsQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ1Byb2Nlc3Npbmcge2NvbnRleHQucmVxdWVzdC51cmx9JylcXG5cXG4gICAgICAgICMgRXh0cmFjdCBwYWdlIHRpdGxlXFxuICAgICAgICB0aXRsZSA9IGNvbnRleHQuc2VsZWN0b3IuY3NzKCd0aXRsZTo6dGV4dCcpLmdldCgpIG9yICdObyB0aXRsZSBmb3VuZCdcXG5cXG4gICAgICAgICMgRXh0cmFjdCBhbmQgc2F2ZSBiYXNpYyBwYWdlIGRhdGFcXG4gICAgICAgIGF3YWl0IGNvbnRleHQucHVzaF9kYXRhKFxcbiAgICAgICAgICAgIHtcXG4gICAgICAgICAgICAgICAgJ3VybCc6IGNvbnRleHQucmVxdWVzdC51cmwsXFxuICAgICAgICAgICAgICAgICd0aXRsZSc6IHRpdGxlLFxcbiAgICAgICAgICAgIH1cXG4gICAgICAgIClcXG5cXG4gICAgICAgICMgRmluZCBhbmQgZW5xdWV1ZSBwcm9kdWN0IGxpbmtzIGZvciBmdXJ0aGVyIGNyYXdsaW5nXFxuICAgICAgICBhd2FpdCBjb250ZXh0LmVucXVldWVfbGlua3Moc2VsZWN0b3I9J2FbaHJlZio9XFxcIi9wcm9kdWN0cy9cXFwiXScsIGxhYmVsPSdQUk9EVUNUJylcXG5cXG4gICAgIyBTdGFydCBjcmF3bGluZ1xcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vd2FyZWhvdXNlLXRoZW1lLW1ldGFsLm15c2hvcGlmeS5jb20vJ10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.5mnBxlq6TdrSyTTcKOgmXFF6Kne8UE_c1NGza5dkmGU\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import ParselCrawler, ParselCrawlingContext


async def main() -> None:
    # Create a crawler instance
    crawler = ParselCrawler(
        max_requests_per_crawl=10,  # Limit the max requests per crawl.
    )

    # Use the crawler's built-in router to define a default handler
    @crawler.router.default_handler
    async def default_handler(context: ParselCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url}')

        # Extract page title
        title = context.selector.css('title::text').get() or 'No title found'

        # Extract and save basic page data
        await context.push_data(
            {
                'url': context.request.url,
                'title': title,
            }
        )

        # Find and enqueue product links for further crawling
        await context.enqueue_links(selector='a[href*="/products/"]', label='PRODUCT')

    # Start crawling
    await crawler.run(['https://warehouse-theme-metal.myshopify.com/'])


if __name__ == '__main__':
    asyncio.run(main())
```

The default handler processes all requests that either lack a label or have a label for which no specific handler has been registered.

### Custom router[​](#custom-router "Direct link to Custom router")

Applications requiring explicit control over router configuration or router reuse across multiple crawler instances can create custom [`Router`](https://crawlee.dev/python/python/api/class/Router.md) instances. Custom routers provide complete control over request routing configuration and enable modular application architecture. Router instances can be configured independently and attached to your crawler instances as needed.

You can also implement a custom request router class from scratch or by inheriting from [`Router`](https://crawlee.dev/python/python/api/class/Router.md). This allows you to define custom routing logic or manage request handlers in a different way.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQYXJzZWxDcmF3bGVyLCBQYXJzZWxDcmF3bGluZ0NvbnRleHRcXG5mcm9tIGNyYXdsZWUucm91dGVyIGltcG9ydCBSb3V0ZXJcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgICMgQ3JlYXRlIGEgY3VzdG9tIHJvdXRlciBpbnN0YW5jZVxcbiAgICByb3V0ZXIgPSBSb3V0ZXJbUGFyc2VsQ3Jhd2xpbmdDb250ZXh0XSgpXFxuXFxuICAgICMgRGVmaW5lIG9ubHkgYSBkZWZhdWx0IGhhbmRsZXJcXG4gICAgQHJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIGRlZmF1bHRfaGFuZGxlcihjb250ZXh0OiBQYXJzZWxDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0nKVxcblxcbiAgICAgICAgIyBFeHRyYWN0IHBhZ2UgdGl0bGVcXG4gICAgICAgIHRpdGxlID0gY29udGV4dC5zZWxlY3Rvci5jc3MoJ3RpdGxlOjp0ZXh0JykuZ2V0KCkgb3IgJ05vIHRpdGxlIGZvdW5kJ1xcblxcbiAgICAgICAgIyBFeHRyYWN0IGFuZCBzYXZlIGJhc2ljIHBhZ2UgZGF0YVxcbiAgICAgICAgYXdhaXQgY29udGV4dC5wdXNoX2RhdGEoXFxuICAgICAgICAgICAge1xcbiAgICAgICAgICAgICAgICAndXJsJzogY29udGV4dC5yZXF1ZXN0LnVybCxcXG4gICAgICAgICAgICAgICAgJ3RpdGxlJzogdGl0bGUsXFxuICAgICAgICAgICAgfVxcbiAgICAgICAgKVxcblxcbiAgICAgICAgIyBGaW5kIGFuZCBlbnF1ZXVlIHByb2R1Y3QgbGlua3MgZm9yIGZ1cnRoZXIgY3Jhd2xpbmdcXG4gICAgICAgIGF3YWl0IGNvbnRleHQuZW5xdWV1ZV9saW5rcyhcXG4gICAgICAgICAgICBzZWxlY3Rvcj0nYVtocmVmKj1cXFwiL3Byb2R1Y3RzL1xcXCJdJyxcXG4gICAgICAgICAgICBsYWJlbD0nUFJPRFVDVCcsICAjIE5vdGU6IG5vIGhhbmRsZXIgZm9yIHRoaXMgbGFiZWwsIHdpbGwgdXNlIGRlZmF1bHRcXG4gICAgICAgIClcXG5cXG4gICAgIyBDcmVhdGUgY3Jhd2xlciB3aXRoIHRoZSBjdXN0b20gcm91dGVyXFxuICAgIGNyYXdsZXIgPSBQYXJzZWxDcmF3bGVyKFxcbiAgICAgICAgcmVxdWVzdF9oYW5kbGVyPXJvdXRlcixcXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsICAjIExpbWl0IHRoZSBtYXggcmVxdWVzdHMgcGVyIGNyYXdsLlxcbiAgICApXFxuXFxuICAgICMgU3RhcnQgY3Jhd2xpbmdcXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL3dhcmVob3VzZS10aGVtZS1tZXRhbC5teXNob3BpZnkuY29tLyddKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.MRNLsHxurF2yf2sbfscYRCQleUdpT6O-4VrL5cRLuq4\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import ParselCrawler, ParselCrawlingContext
from crawlee.router import Router


async def main() -> None:
    # Create a custom router instance
    router = Router[ParselCrawlingContext]()

    # Define only a default handler
    @router.default_handler
    async def default_handler(context: ParselCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url}')

        # Extract page title
        title = context.selector.css('title::text').get() or 'No title found'

        # Extract and save basic page data
        await context.push_data(
            {
                'url': context.request.url,
                'title': title,
            }
        )

        # Find and enqueue product links for further crawling
        await context.enqueue_links(
            selector='a[href*="/products/"]',
            label='PRODUCT',  # Note: no handler for this label, will use default
        )

    # Create crawler with the custom router
    crawler = ParselCrawler(
        request_handler=router,
        max_requests_per_crawl=10,  # Limit the max requests per crawl.
    )

    # Start crawling
    await crawler.run(['https://warehouse-theme-metal.myshopify.com/'])


if __name__ == '__main__':
    asyncio.run(main())
```

### Advanced routing by labels[​](#advanced-routing-by-labels "Direct link to Advanced routing by labels")

More complex crawling projects often require different processing logic for various page types. The router supports label-based routing, which allows registration of specialized handlers for specific content categories. This pattern enables clean separation of concerns and targeted processing logic for different URL patterns or content types.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBSZXF1ZXN0XFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQYXJzZWxDcmF3bGVyLCBQYXJzZWxDcmF3bGluZ0NvbnRleHRcXG5mcm9tIGNyYXdsZWUucm91dGVyIGltcG9ydCBSb3V0ZXJcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgICMgQ3JlYXRlIGEgY3VzdG9tIHJvdXRlciBpbnN0YW5jZVxcbiAgICByb3V0ZXIgPSBSb3V0ZXJbUGFyc2VsQ3Jhd2xpbmdDb250ZXh0XSgpXFxuXFxuICAgICMgRGVmaW5lIHRoZSBkZWZhdWx0IGhhbmRsZXIgKGZhbGxiYWNrIGZvciByZXF1ZXN0cyB3aXRob3V0IHNwZWNpZmljIGxhYmVscylcXG4gICAgQHJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIGRlZmF1bHRfaGFuZGxlcihjb250ZXh0OiBQYXJzZWxDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyBob21lcGFnZToge2NvbnRleHQucmVxdWVzdC51cmx9JylcXG5cXG4gICAgICAgICMgRXh0cmFjdCBwYWdlIHRpdGxlXFxuICAgICAgICB0aXRsZSA9IGNvbnRleHQuc2VsZWN0b3IuY3NzKCd0aXRsZTo6dGV4dCcpLmdldCgpIG9yICdObyB0aXRsZSBmb3VuZCdcXG5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQucHVzaF9kYXRhKFxcbiAgICAgICAgICAgIHtcXG4gICAgICAgICAgICAgICAgJ3VybCc6IGNvbnRleHQucmVxdWVzdC51cmwsXFxuICAgICAgICAgICAgICAgICd0aXRsZSc6IHRpdGxlLFxcbiAgICAgICAgICAgICAgICAncGFnZV90eXBlJzogJ2hvbWVwYWdlJyxcXG4gICAgICAgICAgICB9XFxuICAgICAgICApXFxuXFxuICAgICAgICAjIEZpbmQgYW5kIGVucXVldWUgY29sbGVjdGlvbi9jYXRlZ29yeSBsaW5rc1xcbiAgICAgICAgYXdhaXQgY29udGV4dC5lbnF1ZXVlX2xpbmtzKHNlbGVjdG9yPSdhW2hyZWYqPVxcXCIvY29sbGVjdGlvbnMvXFxcIl0nLCBsYWJlbD0nQ0FURUdPUlknKVxcblxcbiAgICAjIERlZmluZSBhIGhhbmRsZXIgZm9yIGNhdGVnb3J5IHBhZ2VzXFxuICAgIEByb3V0ZXIuaGFuZGxlcignQ0FURUdPUlknKVxcbiAgICBhc3luYyBkZWYgY2F0ZWdvcnlfaGFuZGxlcihjb250ZXh0OiBQYXJzZWxDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyBjYXRlZ29yeSBwYWdlOiB7Y29udGV4dC5yZXF1ZXN0LnVybH0nKVxcblxcbiAgICAgICAgIyBFeHRyYWN0IGNhdGVnb3J5IGluZm9ybWF0aW9uXFxuICAgICAgICBjYXRlZ29yeV90aXRsZSA9IGNvbnRleHQuc2VsZWN0b3IuY3NzKCdoMTo6dGV4dCcpLmdldCgpIG9yICdVbmtub3duIENhdGVnb3J5J1xcbiAgICAgICAgcHJvZHVjdF9jb3VudCA9IGxlbihjb250ZXh0LnNlbGVjdG9yLmNzcygnLnByb2R1Y3QtaXRlbScpLmdldGFsbCgpKVxcblxcbiAgICAgICAgYXdhaXQgY29udGV4dC5wdXNoX2RhdGEoXFxuICAgICAgICAgICAge1xcbiAgICAgICAgICAgICAgICAndXJsJzogY29udGV4dC5yZXF1ZXN0LnVybCxcXG4gICAgICAgICAgICAgICAgJ3R5cGUnOiAnY2F0ZWdvcnknLFxcbiAgICAgICAgICAgICAgICAnY2F0ZWdvcnlfdGl0bGUnOiBjYXRlZ29yeV90aXRsZSxcXG4gICAgICAgICAgICAgICAgJ3Byb2R1Y3RfY291bnQnOiBwcm9kdWN0X2NvdW50LFxcbiAgICAgICAgICAgICAgICAnaGFuZGxlcic6ICdjYXRlZ29yeScsXFxuICAgICAgICAgICAgfVxcbiAgICAgICAgKVxcblxcbiAgICAgICAgIyBFbnF1ZXVlIHByb2R1Y3QgbGlua3MgZnJvbSB0aGlzIGNhdGVnb3J5XFxuICAgICAgICBhd2FpdCBjb250ZXh0LmVucXVldWVfbGlua3Moc2VsZWN0b3I9J2FbaHJlZio9XFxcIi9wcm9kdWN0cy9cXFwiXScsIGxhYmVsPSdQUk9EVUNUJylcXG5cXG4gICAgIyBEZWZpbmUgYSBoYW5kbGVyIGZvciBwcm9kdWN0IGRldGFpbCBwYWdlc1xcbiAgICBAcm91dGVyLmhhbmRsZXIoJ1BST0RVQ1QnKVxcbiAgICBhc3luYyBkZWYgcHJvZHVjdF9oYW5kbGVyKGNvbnRleHQ6IFBhcnNlbENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm9jZXNzaW5nIHByb2R1Y3QgcGFnZToge2NvbnRleHQucmVxdWVzdC51cmx9JylcXG5cXG4gICAgICAgICMgRXh0cmFjdCBkZXRhaWxlZCBwcm9kdWN0IGluZm9ybWF0aW9uXFxuICAgICAgICBwcm9kdWN0X2RhdGEgPSB7XFxuICAgICAgICAgICAgJ3VybCc6IGNvbnRleHQucmVxdWVzdC51cmwsXFxuICAgICAgICAgICAgJ25hbWUnOiBjb250ZXh0LnNlbGVjdG9yLmNzcygnaDE6OnRleHQnKS5nZXQoKSxcXG4gICAgICAgICAgICAncHJpY2UnOiBjb250ZXh0LnNlbGVjdG9yLmNzcygnLnByaWNlOjp0ZXh0JykuZ2V0KCksXFxuICAgICAgICAgICAgJ2Rlc2NyaXB0aW9uJzogY29udGV4dC5zZWxlY3Rvci5jc3MoJy5wcm9kdWN0LWRlc2NyaXB0aW9uIHA6OnRleHQnKS5nZXQoKSxcXG4gICAgICAgICAgICAnaW1hZ2VzJzogY29udGV4dC5zZWxlY3Rvci5jc3MoJy5wcm9kdWN0LWdhbGxlcnkgaW1nOjphdHRyKHNyYyknKS5nZXRhbGwoKSxcXG4gICAgICAgICAgICAnaW5fc3RvY2snOiBib29sKGNvbnRleHQuc2VsZWN0b3IuY3NzKCcuYWRkLXRvLWNhcnQtYnV0dG9uJykuZ2V0KCkpLFxcbiAgICAgICAgICAgICdoYW5kbGVyJzogJ3Byb2R1Y3QnLFxcbiAgICAgICAgfVxcblxcbiAgICAgICAgYXdhaXQgY29udGV4dC5wdXNoX2RhdGEocHJvZHVjdF9kYXRhKVxcblxcbiAgICAjIENyZWF0ZSBjcmF3bGVyIHdpdGggdGhlIHJvdXRlclxcbiAgICBjcmF3bGVyID0gUGFyc2VsQ3Jhd2xlcihcXG4gICAgICAgIHJlcXVlc3RfaGFuZGxlcj1yb3V0ZXIsXFxuICAgICAgICBtYXhfcmVxdWVzdHNfcGVyX2NyYXdsPTEwLCAgIyBMaW1pdCB0aGUgbWF4IHJlcXVlc3RzIHBlciBjcmF3bC5cXG4gICAgKVxcblxcbiAgICAjIFN0YXJ0IGNyYXdsaW5nIHdpdGggc29tZSBpbml0aWFsIHJlcXVlc3RzXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFxcbiAgICAgICAgW1xcbiAgICAgICAgICAgICMgV2lsbCB1c2UgZGVmYXVsdCBoYW5kbGVyXFxuICAgICAgICAgICAgJ2h0dHBzOi8vd2FyZWhvdXNlLXRoZW1lLW1ldGFsLm15c2hvcGlmeS5jb20vJyxcXG4gICAgICAgICAgICAjIFdpbGwgdXNlIGNhdGVnb3J5IGhhbmRsZXJcXG4gICAgICAgICAgICBSZXF1ZXN0LmZyb21fdXJsKFxcbiAgICAgICAgICAgICAgICAnaHR0cHM6Ly93YXJlaG91c2UtdGhlbWUtbWV0YWwubXlzaG9waWZ5LmNvbS9jb2xsZWN0aW9ucy9hbGwnLFxcbiAgICAgICAgICAgICAgICBsYWJlbD0nQ0FURUdPUlknLFxcbiAgICAgICAgICAgICksXFxuICAgICAgICBdXFxuICAgIClcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6MTAyNCwidGltZW91dCI6MTgwfX0.l_HTCrRigogH0u4pzqLGN6zJPk-JiMzvrjL0-t5wV9k\&asrc=run_on_apify)

```
import asyncio

from crawlee import Request
from crawlee.crawlers import ParselCrawler, ParselCrawlingContext
from crawlee.router import Router


async def main() -> None:
    # Create a custom router instance
    router = Router[ParselCrawlingContext]()

    # Define the default handler (fallback for requests without specific labels)
    @router.default_handler
    async def default_handler(context: ParselCrawlingContext) -> None:
        context.log.info(f'Processing homepage: {context.request.url}')

        # Extract page title
        title = context.selector.css('title::text').get() or 'No title found'

        await context.push_data(
            {
                'url': context.request.url,
                'title': title,
                'page_type': 'homepage',
            }
        )

        # Find and enqueue collection/category links
        await context.enqueue_links(selector='a[href*="/collections/"]', label='CATEGORY')

    # Define a handler for category pages
    @router.handler('CATEGORY')
    async def category_handler(context: ParselCrawlingContext) -> None:
        context.log.info(f'Processing category page: {context.request.url}')

        # Extract category information
        category_title = context.selector.css('h1::text').get() or 'Unknown Category'
        product_count = len(context.selector.css('.product-item').getall())

        await context.push_data(
            {
                'url': context.request.url,
                'type': 'category',
                'category_title': category_title,
                'product_count': product_count,
                'handler': 'category',
            }
        )

        # Enqueue product links from this category
        await context.enqueue_links(selector='a[href*="/products/"]', label='PRODUCT')

    # Define a handler for product detail pages
    @router.handler('PRODUCT')
    async def product_handler(context: ParselCrawlingContext) -> None:
        context.log.info(f'Processing product page: {context.request.url}')

        # Extract detailed product information
        product_data = {
            'url': context.request.url,
            'name': context.selector.css('h1::text').get(),
            'price': context.selector.css('.price::text').get(),
            'description': context.selector.css('.product-description p::text').get(),
            'images': context.selector.css('.product-gallery img::attr(src)').getall(),
            'in_stock': bool(context.selector.css('.add-to-cart-button').get()),
            'handler': 'product',
        }

        await context.push_data(product_data)

    # Create crawler with the router
    crawler = ParselCrawler(
        request_handler=router,
        max_requests_per_crawl=10,  # Limit the max requests per crawl.
    )

    # Start crawling with some initial requests
    await crawler.run(
        [
            # Will use default handler
            'https://warehouse-theme-metal.myshopify.com/',
            # Will use category handler
            Request.from_url(
                'https://warehouse-theme-metal.myshopify.com/collections/all',
                label='CATEGORY',
            ),
        ]
    )


if __name__ == '__main__':
    asyncio.run(main())
```

## Error handlers[​](#error-handlers "Direct link to Error handlers")

Crawlee provides error handling mechanisms to manage request processing failures. It distinguishes between recoverable errors that may succeed on retry and permanent failures that require alternative handling strategies.

### Error handler[​](#error-handler "Direct link to Error handler")

The error handler executes when exceptions occur during request processing, before any retry attempts. This handler receives the error context and can implement custom recovery logic, modify request parameters, or determine whether the request should be retried. Error handlers enable control over failure scenarios and allow applications to implement error recovery strategies.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCYXNpY0NyYXdsaW5nQ29udGV4dCwgUGFyc2VsQ3Jhd2xlciwgUGFyc2VsQ3Jhd2xpbmdDb250ZXh0XFxuZnJvbSBjcmF3bGVlLmVycm9ycyBpbXBvcnQgSHR0cFN0YXR1c0NvZGVFcnJvclxcblxcbiMgSFRUUCBzdGF0dXMgY29kZSBjb25zdGFudHNcXG5UT09fTUFOWV9SRVFVRVNUUyA9IDQyOVxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBDcmVhdGUgYSBjcmF3bGVyIGluc3RhbmNlXFxuICAgIGNyYXdsZXIgPSBQYXJzZWxDcmF3bGVyKFxcbiAgICAgICAgbWF4X3JlcXVlc3RzX3Blcl9jcmF3bD0xMCwgICMgTGltaXQgdGhlIG1heCByZXF1ZXN0cyBwZXIgY3Jhd2wuXFxuICAgIClcXG5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgZGVmYXVsdF9oYW5kbGVyKGNvbnRleHQ6IFBhcnNlbENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm9jZXNzaW5nIHtjb250ZXh0LnJlcXVlc3QudXJsfScpXFxuXFxuICAgICAgICAjIEV4dHJhY3QgcHJvZHVjdCBpbmZvcm1hdGlvbiAobWlnaHQgZmFpbCBmb3Igc29tZSBwYWdlcylcXG4gICAgICAgIHByb2R1Y3RfbmFtZSA9IGNvbnRleHQuc2VsZWN0b3IuY3NzKCdoMVtkYXRhLXRlc3RpZD1cXFwicHJvZHVjdC10aXRsZVxcXCJdOjp0ZXh0JykuZ2V0KClcXG4gICAgICAgIGlmIG5vdCBwcm9kdWN0X25hbWU6XFxuICAgICAgICAgICAgcmFpc2UgVmFsdWVFcnJvcignUHJvZHVjdCBuYW1lIG5vdCBmb3VuZCAtIG1pZ2h0IGJlIGEgbm9uLXByb2R1Y3QgcGFnZScpXFxuXFxuICAgICAgICBwcmljZSA9IGNvbnRleHQuc2VsZWN0b3IuY3NzKCcucHJpY2U6OnRleHQnKS5nZXQoKVxcbiAgICAgICAgYXdhaXQgY29udGV4dC5wdXNoX2RhdGEoXFxuICAgICAgICAgICAge1xcbiAgICAgICAgICAgICAgICAndXJsJzogY29udGV4dC5yZXF1ZXN0LnVybCxcXG4gICAgICAgICAgICAgICAgJ3Byb2R1Y3RfbmFtZSc6IHByb2R1Y3RfbmFtZSxcXG4gICAgICAgICAgICAgICAgJ3ByaWNlJzogcHJpY2UsXFxuICAgICAgICAgICAgfVxcbiAgICAgICAgKVxcblxcbiAgICAjIEVycm9yIGhhbmRsZXIgLSBjYWxsZWQgd2hlbiBhbiBlcnJvciBvY2N1cnMgZHVyaW5nIHJlcXVlc3QgcHJvY2Vzc2luZ1xcbiAgICBAY3Jhd2xlci5lcnJvcl9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiBlcnJvcl9oYW5kbGVyKGNvbnRleHQ6IEJhc2ljQ3Jhd2xpbmdDb250ZXh0LCBlcnJvcjogRXhjZXB0aW9uKSAtPiBOb25lOlxcbiAgICAgICAgZXJyb3JfbmFtZSA9IHR5cGUoZXJyb3IpLl9fbmFtZV9fXFxuICAgICAgICBjb250ZXh0LmxvZy53YXJuaW5nKGYnRXJyb3Igb2NjdXJyZWQgZm9yIHtjb250ZXh0LnJlcXVlc3QudXJsfToge2Vycm9yX25hbWV9JylcXG5cXG4gICAgICAgICMgWW91IGNhbiBtb2RpZnkgdGhlIHJlcXVlc3Qgb3IgY29udGV4dCBoZXJlIGJlZm9yZSByZXRyeVxcbiAgICAgICAgaWYgKFxcbiAgICAgICAgICAgIGlzaW5zdGFuY2UoZXJyb3IsIEh0dHBTdGF0dXNDb2RlRXJyb3IpXFxuICAgICAgICAgICAgYW5kIGVycm9yLnN0YXR1c19jb2RlID09IFRPT19NQU5ZX1JFUVVFU1RTXFxuICAgICAgICApOlxcbiAgICAgICAgICAgIGNvbnRleHQubG9nLmluZm8oJ1JhdGUgbGltaXRlZCAtIHdpbGwgcmV0cnkgd2l0aCBkZWxheScpXFxuICAgICAgICAgICAgIyBZb3UgY291bGQgbW9kaWZ5IGhlYWRlcnMsIGFkZCBkZWxheSwgZXRjLlxcbiAgICAgICAgZWxpZiBpc2luc3RhbmNlKGVycm9yLCBWYWx1ZUVycm9yKTpcXG4gICAgICAgICAgICBjb250ZXh0LmxvZy5pbmZvKCdQYXJzZSBlcnJvciAtIG1hcmtpbmcgcmVxdWVzdCBhcyBubyByZXRyeScpXFxuICAgICAgICAgICAgY29udGV4dC5yZXF1ZXN0Lm5vX3JldHJ5ID0gVHJ1ZVxcblxcbiAgICAjIFN0YXJ0IGNyYXdsaW5nXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFxcbiAgICAgICAgW1xcbiAgICAgICAgICAgICdodHRwczovL3dhcmVob3VzZS10aGVtZS1tZXRhbC5teXNob3BpZnkuY29tL3Byb2R1Y3RzL29uLXJ1bm5pbmctY2xvdWRtb25zdGVyLTItbWVucycsXFxuICAgICAgICAgICAgIyBNaWdodCBjYXVzZSBwYXJzZSBlcnJvclxcbiAgICAgICAgICAgICdodHRwczovL3dhcmVob3VzZS10aGVtZS1tZXRhbC5teXNob3BpZnkuY29tL2NvbGxlY3Rpb25zL21lbnMtcnVubmluZycsXFxuICAgICAgICBdXFxuICAgIClcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6MTAyNCwidGltZW91dCI6MTgwfX0.459SinsNRFM3cgmkvvu5Eb7hD0D3fm6vPolPfdFsoPc\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BasicCrawlingContext, ParselCrawler, ParselCrawlingContext
from crawlee.errors import HttpStatusCodeError

# HTTP status code constants
TOO_MANY_REQUESTS = 429


async def main() -> None:
    # Create a crawler instance
    crawler = ParselCrawler(
        max_requests_per_crawl=10,  # Limit the max requests per crawl.
    )

    @crawler.router.default_handler
    async def default_handler(context: ParselCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url}')

        # Extract product information (might fail for some pages)
        product_name = context.selector.css('h1[data-testid="product-title"]::text').get()
        if not product_name:
            raise ValueError('Product name not found - might be a non-product page')

        price = context.selector.css('.price::text').get()
        await context.push_data(
            {
                'url': context.request.url,
                'product_name': product_name,
                'price': price,
            }
        )

    # Error handler - called when an error occurs during request processing
    @crawler.error_handler
    async def error_handler(context: BasicCrawlingContext, error: Exception) -> None:
        error_name = type(error).__name__
        context.log.warning(f'Error occurred for {context.request.url}: {error_name}')

        # You can modify the request or context here before retry
        if (
            isinstance(error, HttpStatusCodeError)
            and error.status_code == TOO_MANY_REQUESTS
        ):
            context.log.info('Rate limited - will retry with delay')
            # You could modify headers, add delay, etc.
        elif isinstance(error, ValueError):
            context.log.info('Parse error - marking request as no retry')
            context.request.no_retry = True

    # Start crawling
    await crawler.run(
        [
            'https://warehouse-theme-metal.myshopify.com/products/on-running-cloudmonster-2-mens',
            # Might cause parse error
            'https://warehouse-theme-metal.myshopify.com/collections/mens-running',
        ]
    )


if __name__ == '__main__':
    asyncio.run(main())
```

### Failed request handler[​](#failed-request-handler "Direct link to Failed request handler")

The failed request handler executes when a request has exhausted all retry attempts and is considered permanently failed. This handler serves as the final opportunity to log failures, store failed requests for later analysis, create alternative requests, or implement fallback processing strategies.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCYXNpY0NyYXdsaW5nQ29udGV4dCwgUGFyc2VsQ3Jhd2xlciwgUGFyc2VsQ3Jhd2xpbmdDb250ZXh0XFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICAjIENyZWF0ZSBhIGNyYXdsZXIgaW5zdGFuY2Ugd2l0aCByZXRyeSBzZXR0aW5nc1xcbiAgICBjcmF3bGVyID0gUGFyc2VsQ3Jhd2xlcihcXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsICAjIExpbWl0IHRoZSBtYXggcmVxdWVzdHMgcGVyIGNyYXdsLlxcbiAgICAgICAgbWF4X3JlcXVlc3RfcmV0cmllcz0yLCAgIyBBbGxvdyAyIHJldHJpZXMgYmVmb3JlIGZhaWxpbmdcXG4gICAgKVxcblxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiBkZWZhdWx0X2hhbmRsZXIoY29udGV4dDogUGFyc2VsQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ1Byb2Nlc3Npbmcge2NvbnRleHQucmVxdWVzdC51cmx9JylcXG5cXG4gICAgICAgICMgRXh0cmFjdCBwcm9kdWN0IGluZm9ybWF0aW9uXFxuICAgICAgICBwcm9kdWN0X25hbWUgPSBjb250ZXh0LnNlbGVjdG9yLmNzcygnaDFbZGF0YS10ZXN0aWQ9XFxcInByb2R1Y3QtdGl0bGVcXFwiXTo6dGV4dCcpLmdldCgpXFxuICAgICAgICBpZiBub3QgcHJvZHVjdF9uYW1lOlxcbiAgICAgICAgICAgIHByb2R1Y3RfbmFtZSA9IGNvbnRleHQuc2VsZWN0b3IuY3NzKCdoMTo6dGV4dCcpLmdldCgpIG9yICdVbmtub3duIFByb2R1Y3QnXFxuXFxuICAgICAgICBwcmljZSA9IGNvbnRleHQuc2VsZWN0b3IuY3NzKCcucHJpY2U6OnRleHQnKS5nZXQoKSBvciAnUHJpY2Ugbm90IGF2YWlsYWJsZSdcXG5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQucHVzaF9kYXRhKFxcbiAgICAgICAgICAgIHtcXG4gICAgICAgICAgICAgICAgJ3VybCc6IGNvbnRleHQucmVxdWVzdC51cmwsXFxuICAgICAgICAgICAgICAgICdwcm9kdWN0X25hbWUnOiBwcm9kdWN0X25hbWUsXFxuICAgICAgICAgICAgICAgICdwcmljZSc6IHByaWNlLFxcbiAgICAgICAgICAgICAgICAnc3RhdHVzJzogJ3N1Y2Nlc3MnLFxcbiAgICAgICAgICAgIH1cXG4gICAgICAgIClcXG5cXG4gICAgIyBGYWlsZWQgcmVxdWVzdCBoYW5kbGVyIC0gY2FsbGVkIHdoZW4gcmVxdWVzdCBoYXMgZXhoYXVzdGVkIGFsbCByZXRyaWVzXFxuICAgIEBjcmF3bGVyLmZhaWxlZF9yZXF1ZXN0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIGZhaWxlZF9oYW5kbGVyKGNvbnRleHQ6IEJhc2ljQ3Jhd2xpbmdDb250ZXh0LCBlcnJvcjogRXhjZXB0aW9uKSAtPiBOb25lOlxcbiAgICAgICAgY29udGV4dC5sb2cuZXJyb3IoXFxuICAgICAgICAgICAgZidGYWlsZWQgdG8gcHJvY2VzcyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gYWZ0ZXIgYWxsIHJldHJpZXM6IHtlcnJvcn0nXFxuICAgICAgICApXFxuXFxuICAgICAgICAjIFNhdmUgZmFpbGVkIHJlcXVlc3QgaW5mb3JtYXRpb24gZm9yIGFuYWx5c2lzXFxuICAgICAgICBhd2FpdCBjb250ZXh0LnB1c2hfZGF0YShcXG4gICAgICAgICAgICB7XFxuICAgICAgICAgICAgICAgICdmYWlsZWRfdXJsJzogY29udGV4dC5yZXF1ZXN0LnVybCxcXG4gICAgICAgICAgICAgICAgJ2xhYmVsJzogY29udGV4dC5yZXF1ZXN0LmxhYmVsLFxcbiAgICAgICAgICAgICAgICAnZXJyb3JfdHlwZSc6IHR5cGUoZXJyb3IpLl9fbmFtZV9fLFxcbiAgICAgICAgICAgICAgICAnZXJyb3JfbWVzc2FnZSc6IHN0cihlcnJvciksXFxuICAgICAgICAgICAgICAgICdyZXRyeV9jb3VudCc6IGNvbnRleHQucmVxdWVzdC5yZXRyeV9jb3VudCxcXG4gICAgICAgICAgICAgICAgJ3N0YXR1cyc6ICdmYWlsZWQnLFxcbiAgICAgICAgICAgIH1cXG4gICAgICAgIClcXG5cXG4gICAgIyBTdGFydCBjcmF3bGluZyB3aXRoIHNvbWUgVVJMcyB0aGF0IG1pZ2h0IGZhaWxcXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oXFxuICAgICAgICBbXFxuICAgICAgICAgICAgJ2h0dHBzOi8vd2FyZWhvdXNlLXRoZW1lLW1ldGFsLm15c2hvcGlmeS5jb20vcHJvZHVjdHMvb24tcnVubmluZy1jbG91ZG1vbnN0ZXItMi1tZW5zJyxcXG4gICAgICAgICAgICAjIFRoaXMgd2lsbCBsaWtlbHkgZmFpbFxcbiAgICAgICAgICAgICdodHRwczovL3dhcmVob3VzZS10aGVtZS1tZXRhbC5teXNob3BpZnkuY29tL2ludmFsaWQtdXJsJyxcXG4gICAgICAgICAgICAnaHR0cHM6Ly93YXJlaG91c2UtdGhlbWUtbWV0YWwubXlzaG9waWZ5LmNvbS9wcm9kdWN0cy92YWxpZC1wcm9kdWN0JyxcXG4gICAgICAgIF1cXG4gICAgKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.1YLr3bPxeOzEYp7qLEkNs5XEM5u5ih1XlbE_xUZCrEE\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BasicCrawlingContext, ParselCrawler, ParselCrawlingContext


async def main() -> None:
    # Create a crawler instance with retry settings
    crawler = ParselCrawler(
        max_requests_per_crawl=10,  # Limit the max requests per crawl.
        max_request_retries=2,  # Allow 2 retries before failing
    )

    @crawler.router.default_handler
    async def default_handler(context: ParselCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url}')

        # Extract product information
        product_name = context.selector.css('h1[data-testid="product-title"]::text').get()
        if not product_name:
            product_name = context.selector.css('h1::text').get() or 'Unknown Product'

        price = context.selector.css('.price::text').get() or 'Price not available'

        await context.push_data(
            {
                'url': context.request.url,
                'product_name': product_name,
                'price': price,
                'status': 'success',
            }
        )

    # Failed request handler - called when request has exhausted all retries
    @crawler.failed_request_handler
    async def failed_handler(context: BasicCrawlingContext, error: Exception) -> None:
        context.log.error(
            f'Failed to process {context.request.url} after all retries: {error}'
        )

        # Save failed request information for analysis
        await context.push_data(
            {
                'failed_url': context.request.url,
                'label': context.request.label,
                'error_type': type(error).__name__,
                'error_message': str(error),
                'retry_count': context.request.retry_count,
                'status': 'failed',
            }
        )

    # Start crawling with some URLs that might fail
    await crawler.run(
        [
            'https://warehouse-theme-metal.myshopify.com/products/on-running-cloudmonster-2-mens',
            # This will likely fail
            'https://warehouse-theme-metal.myshopify.com/invalid-url',
            'https://warehouse-theme-metal.myshopify.com/products/valid-product',
        ]
    )


if __name__ == '__main__':
    asyncio.run(main())
```

## Pre-navigation hooks[​](#pre-navigation-hooks "Direct link to Pre-navigation hooks")

Pre-navigation hooks execute before each request is processed, providing opportunities to configure request parameters, modify browser settings, or implement request-specific optimizations. You can use pre-navigation hooks for example for viewport configuration, resource blocking, timeout management, header customization, custom proxy rotation, and request interception.

### HTTP crawler[​](#http-crawler "Direct link to HTTP crawler")

HTTP crawlers support pre-navigation hooks that execute before making HTTP requests. These hooks enable request modification, header configuration, and other HTTP-specific optimizations.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBIdHRwSGVhZGVyc1xcbmZyb20gY3Jhd2xlZS5jcmF3bGVycyBpbXBvcnQgQmFzaWNDcmF3bGluZ0NvbnRleHQsIFBhcnNlbENyYXdsZXIsIFBhcnNlbENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IFBhcnNlbENyYXdsZXIoXFxuICAgICAgICBtYXhfcmVxdWVzdHNfcGVyX2NyYXdsPTEwLCAgIyBMaW1pdCB0aGUgbWF4IHJlcXVlc3RzIHBlciBjcmF3bC5cXG4gICAgKVxcblxcbiAgICBAY3Jhd2xlci5wcmVfbmF2aWdhdGlvbl9ob29rXFxuICAgIGFzeW5jIGRlZiBzZXR1cF9yZXF1ZXN0KGNvbnRleHQ6IEJhc2ljQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgIyBBZGQgY3VzdG9tIGhlYWRlcnMgYmVmb3JlIG1ha2luZyB0aGUgcmVxdWVzdFxcbiAgICAgICAgY29udGV4dC5yZXF1ZXN0LmhlYWRlcnMgfD0gSHR0cEhlYWRlcnMoXFxuICAgICAgICAgICAge1xcbiAgICAgICAgICAgICAgICAnVXNlci1BZ2VudCc6ICdDcmF3bGVlIEJvdCAxLjAnLFxcbiAgICAgICAgICAgICAgICAnQWNjZXB0JzogJ3RleHQvaHRtbCxhcHBsaWNhdGlvbi94aHRtbCt4bWwnLFxcbiAgICAgICAgICAgIH0sXFxuICAgICAgICApXFxuXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIGRlZmF1bHRfaGFuZGxlcihjb250ZXh0OiBQYXJzZWxDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICAjIEV4dHJhY3QgYmFzaWMgcGFnZSBpbmZvcm1hdGlvblxcbiAgICAgICAgdGl0bGUgPSBjb250ZXh0LnNlbGVjdG9yLmNzcygndGl0bGU6OnRleHQnKS5nZXQoKVxcbiAgICAgICAgYXdhaXQgY29udGV4dC5wdXNoX2RhdGEoXFxuICAgICAgICAgICAge1xcbiAgICAgICAgICAgICAgICAndXJsJzogY29udGV4dC5yZXF1ZXN0LnVybCxcXG4gICAgICAgICAgICAgICAgJ3RpdGxlJzogdGl0bGUsXFxuICAgICAgICAgICAgfVxcbiAgICAgICAgKVxcblxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vd2FyZWhvdXNlLXRoZW1lLW1ldGFsLm15c2hvcGlmeS5jb20vJ10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.0t2Nk5M8vPTcBLblAM3WZJcfJfqrhp5eerodfwSRTd0\&asrc=run_on_apify)

```
import asyncio

from crawlee import HttpHeaders
from crawlee.crawlers import BasicCrawlingContext, ParselCrawler, ParselCrawlingContext


async def main() -> None:
    crawler = ParselCrawler(
        max_requests_per_crawl=10,  # Limit the max requests per crawl.
    )

    @crawler.pre_navigation_hook
    async def setup_request(context: BasicCrawlingContext) -> None:
        # Add custom headers before making the request
        context.request.headers |= HttpHeaders(
            {
                'User-Agent': 'Crawlee Bot 1.0',
                'Accept': 'text/html,application/xhtml+xml',
            },
        )

    @crawler.router.default_handler
    async def default_handler(context: ParselCrawlingContext) -> None:
        # Extract basic page information
        title = context.selector.css('title::text').get()
        await context.push_data(
            {
                'url': context.request.url,
                'title': title,
            }
        )

    await crawler.run(['https://warehouse-theme-metal.myshopify.com/'])


if __name__ == '__main__':
    asyncio.run(main())
```

### Playwright crawler[​](#playwright-crawler "Direct link to Playwright crawler")

Playwright crawlers provide extensive pre-navigation capabilities that allow browser page configuration before navigation. These hooks can modify browser behavior and configure page settings.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCAoXFxuICAgIFBsYXl3cmlnaHRDcmF3bGVyLFxcbiAgICBQbGF5d3JpZ2h0Q3Jhd2xpbmdDb250ZXh0LFxcbiAgICBQbGF5d3JpZ2h0UHJlTmF2Q3Jhd2xpbmdDb250ZXh0LFxcbilcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgIGNyYXdsZXIgPSBQbGF5d3JpZ2h0Q3Jhd2xlcihcXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsICAjIExpbWl0IHRoZSBtYXggcmVxdWVzdHMgcGVyIGNyYXdsLlxcbiAgICApXFxuXFxuICAgIEBjcmF3bGVyLnByZV9uYXZpZ2F0aW9uX2hvb2tcXG4gICAgYXN5bmMgZGVmIHNldHVwX3BhZ2UoY29udGV4dDogUGxheXdyaWdodFByZU5hdkNyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgICMgU2V0IHZpZXdwb3J0IHNpemUgZm9yIGNvbnNpc3RlbnQgcmVuZGVyaW5nXFxuICAgICAgICBhd2FpdCBjb250ZXh0LnBhZ2Uuc2V0X3ZpZXdwb3J0X3NpemUoeyd3aWR0aCc6IDEyODAsICdoZWlnaHQnOiA3MjB9KVxcblxcbiAgICAgICAgIyBCbG9jayB1bm5lY2Vzc2FyeSByZXNvdXJjZXMgdG8gc3BlZWQgdXAgY3Jhd2xpbmdcXG4gICAgICAgIGF3YWl0IGNvbnRleHQuYmxvY2tfcmVxdWVzdHMoXFxuICAgICAgICAgICAgZXh0cmFfdXJsX3BhdHRlcm5zPVtcXG4gICAgICAgICAgICAgICAgJyoucG5nJyxcXG4gICAgICAgICAgICAgICAgJyouanBnJyxcXG4gICAgICAgICAgICAgICAgJyouanBlZycsXFxuICAgICAgICAgICAgICAgICcqLmdpZicsXFxuICAgICAgICAgICAgICAgICcqLnN2ZycsXFxuICAgICAgICAgICAgICAgICcqLmNzcycsXFxuICAgICAgICAgICAgICAgICcqLndvZmYnLFxcbiAgICAgICAgICAgICAgICAnKi53b2ZmMicsXFxuICAgICAgICAgICAgICAgICcqLnR0ZicsXFxuICAgICAgICAgICAgICAgICcqZ29vZ2xlLWFuYWx5dGljcyonLFxcbiAgICAgICAgICAgICAgICAnKmZhY2Vib29rKicsXFxuICAgICAgICAgICAgICAgICcqdHdpdHRlcionLFxcbiAgICAgICAgICAgIF1cXG4gICAgICAgIClcXG5cXG4gICAgICAgICMgU2V0IGN1c3RvbSB1c2VyIGFnZW50XFxuICAgICAgICBhd2FpdCBjb250ZXh0LnBhZ2Uuc2V0X2V4dHJhX2h0dHBfaGVhZGVycyhcXG4gICAgICAgICAgICB7XFxuICAgICAgICAgICAgICAgICdVc2VyLUFnZW50JzogJ01vemlsbGEvNS4wIChjb21wYXRpYmxlOyBDcmF3bGVlIEJvdCknLFxcbiAgICAgICAgICAgIH1cXG4gICAgICAgIClcXG5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgZGVmYXVsdF9oYW5kbGVyKGNvbnRleHQ6IFBsYXl3cmlnaHRDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICB0aXRsZSA9IGF3YWl0IGNvbnRleHQucGFnZS50aXRsZSgpXFxuICAgICAgICBhd2FpdCBjb250ZXh0LnB1c2hfZGF0YShcXG4gICAgICAgICAgICB7XFxuICAgICAgICAgICAgICAgICd1cmwnOiBjb250ZXh0LnJlcXVlc3QudXJsLFxcbiAgICAgICAgICAgICAgICAndGl0bGUnOiB0aXRsZSxcXG4gICAgICAgICAgICB9XFxuICAgICAgICApXFxuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9jcmF3bGVlLmRldi8nXSlcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6NDA5NiwidGltZW91dCI6MTgwfX0.CYJnpPXX0jmTzr82YPQAuadd8ldW4fLyKHed_pAr-nY\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import (
    PlaywrightCrawler,
    PlaywrightCrawlingContext,
    PlaywrightPreNavCrawlingContext,
)


async def main() -> None:
    crawler = PlaywrightCrawler(
        max_requests_per_crawl=10,  # Limit the max requests per crawl.
    )

    @crawler.pre_navigation_hook
    async def setup_page(context: PlaywrightPreNavCrawlingContext) -> None:
        # Set viewport size for consistent rendering
        await context.page.set_viewport_size({'width': 1280, 'height': 720})

        # Block unnecessary resources to speed up crawling
        await context.block_requests(
            extra_url_patterns=[
                '*.png',
                '*.jpg',
                '*.jpeg',
                '*.gif',
                '*.svg',
                '*.css',
                '*.woff',
                '*.woff2',
                '*.ttf',
                '*google-analytics*',
                '*facebook*',
                '*twitter*',
            ]
        )

        # Set custom user agent
        await context.page.set_extra_http_headers(
            {
                'User-Agent': 'Mozilla/5.0 (compatible; Crawlee Bot)',
            }
        )

    @crawler.router.default_handler
    async def default_handler(context: PlaywrightCrawlingContext) -> None:
        title = await context.page.title()
        await context.push_data(
            {
                'url': context.request.url,
                'title': title,
            }
        )

    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

### Adaptive Playwright crawler[​](#adaptive-playwright-crawler "Direct link to Adaptive Playwright crawler")

The [`AdaptivePlaywrightCrawler`](https://crawlee.dev/python/python/api/class/AdaptivePlaywrightCrawler.md) implements a dual-hook system with common hooks that execute for all requests and Playwright-specific hooks that execute only when browser automation is required. This is perfect for projects that need both static and dynamic content handling.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBIdHRwSGVhZGVyc1xcbmZyb20gY3Jhd2xlZS5jcmF3bGVycyBpbXBvcnQgKFxcbiAgICBBZGFwdGl2ZVBsYXl3cmlnaHRDcmF3bGVyLFxcbiAgICBBZGFwdGl2ZVBsYXl3cmlnaHRDcmF3bGluZ0NvbnRleHQsXFxuICAgIEFkYXB0aXZlUGxheXdyaWdodFByZU5hdkNyYXdsaW5nQ29udGV4dCxcXG4pXFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICBjcmF3bGVyID0gQWRhcHRpdmVQbGF5d3JpZ2h0Q3Jhd2xlci53aXRoX2JlYXV0aWZ1bHNvdXBfc3RhdGljX3BhcnNlcihcXG4gICAgICAgIG1heF9yZXF1ZXN0c19wZXJfY3Jhd2w9MTAsICAjIExpbWl0IHRoZSBtYXggcmVxdWVzdHMgcGVyIGNyYXdsLlxcbiAgICApXFxuXFxuICAgIEBjcmF3bGVyLnByZV9uYXZpZ2F0aW9uX2hvb2tcXG4gICAgYXN5bmMgZGVmIGNvbW1vbl9zZXR1cChjb250ZXh0OiBBZGFwdGl2ZVBsYXl3cmlnaHRQcmVOYXZDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICAjIENvbW1vbiBwcmUtbmF2aWdhdGlvbiBob29rIC0gcnVucyBmb3IgYm90aCBIVFRQIGFuZCBicm93c2VyIHJlcXVlc3RzLlxcbiAgICAgICAgY29udGV4dC5yZXF1ZXN0LmhlYWRlcnMgfD0gSHR0cEhlYWRlcnMoXFxuICAgICAgICAgICAgeydBY2NlcHQnOiAndGV4dC9odG1sLGFwcGxpY2F0aW9uL3hodG1sK3htbCd9LFxcbiAgICAgICAgKVxcblxcbiAgICBAY3Jhd2xlci5wcmVfbmF2aWdhdGlvbl9ob29rKHBsYXl3cmlnaHRfb25seT1UcnVlKVxcbiAgICBhc3luYyBkZWYgYnJvd3Nlcl9zZXR1cChjb250ZXh0OiBBZGFwdGl2ZVBsYXl3cmlnaHRQcmVOYXZDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICAjIFBsYXl3cmlnaHQtc3BlY2lmaWMgcHJlLW5hdmlnYXRpb24gaG9vayAtIHJ1bnMgb25seSB3aGVuIGJyb3dzZXIgaXMgdXNlZC5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQucGFnZS5zZXRfdmlld3BvcnRfc2l6ZSh7J3dpZHRoJzogMTI4MCwgJ2hlaWdodCc6IDcyMH0pXFxuICAgICAgICBpZiBjb250ZXh0LmJsb2NrX3JlcXVlc3RzOlxcbiAgICAgICAgICAgIGF3YWl0IGNvbnRleHQuYmxvY2tfcmVxdWVzdHMoZXh0cmFfdXJsX3BhdHRlcm5zPVsnKi5jc3MnLCAnKi5qcyddKVxcblxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiBkZWZhdWx0X2hhbmRsZXIoY29udGV4dDogQWRhcHRpdmVQbGF5d3JpZ2h0Q3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgIyBFeHRyYWN0IHRpdGxlIHVzaW5nIHRoZSB1bmlmaWVkIGNvbnRleHQgaW50ZXJmYWNlLlxcbiAgICAgICAgdGl0bGVfdGFnID0gY29udGV4dC5wYXJzZWRfY29udGVudC5maW5kKCd0aXRsZScpXFxuICAgICAgICB0aXRsZSA9IHRpdGxlX3RhZy5nZXRfdGV4dCgpIGlmIHRpdGxlX3RhZyBlbHNlIE5vbmVcXG5cXG4gICAgICAgICMgRXh0cmFjdCBvdGhlciBkYXRhIGNvbnNpc3RlbnRseSBhY3Jvc3MgYm90aCBtb2Rlcy5cXG4gICAgICAgIGxpbmtzID0gW2EuZ2V0KCdocmVmJykgZm9yIGEgaW4gY29udGV4dC5wYXJzZWRfY29udGVudC5maW5kX2FsbCgnYScsIGhyZWY9VHJ1ZSldXFxuXFxuICAgICAgICBhd2FpdCBjb250ZXh0LnB1c2hfZGF0YShcXG4gICAgICAgICAgICB7XFxuICAgICAgICAgICAgICAgICd1cmwnOiBjb250ZXh0LnJlcXVlc3QudXJsLFxcbiAgICAgICAgICAgICAgICAndGl0bGUnOiB0aXRsZSxcXG4gICAgICAgICAgICAgICAgJ2xpbmtzJzogbGlua3MsXFxuICAgICAgICAgICAgfVxcbiAgICAgICAgKVxcblxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vY3Jhd2xlZS5kZXYvJ10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjQwOTYsInRpbWVvdXQiOjE4MH19.YmD5aYL32YBGN56qs5F7g-nSf5qa2vqSpJNfhN0frDc\&asrc=run_on_apify)

```
import asyncio

from crawlee import HttpHeaders
from crawlee.crawlers import (
    AdaptivePlaywrightCrawler,
    AdaptivePlaywrightCrawlingContext,
    AdaptivePlaywrightPreNavCrawlingContext,
)


async def main() -> None:
    crawler = AdaptivePlaywrightCrawler.with_beautifulsoup_static_parser(
        max_requests_per_crawl=10,  # Limit the max requests per crawl.
    )

    @crawler.pre_navigation_hook
    async def common_setup(context: AdaptivePlaywrightPreNavCrawlingContext) -> None:
        # Common pre-navigation hook - runs for both HTTP and browser requests.
        context.request.headers |= HttpHeaders(
            {'Accept': 'text/html,application/xhtml+xml'},
        )

    @crawler.pre_navigation_hook(playwright_only=True)
    async def browser_setup(context: AdaptivePlaywrightPreNavCrawlingContext) -> None:
        # Playwright-specific pre-navigation hook - runs only when browser is used.
        await context.page.set_viewport_size({'width': 1280, 'height': 720})
        if context.block_requests:
            await context.block_requests(extra_url_patterns=['*.css', '*.js'])

    @crawler.router.default_handler
    async def default_handler(context: AdaptivePlaywrightCrawlingContext) -> None:
        # Extract title using the unified context interface.
        title_tag = context.parsed_content.find('title')
        title = title_tag.get_text() if title_tag else None

        # Extract other data consistently across both modes.
        links = [a.get('href') for a in context.parsed_content.find_all('a', href=True)]

        await context.push_data(
            {
                'url': context.request.url,
                'title': title,
                'links': links,
            }
        )

    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

## Conclusion[​](#conclusion "Direct link to Conclusion")

This guide introduced you to the [`Router`](https://crawlee.dev/python/python/api/class/Router.md) class and how to organize your crawling logic. You learned how to use built-in and custom routers, implement request handlers with label-based routing, handle errors with error and failed request handlers, and configure pre-navigation hooks for different crawler types.

If you have questions or need assistance, feel free to reach out on our [GitHub](https://github.com/apify/crawlee-python) or join our [Discord community](https://discord.com/invite/jyEM2PRvMU). Happy scraping!

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/guides/request_router.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/guides/request-loaders.md)

[Request loaders](https://crawlee.dev/python/python/docs/guides/request-loaders.md)

[Next](https://crawlee.dev/python/python/docs/guides/running-in-web-server.md)

[Running in web server](https://crawlee.dev/python/python/docs/guides/running-in-web-server.md)


---

* [](https://crawlee.dev/python/python)
* [Guides](https://crawlee.dev/python/python/docs/guides.md)
* Running in web server

Version: 1.6

On this page

# Running in web server

Most of the time, Crawlee jobs are run as batch jobs. You have a list of URLs you want to scrape every week or you might want to scrape a whole website once per day. After the scrape, you send the data to your warehouse for analytics. Batch jobs are efficient because they can use Crawlee's built-in autoscaling to fully utilize the resources you have available. But sometimes you have a use-case where you need to return scrape data as soon as possible. There might be a user waiting on the other end so every millisecond counts. This is where running Crawlee in a web server comes in.

We will build a simple HTTP server that receives a page URL and returns the page title in the response.

## Set up a web server[​](#set-up-a-web-server "Direct link to Set up a web server")

There are many popular web server frameworks for Python, such as [Flask](https://flask.palletsprojects.com/en/stable/), [Django](https://www.djangoproject.com/), [Pyramid](https://trypyramid.com/), ... In this guide, we will use the [FastAPI](https://fastapi.tiangolo.com/) to keep things simple.

This will be our core server setup:

server.py

```
from __future__ import annotations

import asyncio
from uuid import uuid4

from fastapi import FastAPI
from starlette.requests import Request
from starlette.responses import HTMLResponse

import crawlee

from .crawler import lifespan

app = FastAPI(lifespan=lifespan, title='Crawler app')


@app.get('/', response_class=HTMLResponse)
def index() -> str:
    return """
<!DOCTYPE html>
<html>
<body>
    <h1>Scraper server</h1>
        <p>To scrape some page, visit "scrape" endpoint with url parameter.
            For example:
            <a href="/scrape?url=https://www.example.com">
                /scrape?url=https://www.example.com
            </a>
        </p>
</body>
</html>
"""


@app.get('/scrape')
async def scrape_url(request: Request, url: str | None = None) -> dict:
    if not url:
        return {'url': 'missing', 'scrape result': 'no results'}

    # Generate random unique key for the request
    unique_key = str(uuid4())

    # Set the result future in the result dictionary so that it can be awaited
    request.state.requests_to_results[unique_key] = asyncio.Future[dict[str, str]]()

    # Add the request to the crawler queue
    await request.state.crawler.add_requests(
        [crawlee.Request.from_url(url, unique_key=unique_key)]
    )

    # Wait for the result future to be finished
    result = await request.state.requests_to_results[unique_key]

    # Clean the result from the result dictionary to free up memory
    request.state.requests_to_results.pop(unique_key)

    # Return the result
    return {'url': url, 'scrape result': result}
```

The server has two endpoints.

* `/` - The index is just giving short description of the server with example link to the second endpoint.
* `/scrape` - This is the endpoint that receives a `url` parameter and returns the page title scraped from the URL

To run the example server, make sure that you have installed the [fastapi\[standard\]](https://fastapi.tiangolo.com/#installation) and from the directory where the example code is located you can use the following command:

```
fastapi dev server.py
```

## Create a crawler[​](#create-a-crawler "Direct link to Create a crawler")

We will create a standard [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md) and use the `keep_alive=true` option to keep the crawler running even if there are no requests currently in the [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md). This way it will always be waiting for new requests to come in.

crawler.py

```
import asyncio
from collections.abc import AsyncIterator
from contextlib import asynccontextmanager
from typing import TypedDict

from fastapi import FastAPI

from crawlee.crawlers import ParselCrawler, ParselCrawlingContext


class State(TypedDict):
    """State available in the app."""

    crawler: ParselCrawler
    requests_to_results: dict[str, asyncio.Future[dict[str, str]]]


@asynccontextmanager
async def lifespan(app: FastAPI) -> AsyncIterator[State]:
    # Start up code that runs once when the app starts

    # Results will be stored in this dictionary
    requests_to_results = dict[str, asyncio.Future[dict[str, str]]]()

    crawler = ParselCrawler(
        # Keep the crawler alive even when there are no more requests to process now.
        # This makes the crawler wait for more requests to be added later.
        keep_alive=True
    )

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: ParselCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')
        title = context.selector.xpath('//title/text()').get() or ''

        # Extract data from the page and save it to the result dictionary.
        requests_to_results[context.request.unique_key].set_result(
            {
                'title': title,
            }
        )

    # Start the crawler without awaiting it to finish
    crawler.log.info(f'Starting crawler for the {app.title}')
    run_task = asyncio.create_task(crawler.run([]))

    # Make the crawler and the result dictionary available in the app state
    yield {'crawler': crawler, 'requests_to_results': requests_to_results}

    # Cleanup code that runs once when the app shuts down
    crawler.stop()
    # Wait for the crawler to finish
    await run_task
```

Crawler is defined inside of [Lifespan](https://fastapi.tiangolo.com/advanced/events/#lifespan) which is a FastAPI way to run some start up/ teardown code for the app. There are two objects that we want to save to the app state so that they can be accessed in any endpoint through `request.state`:

* `crawler` holds instance of our crawler and allows the app to interact with it.
* `requests_to_results` is dictionary that is used to temporarily register expected results for each request and populate them when they are made available by the crawler.

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/guides/running_in_web_server.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/guides/request-router.md)

[Request router](https://crawlee.dev/python/python/docs/guides/request-router.md)

[Next](https://crawlee.dev/python/python/docs/guides/scaling-crawlers.md)

[Scaling crawlers](https://crawlee.dev/python/python/docs/guides/scaling-crawlers.md)


---

* [](https://crawlee.dev/python/python)
* [Guides](https://crawlee.dev/python/python/docs/guides.md)
* Scaling crawlers

Version: 1.6

On this page

# Scaling crawlers

As we build our crawler, we may want to control how many tasks it performs at any given time. In other words, how many requests it makes to the web we are trying to scrape. Crawlee offers several options to fine-tune the number of parallel tasks, limit the number of requests per minute, and optimize scaling based on available system resources.

tip

All of these options are available across all crawlers provided by Crawlee. In this guide, we are using the [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md) as an example. You should also explore the [`ConcurrencySettings`](https://crawlee.dev/python/python/api/class/ConcurrencySettings.md).

## Max tasks per minute[​](#max-tasks-per-minute "Direct link to Max tasks per minute")

The `max_tasks_per_minute` setting in [`ConcurrencySettings`](https://crawlee.dev/python/python/api/class/ConcurrencySettings.md) controls how many total tasks the crawler can process per minute. It ensures that tasks are spread evenly throughout the minute, preventing a sudden burst at the `max_concurrency` limit followed by idle time. By default, this is set to `Infinity`, meaning the crawler can run at full speed, limited only by `max_concurrency`. Use this option if you want to throttle your crawler to avoid overwhelming the target website with continuous requests.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBDb25jdXJyZW5jeVNldHRpbmdzXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlclxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY29uY3VycmVuY3lfc2V0dGluZ3MgPSBDb25jdXJyZW5jeVNldHRpbmdzKFxcbiAgICAgICAgIyBTZXQgdGhlIG1heGltdW0gbnVtYmVyIG9mIGNvbmN1cnJlbnQgcmVxdWVzdHMgdGhlIGNyYXdsZXIgY2FuIHJ1biB0byAxMDAuXFxuICAgICAgICBtYXhfY29uY3VycmVuY3k9MTAwLFxcbiAgICAgICAgIyBMaW1pdCB0aGUgdG90YWwgbnVtYmVyIG9mIHJlcXVlc3RzIHRvIDEwIHBlciBtaW51dGUgdG8gYXZvaWQgb3ZlcndoZWxtaW5nXFxuICAgICAgICAjIHRoZSB0YXJnZXQgd2Vic2l0ZS5cXG4gICAgICAgIG1heF90YXNrc19wZXJfbWludXRlPTEwLFxcbiAgICApXFxuXFxuICAgIGNyYXdsZXIgPSBCZWF1dGlmdWxTb3VwQ3Jhd2xlcihcXG4gICAgICAgICMgQXBwbHkgdGhlIGRlZmluZWQgY29uY3VycmVuY3kgc2V0dGluZ3MgdG8gdGhlIGNyYXdsZXIuXFxuICAgICAgICBjb25jdXJyZW5jeV9zZXR0aW5ncz1jb25jdXJyZW5jeV9zZXR0aW5ncyxcXG4gICAgKVxcblxcbiAgICAjIC4uLlxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.jqqouk023v80aJ59lokUOPJR8i1jaqp-zl_62e9TTb0\&asrc=run_on_apify)

```
import asyncio

from crawlee import ConcurrencySettings
from crawlee.crawlers import BeautifulSoupCrawler


async def main() -> None:
    concurrency_settings = ConcurrencySettings(
        # Set the maximum number of concurrent requests the crawler can run to 100.
        max_concurrency=100,
        # Limit the total number of requests to 10 per minute to avoid overwhelming
        # the target website.
        max_tasks_per_minute=10,
    )

    crawler = BeautifulSoupCrawler(
        # Apply the defined concurrency settings to the crawler.
        concurrency_settings=concurrency_settings,
    )

    # ...


if __name__ == '__main__':
    asyncio.run(main())
```

## Minimum and maximum concurrency[​](#minimum-and-maximum-concurrency "Direct link to Minimum and maximum concurrency")

The `min_concurrency` and `max_concurrency` options in the [`ConcurrencySettings`](https://crawlee.dev/python/python/api/class/ConcurrencySettings.md) define the minimum and maximum number of parallel tasks that can run at any given time. By default, crawlers start with a single parallel task and gradually scale up to a maximum of concurrent requests.

Avoid setting minimum concurrency too high

If you set `min_concurrency` too high compared to the available system resources, the crawler may run very slowly or even crash. It is recommended to stick with the default value and let the crawler automatically adjust concurrency based on the system's available resources.

## Desired concurrency[​](#desired-concurrency "Direct link to Desired concurrency")

The `desired_concurrency` option in the [`ConcurrencySettings`](https://crawlee.dev/python/python/api/class/ConcurrencySettings.md) specifies the initial number of parallel tasks to start with, assuming sufficient resources are available. It defaults to the same value as `min_concurrency`.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBDb25jdXJyZW5jeVNldHRpbmdzXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlclxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY29uY3VycmVuY3lfc2V0dGluZ3MgPSBDb25jdXJyZW5jeVNldHRpbmdzKFxcbiAgICAgICAgIyBTdGFydCB3aXRoIDggY29uY3VycmVudCB0YXNrcywgYXMgbG9uZyBhcyByZXNvdXJjZXMgYXJlIGF2YWlsYWJsZS5cXG4gICAgICAgIGRlc2lyZWRfY29uY3VycmVuY3k9OCxcXG4gICAgICAgICMgTWFpbnRhaW4gYSBtaW5pbXVtIG9mIDUgY29uY3VycmVudCB0YXNrcyB0byBlbnN1cmUgc3RlYWR5IGNyYXdsaW5nLlxcbiAgICAgICAgbWluX2NvbmN1cnJlbmN5PTUsXFxuICAgICAgICAjIExpbWl0IHRoZSBtYXhpbXVtIG51bWJlciBvZiBjb25jdXJyZW50IHRhc2tzIHRvIDEwIHRvIHByZXZlbnRcXG4gICAgICAgICMgb3ZlcmxvYWRpbmcgdGhlIHN5c3RlbS5cXG4gICAgICAgIG1heF9jb25jdXJyZW5jeT0xMCxcXG4gICAgKVxcblxcbiAgICBjcmF3bGVyID0gQmVhdXRpZnVsU291cENyYXdsZXIoXFxuICAgICAgICAjIFVzZSB0aGUgY29uZmlndXJlZCBjb25jdXJyZW5jeSBzZXR0aW5ncyBmb3IgdGhlIGNyYXdsZXIuXFxuICAgICAgICBjb25jdXJyZW5jeV9zZXR0aW5ncz1jb25jdXJyZW5jeV9zZXR0aW5ncyxcXG4gICAgKVxcblxcbiAgICAjIC4uLlxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.g4BAOJaosHpio2fcBlKyKRXK-rz70eO-gN2jNYHMxzw\&asrc=run_on_apify)

```
import asyncio

from crawlee import ConcurrencySettings
from crawlee.crawlers import BeautifulSoupCrawler


async def main() -> None:
    concurrency_settings = ConcurrencySettings(
        # Start with 8 concurrent tasks, as long as resources are available.
        desired_concurrency=8,
        # Maintain a minimum of 5 concurrent tasks to ensure steady crawling.
        min_concurrency=5,
        # Limit the maximum number of concurrent tasks to 10 to prevent
        # overloading the system.
        max_concurrency=10,
    )

    crawler = BeautifulSoupCrawler(
        # Use the configured concurrency settings for the crawler.
        concurrency_settings=concurrency_settings,
    )

    # ...


if __name__ == '__main__':
    asyncio.run(main())
```

## Autoscaled pool[​](#autoscaled-pool "Direct link to Autoscaled pool")

The [`AutoscaledPool`](https://crawlee.dev/python/python/api/class/AutoscaledPool.md) manages a pool of asynchronous, resource-intensive tasks that run in parallel. It automatically starts new tasks only when there is enough free CPU and memory. To monitor system resources, it leverages the [`Snapshotter`](https://crawlee.dev/python/python/api/class/Snapshotter.md) and [`SystemStatus`](https://crawlee.dev/python/python/api/class/SystemStatus.md) classes. If any task raises an exception, the error is propagated, and the pool is stopped. Every crawler uses an [`AutoscaledPool`](https://crawlee.dev/python/python/api/class/AutoscaledPool.md) under the hood.

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/guides/scaling_crawlers.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/guides/running-in-web-server.md)

[Running in web server](https://crawlee.dev/python/python/docs/guides/running-in-web-server.md)

[Next](https://crawlee.dev/python/python/docs/guides/service-locator.md)

[Service locator](https://crawlee.dev/python/python/docs/guides/service-locator.md)


---

* [](https://crawlee.dev/python/python)
* [Guides](https://crawlee.dev/python/python/docs/guides.md)
* Service locator

Version: 1.6

On this page

# Service locator

The [`ServiceLocator`](https://crawlee.dev/python/python/api/class/ServiceLocator.md) is a central registry for global services. It manages and provides access to these services throughout the framework, ensuring their consistent configuration and across all components.

The service locator manages three core services: [`Configuration`](https://crawlee.dev/python/python/api/class/Configuration.md), [`EventManager`](https://crawlee.dev/python/python/api/class/EventManager.md), and [`StorageClient`](https://crawlee.dev/python/python/api/class/StorageClient.md). All services are initialized lazily with defaults when first accessed.

## Services[​](#services "Direct link to Services")

There are three core services that are managed by the service locator:

### Configuration[​](#configuration "Direct link to Configuration")

[`Configuration`](https://crawlee.dev/python/python/api/class/Configuration.md) is a class that provides access to application-wide settings and parameters. It allows you to configure various aspects of Crawlee, such as timeouts, logging level, persistence intervals, and various other settings. The configuration can be set directly in the code or via environment variables.

### StorageClient[​](#storageclient "Direct link to StorageClient")

[`StorageClient`](https://crawlee.dev/python/python/api/class/StorageClient.md) is the backend implementation for storages in Crawlee. It provides a unified interface for [`Dataset`](https://crawlee.dev/python/python/api/class/Dataset.md), [`KeyValueStore`](https://crawlee.dev/python/python/api/class/KeyValueStore.md), and [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md), regardless of the underlying storage implementation. Storage clients were already explained in the storage clients section.

Refer to the [Storage clients guide](https://crawlee.dev/python/python/docs/guides/storage-clients.md) for more information about storage clients and how to use them.

### EventManager[​](#eventmanager "Direct link to EventManager")

[`EventManager`](https://crawlee.dev/python/python/api/class/EventManager.md) is responsible for coordinating internal events in Crawlee. It allows you to register event listeners and emit events throughout the framework. Examples of such events aborting, migrating, system info, or browser-specific events like page created, page closed and more. It provides a way to listen to events and execute custom logic when certain events occur.

## Service registration[​](#service-registration "Direct link to Service registration")

There are several ways to register services in Crawlee, depending on your use case and preferences.

### Via service locator[​](#via-service-locator "Direct link to Via service locator")

Services can be registered globally through the [`ServiceLocator`](https://crawlee.dev/python/python/api/class/ServiceLocator.md) before they are first accessed. There is a singleton `service_locator` instance that is used throughout the framework, making the services available to all components throughout the whole framework.

* Storage client
* Configuration
* Event manager

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBzZXJ2aWNlX2xvY2F0b3JcXG5mcm9tIGNyYXdsZWUuc3RvcmFnZV9jbGllbnRzIGltcG9ydCBNZW1vcnlTdG9yYWdlQ2xpZW50XFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICBzdG9yYWdlX2NsaWVudCA9IE1lbW9yeVN0b3JhZ2VDbGllbnQoKVxcblxcbiAgICAjIFJlZ2lzdGVyIHN0b3JhZ2UgY2xpZW50IHZpYSBzZXJ2aWNlIGxvY2F0b3IuXFxuICAgIHNlcnZpY2VfbG9jYXRvci5zZXRfc3RvcmFnZV9jbGllbnQoc3RvcmFnZV9jbGllbnQpXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.qWdYmfBuwsxHEd43BxSvuk22qqlR-JFcRScwPtaRYKc\&asrc=run_on_apify)

```
import asyncio

from crawlee import service_locator
from crawlee.storage_clients import MemoryStorageClient


async def main() -> None:
    storage_client = MemoryStorageClient()

    # Register storage client via service locator.
    service_locator.set_storage_client(storage_client)


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuZnJvbSBkYXRldGltZSBpbXBvcnQgdGltZWRlbHRhXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBzZXJ2aWNlX2xvY2F0b3JcXG5mcm9tIGNyYXdsZWUuY29uZmlndXJhdGlvbiBpbXBvcnQgQ29uZmlndXJhdGlvblxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY29uZmlndXJhdGlvbiA9IENvbmZpZ3VyYXRpb24oXFxuICAgICAgICBsb2dfbGV2ZWw9J0RFQlVHJyxcXG4gICAgICAgIGhlYWRsZXNzPUZhbHNlLFxcbiAgICAgICAgcGVyc2lzdF9zdGF0ZV9pbnRlcnZhbD10aW1lZGVsdGEoc2Vjb25kcz0zMCksXFxuICAgIClcXG5cXG4gICAgIyBSZWdpc3RlciBjb25maWd1cmF0aW9uIHZpYSBzZXJ2aWNlIGxvY2F0b3IuXFxuICAgIHNlcnZpY2VfbG9jYXRvci5zZXRfY29uZmlndXJhdGlvbihjb25maWd1cmF0aW9uKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.kjhvBP31xpg1MqMHUgxSNB6GXomd0-s688M0J2wRCgw\&asrc=run_on_apify)

```
import asyncio
from datetime import timedelta

from crawlee import service_locator
from crawlee.configuration import Configuration


async def main() -> None:
    configuration = Configuration(
        log_level='DEBUG',
        headless=False,
        persist_state_interval=timedelta(seconds=30),
    )

    # Register configuration via service locator.
    service_locator.set_configuration(configuration)


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuZnJvbSBkYXRldGltZSBpbXBvcnQgdGltZWRlbHRhXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBzZXJ2aWNlX2xvY2F0b3JcXG5mcm9tIGNyYXdsZWUuZXZlbnRzIGltcG9ydCBMb2NhbEV2ZW50TWFuYWdlclxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgZXZlbnRfbWFuYWdlciA9IExvY2FsRXZlbnRNYW5hZ2VyKFxcbiAgICAgICAgc3lzdGVtX2luZm9faW50ZXJ2YWw9dGltZWRlbHRhKHNlY29uZHM9NSksXFxuICAgIClcXG5cXG4gICAgIyBSZWdpc3RlciBldmVudCBtYW5hZ2VyIHZpYSBzZXJ2aWNlIGxvY2F0b3IuXFxuICAgIHNlcnZpY2VfbG9jYXRvci5zZXRfZXZlbnRfbWFuYWdlcihldmVudF9tYW5hZ2VyKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.2rYS2R7Rn3Q8ffU9xEkMV6Plsz0PBPenFKpsqodOgWA\&asrc=run_on_apify)

```
import asyncio
from datetime import timedelta

from crawlee import service_locator
from crawlee.events import LocalEventManager


async def main() -> None:
    event_manager = LocalEventManager(
        system_info_interval=timedelta(seconds=5),
    )

    # Register event manager via service locator.
    service_locator.set_event_manager(event_manager)


if __name__ == '__main__':
    asyncio.run(main())
```

### Via crawler constructors[​](#via-crawler-constructors "Direct link to Via crawler constructors")

Alternatively services can be passed to the crawler constructors. They will be registered globally to the [`ServiceLocator`](https://crawlee.dev/python/python/api/class/ServiceLocator.md) under the hood, making them available to all components and reaching consistent configuration.

* Storage client
* Configuration
* Event manager

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQYXJzZWxDcmF3bGVyXFxuZnJvbSBjcmF3bGVlLnN0b3JhZ2VfY2xpZW50cyBpbXBvcnQgTWVtb3J5U3RvcmFnZUNsaWVudFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgc3RvcmFnZV9jbGllbnQgPSBNZW1vcnlTdG9yYWdlQ2xpZW50KClcXG5cXG4gICAgIyBSZWdpc3RlciBzdG9yYWdlIGNsaWVudCB2aWEgY3Jhd2xlci5cXG4gICAgY3Jhd2xlciA9IFBhcnNlbENyYXdsZXIoXFxuICAgICAgICBzdG9yYWdlX2NsaWVudD1zdG9yYWdlX2NsaWVudCxcXG4gICAgKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.tM2ivMmojDtk7ipqUnBc7Ix65aq4BbzljgzTOOHENMI\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import ParselCrawler
from crawlee.storage_clients import MemoryStorageClient


async def main() -> None:
    storage_client = MemoryStorageClient()

    # Register storage client via crawler.
    crawler = ParselCrawler(
        storage_client=storage_client,
    )


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuZnJvbSBkYXRldGltZSBpbXBvcnQgdGltZWRlbHRhXFxuXFxuZnJvbSBjcmF3bGVlLmNvbmZpZ3VyYXRpb24gaW1wb3J0IENvbmZpZ3VyYXRpb25cXG5mcm9tIGNyYXdsZWUuY3Jhd2xlcnMgaW1wb3J0IFBhcnNlbENyYXdsZXJcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgIGNvbmZpZ3VyYXRpb24gPSBDb25maWd1cmF0aW9uKFxcbiAgICAgICAgbG9nX2xldmVsPSdERUJVRycsXFxuICAgICAgICBoZWFkbGVzcz1GYWxzZSxcXG4gICAgICAgIHBlcnNpc3Rfc3RhdGVfaW50ZXJ2YWw9dGltZWRlbHRhKHNlY29uZHM9MzApLFxcbiAgICApXFxuXFxuICAgICMgUmVnaXN0ZXIgY29uZmlndXJhdGlvbiB2aWEgY3Jhd2xlci5cXG4gICAgY3Jhd2xlciA9IFBhcnNlbENyYXdsZXIoXFxuICAgICAgICBjb25maWd1cmF0aW9uPWNvbmZpZ3VyYXRpb24sXFxuICAgIClcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6MTAyNCwidGltZW91dCI6MTgwfX0.H0fwUgT0XEzbj4sirOs_QlegbBO7_ccZCRA77Wkc07I\&asrc=run_on_apify)

```
import asyncio
from datetime import timedelta

from crawlee.configuration import Configuration
from crawlee.crawlers import ParselCrawler


async def main() -> None:
    configuration = Configuration(
        log_level='DEBUG',
        headless=False,
        persist_state_interval=timedelta(seconds=30),
    )

    # Register configuration via crawler.
    crawler = ParselCrawler(
        configuration=configuration,
    )


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuZnJvbSBkYXRldGltZSBpbXBvcnQgdGltZWRlbHRhXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQYXJzZWxDcmF3bGVyXFxuZnJvbSBjcmF3bGVlLmV2ZW50cyBpbXBvcnQgTG9jYWxFdmVudE1hbmFnZXJcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgIGV2ZW50X21hbmFnZXIgPSBMb2NhbEV2ZW50TWFuYWdlcihcXG4gICAgICAgIHN5c3RlbV9pbmZvX2ludGVydmFsPXRpbWVkZWx0YShzZWNvbmRzPTUpLFxcbiAgICApXFxuXFxuICAgICMgUmVnaXN0ZXIgZXZlbnQgbWFuYWdlciB2aWEgY3Jhd2xlci5cXG4gICAgY3Jhd2xlciA9IFBhcnNlbENyYXdsZXIoXFxuICAgICAgICBldmVudF9tYW5hZ2VyPWV2ZW50X21hbmFnZXIsXFxuICAgIClcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6MTAyNCwidGltZW91dCI6MTgwfX0.jVo1QPvaAmYGJD4Lk8A-KZS7giLC7o53cJlcNvk70Ks\&asrc=run_on_apify)

```
import asyncio
from datetime import timedelta

from crawlee.crawlers import ParselCrawler
from crawlee.events import LocalEventManager


async def main() -> None:
    event_manager = LocalEventManager(
        system_info_interval=timedelta(seconds=5),
    )

    # Register event manager via crawler.
    crawler = ParselCrawler(
        event_manager=event_manager,
    )


if __name__ == '__main__':
    asyncio.run(main())
```

### Via storage constructors[​](#via-storage-constructors "Direct link to Via storage constructors")

Alternatively, services can be provided when opening specific storage instances, which uses them only for that particular instance without affecting global configuration.

* Storage client
* Configuration

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLnN0b3JhZ2VfY2xpZW50cyBpbXBvcnQgTWVtb3J5U3RvcmFnZUNsaWVudFxcbmZyb20gY3Jhd2xlZS5zdG9yYWdlcyBpbXBvcnQgRGF0YXNldFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgc3RvcmFnZV9jbGllbnQgPSBNZW1vcnlTdG9yYWdlQ2xpZW50KClcXG5cXG4gICAgIyBQYXNzIHRoZSBzdG9yYWdlIGNsaWVudCB0byB0aGUgZGF0YXNldCAob3Igb3RoZXIgc3RvcmFnZSkgd2hlbiBvcGVuaW5nIGl0LlxcbiAgICBkYXRhc2V0ID0gYXdhaXQgRGF0YXNldC5vcGVuKFxcbiAgICAgICAgc3RvcmFnZV9jbGllbnQ9c3RvcmFnZV9jbGllbnQsXFxuICAgIClcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6MTAyNCwidGltZW91dCI6MTgwfX0.W49rIWZ4gBy6bmUFINddkyWc6kC5qLJQwGi6Y1dVqbI\&asrc=run_on_apify)

```
import asyncio

from crawlee.storage_clients import MemoryStorageClient
from crawlee.storages import Dataset


async def main() -> None:
    storage_client = MemoryStorageClient()

    # Pass the storage client to the dataset (or other storage) when opening it.
    dataset = await Dataset.open(
        storage_client=storage_client,
    )


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuZnJvbSBkYXRldGltZSBpbXBvcnQgdGltZWRlbHRhXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBzZXJ2aWNlX2xvY2F0b3JcXG5mcm9tIGNyYXdsZWUuY29uZmlndXJhdGlvbiBpbXBvcnQgQ29uZmlndXJhdGlvblxcbmZyb20gY3Jhd2xlZS5zdG9yYWdlX2NsaWVudHMgaW1wb3J0IE1lbW9yeVN0b3JhZ2VDbGllbnRcXG5mcm9tIGNyYXdsZWUuc3RvcmFnZXMgaW1wb3J0IERhdGFzZXRcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgIGNvbmZpZ3VyYXRpb24gPSBDb25maWd1cmF0aW9uKFxcbiAgICAgICAgbG9nX2xldmVsPSdERUJVRycsXFxuICAgICAgICBoZWFkbGVzcz1GYWxzZSxcXG4gICAgICAgIHBlcnNpc3Rfc3RhdGVfaW50ZXJ2YWw9dGltZWRlbHRhKHNlY29uZHM9MzApLFxcbiAgICApXFxuICAgICMgU2V0IHRoZSBjdXN0b20gY29uZmlndXJhdGlvbiBhcyB0aGUgZ2xvYmFsIGRlZmF1bHQgY29uZmlndXJhdGlvbi5cXG4gICAgc2VydmljZV9sb2NhdG9yLnNldF9jb25maWd1cmF0aW9uKGNvbmZpZ3VyYXRpb24pXFxuXFxuICAgICMgVXNlIHRoZSBnbG9iYWwgZGVmYXVsdHMgd2hlbiBjcmVhdGluZyB0aGUgZGF0YXNldCAob3Igb3RoZXIgc3RvcmFnZSkuXFxuICAgIGRhdGFzZXRfMSA9IGF3YWl0IERhdGFzZXQub3BlbigpXFxuXFxuICAgICMgT3Igc2V0IGV4cGxpY2l0bHkgc3BlY2lmaWMgY29uZmlndXJhdGlvbiBpZlxcbiAgICAjIHlvdSBkbyBub3Qgd2FudCB0byByZWx5IG9uIGdsb2JhbCBkZWZhdWx0cy5cXG4gICAgZGF0YXNldF8yID0gYXdhaXQgRGF0YXNldC5vcGVuKFxcbiAgICAgICAgc3RvcmFnZV9jbGllbnQ9TWVtb3J5U3RvcmFnZUNsaWVudCgpLCBjb25maWd1cmF0aW9uPWNvbmZpZ3VyYXRpb25cXG4gICAgKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.ZQdBPfba-b3QffzdKyqVUxnhiMXYX9RveYFaXnvEelI\&asrc=run_on_apify)

```
import asyncio
from datetime import timedelta

from crawlee import service_locator
from crawlee.configuration import Configuration
from crawlee.storage_clients import MemoryStorageClient
from crawlee.storages import Dataset


async def main() -> None:
    configuration = Configuration(
        log_level='DEBUG',
        headless=False,
        persist_state_interval=timedelta(seconds=30),
    )
    # Set the custom configuration as the global default configuration.
    service_locator.set_configuration(configuration)

    # Use the global defaults when creating the dataset (or other storage).
    dataset_1 = await Dataset.open()

    # Or set explicitly specific configuration if
    # you do not want to rely on global defaults.
    dataset_2 = await Dataset.open(
        storage_client=MemoryStorageClient(), configuration=configuration
    )


if __name__ == '__main__':
    asyncio.run(main())
```

## Conflict prevention[​](#conflict-prevention "Direct link to Conflict prevention")

Once a service has been retrieved from the service locator, attempting to set a different instance will raise a [`ServiceConflictError`](https://crawlee.dev/python/python/api/class/ServiceConflictError.md) to prevent accidental configuration conflicts.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBzZXJ2aWNlX2xvY2F0b3JcXG5mcm9tIGNyYXdsZWUuc3RvcmFnZV9jbGllbnRzIGltcG9ydCBGaWxlU3lzdGVtU3RvcmFnZUNsaWVudCwgTWVtb3J5U3RvcmFnZUNsaWVudFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBSZWdpc3RlciB0aGUgc3RvcmFnZSBjbGllbnQgdmlhIHNlcnZpY2UgbG9jYXRvci5cXG4gICAgbWVtb3J5X3N0b3JhZ2VfY2xpZW50ID0gTWVtb3J5U3RvcmFnZUNsaWVudCgpXFxuICAgIHNlcnZpY2VfbG9jYXRvci5zZXRfc3RvcmFnZV9jbGllbnQobWVtb3J5X3N0b3JhZ2VfY2xpZW50KVxcblxcbiAgICAjIFJldHJpZXZlIHRoZSBzdG9yYWdlIGNsaWVudC5cXG4gICAgY3VycmVudF9zdG9yYWdlX2NsaWVudCA9IHNlcnZpY2VfbG9jYXRvci5nZXRfc3RvcmFnZV9jbGllbnQoKVxcblxcbiAgICAjIFRyeSB0byBzZXQgYSBkaWZmZXJlbnQgc3RvcmFnZSBjbGllbnQsIHdoaWNoIHdpbGwgcmFpc2UgU2VydmljZUNvbmZsaWN0RXJyb3JcXG4gICAgIyBpZiBzdG9yYWdlIGNsaWVudCB3YXMgYWxyZWFkeSByZXRyaWV2ZWQuXFxuICAgIGZpbGVfc3lzdGVtX3N0b3JhZ2VfY2xpZW50ID0gRmlsZVN5c3RlbVN0b3JhZ2VDbGllbnQoKVxcbiAgICBzZXJ2aWNlX2xvY2F0b3Iuc2V0X3N0b3JhZ2VfY2xpZW50KGZpbGVfc3lzdGVtX3N0b3JhZ2VfY2xpZW50KVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.MVj_Hogwac7FfuRjPjrSs9Ki7JnrmiDrVfTHSOcoRWo\&asrc=run_on_apify)

```
import asyncio

from crawlee import service_locator
from crawlee.storage_clients import FileSystemStorageClient, MemoryStorageClient


async def main() -> None:
    # Register the storage client via service locator.
    memory_storage_client = MemoryStorageClient()
    service_locator.set_storage_client(memory_storage_client)

    # Retrieve the storage client.
    current_storage_client = service_locator.get_storage_client()

    # Try to set a different storage client, which will raise ServiceConflictError
    # if storage client was already retrieved.
    file_system_storage_client = FileSystemStorageClient()
    service_locator.set_storage_client(file_system_storage_client)


if __name__ == '__main__':
    asyncio.run(main())
```

## Conclusion[​](#conclusion "Direct link to Conclusion")

The [`ServiceLocator`](https://crawlee.dev/python/python/api/class/ServiceLocator.md) is a tool for managing global services in Crawlee. It provides a consistent way to configure and access services throughout the framework, ensuring that all components have access to the same configuration and services.

If you have questions or need assistance, feel free to reach out on our [GitHub](https://github.com/apify/crawlee-python) or join our [Discord community](https://discord.com/invite/jyEM2PRvMU). Happy scraping!

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/guides/service_locator.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/guides/scaling-crawlers.md)

[Scaling crawlers](https://crawlee.dev/python/python/docs/guides/scaling-crawlers.md)

[Next](https://crawlee.dev/python/python/docs/guides/session-management.md)

[Session management](https://crawlee.dev/python/python/docs/guides/session-management.md)


---

* [](https://crawlee.dev/python/python)
* [Guides](https://crawlee.dev/python/python/docs/guides.md)
* Session management

Version: 1.6

On this page

# Session management

The [`SessionPool`](https://crawlee.dev/python/python/api/class/SessionPool.md) class provides a robust way to manage the rotation of proxy IP addresses, cookies, and other custom settings in Crawlee. Its primary advantage is the ability to filter out blocked or non-functional proxies, ensuring that your scraper avoids retrying requests through known problematic proxies.

Additionally, it enables storing information tied to specific IP addresses, such as cookies, authentication tokens, and custom headers. This association reduces the probability of detection and blocking by ensuring cookies and other identifiers are used consistently with the same IP address.

Finally, it ensures even IP address rotation by randomly selecting sessions. This helps prevent overuse of a limited pool of available IPs, reducing the risk of IP bans and enhancing the efficiency of your scraper.

For more details on configuring proxies, refer to the [Proxy management](https://crawlee.dev/python/python/docs/guides/proxy-management.md) guide.

Now, let's explore examples of how to use the [`SessionPool`](https://crawlee.dev/python/python/api/class/SessionPool.md) in different scenarios:

* with [`BasicCrawler`](https://crawlee.dev/python/python/api/class/BasicCrawler.md);
* with [`HttpCrawler`](https://crawlee.dev/python/python/api/class/HttpCrawler.md);
* with [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md);
* with [`ParselCrawler`](https://crawlee.dev/python/python/api/class/ParselCrawler.md);
* with [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md);
* without a crawler (standalone usage to manage sessions manually).

- BasicSource
- HttpCrawler
- BeautifulSoupCrawler
- ParselCrawler
- PlaywrightCrawler
- Standalone

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuaW1wb3J0IHJlXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCYXNpY0NyYXdsZXIsIEJhc2ljQ3Jhd2xpbmdDb250ZXh0XFxuZnJvbSBjcmF3bGVlLnByb3h5X2NvbmZpZ3VyYXRpb24gaW1wb3J0IFByb3h5Q29uZmlndXJhdGlvblxcbmZyb20gY3Jhd2xlZS5zZXNzaW9ucyBpbXBvcnQgU2Vzc2lvblBvb2xcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgICMgVG8gdXNlIHRoZSBwcm94eSBJUCBzZXNzaW9uIHJvdGF0aW9uIGxvZ2ljLCB5b3UgbXVzdCB0dXJuIHRoZSBwcm94eSB1c2FnZSBvbi5cXG4gICAgcHJveHlfY29uZmlndXJhdGlvbiA9IFByb3h5Q29uZmlndXJhdGlvbihcXG4gICAgICAgICMgb3B0aW9uc1xcbiAgICApXFxuXFxuICAgICMgSW5pdGlhbGl6ZSBjcmF3bGVyIHdpdGggYSBjdXN0b20gU2Vzc2lvblBvb2wgY29uZmlndXJhdGlvblxcbiAgICAjIHRvIG1hbmFnZSBjb25jdXJyZW50IHNlc3Npb25zIGFuZCBwcm94eSByb3RhdGlvblxcbiAgICBjcmF3bGVyID0gQmFzaWNDcmF3bGVyKFxcbiAgICAgICAgcHJveHlfY29uZmlndXJhdGlvbj1wcm94eV9jb25maWd1cmF0aW9uLFxcbiAgICAgICAgIyBBY3RpdmF0ZXMgdGhlIFNlc3Npb24gcG9vbCAoZGVmYXVsdCBpcyB0cnVlKS5cXG4gICAgICAgIHVzZV9zZXNzaW9uX3Bvb2w9VHJ1ZSxcXG4gICAgICAgICMgT3ZlcnJpZGVzIGRlZmF1bHQgU2Vzc2lvbiBwb29sIGNvbmZpZ3VyYXRpb24uXFxuICAgICAgICBzZXNzaW9uX3Bvb2w9U2Vzc2lvblBvb2wobWF4X3Bvb2xfc2l6ZT0xMDApLFxcbiAgICApXFxuXFxuICAgICMgRGVmaW5lIHRoZSBkZWZhdWx0IHJlcXVlc3QgaGFuZGxlciB0aGF0IG1hbmFnZXMgc2Vzc2lvbiBzdGF0ZXNcXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgZGVmYXVsdF9oYW5kbGVyKGNvbnRleHQ6IEJhc2ljQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgIyBTZW5kIHJlcXVlc3QsIEJhc2ljQ3Jhd2xlciBhdXRvbWF0aWNhbGx5IHNlbGVjdHMgYSBzZXNzaW9uIGZyb20gdGhlIHBvb2xcXG4gICAgICAgICMgYW5kIHNldHMgYSBwcm94eSBmb3IgaXQuIFlvdSBjYW4gY2hlY2sgaXQgd2l0aCBgY29udGV4dC5zZXNzaW9uYFxcbiAgICAgICAgIyBhbmQgYGNvbnRleHQucHJveHlfaW5mb2AuXFxuICAgICAgICByZXNwb25zZSA9IGF3YWl0IGNvbnRleHQuc2VuZF9yZXF1ZXN0KGNvbnRleHQucmVxdWVzdC51cmwpXFxuXFxuICAgICAgICBwYWdlX2NvbnRlbnQgPSAoYXdhaXQgcmVzcG9uc2UucmVhZCgpKS5kZWNvZGUoKVxcbiAgICAgICAgdGl0bGVfbWF0Y2ggPSByZS5zZWFyY2gocic8dGl0bGUoPzouKj8pPiguKj8pPC90aXRsZT4nLCBwYWdlX2NvbnRlbnQpXFxuXFxuICAgICAgICBpZiBjb250ZXh0LnNlc3Npb24gYW5kICh0aXRsZSA6PSB0aXRsZV9tYXRjaC5ncm91cCgxKSBpZiB0aXRsZV9tYXRjaCBlbHNlIE5vbmUpOlxcbiAgICAgICAgICAgIGlmIHRpdGxlID09ICdCbG9ja2VkJzpcXG4gICAgICAgICAgICAgICAgY29udGV4dC5zZXNzaW9uLnJldGlyZSgpXFxuICAgICAgICAgICAgZWxpZiB0aXRsZSA9PSAnTm90IHN1cmUgaWYgYmxvY2tlZCwgbWlnaHQgYWxzbyBiZSBhIGNvbm5lY3Rpb24gZXJyb3InOlxcbiAgICAgICAgICAgICAgICBjb250ZXh0LnNlc3Npb24ubWFya19iYWQoKVxcbiAgICAgICAgICAgIGVsc2U6XFxuICAgICAgICAgICAgICAgIGNvbnRleHQuc2Vzc2lvbi5tYXJrX2dvb2QoKSAgIyBCYXNpY0NyYXdsZXIgaGFuZGxlcyB0aGlzIGF1dG9tYXRpY2FsbHkuXFxuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9jcmF3bGVlLmRldi8nXSlcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6MTAyNCwidGltZW91dCI6MTgwfX0.EMbU7y1ZfWzHJt8WrOFCAQMOG7UozDl2KXwZ0a9_HGg\&asrc=run_on_apify)

```
import asyncio
import re

from crawlee.crawlers import BasicCrawler, BasicCrawlingContext
from crawlee.proxy_configuration import ProxyConfiguration
from crawlee.sessions import SessionPool


async def main() -> None:
    # To use the proxy IP session rotation logic, you must turn the proxy usage on.
    proxy_configuration = ProxyConfiguration(
        # options
    )

    # Initialize crawler with a custom SessionPool configuration
    # to manage concurrent sessions and proxy rotation
    crawler = BasicCrawler(
        proxy_configuration=proxy_configuration,
        # Activates the Session pool (default is true).
        use_session_pool=True,
        # Overrides default Session pool configuration.
        session_pool=SessionPool(max_pool_size=100),
    )

    # Define the default request handler that manages session states
    @crawler.router.default_handler
    async def default_handler(context: BasicCrawlingContext) -> None:
        # Send request, BasicCrawler automatically selects a session from the pool
        # and sets a proxy for it. You can check it with `context.session`
        # and `context.proxy_info`.
        response = await context.send_request(context.request.url)

        page_content = (await response.read()).decode()
        title_match = re.search(r'<title(?:.*?)>(.*?)</title>', page_content)

        if context.session and (title := title_match.group(1) if title_match else None):
            if title == 'Blocked':
                context.session.retire()
            elif title == 'Not sure if blocked, might also be a connection error':
                context.session.mark_bad()
            else:
                context.session.mark_good()  # BasicCrawler handles this automatically.

    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuaW1wb3J0IHJlXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBIdHRwQ3Jhd2xlciwgSHR0cENyYXdsaW5nQ29udGV4dFxcbmZyb20gY3Jhd2xlZS5wcm94eV9jb25maWd1cmF0aW9uIGltcG9ydCBQcm94eUNvbmZpZ3VyYXRpb25cXG5mcm9tIGNyYXdsZWUuc2Vzc2lvbnMgaW1wb3J0IFNlc3Npb25Qb29sXFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICAjIFRvIHVzZSB0aGUgcHJveHkgSVAgc2Vzc2lvbiByb3RhdGlvbiBsb2dpYywgeW91IG11c3QgdHVybiB0aGUgcHJveHkgdXNhZ2Ugb24uXFxuICAgIHByb3h5X2NvbmZpZ3VyYXRpb24gPSBQcm94eUNvbmZpZ3VyYXRpb24oXFxuICAgICAgICAjIG9wdGlvbnNcXG4gICAgKVxcblxcbiAgICAjIEluaXRpYWxpemUgY3Jhd2xlciB3aXRoIGEgY3VzdG9tIFNlc3Npb25Qb29sIGNvbmZpZ3VyYXRpb25cXG4gICAgIyB0byBtYW5hZ2UgY29uY3VycmVudCBzZXNzaW9ucyBhbmQgcHJveHkgcm90YXRpb25cXG4gICAgY3Jhd2xlciA9IEh0dHBDcmF3bGVyKFxcbiAgICAgICAgcHJveHlfY29uZmlndXJhdGlvbj1wcm94eV9jb25maWd1cmF0aW9uLFxcbiAgICAgICAgIyBBY3RpdmF0ZXMgdGhlIFNlc3Npb24gcG9vbCAoZGVmYXVsdCBpcyB0cnVlKS5cXG4gICAgICAgIHVzZV9zZXNzaW9uX3Bvb2w9VHJ1ZSxcXG4gICAgICAgICMgT3ZlcnJpZGVzIGRlZmF1bHQgU2Vzc2lvbiBwb29sIGNvbmZpZ3VyYXRpb24uXFxuICAgICAgICBzZXNzaW9uX3Bvb2w9U2Vzc2lvblBvb2wobWF4X3Bvb2xfc2l6ZT0xMDApLFxcbiAgICApXFxuXFxuICAgICMgRGVmaW5lIHRoZSBkZWZhdWx0IHJlcXVlc3QgaGFuZGxlciB0aGF0IG1hbmFnZXMgc2Vzc2lvbiBzdGF0ZXNcXG4gICAgIyBiYXNlZCBvbiB0aGUgcmVzcG9uc2UgY29udGVudCBhbmQgcG90ZW50aWFsIGJsb2NraW5nXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIGRlZmF1bHRfaGFuZGxlcihjb250ZXh0OiBIdHRwQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgcGFnZV9jb250ZW50ID0gKGF3YWl0IGNvbnRleHQuaHR0cF9yZXNwb25zZS5yZWFkKCkpLmRlY29kZSgpXFxuICAgICAgICB0aXRsZV9tYXRjaCA9IHJlLnNlYXJjaChyJzx0aXRsZSg_Oi4qPyk-KC4qPyk8L3RpdGxlPicsIHBhZ2VfY29udGVudClcXG5cXG4gICAgICAgIGlmIGNvbnRleHQuc2Vzc2lvbiBhbmQgKHRpdGxlIDo9IHRpdGxlX21hdGNoLmdyb3VwKDEpIGlmIHRpdGxlX21hdGNoIGVsc2UgTm9uZSk6XFxuICAgICAgICAgICAgaWYgdGl0bGUgPT0gJ0Jsb2NrZWQnOlxcbiAgICAgICAgICAgICAgICBjb250ZXh0LnNlc3Npb24ucmV0aXJlKClcXG4gICAgICAgICAgICBlbGlmIHRpdGxlID09ICdOb3Qgc3VyZSBpZiBibG9ja2VkLCBtaWdodCBhbHNvIGJlIGEgY29ubmVjdGlvbiBlcnJvcic6XFxuICAgICAgICAgICAgICAgIGNvbnRleHQuc2Vzc2lvbi5tYXJrX2JhZCgpXFxuICAgICAgICAgICAgZWxzZTpcXG4gICAgICAgICAgICAgICAgY29udGV4dC5zZXNzaW9uLm1hcmtfZ29vZCgpICAjIEJhc2ljQ3Jhd2xlciBoYW5kbGVzIHRoaXMgYXV0b21hdGljYWxseS5cXG5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2NyYXdsZWUuZGV2LyddKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ._hnjLy0dTokK9Xq6tUuRu9i6VmDmmxsoDZBfeOEMyF0\&asrc=run_on_apify)

```
import asyncio
import re

from crawlee.crawlers import HttpCrawler, HttpCrawlingContext
from crawlee.proxy_configuration import ProxyConfiguration
from crawlee.sessions import SessionPool


async def main() -> None:
    # To use the proxy IP session rotation logic, you must turn the proxy usage on.
    proxy_configuration = ProxyConfiguration(
        # options
    )

    # Initialize crawler with a custom SessionPool configuration
    # to manage concurrent sessions and proxy rotation
    crawler = HttpCrawler(
        proxy_configuration=proxy_configuration,
        # Activates the Session pool (default is true).
        use_session_pool=True,
        # Overrides default Session pool configuration.
        session_pool=SessionPool(max_pool_size=100),
    )

    # Define the default request handler that manages session states
    # based on the response content and potential blocking
    @crawler.router.default_handler
    async def default_handler(context: HttpCrawlingContext) -> None:
        page_content = (await context.http_response.read()).decode()
        title_match = re.search(r'<title(?:.*?)>(.*?)</title>', page_content)

        if context.session and (title := title_match.group(1) if title_match else None):
            if title == 'Blocked':
                context.session.retire()
            elif title == 'Not sure if blocked, might also be a connection error':
                context.session.mark_bad()
            else:
                context.session.mark_good()  # BasicCrawler handles this automatically.

    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcbmZyb20gY3Jhd2xlZS5wcm94eV9jb25maWd1cmF0aW9uIGltcG9ydCBQcm94eUNvbmZpZ3VyYXRpb25cXG5mcm9tIGNyYXdsZWUuc2Vzc2lvbnMgaW1wb3J0IFNlc3Npb25Qb29sXFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICAjIFRvIHVzZSB0aGUgcHJveHkgSVAgc2Vzc2lvbiByb3RhdGlvbiBsb2dpYywgeW91IG11c3QgdHVybiB0aGUgcHJveHkgdXNhZ2Ugb24uXFxuICAgIHByb3h5X2NvbmZpZ3VyYXRpb24gPSBQcm94eUNvbmZpZ3VyYXRpb24oXFxuICAgICAgICAjIG9wdGlvbnNcXG4gICAgKVxcblxcbiAgICAjIEluaXRpYWxpemUgY3Jhd2xlciB3aXRoIGEgY3VzdG9tIFNlc3Npb25Qb29sIGNvbmZpZ3VyYXRpb25cXG4gICAgIyB0byBtYW5hZ2UgY29uY3VycmVudCBzZXNzaW9ucyBhbmQgcHJveHkgcm90YXRpb25cXG4gICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKFxcbiAgICAgICAgcHJveHlfY29uZmlndXJhdGlvbj1wcm94eV9jb25maWd1cmF0aW9uLFxcbiAgICAgICAgIyBBY3RpdmF0ZXMgdGhlIFNlc3Npb24gcG9vbCAoZGVmYXVsdCBpcyB0cnVlKS5cXG4gICAgICAgIHVzZV9zZXNzaW9uX3Bvb2w9VHJ1ZSxcXG4gICAgICAgICMgT3ZlcnJpZGVzIGRlZmF1bHQgU2Vzc2lvbiBwb29sIGNvbmZpZ3VyYXRpb24uXFxuICAgICAgICBzZXNzaW9uX3Bvb2w9U2Vzc2lvblBvb2wobWF4X3Bvb2xfc2l6ZT0xMDApLFxcbiAgICApXFxuXFxuICAgICMgRGVmaW5lIHRoZSBkZWZhdWx0IHJlcXVlc3QgaGFuZGxlciB0aGF0IG1hbmFnZXMgc2Vzc2lvbiBzdGF0ZXNcXG4gICAgIyBiYXNlZCBvbiB0aGUgcmVzcG9uc2UgY29udGVudCBhbmQgcG90ZW50aWFsIGJsb2NraW5nXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIGRlZmF1bHRfaGFuZGxlcihjb250ZXh0OiBCZWF1dGlmdWxTb3VwQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgdGl0bGUgPSBjb250ZXh0LnNvdXAudGl0bGUuZ2V0X3RleHQoKSBpZiBjb250ZXh0LnNvdXAudGl0bGUgZWxzZSBOb25lXFxuXFxuICAgICAgICBpZiBjb250ZXh0LnNlc3Npb246XFxuICAgICAgICAgICAgaWYgdGl0bGUgPT0gJ0Jsb2NrZWQnOlxcbiAgICAgICAgICAgICAgICBjb250ZXh0LnNlc3Npb24ucmV0aXJlKClcXG4gICAgICAgICAgICBlbGlmIHRpdGxlID09ICdOb3Qgc3VyZSBpZiBibG9ja2VkLCBtaWdodCBhbHNvIGJlIGEgY29ubmVjdGlvbiBlcnJvcic6XFxuICAgICAgICAgICAgICAgIGNvbnRleHQuc2Vzc2lvbi5tYXJrX2JhZCgpXFxuICAgICAgICAgICAgZWxzZTpcXG4gICAgICAgICAgICAgICAgY29udGV4dC5zZXNzaW9uLm1hcmtfZ29vZCgpICAjIEJhc2ljQ3Jhd2xlciBoYW5kbGVzIHRoaXMgYXV0b21hdGljYWxseS5cXG5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2NyYXdsZWUuZGV2LyddKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.BBAfvBVRnmOCYQ2ojcJelXrSYzza4-OwhE9oWsLGZbo\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext
from crawlee.proxy_configuration import ProxyConfiguration
from crawlee.sessions import SessionPool


async def main() -> None:
    # To use the proxy IP session rotation logic, you must turn the proxy usage on.
    proxy_configuration = ProxyConfiguration(
        # options
    )

    # Initialize crawler with a custom SessionPool configuration
    # to manage concurrent sessions and proxy rotation
    crawler = BeautifulSoupCrawler(
        proxy_configuration=proxy_configuration,
        # Activates the Session pool (default is true).
        use_session_pool=True,
        # Overrides default Session pool configuration.
        session_pool=SessionPool(max_pool_size=100),
    )

    # Define the default request handler that manages session states
    # based on the response content and potential blocking
    @crawler.router.default_handler
    async def default_handler(context: BeautifulSoupCrawlingContext) -> None:
        title = context.soup.title.get_text() if context.soup.title else None

        if context.session:
            if title == 'Blocked':
                context.session.retire()
            elif title == 'Not sure if blocked, might also be a connection error':
                context.session.mark_bad()
            else:
                context.session.mark_good()  # BasicCrawler handles this automatically.

    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQYXJzZWxDcmF3bGVyLCBQYXJzZWxDcmF3bGluZ0NvbnRleHRcXG5mcm9tIGNyYXdsZWUucHJveHlfY29uZmlndXJhdGlvbiBpbXBvcnQgUHJveHlDb25maWd1cmF0aW9uXFxuZnJvbSBjcmF3bGVlLnNlc3Npb25zIGltcG9ydCBTZXNzaW9uUG9vbFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBUbyB1c2UgdGhlIHByb3h5IElQIHNlc3Npb24gcm90YXRpb24gbG9naWMsIHlvdSBtdXN0IHR1cm4gdGhlIHByb3h5IHVzYWdlIG9uLlxcbiAgICBwcm94eV9jb25maWd1cmF0aW9uID0gUHJveHlDb25maWd1cmF0aW9uKFxcbiAgICAgICAgIyBvcHRpb25zXFxuICAgIClcXG5cXG4gICAgIyBJbml0aWFsaXplIGNyYXdsZXIgd2l0aCBhIGN1c3RvbSBTZXNzaW9uUG9vbCBjb25maWd1cmF0aW9uXFxuICAgICMgdG8gbWFuYWdlIGNvbmN1cnJlbnQgc2Vzc2lvbnMgYW5kIHByb3h5IHJvdGF0aW9uXFxuICAgIGNyYXdsZXIgPSBQYXJzZWxDcmF3bGVyKFxcbiAgICAgICAgcHJveHlfY29uZmlndXJhdGlvbj1wcm94eV9jb25maWd1cmF0aW9uLFxcbiAgICAgICAgIyBBY3RpdmF0ZXMgdGhlIFNlc3Npb24gcG9vbCAoZGVmYXVsdCBpcyB0cnVlKS5cXG4gICAgICAgIHVzZV9zZXNzaW9uX3Bvb2w9VHJ1ZSxcXG4gICAgICAgICMgT3ZlcnJpZGVzIGRlZmF1bHQgU2Vzc2lvbiBwb29sIGNvbmZpZ3VyYXRpb24uXFxuICAgICAgICBzZXNzaW9uX3Bvb2w9U2Vzc2lvblBvb2wobWF4X3Bvb2xfc2l6ZT0xMDApLFxcbiAgICApXFxuXFxuICAgICMgRGVmaW5lIHRoZSBkZWZhdWx0IHJlcXVlc3QgaGFuZGxlciB0aGF0IG1hbmFnZXMgc2Vzc2lvbiBzdGF0ZXNcXG4gICAgIyBiYXNlZCBvbiB0aGUgcmVzcG9uc2UgY29udGVudCBhbmQgcG90ZW50aWFsIGJsb2NraW5nXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIGRlZmF1bHRfaGFuZGxlcihjb250ZXh0OiBQYXJzZWxDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICB0aXRsZSA9IGNvbnRleHQuc2VsZWN0b3IuY3NzKCd0aXRsZTo6dGV4dCcpLmdldCgpXFxuXFxuICAgICAgICBpZiBjb250ZXh0LnNlc3Npb246XFxuICAgICAgICAgICAgaWYgdGl0bGUgPT0gJ0Jsb2NrZWQnOlxcbiAgICAgICAgICAgICAgICBjb250ZXh0LnNlc3Npb24ucmV0aXJlKClcXG4gICAgICAgICAgICBlbGlmIHRpdGxlID09ICdOb3Qgc3VyZSBpZiBibG9ja2VkLCBtaWdodCBhbHNvIGJlIGEgY29ubmVjdGlvbiBlcnJvcic6XFxuICAgICAgICAgICAgICAgIGNvbnRleHQuc2Vzc2lvbi5tYXJrX2JhZCgpXFxuICAgICAgICAgICAgZWxzZTpcXG4gICAgICAgICAgICAgICAgY29udGV4dC5zZXNzaW9uLm1hcmtfZ29vZCgpICAjIEJhc2ljQ3Jhd2xlciBoYW5kbGVzIHRoaXMgYXV0b21hdGljYWxseS5cXG5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2NyYXdsZWUuZGV2LyddKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.RwtoUd-PwKa2F58j_FpOVnhtnixdPJVBIgpiBVbS_Lk\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import ParselCrawler, ParselCrawlingContext
from crawlee.proxy_configuration import ProxyConfiguration
from crawlee.sessions import SessionPool


async def main() -> None:
    # To use the proxy IP session rotation logic, you must turn the proxy usage on.
    proxy_configuration = ProxyConfiguration(
        # options
    )

    # Initialize crawler with a custom SessionPool configuration
    # to manage concurrent sessions and proxy rotation
    crawler = ParselCrawler(
        proxy_configuration=proxy_configuration,
        # Activates the Session pool (default is true).
        use_session_pool=True,
        # Overrides default Session pool configuration.
        session_pool=SessionPool(max_pool_size=100),
    )

    # Define the default request handler that manages session states
    # based on the response content and potential blocking
    @crawler.router.default_handler
    async def default_handler(context: ParselCrawlingContext) -> None:
        title = context.selector.css('title::text').get()

        if context.session:
            if title == 'Blocked':
                context.session.retire()
            elif title == 'Not sure if blocked, might also be a connection error':
                context.session.mark_bad()
            else:
                context.session.mark_good()  # BasicCrawler handles this automatically.

    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQbGF5d3JpZ2h0Q3Jhd2xlciwgUGxheXdyaWdodENyYXdsaW5nQ29udGV4dFxcbmZyb20gY3Jhd2xlZS5wcm94eV9jb25maWd1cmF0aW9uIGltcG9ydCBQcm94eUNvbmZpZ3VyYXRpb25cXG5mcm9tIGNyYXdsZWUuc2Vzc2lvbnMgaW1wb3J0IFNlc3Npb25Qb29sXFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICAjIFRvIHVzZSB0aGUgcHJveHkgSVAgc2Vzc2lvbiByb3RhdGlvbiBsb2dpYywgeW91IG11c3QgdHVybiB0aGUgcHJveHkgdXNhZ2Ugb24uXFxuICAgIHByb3h5X2NvbmZpZ3VyYXRpb24gPSBQcm94eUNvbmZpZ3VyYXRpb24oXFxuICAgICAgICAjIG9wdGlvbnNcXG4gICAgKVxcblxcbiAgICAjIEluaXRpYWxpemUgY3Jhd2xlciB3aXRoIGEgY3VzdG9tIFNlc3Npb25Qb29sIGNvbmZpZ3VyYXRpb25cXG4gICAgIyB0byBtYW5hZ2UgY29uY3VycmVudCBzZXNzaW9ucyBhbmQgcHJveHkgcm90YXRpb25cXG4gICAgY3Jhd2xlciA9IFBsYXl3cmlnaHRDcmF3bGVyKFxcbiAgICAgICAgcHJveHlfY29uZmlndXJhdGlvbj1wcm94eV9jb25maWd1cmF0aW9uLFxcbiAgICAgICAgIyBBY3RpdmF0ZXMgdGhlIFNlc3Npb24gcG9vbCAoZGVmYXVsdCBpcyB0cnVlKS5cXG4gICAgICAgIHVzZV9zZXNzaW9uX3Bvb2w9VHJ1ZSxcXG4gICAgICAgICMgT3ZlcnJpZGVzIGRlZmF1bHQgU2Vzc2lvbiBwb29sIGNvbmZpZ3VyYXRpb24uXFxuICAgICAgICBzZXNzaW9uX3Bvb2w9U2Vzc2lvblBvb2wobWF4X3Bvb2xfc2l6ZT0xMDApLFxcbiAgICApXFxuXFxuICAgICMgRGVmaW5lIHRoZSBkZWZhdWx0IHJlcXVlc3QgaGFuZGxlciB0aGF0IG1hbmFnZXMgc2Vzc2lvbiBzdGF0ZXNcXG4gICAgIyBiYXNlZCBvbiB0aGUgcmVzcG9uc2UgY29udGVudCBhbmQgcG90ZW50aWFsIGJsb2NraW5nXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIGRlZmF1bHRfaGFuZGxlcihjb250ZXh0OiBQbGF5d3JpZ2h0Q3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgdGl0bGUgPSBhd2FpdCBjb250ZXh0LnBhZ2UudGl0bGUoKVxcblxcbiAgICAgICAgaWYgY29udGV4dC5zZXNzaW9uOlxcbiAgICAgICAgICAgIGlmIHRpdGxlID09ICdCbG9ja2VkJzpcXG4gICAgICAgICAgICAgICAgY29udGV4dC5zZXNzaW9uLnJldGlyZSgpXFxuICAgICAgICAgICAgZWxpZiB0aXRsZSA9PSAnTm90IHN1cmUgaWYgYmxvY2tlZCwgbWlnaHQgYWxzbyBiZSBhIGNvbm5lY3Rpb24gZXJyb3InOlxcbiAgICAgICAgICAgICAgICBjb250ZXh0LnNlc3Npb24ubWFya19iYWQoKVxcbiAgICAgICAgICAgIGVsc2U6XFxuICAgICAgICAgICAgICAgIGNvbnRleHQuc2Vzc2lvbi5tYXJrX2dvb2QoKSAgIyBCYXNpY0NyYXdsZXIgaGFuZGxlcyB0aGlzIGF1dG9tYXRpY2FsbHkuXFxuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9jcmF3bGVlLmRldi8nXSlcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6NDA5NiwidGltZW91dCI6MTgwfX0.36EwhtFhyCwUi4sZzL9EeUxIKUy3TiMcSXTbw2jBr0U\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext
from crawlee.proxy_configuration import ProxyConfiguration
from crawlee.sessions import SessionPool


async def main() -> None:
    # To use the proxy IP session rotation logic, you must turn the proxy usage on.
    proxy_configuration = ProxyConfiguration(
        # options
    )

    # Initialize crawler with a custom SessionPool configuration
    # to manage concurrent sessions and proxy rotation
    crawler = PlaywrightCrawler(
        proxy_configuration=proxy_configuration,
        # Activates the Session pool (default is true).
        use_session_pool=True,
        # Overrides default Session pool configuration.
        session_pool=SessionPool(max_pool_size=100),
    )

    # Define the default request handler that manages session states
    # based on the response content and potential blocking
    @crawler.router.default_handler
    async def default_handler(context: PlaywrightCrawlingContext) -> None:
        title = await context.page.title()

        if context.session:
            if title == 'Blocked':
                context.session.retire()
            elif title == 'Not sure if blocked, might also be a connection error':
                context.session.mark_bad()
            else:
                context.session.mark_good()  # BasicCrawler handles this automatically.

    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLnNlc3Npb25zIGltcG9ydCBTZXNzaW9uUG9vbFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBPdmVycmlkZSB0aGUgZGVmYXVsdCBTZXNzaW9uIHBvb2wgY29uZmlndXJhdGlvbi5cXG4gICAgYXN5bmMgd2l0aCBTZXNzaW9uUG9vbChcXG4gICAgICAgIG1heF9wb29sX3NpemU9MTAwLFxcbiAgICAgICAgY3JlYXRlX3Nlc3Npb25fc2V0dGluZ3M9eydtYXhfdXNhZ2VfY291bnQnOiAxMCwgJ2Jsb2NrZWRfc3RhdHVzX2NvZGVzJzogWzQwM119LFxcbiAgICApIGFzIHNlc3Npb25fcG9vbDpcXG4gICAgICAgIHNlc3Npb24gPSBhd2FpdCBzZXNzaW9uX3Bvb2wuZ2V0X3Nlc3Npb24oKVxcblxcbiAgICAgICAgIyBJbmNyZWFzZSB0aGUgZXJyb3Jfc2NvcmUuXFxuICAgICAgICBzZXNzaW9uLm1hcmtfYmFkKClcXG5cXG4gICAgICAgICMgVGhyb3cgYXdheSB0aGUgc2Vzc2lvbi5cXG4gICAgICAgIHNlc3Npb24ucmV0aXJlKClcXG5cXG4gICAgICAgICMgTG93ZXIgdGhlIGVycm9yX3Njb3JlIGFuZCBtYXJrIHRoZSBzZXNzaW9uIGdvb2QuXFxuICAgICAgICBzZXNzaW9uLm1hcmtfZ29vZCgpXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.teNocQyZeoWnUf3tWn_IZw3RkX-6LapgiVZQjlqWzTc\&asrc=run_on_apify)

```
import asyncio

from crawlee.sessions import SessionPool


async def main() -> None:
    # Override the default Session pool configuration.
    async with SessionPool(
        max_pool_size=100,
        create_session_settings={'max_usage_count': 10, 'blocked_status_codes': [403]},
    ) as session_pool:
        session = await session_pool.get_session()

        # Increase the error_score.
        session.mark_bad()

        # Throw away the session.
        session.retire()

        # Lower the error_score and mark the session good.
        session.mark_good()


if __name__ == '__main__':
    asyncio.run(main())
```

These examples demonstrate the basics of configuring and using the [`SessionPool`](https://crawlee.dev/python/python/api/class/SessionPool.md).

Please, bear in mind that [`SessionPool`](https://crawlee.dev/python/python/api/class/SessionPool.md) requires some time to establish a stable pool of working IPs. During the initial setup, you may encounter errors as the pool identifies and filters out blocked or non-functional IPs. This stabilization period is expected and will improve over time.

## Configuring a single session[​](#configuring-a-single-session "Direct link to Configuring a single session")

In some cases, you need full control over session usage. For example, when working with websites requiring authentication or initialization of certain parameters like cookies.

When working with a site that requires authentication, we typically don't want multiple sessions with different browser fingerprints or client parameters accessing the site. In this case, we need to configure the [`SessionPool`](https://crawlee.dev/python/python/api/class/SessionPool.md) appropriately:

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuZnJvbSBkYXRldGltZSBpbXBvcnQgdGltZWRlbHRhXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBDb25jdXJyZW5jeVNldHRpbmdzLCBSZXF1ZXN0XFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCYXNpY0NyYXdsaW5nQ29udGV4dCwgSHR0cENyYXdsZXIsIEh0dHBDcmF3bGluZ0NvbnRleHRcXG5mcm9tIGNyYXdsZWUuZXJyb3JzIGltcG9ydCBTZXNzaW9uRXJyb3JcXG5mcm9tIGNyYXdsZWUuc2Vzc2lvbnMgaW1wb3J0IFNlc3Npb25Qb29sXFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICBjcmF3bGVyID0gSHR0cENyYXdsZXIoXFxuICAgICAgICAjIExpbWl0IHJlcXVlc3RzIHBlciBtaW51dGUgdG8gcmVkdWNlIHRoZSBjaGFuY2Ugb2YgYmVpbmcgYmxvY2tlZFxcbiAgICAgICAgY29uY3VycmVuY3lfc2V0dGluZ3M9Q29uY3VycmVuY3lTZXR0aW5ncyhtYXhfdGFza3NfcGVyX21pbnV0ZT01MCksXFxuICAgICAgICAjIERpc2FibGUgc2Vzc2lvbiByb3RhdGlvblxcbiAgICAgICAgbWF4X3Nlc3Npb25fcm90YXRpb25zPTAsXFxuICAgICAgICBzZXNzaW9uX3Bvb2w9U2Vzc2lvblBvb2woXFxuICAgICAgICAgICAgIyBPbmx5IG9uZSBzZXNzaW9uIGluIHRoZSBwb29sXFxuICAgICAgICAgICAgbWF4X3Bvb2xfc2l6ZT0xLFxcbiAgICAgICAgICAgIGNyZWF0ZV9zZXNzaW9uX3NldHRpbmdzPXtcXG4gICAgICAgICAgICAgICAgIyBIaWdoIHZhbHVlIGZvciBzZXNzaW9uIHVzYWdlIGxpbWl0XFxuICAgICAgICAgICAgICAgICdtYXhfdXNhZ2VfY291bnQnOiA5OTlfOTk5LFxcbiAgICAgICAgICAgICAgICAjIEhpZ2ggdmFsdWUgZm9yIHNlc3Npb24gbGlmZXRpbWVcXG4gICAgICAgICAgICAgICAgJ21heF9hZ2UnOiB0aW1lZGVsdGEoaG91cnM9OTk5Xzk5OSksXFxuICAgICAgICAgICAgICAgICMgSGlnaCBzY29yZSBhbGxvd3MgdGhlIHNlc3Npb24gdG8gZW5jb3VudGVyIG1vcmUgZXJyb3JzXFxuICAgICAgICAgICAgICAgICMgYmVmb3JlIGNyYXdsZWUgZGVjaWRlcyB0aGUgc2Vzc2lvbiBpcyBibG9ja2VkXFxuICAgICAgICAgICAgICAgICMgTWFrZSBzdXJlIHlvdSBrbm93IGhvdyB0byBoYW5kbGUgdGhlc2UgZXJyb3JzXFxuICAgICAgICAgICAgICAgICdtYXhfZXJyb3Jfc2NvcmUnOiAxMDAsXFxuICAgICAgICAgICAgICAgICMgNDAzIHN0YXR1cyB1c3VhbGx5IGluZGljYXRlcyB5b3UncmUgYWxyZWFkeSBibG9ja2VkXFxuICAgICAgICAgICAgICAgICdibG9ja2VkX3N0YXR1c19jb2Rlcyc6IFs0MDNdLFxcbiAgICAgICAgICAgIH0sXFxuICAgICAgICApLFxcbiAgICApXFxuXFxuICAgICMgQmFzaWMgcmVxdWVzdCBoYW5kbGluZyBsb2dpY1xcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiBiYXNpY19oYW5kbGVyKGNvbnRleHQ6IEh0dHBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0nKVxcblxcbiAgICAjIEhhbmRsZXIgZm9yIHNlc3Npb24gaW5pdGlhbGl6YXRpb24gKGF1dGhlbnRpY2F0aW9uLCBpbml0aWFsIGNvb2tpZXMsIGV0Yy4pXFxuICAgIEBjcmF3bGVyLnJvdXRlci5oYW5kbGVyKGxhYmVsPSdzZXNzaW9uX2luaXQnKVxcbiAgICBhc3luYyBkZWYgc2Vzc2lvbl9pbml0KGNvbnRleHQ6IEh0dHBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBpZiBjb250ZXh0LnNlc3Npb246XFxuICAgICAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ0luaXQgc2Vzc2lvbiB7Y29udGV4dC5zZXNzaW9uLmlkfScpXFxuXFxuICAgICMgTW9uaXRvciBpZiBvdXIgc2Vzc2lvbiBnZXRzIGJsb2NrZWQgYW5kIGV4cGxpY2l0bHkgc3RvcCB0aGUgY3Jhd2xlclxcbiAgICBAY3Jhd2xlci5lcnJvcl9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiBlcnJvcl9wcm9jZXNzaW5nKGNvbnRleHQ6IEJhc2ljQ3Jhd2xpbmdDb250ZXh0LCBlcnJvcjogRXhjZXB0aW9uKSAtPiBOb25lOlxcbiAgICAgICAgaWYgaXNpbnN0YW5jZShlcnJvciwgU2Vzc2lvbkVycm9yKSBhbmQgY29udGV4dC5zZXNzaW9uOlxcbiAgICAgICAgICAgIGNvbnRleHQubG9nLmluZm8oZidTZXNzaW9uIHtjb250ZXh0LnNlc3Npb24uaWR9IGJsb2NrZWQnKVxcbiAgICAgICAgICAgIGNyYXdsZXIuc3RvcCgpXFxuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFtSZXF1ZXN0LmZyb21fdXJsKCdodHRwczovL2V4YW1wbGUub3JnLycsIGxhYmVsPSdzZXNzaW9uX2luaXQnKV0pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.gC0AGsQfyLZKdbOnLfqVrDB7sDNqUUF_v1vyQuX8IQE\&asrc=run_on_apify)

```
import asyncio
from datetime import timedelta

from crawlee import ConcurrencySettings, Request
from crawlee.crawlers import BasicCrawlingContext, HttpCrawler, HttpCrawlingContext
from crawlee.errors import SessionError
from crawlee.sessions import SessionPool


async def main() -> None:
    crawler = HttpCrawler(
        # Limit requests per minute to reduce the chance of being blocked
        concurrency_settings=ConcurrencySettings(max_tasks_per_minute=50),
        # Disable session rotation
        max_session_rotations=0,
        session_pool=SessionPool(
            # Only one session in the pool
            max_pool_size=1,
            create_session_settings={
                # High value for session usage limit
                'max_usage_count': 999_999,
                # High value for session lifetime
                'max_age': timedelta(hours=999_999),
                # High score allows the session to encounter more errors
                # before crawlee decides the session is blocked
                # Make sure you know how to handle these errors
                'max_error_score': 100,
                # 403 status usually indicates you're already blocked
                'blocked_status_codes': [403],
            },
        ),
    )

    # Basic request handling logic
    @crawler.router.default_handler
    async def basic_handler(context: HttpCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url}')

    # Handler for session initialization (authentication, initial cookies, etc.)
    @crawler.router.handler(label='session_init')
    async def session_init(context: HttpCrawlingContext) -> None:
        if context.session:
            context.log.info(f'Init session {context.session.id}')

    # Monitor if our session gets blocked and explicitly stop the crawler
    @crawler.error_handler
    async def error_processing(context: BasicCrawlingContext, error: Exception) -> None:
        if isinstance(error, SessionError) and context.session:
            context.log.info(f'Session {context.session.id} blocked')
            crawler.stop()

    await crawler.run([Request.from_url('https://example.org/', label='session_init')])


if __name__ == '__main__':
    asyncio.run(main())
```

## Binding requests to specific sessions[​](#binding-requests-to-specific-sessions "Direct link to Binding requests to specific sessions")

In the previous example, there's one obvious limitation - you're restricted to only one session.

In some cases, we need to achieve the same behavior but using multiple sessions in parallel, such as authenticating with different profiles or using different proxies.

To do this, use the `session_id` parameter for the [`Request`](https://crawlee.dev/python/python/api/class/Request.md) object to bind a request to a specific session:

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuZnJvbSBjb2xsZWN0aW9ucy5hYmMgaW1wb3J0IENhbGxhYmxlXFxuZnJvbSBkYXRldGltZSBpbXBvcnQgdGltZWRlbHRhXFxuZnJvbSBpdGVydG9vbHMgaW1wb3J0IGNvdW50XFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBDb25jdXJyZW5jeVNldHRpbmdzLCBSZXF1ZXN0XFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCYXNpY0NyYXdsaW5nQ29udGV4dCwgSHR0cENyYXdsZXIsIEh0dHBDcmF3bGluZ0NvbnRleHRcXG5mcm9tIGNyYXdsZWUuZXJyb3JzIGltcG9ydCBSZXF1ZXN0Q29sbGlzaW9uRXJyb3JcXG5mcm9tIGNyYXdsZWUuc2Vzc2lvbnMgaW1wb3J0IFNlc3Npb24sIFNlc3Npb25Qb29sXFxuXFxuXFxuIyBEZWZpbmUgYSBmdW5jdGlvbiBmb3IgY3JlYXRpbmcgc2Vzc2lvbnMgd2l0aCBzaW1wbGUgbG9naWMgZm9yIHVuaXF1ZSBgaWRgIGdlbmVyYXRpb24uXFxuIyBUaGlzIGlzIG5lY2Vzc2FyeSBpZiB5b3UgbmVlZCB0byBzcGVjaWZ5IGEgcGFydGljdWxhciBzZXNzaW9uIGZvciB0aGUgZmlyc3QgcmVxdWVzdCxcXG4jIGZvciBleGFtcGxlIGR1cmluZyBhdXRoZW50aWNhdGlvblxcbmRlZiBjcmVhdGVfc2Vzc2lvbl9mdW5jdGlvbigpIC0-IENhbGxhYmxlW1tdLCBTZXNzaW9uXTpcXG4gICAgY291bnRlciA9IGNvdW50KClcXG5cXG4gICAgZGVmIGNyZWF0ZV9zZXNzaW9uKCkgLT4gU2Vzc2lvbjpcXG4gICAgICAgIHJldHVybiBTZXNzaW9uKFxcbiAgICAgICAgICAgIGlkPXN0cihuZXh0KGNvdW50ZXIpKSxcXG4gICAgICAgICAgICBtYXhfdXNhZ2VfY291bnQ9OTk5Xzk5OSxcXG4gICAgICAgICAgICBtYXhfYWdlPXRpbWVkZWx0YShob3Vycz05OTlfOTk5KSxcXG4gICAgICAgICAgICBtYXhfZXJyb3Jfc2NvcmU9MTAwLFxcbiAgICAgICAgICAgIGJsb2NrZWRfc3RhdHVzX2NvZGVzPVs0MDNdLFxcbiAgICAgICAgKVxcblxcbiAgICByZXR1cm4gY3JlYXRlX3Nlc3Npb25cXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgIGNyYXdsZXIgPSBIdHRwQ3Jhd2xlcihcXG4gICAgICAgICMgQWRqdXN0IHJlcXVlc3QgbGltaXRzIGFjY29yZGluZyB0byB5b3VyIHBvb2wgc2l6ZVxcbiAgICAgICAgY29uY3VycmVuY3lfc2V0dGluZ3M9Q29uY3VycmVuY3lTZXR0aW5ncyhtYXhfdGFza3NfcGVyX21pbnV0ZT01MDApLFxcbiAgICAgICAgIyBSZXF1ZXN0cyBhcmUgYm91bmQgdG8gc3BlY2lmaWMgc2Vzc2lvbnMsIG5vIHJvdGF0aW9uIG5lZWRlZFxcbiAgICAgICAgbWF4X3Nlc3Npb25fcm90YXRpb25zPTAsXFxuICAgICAgICBzZXNzaW9uX3Bvb2w9U2Vzc2lvblBvb2woXFxuICAgICAgICAgICAgbWF4X3Bvb2xfc2l6ZT0xMCwgY3JlYXRlX3Nlc3Npb25fZnVuY3Rpb249Y3JlYXRlX3Nlc3Npb25fZnVuY3Rpb24oKVxcbiAgICAgICAgKSxcXG4gICAgKVxcblxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiBiYXNpY19oYW5kbGVyKGNvbnRleHQ6IEh0dHBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0nKVxcblxcbiAgICAjIEluaXRpYWxpemUgdGhlIHNlc3Npb24gYW5kIGJpbmQgdGhlIG5leHQgcmVxdWVzdCB0byB0aGlzIHNlc3Npb24gaWYgbmVlZGVkXFxuICAgIEBjcmF3bGVyLnJvdXRlci5oYW5kbGVyKGxhYmVsPSdzZXNzaW9uX2luaXQnKVxcbiAgICBhc3luYyBkZWYgc2Vzc2lvbl9pbml0KGNvbnRleHQ6IEh0dHBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBuZXh0X3JlcXVlc3RzID0gW11cXG4gICAgICAgIGlmIGNvbnRleHQuc2Vzc2lvbjpcXG4gICAgICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnSW5pdCBzZXNzaW9uIHtjb250ZXh0LnNlc3Npb24uaWR9JylcXG4gICAgICAgICAgICBuZXh0X3JlcXVlc3QgPSBSZXF1ZXN0LmZyb21fdXJsKFxcbiAgICAgICAgICAgICAgICAnaHR0cHM6Ly9hLnBsYWNlaG9sZGVyLmNvbScsIHNlc3Npb25faWQ9Y29udGV4dC5zZXNzaW9uLmlkXFxuICAgICAgICAgICAgKVxcbiAgICAgICAgICAgIG5leHRfcmVxdWVzdHMuYXBwZW5kKG5leHRfcmVxdWVzdClcXG5cXG4gICAgICAgIGF3YWl0IGNvbnRleHQuYWRkX3JlcXVlc3RzKG5leHRfcmVxdWVzdHMpXFxuXFxuICAgICMgSGFuZGxlIGVycm9ycyB3aGVuIGEgc2Vzc2lvbiBpcyBibG9ja2VkIGFuZCBubyBsb25nZXIgYXZhaWxhYmxlIGluIHRoZSBwb29sXFxuICAgICMgd2hlbiBhdHRlbXB0aW5nIHRvIGV4ZWN1dGUgcmVxdWVzdHMgYm91bmQgdG8gaXRcXG4gICAgQGNyYXdsZXIuZmFpbGVkX3JlcXVlc3RfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgZXJyb3JfcHJvY2Vzc2luZyhjb250ZXh0OiBCYXNpY0NyYXdsaW5nQ29udGV4dCwgZXJyb3I6IEV4Y2VwdGlvbikgLT4gTm9uZTpcXG4gICAgICAgIGlmIGlzaW5zdGFuY2UoZXJyb3IsIFJlcXVlc3RDb2xsaXNpb25FcnJvcikgYW5kIGNvbnRleHQuc2Vzc2lvbjpcXG4gICAgICAgICAgICBjb250ZXh0LmxvZy5lcnJvcihcXG4gICAgICAgICAgICAgICAgZidSZXF1ZXN0IHtjb250ZXh0LnJlcXVlc3QudXJsfSBmYWlsZWQsIGJlY2F1c2UgdGhlIGJvdW5kICdcXG4gICAgICAgICAgICAgICAgJ3Nlc3Npb24gaXMgdW5hdmFpbGFibGUnXFxuICAgICAgICAgICAgKVxcblxcbiAgICAjIENyZWF0ZSBhIHBvb2wgb2YgcmVxdWVzdHMgYm91bmQgdG8gdGhlaXIgcmVzcGVjdGl2ZSBzZXNzaW9uc1xcbiAgICAjIFVzZSBgYWx3YXlzX2VucXVldWU9VHJ1ZWAgaWYgc2Vzc2lvbiBpbml0aWFsaXphdGlvbiBoYXBwZW5zIG9uIGEgbm9uLXVuaXF1ZSBhZGRyZXNzLFxcbiAgICAjIHN1Y2ggYXMgdGhlIHNpdGUncyBtYWluIHBhZ2VcXG4gICAgaW5pdF9yZXF1ZXN0cyA9IFtcXG4gICAgICAgIFJlcXVlc3QuZnJvbV91cmwoXFxuICAgICAgICAgICAgJ2h0dHBzOi8vZXhhbXBsZS5vcmcvJyxcXG4gICAgICAgICAgICBsYWJlbD0nc2Vzc2lvbl9pbml0JyxcXG4gICAgICAgICAgICBzZXNzaW9uX2lkPXN0cihzZXNzaW9uX2lkKSxcXG4gICAgICAgICAgICB1c2VfZXh0ZW5kZWRfdW5pcXVlX2tleT1UcnVlLFxcbiAgICAgICAgKVxcbiAgICAgICAgZm9yIHNlc3Npb25faWQgaW4gcmFuZ2UoMSwgMTEpXFxuICAgIF1cXG5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oaW5pdF9yZXF1ZXN0cylcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6MTAyNCwidGltZW91dCI6MTgwfX0.LSVLvJ-LxpvxWG6kZs5xp-NiMrnrDPi8GEZYBaxybp8\&asrc=run_on_apify)

```
import asyncio
from collections.abc import Callable
from datetime import timedelta
from itertools import count

from crawlee import ConcurrencySettings, Request
from crawlee.crawlers import BasicCrawlingContext, HttpCrawler, HttpCrawlingContext
from crawlee.errors import RequestCollisionError
from crawlee.sessions import Session, SessionPool


# Define a function for creating sessions with simple logic for unique `id` generation.
# This is necessary if you need to specify a particular session for the first request,
# for example during authentication
def create_session_function() -> Callable[[], Session]:
    counter = count()

    def create_session() -> Session:
        return Session(
            id=str(next(counter)),
            max_usage_count=999_999,
            max_age=timedelta(hours=999_999),
            max_error_score=100,
            blocked_status_codes=[403],
        )

    return create_session


async def main() -> None:
    crawler = HttpCrawler(
        # Adjust request limits according to your pool size
        concurrency_settings=ConcurrencySettings(max_tasks_per_minute=500),
        # Requests are bound to specific sessions, no rotation needed
        max_session_rotations=0,
        session_pool=SessionPool(
            max_pool_size=10, create_session_function=create_session_function()
        ),
    )

    @crawler.router.default_handler
    async def basic_handler(context: HttpCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url}')

    # Initialize the session and bind the next request to this session if needed
    @crawler.router.handler(label='session_init')
    async def session_init(context: HttpCrawlingContext) -> None:
        next_requests = []
        if context.session:
            context.log.info(f'Init session {context.session.id}')
            next_request = Request.from_url(
                'https://a.placeholder.com', session_id=context.session.id
            )
            next_requests.append(next_request)

        await context.add_requests(next_requests)

    # Handle errors when a session is blocked and no longer available in the pool
    # when attempting to execute requests bound to it
    @crawler.failed_request_handler
    async def error_processing(context: BasicCrawlingContext, error: Exception) -> None:
        if isinstance(error, RequestCollisionError) and context.session:
            context.log.error(
                f'Request {context.request.url} failed, because the bound '
                'session is unavailable'
            )

    # Create a pool of requests bound to their respective sessions
    # Use `always_enqueue=True` if session initialization happens on a non-unique address,
    # such as the site's main page
    init_requests = [
        Request.from_url(
            'https://example.org/',
            label='session_init',
            session_id=str(session_id),
            use_extended_unique_key=True,
        )
        for session_id in range(1, 11)
    ]

    await crawler.run(init_requests)


if __name__ == '__main__':
    asyncio.run(main())
```

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/guides/session_management.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/guides/service-locator.md)

[Service locator](https://crawlee.dev/python/python/docs/guides/service-locator.md)

[Next](https://crawlee.dev/python/python/docs/guides/storage-clients.md)

[Storage clients](https://crawlee.dev/python/python/docs/guides/storage-clients.md)


---

* [](https://crawlee.dev/python/python)
* [Guides](https://crawlee.dev/python/python/docs/guides.md)
* Storage clients

Version: 1.6

On this page

# Storage clients

Storage clients provide a unified interface for interacting with [`Dataset`](https://crawlee.dev/python/python/api/class/Dataset.md), [`KeyValueStore`](https://crawlee.dev/python/python/api/class/KeyValueStore.md), and [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md), regardless of the underlying implementation. They handle operations like creating, reading, updating, and deleting storage instances, as well as managing data persistence and cleanup. This abstraction makes it easy to switch between different environments, such as local development and cloud production setups.

## Built-in storage clients[​](#built-in-storage-clients "Direct link to Built-in storage clients")

Crawlee provides three main storage client implementations:

* [`FileSystemStorageClient`](https://crawlee.dev/python/python/api/class/FileSystemStorageClient.md) - Provides persistent file system storage with in-memory caching.
* [`MemoryStorageClient`](https://crawlee.dev/python/python/api/class/MemoryStorageClient.md) - Stores data in memory with no persistence.
* [`SqlStorageClient`](https://crawlee.dev/python/python/api/class/SqlStorageClient.md) - Provides persistent storage using a SQL database ([SQLite](https://sqlite.org/), [PostgreSQL](https://www.postgresql.org/), [MySQL](https://www.mysql.com/) or [MariaDB](https://mariadb.org/)). Requires installing the extra dependency: `crawlee[sql_sqlite]` for SQLite, `crawlee[sql_postgres]` for PostgreSQL or `crawlee[sql_mysql]` for MySQL and MariaDB.
* [`RedisStorageClient`](https://crawlee.dev/python/python/api/class/RedisStorageClient.md) - Provides persistent storage using a [Redis](https://redis.io/) database v8.0+. Requires installing the extra dependency `crawlee[redis]`.
* [`ApifyStorageClient`](https://docs.apify.com/sdk/python/reference/class/ApifyStorageClient) - Manages storage on the [Apify platform](https://apify.com), implemented in the [Apify SDK](https://github.com/apify/apify-sdk-python).

<!-- -->

### File system storage client[​](#file-system-storage-client "Direct link to File system storage client")

The [`FileSystemStorageClient`](https://crawlee.dev/python/python/api/class/FileSystemStorageClient.md) provides persistent storage by writing data directly to the file system. It uses intelligent caching and batch processing for better performance while storing data in human-readable JSON format. This is the default storage client used by Crawlee when no other storage client is specified, making it ideal for large datasets and long-running operations where data persistence is required.

Concurrency limitation

The `FileSystemStorageClient` is not safe for concurrent access from multiple crawler processes. Use it only when running a single crawler process at a time.

This storage client is ideal for large datasets, and long-running operations where data persistence is required. Data can be easily inspected and shared with other tools.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImZyb20gY3Jhd2xlZS5jcmF3bGVycyBpbXBvcnQgUGFyc2VsQ3Jhd2xlclxcbmZyb20gY3Jhd2xlZS5zdG9yYWdlX2NsaWVudHMgaW1wb3J0IEZpbGVTeXN0ZW1TdG9yYWdlQ2xpZW50XFxuXFxuIyBDcmVhdGUgYSBuZXcgaW5zdGFuY2Ugb2Ygc3RvcmFnZSBjbGllbnQuXFxuc3RvcmFnZV9jbGllbnQgPSBGaWxlU3lzdGVtU3RvcmFnZUNsaWVudCgpXFxuXFxuIyBBbmQgcGFzcyBpdCB0byB0aGUgY3Jhd2xlci5cXG5jcmF3bGVyID0gUGFyc2VsQ3Jhd2xlcihzdG9yYWdlX2NsaWVudD1zdG9yYWdlX2NsaWVudClcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.A6jUfpsJd7fAsR_-GQzCcHsuq5bkNKXn2FgsU9csrrU\&asrc=run_on_apify)

```
from crawlee.crawlers import ParselCrawler
from crawlee.storage_clients import FileSystemStorageClient

# Create a new instance of storage client.
storage_client = FileSystemStorageClient()

# And pass it to the crawler.
crawler = ParselCrawler(storage_client=storage_client)
```

Configuration options for the [`FileSystemStorageClient`](https://crawlee.dev/python/python/api/class/FileSystemStorageClient.md) can be set through environment variables or the [`Configuration`](https://crawlee.dev/python/python/api/class/Configuration.md) class:

* **`storage_dir`** (env: `CRAWLEE_STORAGE_DIR`, default: `'./storage'`) - The root directory for all storage data.
* **`purge_on_start`** (env: `CRAWLEE_PURGE_ON_START`, default: `True`) - Whether to purge default storages on start.

Data is stored using the following directory structure:

```
{CRAWLEE_STORAGE_DIR}/
├── datasets/
│   └── {DATASET_NAME}/
│       ├── __metadata__.json
│       ├── 000000001.json
│       └── 000000002.json
├── key_value_stores/
│   └── {KVS_NAME}/
│       ├── __metadata__.json
│       ├── key1.json
│       ├── key2.txt
│       └── key3.json
└── request_queues/
    └── {RQ_NAME}/
        ├── __metadata__.json
        ├── {REQUEST_ID_1}.json
        └── {REQUEST_ID_2}.json
```

Where:

* `{CRAWLEE_STORAGE_DIR}` - The root directory for local storage.
* `{DATASET_NAME}`, `{KVS_NAME}`, `{RQ_NAME}` - The unique names for each storage instance (defaults to `"default"`).
* Files are stored directly without additional metadata files for simpler structure.

Here is an example of how to configure the [`FileSystemStorageClient`](https://crawlee.dev/python/python/api/class/FileSystemStorageClient.md):

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImZyb20gY3Jhd2xlZS5jb25maWd1cmF0aW9uIGltcG9ydCBDb25maWd1cmF0aW9uXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQYXJzZWxDcmF3bGVyXFxuZnJvbSBjcmF3bGVlLnN0b3JhZ2VfY2xpZW50cyBpbXBvcnQgRmlsZVN5c3RlbVN0b3JhZ2VDbGllbnRcXG5cXG4jIENyZWF0ZSBhIG5ldyBpbnN0YW5jZSBvZiBzdG9yYWdlIGNsaWVudC5cXG5zdG9yYWdlX2NsaWVudCA9IEZpbGVTeXN0ZW1TdG9yYWdlQ2xpZW50KClcXG5cXG4jIENyZWF0ZSBhIGNvbmZpZ3VyYXRpb24gd2l0aCBjdXN0b20gc2V0dGluZ3MuXFxuY29uZmlndXJhdGlvbiA9IENvbmZpZ3VyYXRpb24oXFxuICAgIHN0b3JhZ2VfZGlyPScuL215X3N0b3JhZ2UnLFxcbiAgICBwdXJnZV9vbl9zdGFydD1GYWxzZSxcXG4pXFxuXFxuIyBBbmQgcGFzcyB0aGVtIHRvIHRoZSBjcmF3bGVyLlxcbmNyYXdsZXIgPSBQYXJzZWxDcmF3bGVyKFxcbiAgICBzdG9yYWdlX2NsaWVudD1zdG9yYWdlX2NsaWVudCxcXG4gICAgY29uZmlndXJhdGlvbj1jb25maWd1cmF0aW9uLFxcbilcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.V9QELSLNsXePzE5bTYIMipHKsu6ey0nVdCIh5SeQ6Qg\&asrc=run_on_apify)

```
from crawlee.configuration import Configuration
from crawlee.crawlers import ParselCrawler
from crawlee.storage_clients import FileSystemStorageClient

# Create a new instance of storage client.
storage_client = FileSystemStorageClient()

# Create a configuration with custom settings.
configuration = Configuration(
    storage_dir='./my_storage',
    purge_on_start=False,
)

# And pass them to the crawler.
crawler = ParselCrawler(
    storage_client=storage_client,
    configuration=configuration,
)
```

### Memory storage client[​](#memory-storage-client "Direct link to Memory storage client")

The [`MemoryStorageClient`](https://crawlee.dev/python/python/api/class/MemoryStorageClient.md) stores all data in memory using Python data structures. It provides fast access but does not persist data between runs, meaning all data is lost when the program terminates. This storage client is primarily suitable for testing and development, and is usually not a good fit for production use. However, in some cases where speed is prioritized over persistence, it can make sense.

Persistence limitation

The `MemoryStorageClient` does not persist data between runs. All data is lost when the program terminates.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImZyb20gY3Jhd2xlZS5jcmF3bGVycyBpbXBvcnQgUGFyc2VsQ3Jhd2xlclxcbmZyb20gY3Jhd2xlZS5zdG9yYWdlX2NsaWVudHMgaW1wb3J0IE1lbW9yeVN0b3JhZ2VDbGllbnRcXG5cXG4jIENyZWF0ZSBhIG5ldyBpbnN0YW5jZSBvZiBzdG9yYWdlIGNsaWVudC5cXG5zdG9yYWdlX2NsaWVudCA9IE1lbW9yeVN0b3JhZ2VDbGllbnQoKVxcblxcbiMgQW5kIHBhc3MgaXQgdG8gdGhlIGNyYXdsZXIuXFxuY3Jhd2xlciA9IFBhcnNlbENyYXdsZXIoc3RvcmFnZV9jbGllbnQ9c3RvcmFnZV9jbGllbnQpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6MTAyNCwidGltZW91dCI6MTgwfX0.7Wo3I1oU15GgT9vrwyn9GQ-SaH4ffYU2GjCi9y3Wn6I\&asrc=run_on_apify)

```
from crawlee.crawlers import ParselCrawler
from crawlee.storage_clients import MemoryStorageClient

# Create a new instance of storage client.
storage_client = MemoryStorageClient()

# And pass it to the crawler.
crawler = ParselCrawler(storage_client=storage_client)
```

### SQL storage client[​](#sql-storage-client "Direct link to SQL storage client")

Experimental feature

The `SqlStorageClient` is experimental. Its API and behavior may change in future releases.

The [`SqlStorageClient`](https://crawlee.dev/python/python/api/class/SqlStorageClient.md) provides persistent storage using a SQL database (SQLite by default, or PostgreSQL, MySQL, MariaDB). It supports all Crawlee storage types and enables concurrent access from multiple independent clients or processes.

dependencies

The [`SqlStorageClient`](https://crawlee.dev/python/python/api/class/SqlStorageClient.md) is not included in the core Crawlee package. To use it, you need to install Crawlee with the appropriate extra dependency:

* For SQLite support, run: `pip install 'crawlee[sql_sqlite]'`
* For PostgreSQL support, run: `pip install 'crawlee[sql_postgres]'`
* For MySQL or MariaDB support, run: `pip install 'crawlee[sql_mysql]'`

By default, [SqlStorageClient](https://crawlee.dev/python/python/api/class/SqlStorageClient.md) uses SQLite. To use a different database, just provide the appropriate connection string via the `connection_string` parameter. No other code changes are needed—the same client works for all supported databases.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImZyb20gY3Jhd2xlZS5jcmF3bGVycyBpbXBvcnQgUGFyc2VsQ3Jhd2xlclxcbmZyb20gY3Jhd2xlZS5zdG9yYWdlX2NsaWVudHMgaW1wb3J0IFNxbFN0b3JhZ2VDbGllbnRcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgICMgQ3JlYXRlIGEgbmV3IGluc3RhbmNlIG9mIHN0b3JhZ2UgY2xpZW50LlxcbiAgICAjIFRoaXMgd2lsbCBjcmVhdGUgYW4gU1FMaXRlIGRhdGFiYXNlIGZpbGUgY3Jhd2xlZS5kYiBvciBjcmVhdGVkIHRhYmxlcyBpbiB5b3VyXFxuICAgICMgZGF0YWJhc2UgaWYgeW91IHBhc3MgYGNvbm5lY3Rpb25fc3RyaW5nYCBvciBgZW5naW5lYFxcbiAgICAjIFVzZSB0aGUgY29udGV4dCBtYW5hZ2VyIHRvIGVuc3VyZSB0aGF0IGNvbm5lY3Rpb25zIGFyZSBwcm9wZXJseSBjbGVhbmVkIHVwLlxcbiAgICBhc3luYyB3aXRoIFNxbFN0b3JhZ2VDbGllbnQoKSBhcyBzdG9yYWdlX2NsaWVudDpcXG4gICAgICAgICMgQW5kIHBhc3MgaXQgdG8gdGhlIGNyYXdsZXIuXFxuICAgICAgICBjcmF3bGVyID0gUGFyc2VsQ3Jhd2xlcihzdG9yYWdlX2NsaWVudD1zdG9yYWdlX2NsaWVudClcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.u1p8mTo1_lRLuYFnggEG4GtXE-nE7ZYHzfwnpKtaXSg\&asrc=run_on_apify)

```
from crawlee.crawlers import ParselCrawler
from crawlee.storage_clients import SqlStorageClient


async def main() -> None:
    # Create a new instance of storage client.
    # This will create an SQLite database file crawlee.db or created tables in your
    # database if you pass `connection_string` or `engine`
    # Use the context manager to ensure that connections are properly cleaned up.
    async with SqlStorageClient() as storage_client:
        # And pass it to the crawler.
        crawler = ParselCrawler(storage_client=storage_client)
```

Data is organized in relational tables. Below are the main tables and columns used for each storage type:

<!-- -->

<!-- -->

Configuration options for the [`SqlStorageClient`](https://crawlee.dev/python/python/api/class/SqlStorageClient.md) can be set through environment variables or the [`Configuration`](https://crawlee.dev/python/python/api/class/Configuration.md) class:

* **`storage_dir`** (env: `CRAWLEE_STORAGE_DIR`, default: `'./storage'`) - The root directory where the default SQLite database will be created if no connection string is provided.
* **`purge_on_start`** (env: `CRAWLEE_PURGE_ON_START`, default: `True`) - Whether to purge default storages on start.

Configuration options for the [`SqlStorageClient`](https://crawlee.dev/python/python/api/class/SqlStorageClient.md) can be set via constructor arguments:

* **`connection_string`** (default: SQLite in [`Configuration`](https://crawlee.dev/python/python/api/class/Configuration.md) storage dir) - SQLAlchemy connection string, e.g. `sqlite+aiosqlite:///my.db`, `postgresql+asyncpg://user:pass@host/db`, `mysql+aiomysql://user:pass@host/db` or `mariadb+aiomysql://user:pass@host/db`.
* **`engine`** - Pre-configured SQLAlchemy AsyncEngine (optional).

For advanced scenarios, you can configure [`SqlStorageClient`](https://crawlee.dev/python/python/api/class/SqlStorageClient.md) with a custom SQLAlchemy engine and additional options via the [`Configuration`](https://crawlee.dev/python/python/api/class/Configuration.md) class. This is useful, for example, when connecting to an external PostgreSQL database or customizing connection pooling.

warning

If you use MySQL or MariaDB, pass the `isolation_level='READ COMMITTED'` argument to `create_async_engine`. MySQL/MariaDB default to the `REPEATABLE READ` isolation level, which can cause unnecessary locking, deadlocks, or stale reads when multiple Crawlee workers access the same tables concurrently. Using `READ COMMITTED` ensures more predictable row-level locking and visibility semantics for `SqlStorageClient`.

```
from sqlalchemy.ext.asyncio import create_async_engine

from crawlee.configuration import Configuration
from crawlee.crawlers import ParselCrawler
from crawlee.storage_clients import SqlStorageClient


async def main() -> None:
    # Create a new instance of storage client.
    # On first run, also creates tables in your PostgreSQL database.
    # Use the context manager to ensure that connections are properly cleaned up.
    async with SqlStorageClient(
        # Create an `engine` with the desired configuration
        engine=create_async_engine(
            'postgresql+asyncpg://myuser:mypassword@localhost:5432/postgres',
            future=True,
            pool_size=5,
            max_overflow=10,
            pool_recycle=3600,
            pool_pre_ping=True,
            echo=False,
        )
    ) as storage_client:
        # Create a configuration with custom settings.
        configuration = Configuration(
            purge_on_start=False,
        )

        # And pass them to the crawler.
        crawler = ParselCrawler(
            storage_client=storage_client,
            configuration=configuration,
        )
```

### Redis storage client[​](#redis-storage-client "Direct link to Redis storage client")

Experimental feature

The [`RedisStorageClient`](https://crawlee.dev/python/python/api/class/RedisStorageClient.md) is experimental. Its API and behavior may change in future releases.

The [`RedisStorageClient`](https://crawlee.dev/python/python/api/class/RedisStorageClient.md) provides persistent storage using [Redis](https://redis.io/) database. It supports concurrent access from multiple independent clients or processes and uses Redis native data structures for efficient operations.

dependencies

The [`RedisStorageClient`](https://crawlee.dev/python/python/api/class/RedisStorageClient.md) is not included in the core Crawlee package. To use it, you need to install Crawlee with the Redis extra dependency:

`pip install 'crawlee[redis]'`

Additionally, Redis version 8.0 or higher is required.

Redis persistence

Data persistence in Redis depends on your [database configuration](https://redis.io/docs/latest/operate/oss_and_stack/management/persistence/).

The client requires either a Redis connection string or a pre-configured Redis client instance. Use a pre-configured client when you need custom Redis settings such as connection pooling, timeouts, or SSL/TLS encryption.

```
from crawlee.crawlers import ParselCrawler
from crawlee.storage_clients import RedisStorageClient

# Create a new instance of storage client using connection string.
# 'redis://localhost:6379' is the just placeholder, replace it with your actual
# connection string.
storage_client = RedisStorageClient(connection_string='redis://localhost:6379')

# And pass it to the crawler.
crawler = ParselCrawler(storage_client=storage_client)
```

Data is organized using Redis key patterns. Below are the main data structures used for each storage type:

<!-- -->

<!-- -->

<!-- -->

Configuration options for the [`RedisStorageClient`](https://crawlee.dev/python/python/api/class/RedisStorageClient.md) can be set through environment variables or the [`Configuration`](https://crawlee.dev/python/python/api/class/Configuration.md) class:

* **`purge_on_start`** (env: `CRAWLEE_PURGE_ON_START`, default: `True`) - Whether to purge default storages on start.

Configuration options for the [`RedisStorageClient`](https://crawlee.dev/python/python/api/class/RedisStorageClient.md) can be set via constructor arguments:

* **`connection_string`** - Redis connection string, e.g. `redis://localhost:6379/0`.
* **`redis`** - Pre-configured Redis client instance (optional).

```
from redis.asyncio import Redis

from crawlee.configuration import Configuration
from crawlee.crawlers import ParselCrawler
from crawlee.storage_clients import RedisStorageClient

# Create a new instance of storage client using a Redis client with custom settings.
# Replace host and port with your actual Redis server configuration.
# Other Redis client settings can be adjusted as needed.
storage_client = RedisStorageClient(
    redis=Redis(
        host='localhost',
        port=6379,
        retry_on_timeout=True,
        socket_keepalive=True,
        socket_connect_timeout=10,
    )
)

# Create a configuration with custom settings.
configuration = Configuration(purge_on_start=False)

# And pass them to the crawler.
crawler = ParselCrawler(
    storage_client=storage_client,
    configuration=configuration,
)
```

## Creating a custom storage client[​](#creating-a-custom-storage-client "Direct link to Creating a custom storage client")

A storage client consists of two parts: the storage client factory and individual storage type clients. The [`StorageClient`](https://crawlee.dev/python/python/api/class/StorageClient.md) acts as a factory that creates specific clients ([`DatasetClient`](https://crawlee.dev/python/python/api/class/DatasetClient.md), [`KeyValueStoreClient`](https://crawlee.dev/python/python/api/class/KeyValueStoreClient.md), [`RequestQueueClient`](https://crawlee.dev/python/python/api/class/RequestQueueClient.md)) where the actual storage logic is implemented.

Here is an example of a custom storage client that implements the [`StorageClient`](https://crawlee.dev/python/python/api/class/StorageClient.md) interface:

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImZyb20gX19mdXR1cmVfXyBpbXBvcnQgYW5ub3RhdGlvbnNcXG5cXG5mcm9tIHR5cGluZyBpbXBvcnQgVFlQRV9DSEVDS0lOR1xcblxcbmZyb20gY3Jhd2xlZS5zdG9yYWdlX2NsaWVudHMgaW1wb3J0IFN0b3JhZ2VDbGllbnRcXG5mcm9tIGNyYXdsZWUuc3RvcmFnZV9jbGllbnRzLl9iYXNlIGltcG9ydCAoXFxuICAgIERhdGFzZXRDbGllbnQsXFxuICAgIEtleVZhbHVlU3RvcmVDbGllbnQsXFxuICAgIFJlcXVlc3RRdWV1ZUNsaWVudCxcXG4pXFxuXFxuaWYgVFlQRV9DSEVDS0lORzpcXG4gICAgZnJvbSBjcmF3bGVlLmNvbmZpZ3VyYXRpb24gaW1wb3J0IENvbmZpZ3VyYXRpb25cXG5cXG4jIEltcGxlbWVudCB0aGUgc3RvcmFnZSB0eXBlIGNsaWVudHMgd2l0aCB5b3VyIGJhY2tlbmQgbG9naWMuXFxuXFxuXFxuY2xhc3MgQ3VzdG9tRGF0YXNldENsaWVudChEYXRhc2V0Q2xpZW50KTpcXG4gICAgIyBJbXBsZW1lbnQgbWV0aG9kcyBsaWtlIHB1c2hfZGF0YSwgZ2V0X2RhdGEsIGl0ZXJhdGVfaXRlbXMsIGV0Yy5cXG4gICAgcGFzc1xcblxcblxcbmNsYXNzIEN1c3RvbUtleVZhbHVlU3RvcmVDbGllbnQoS2V5VmFsdWVTdG9yZUNsaWVudCk6XFxuICAgICMgSW1wbGVtZW50IG1ldGhvZHMgbGlrZSBnZXRfdmFsdWUsIHNldF92YWx1ZSwgZGVsZXRlLCBldGMuXFxuICAgIHBhc3NcXG5cXG5cXG5jbGFzcyBDdXN0b21SZXF1ZXN0UXVldWVDbGllbnQoUmVxdWVzdFF1ZXVlQ2xpZW50KTpcXG4gICAgIyBJbXBsZW1lbnQgbWV0aG9kcyBsaWtlIGFkZF9yZXF1ZXN0LCBmZXRjaF9uZXh0X3JlcXVlc3QsIGV0Yy5cXG4gICAgcGFzc1xcblxcblxcbiMgSW1wbGVtZW50IHRoZSBzdG9yYWdlIGNsaWVudCBmYWN0b3J5LlxcblxcblxcbmNsYXNzIEN1c3RvbVN0b3JhZ2VDbGllbnQoU3RvcmFnZUNsaWVudCk6XFxuICAgIGFzeW5jIGRlZiBjcmVhdGVfZGF0YXNldF9jbGllbnQoXFxuICAgICAgICBzZWxmLFxcbiAgICAgICAgKixcXG4gICAgICAgIGlkOiBzdHIgfCBOb25lID0gTm9uZSxcXG4gICAgICAgIG5hbWU6IHN0ciB8IE5vbmUgPSBOb25lLFxcbiAgICAgICAgY29uZmlndXJhdGlvbjogQ29uZmlndXJhdGlvbiB8IE5vbmUgPSBOb25lLFxcbiAgICApIC0-IEN1c3RvbURhdGFzZXRDbGllbnQ6XFxuICAgICAgICAjIENyZWF0ZSBhbmQgcmV0dXJuIHlvdXIgY3VzdG9tIGRhdGFzZXQgY2xpZW50LlxcbiAgICAgICAgcGFzc1xcblxcbiAgICBhc3luYyBkZWYgY3JlYXRlX2t2c19jbGllbnQoXFxuICAgICAgICBzZWxmLFxcbiAgICAgICAgKixcXG4gICAgICAgIGlkOiBzdHIgfCBOb25lID0gTm9uZSxcXG4gICAgICAgIG5hbWU6IHN0ciB8IE5vbmUgPSBOb25lLFxcbiAgICAgICAgY29uZmlndXJhdGlvbjogQ29uZmlndXJhdGlvbiB8IE5vbmUgPSBOb25lLFxcbiAgICApIC0-IEN1c3RvbUtleVZhbHVlU3RvcmVDbGllbnQ6XFxuICAgICAgICAjIENyZWF0ZSBhbmQgcmV0dXJuIHlvdXIgY3VzdG9tIGtleS12YWx1ZSBzdG9yZSBjbGllbnQuXFxuICAgICAgICBwYXNzXFxuXFxuICAgIGFzeW5jIGRlZiBjcmVhdGVfcnFfY2xpZW50KFxcbiAgICAgICAgc2VsZixcXG4gICAgICAgICosXFxuICAgICAgICBpZDogc3RyIHwgTm9uZSA9IE5vbmUsXFxuICAgICAgICBuYW1lOiBzdHIgfCBOb25lID0gTm9uZSxcXG4gICAgICAgIGNvbmZpZ3VyYXRpb246IENvbmZpZ3VyYXRpb24gfCBOb25lID0gTm9uZSxcXG4gICAgKSAtPiBDdXN0b21SZXF1ZXN0UXVldWVDbGllbnQ6XFxuICAgICAgICAjIENyZWF0ZSBhbmQgcmV0dXJuIHlvdXIgY3VzdG9tIHJlcXVlc3QgcXVldWUgY2xpZW50LlxcbiAgICAgICAgcGFzc1xcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.394LP8AntytX9_qXXXVrL7D1DUw8ctqJX7pcHSAfsAM\&asrc=run_on_apify)

```
from __future__ import annotations

from typing import TYPE_CHECKING

from crawlee.storage_clients import StorageClient
from crawlee.storage_clients._base import (
    DatasetClient,
    KeyValueStoreClient,
    RequestQueueClient,
)

if TYPE_CHECKING:
    from crawlee.configuration import Configuration

# Implement the storage type clients with your backend logic.


class CustomDatasetClient(DatasetClient):
    # Implement methods like push_data, get_data, iterate_items, etc.
    pass


class CustomKeyValueStoreClient(KeyValueStoreClient):
    # Implement methods like get_value, set_value, delete, etc.
    pass


class CustomRequestQueueClient(RequestQueueClient):
    # Implement methods like add_request, fetch_next_request, etc.
    pass


# Implement the storage client factory.


class CustomStorageClient(StorageClient):
    async def create_dataset_client(
        self,
        *,
        id: str | None = None,
        name: str | None = None,
        configuration: Configuration | None = None,
    ) -> CustomDatasetClient:
        # Create and return your custom dataset client.
        pass

    async def create_kvs_client(
        self,
        *,
        id: str | None = None,
        name: str | None = None,
        configuration: Configuration | None = None,
    ) -> CustomKeyValueStoreClient:
        # Create and return your custom key-value store client.
        pass

    async def create_rq_client(
        self,
        *,
        id: str | None = None,
        name: str | None = None,
        configuration: Configuration | None = None,
    ) -> CustomRequestQueueClient:
        # Create and return your custom request queue client.
        pass
```

Custom storage clients can implement any storage logic, such as connecting to a database, using a cloud storage service, or integrating with other systems. They must implement the required methods for creating, reading, updating, and deleting data in the respective storages.

## Registering storage clients[​](#registering-storage-clients "Direct link to Registering storage clients")

Storage clients can be registered in multiple ways:

* **Globally** - Using the [`ServiceLocator`](https://crawlee.dev/python/python/api/class/ServiceLocator.md) or passing directly to the crawler.
* **Per storage** - When opening a specific storage instance like [`Dataset`](https://crawlee.dev/python/python/api/class/Dataset.md), [`KeyValueStore`](https://crawlee.dev/python/python/api/class/KeyValueStore.md), or [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md).

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBzZXJ2aWNlX2xvY2F0b3JcXG5mcm9tIGNyYXdsZWUuY3Jhd2xlcnMgaW1wb3J0IFBhcnNlbENyYXdsZXJcXG5mcm9tIGNyYXdsZWUuc3RvcmFnZV9jbGllbnRzIGltcG9ydCBNZW1vcnlTdG9yYWdlQ2xpZW50XFxuZnJvbSBjcmF3bGVlLnN0b3JhZ2VzIGltcG9ydCBEYXRhc2V0XFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICAjIENyZWF0ZSBjdXN0b20gc3RvcmFnZSBjbGllbnQsIE1lbW9yeVN0b3JhZ2VDbGllbnQgZm9yIGV4YW1wbGUuXFxuICAgIHN0b3JhZ2VfY2xpZW50ID0gTWVtb3J5U3RvcmFnZUNsaWVudCgpXFxuXFxuICAgICMgUmVnaXN0ZXIgaXQgZ2xvYmFsbHkgdmlhIHRoZSBzZXJ2aWNlIGxvY2F0b3IuXFxuICAgIHNlcnZpY2VfbG9jYXRvci5zZXRfc3RvcmFnZV9jbGllbnQoc3RvcmFnZV9jbGllbnQpXFxuXFxuICAgICMgT3IgcGFzcyBpdCBkaXJlY3RseSB0byB0aGUgY3Jhd2xlciwgaXQgd2lsbCBiZSByZWdpc3RlcmVkIGdsb2JhbGx5XFxuICAgICMgdG8gdGhlIHNlcnZpY2UgbG9jYXRvciB1bmRlciB0aGUgaG9vZC5cXG4gICAgY3Jhd2xlciA9IFBhcnNlbENyYXdsZXIoc3RvcmFnZV9jbGllbnQ9c3RvcmFnZV9jbGllbnQpXFxuXFxuICAgICMgT3IganVzdCBwcm92aWRlIGl0IHdoZW4gb3BlbmluZyBhIHN0b3JhZ2UgKGUuZy4gZGF0YXNldCksIGl0IHdpbGwgYmUgdXNlZFxcbiAgICAjIGZvciB0aGlzIHN0b3JhZ2Ugb25seSwgbm90IGdsb2JhbGx5LlxcbiAgICBkYXRhc2V0ID0gYXdhaXQgRGF0YXNldC5vcGVuKFxcbiAgICAgICAgbmFtZT0nbXktZGF0YXNldCcsXFxuICAgICAgICBzdG9yYWdlX2NsaWVudD1zdG9yYWdlX2NsaWVudCxcXG4gICAgKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.NxF2PX-vHKXVi4QdJhZ5JViDuNPzb9xXftmkLVZb90Y\&asrc=run_on_apify)

```
import asyncio

from crawlee import service_locator
from crawlee.crawlers import ParselCrawler
from crawlee.storage_clients import MemoryStorageClient
from crawlee.storages import Dataset


async def main() -> None:
    # Create custom storage client, MemoryStorageClient for example.
    storage_client = MemoryStorageClient()

    # Register it globally via the service locator.
    service_locator.set_storage_client(storage_client)

    # Or pass it directly to the crawler, it will be registered globally
    # to the service locator under the hood.
    crawler = ParselCrawler(storage_client=storage_client)

    # Or just provide it when opening a storage (e.g. dataset), it will be used
    # for this storage only, not globally.
    dataset = await Dataset.open(
        name='my-dataset',
        storage_client=storage_client,
    )


if __name__ == '__main__':
    asyncio.run(main())
```

You can also register different storage clients for each storage instance, allowing you to use different backends for different storages. This is useful when you want to use a fast in-memory storage for [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md) while persisting scraping results in [`Dataset`](https://crawlee.dev/python/python/api/class/Dataset.md) or [`KeyValueStore`](https://crawlee.dev/python/python/api/class/KeyValueStore.md).

## Conclusion[​](#conclusion "Direct link to Conclusion")

Storage clients in Crawlee provide different backends for data storage. Use [`MemoryStorageClient`](https://crawlee.dev/python/python/api/class/MemoryStorageClient.md) for testing and fast operations without persistence, or [`FileSystemStorageClient`](https://crawlee.dev/python/python/api/class/FileSystemStorageClient.md) for environments where data needs to persist. You can also create custom storage clients for specialized backends by implementing the [`StorageClient`](https://crawlee.dev/python/python/api/class/StorageClient.md) interface.

If you have questions or need assistance, feel free to reach out on our [GitHub](https://github.com/apify/crawlee-python) or join our [Discord community](https://discord.com/invite/jyEM2PRvMU). Happy scraping!

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/guides/storage_clients.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/guides/session-management.md)

[Session management](https://crawlee.dev/python/python/docs/guides/session-management.md)

[Next](https://crawlee.dev/python/python/docs/guides/storages.md)

[Storages](https://crawlee.dev/python/python/docs/guides/storages.md)


---

* [](https://crawlee.dev/python/python)
* [Guides](https://crawlee.dev/python/python/docs/guides.md)
* Storages

Version: 1.6

On this page

# Storages

Crawlee offers several storage types for managing and persisting your crawling data. Request-oriented storages, such as the [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md), help you store and deduplicate URLs, while result-oriented storages, like [`Dataset`](https://crawlee.dev/python/python/api/class/Dataset.md) and [`KeyValueStore`](https://crawlee.dev/python/python/api/class/KeyValueStore.md), focus on storing and retrieving scraping results. This guide explains when to use each type, how to interact with them, and how to control their lifecycle.

## Overview[​](#overview "Direct link to Overview")

Crawlee's storage system consists of two main layers:

* **Storages** ([`Dataset`](https://crawlee.dev/python/python/api/class/Dataset.md), [`KeyValueStore`](https://crawlee.dev/python/python/api/class/KeyValueStore.md), [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md)): High-level interfaces for interacting with different storage types.
* **Storage clients** ([`MemoryStorageClient`](https://crawlee.dev/python/python/api/class/MemoryStorageClient.md), [`FileSystemStorageClient`](https://crawlee.dev/python/python/api/class/FileSystemStorageClient.md), etc.): Backend implementations that handle the actual data persistence and management.

For more information about storage clients and their configuration, see the [Storage clients guide](https://crawlee.dev/python/python/docs/guides/storage-clients.md).

<!-- -->

### Named and unnamed storages[​](#named-and-unnamed-storages "Direct link to Named and unnamed storages")

Crawlee supports two types of storages:

* **Named storages**: Persistent storages with a specific name that persist across runs. These are useful when you want to share data between different crawler runs or access the same storage from multiple places.
* **Unnamed storages**: Temporary storages identified by an alias that are scoped to a single run. These are automatically purged at the start of each run (when `purge_on_start` is enabled, which is the default).

### Default storage[​](#default-storage "Direct link to Default storage")

Each storage type ([`Dataset`](https://crawlee.dev/python/python/api/class/Dataset.md), [`KeyValueStore`](https://crawlee.dev/python/python/api/class/KeyValueStore.md), [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md)) has a default instance that can be accessed without specifying `id`, `name` or `alias`. Default unnamed storage is accessed by calling storage's `open` method without parameters. This is the most common way to use storages in simple crawlers.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLnN0b3JhZ2VzIGltcG9ydCBEYXRhc2V0XFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICAjIE5hbWVkIHN0b3JhZ2UgKHBlcnNpc3RzIGFjcm9zcyBydW5zKVxcbiAgICBkYXRhc2V0X25hbWVkID0gYXdhaXQgRGF0YXNldC5vcGVuKG5hbWU9J215LXBlcnNpc3RlbnQtZGF0YXNldCcpXFxuXFxuICAgICMgVW5uYW1lZCBzdG9yYWdlIHdpdGggYWxpYXMgKHB1cmdlZCBvbiBzdGFydClcXG4gICAgZGF0YXNldF91bm5hbWVkID0gYXdhaXQgRGF0YXNldC5vcGVuKGFsaWFzPSd0ZW1wb3JhcnktcmVzdWx0cycpXFxuXFxuICAgICMgRGVmYXVsdCB1bm5hbWVkIHN0b3JhZ2UgKHB1cmdlZCBvbiBzdGFydClcXG4gICAgZGF0YXNldF9kZWZhdWx0ID0gYXdhaXQgRGF0YXNldC5vcGVuKClcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6MTAyNCwidGltZW91dCI6MTgwfX0.aJboc5TyBtCswQIcj9ucP-FjYMz-cEtEEVYhi1A-UGk\&asrc=run_on_apify)

```
import asyncio

from crawlee.storages import Dataset


async def main() -> None:
    # Named storage (persists across runs)
    dataset_named = await Dataset.open(name='my-persistent-dataset')

    # Unnamed storage with alias (purged on start)
    dataset_unnamed = await Dataset.open(alias='temporary-results')

    # Default unnamed storage (purged on start)
    dataset_default = await Dataset.open()


if __name__ == '__main__':
    asyncio.run(main())
```

## Request queue[​](#request-queue "Direct link to Request queue")

The [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md) is the primary storage for URLs in Crawlee, especially useful for deep crawling. It supports dynamic addition of URLs, making it ideal for recursive tasks where URLs are discovered and added during the crawling process (e.g., following links across multiple pages). Each Crawlee project has a **default request queue**, which can be used to store URLs during a specific run.

The following code demonstrates the usage of the [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md):

* Basic usage
* Usage with Crawler
* Explicit usage with Crawler

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLnN0b3JhZ2VzIGltcG9ydCBSZXF1ZXN0UXVldWVcXG5cXG5cXG5hc3luYyBkZWYgbWFpbigpIC0-IE5vbmU6XFxuICAgICMgT3BlbiB0aGUgcmVxdWVzdCBxdWV1ZSwgaWYgaXQgZG9lcyBub3QgZXhpc3QsIGl0IHdpbGwgYmUgY3JlYXRlZC5cXG4gICAgIyBMZWF2ZSBuYW1lIGVtcHR5IHRvIHVzZSB0aGUgZGVmYXVsdCByZXF1ZXN0IHF1ZXVlLlxcbiAgICByZXF1ZXN0X3F1ZXVlID0gYXdhaXQgUmVxdWVzdFF1ZXVlLm9wZW4obmFtZT0nbXktcmVxdWVzdC1xdWV1ZScpXFxuXFxuICAgICMgQWRkIGEgc2luZ2xlIHJlcXVlc3QuXFxuICAgIGF3YWl0IHJlcXVlc3RfcXVldWUuYWRkX3JlcXVlc3QoJ2h0dHBzOi8vYXBpZnkuY29tLycpXFxuXFxuICAgICMgQWRkIG11bHRpcGxlIHJlcXVlc3RzIGFzIGEgYmF0Y2guXFxuICAgIGF3YWl0IHJlcXVlc3RfcXVldWUuYWRkX3JlcXVlc3RzKFxcbiAgICAgICAgWydodHRwczovL2NyYXdsZWUuZGV2LycsICdodHRwczovL2NyYXdsZWUuZGV2L3B5dGhvbi8nXVxcbiAgICApXFxuXFxuICAgICMgRmV0Y2ggYW5kIHByb2Nlc3MgcmVxdWVzdHMgZnJvbSB0aGUgcXVldWUuXFxuICAgIHdoaWxlIHJlcXVlc3QgOj0gYXdhaXQgcmVxdWVzdF9xdWV1ZS5mZXRjaF9uZXh0X3JlcXVlc3QoKTpcXG4gICAgICAgICMgRG8gc29tZXRoaW5nIHdpdGggaXQuLi5cXG5cXG4gICAgICAgICMgQW5kIG1hcmsgaXQgYXMgaGFuZGxlZC5cXG4gICAgICAgIGF3YWl0IHJlcXVlc3RfcXVldWUubWFya19yZXF1ZXN0X2FzX2hhbmRsZWQocmVxdWVzdClcXG5cXG4gICAgIyBSZW1vdmUgdGhlIHJlcXVlc3QgcXVldWUuXFxuICAgIGF3YWl0IHJlcXVlc3RfcXVldWUuZHJvcCgpXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.4bs2Zx9i-WZpdW8Q8N9ZjLwsgiBGeHwvdC8zb_ISFHs\&asrc=run_on_apify)

```
import asyncio

from crawlee.storages import RequestQueue


async def main() -> None:
    # Open the request queue, if it does not exist, it will be created.
    # Leave name empty to use the default request queue.
    request_queue = await RequestQueue.open(name='my-request-queue')

    # Add a single request.
    await request_queue.add_request('https://apify.com/')

    # Add multiple requests as a batch.
    await request_queue.add_requests(
        ['https://crawlee.dev/', 'https://crawlee.dev/python/']
    )

    # Fetch and process requests from the queue.
    while request := await request_queue.fetch_next_request():
        # Do something with it...

        # And mark it as handled.
        await request_queue.mark_request_as_handled(request)

    # Remove the request queue.
    await request_queue.drop()


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBIdHRwQ3Jhd2xlciwgSHR0cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBDcmVhdGUgYSBuZXcgY3Jhd2xlciAoaXQgY2FuIGJlIGFueSBzdWJjbGFzcyBvZiBCYXNpY0NyYXdsZXIpLiBSZXF1ZXN0IHF1ZXVlIGlzXFxuICAgICMgYSBkZWZhdWx0IHJlcXVlc3QgbWFuYWdlciwgaXQgd2lsbCBiZSBvcGVuZWQsIGFuZCBmdWxseSBtYW5hZ2VkIGlmIG5vdCBzcGVjaWZpZWQuXFxuICAgIGNyYXdsZXIgPSBIdHRwQ3Jhd2xlcigpXFxuXFxuICAgICMgRGVmaW5lIHRoZSBkZWZhdWx0IHJlcXVlc3QgaGFuZGxlciwgd2hpY2ggd2lsbCBiZSBjYWxsZWQgZm9yIGV2ZXJ5IHJlcXVlc3QuXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIHJlcXVlc3RfaGFuZGxlcihjb250ZXh0OiBIdHRwQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ1Byb2Nlc3Npbmcge2NvbnRleHQucmVxdWVzdC51cmx9IC4uLicpXFxuXFxuICAgICAgICAjIFVzZSBjb250ZXh0J3MgYWRkX3JlcXVlc3RzIG1ldGhvZCBoZWxwZXIgdG8gYWRkIG5ldyByZXF1ZXN0cyBmcm9tIHRoZSBoYW5kbGVyLlxcbiAgICAgICAgYXdhaXQgY29udGV4dC5hZGRfcmVxdWVzdHMoWydodHRwczovL2NyYXdsZWUuZGV2L3B5dGhvbi8nXSlcXG5cXG4gICAgIyBVc2UgY3Jhd2xlcidzIGFkZF9yZXF1ZXN0cyBtZXRob2QgaGVscGVyIHRvIGFkZCBuZXcgcmVxdWVzdHMuXFxuICAgIGF3YWl0IGNyYXdsZXIuYWRkX3JlcXVlc3RzKFsnaHR0cHM6Ly9hcGlmeS5jb20vJ10pXFxuXFxuICAgICMgUnVuIHRoZSBjcmF3bGVyLiBZb3UgY2FuIG9wdGlvbmFsbHkgcGFzcyB0aGUgbGlzdCBvZiBpbml0aWFsIHJlcXVlc3RzLlxcbiAgICBhd2FpdCBjcmF3bGVyLnJ1bihbJ2h0dHBzOi8vY3Jhd2xlZS5kZXYvJ10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.ftuEOfHKRaWr14tvMfB0JskbU09YrDA6qhUq2w_jdbI\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import HttpCrawler, HttpCrawlingContext


async def main() -> None:
    # Create a new crawler (it can be any subclass of BasicCrawler). Request queue is
    # a default request manager, it will be opened, and fully managed if not specified.
    crawler = HttpCrawler()

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: HttpCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Use context's add_requests method helper to add new requests from the handler.
        await context.add_requests(['https://crawlee.dev/python/'])

    # Use crawler's add_requests method helper to add new requests.
    await crawler.add_requests(['https://apify.com/'])

    # Run the crawler. You can optionally pass the list of initial requests.
    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBIdHRwQ3Jhd2xlciwgSHR0cENyYXdsaW5nQ29udGV4dFxcbmZyb20gY3Jhd2xlZS5zdG9yYWdlcyBpbXBvcnQgUmVxdWVzdFF1ZXVlXFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICAjIE9wZW4gdGhlIHJlcXVlc3QgcXVldWUsIGlmIGl0IGRvZXMgbm90IGV4aXN0LCBpdCB3aWxsIGJlIGNyZWF0ZWQuXFxuICAgICMgTGVhdmUgbmFtZSBlbXB0eSB0byB1c2UgdGhlIGRlZmF1bHQgcmVxdWVzdCBxdWV1ZS5cXG4gICAgcmVxdWVzdF9xdWV1ZSA9IGF3YWl0IFJlcXVlc3RRdWV1ZS5vcGVuKG5hbWU9J215LXJlcXVlc3QtcXVldWUnKVxcblxcbiAgICAjIEludGVyYWN0IHdpdGggdGhlIHJlcXVlc3QgcXVldWUgZGlyZWN0bHksIGUuZy4gYWRkIGEgYmF0Y2ggb2YgcmVxdWVzdHMuXFxuICAgIGF3YWl0IHJlcXVlc3RfcXVldWUuYWRkX3JlcXVlc3RzKFsnaHR0cHM6Ly9hcGlmeS5jb20vJywgJ2h0dHBzOi8vY3Jhd2xlZS5kZXYvJ10pXFxuXFxuICAgICMgQ3JlYXRlIGEgbmV3IGNyYXdsZXIgKGl0IGNhbiBiZSBhbnkgc3ViY2xhc3Mgb2YgQmFzaWNDcmF3bGVyKSBhbmQgcGFzcyB0aGUgcmVxdWVzdFxcbiAgICAjIHF1ZXVlIGFzIHJlcXVlc3QgbWFuYWdlciB0byBpdC4gSXQgd2lsbCBiZSBtYW5hZ2VkIGJ5IHRoZSBjcmF3bGVyLlxcbiAgICBjcmF3bGVyID0gSHR0cENyYXdsZXIocmVxdWVzdF9tYW5hZ2VyPXJlcXVlc3RfcXVldWUpXFxuXFxuICAgICMgRGVmaW5lIHRoZSBkZWZhdWx0IHJlcXVlc3QgaGFuZGxlciwgd2hpY2ggd2lsbCBiZSBjYWxsZWQgZm9yIGV2ZXJ5IHJlcXVlc3QuXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIHJlcXVlc3RfaGFuZGxlcihjb250ZXh0OiBIdHRwQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ1Byb2Nlc3Npbmcge2NvbnRleHQucmVxdWVzdC51cmx9IC4uLicpXFxuXFxuICAgICMgQW5kIGV4ZWN1dGUgdGhlIGNyYXdsZXIuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKClcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6MTAyNCwidGltZW91dCI6MTgwfX0.x5wh-Ghs5frOprUquFFHrMNQ5pZInb_KMeE120gyA1Q\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import HttpCrawler, HttpCrawlingContext
from crawlee.storages import RequestQueue


async def main() -> None:
    # Open the request queue, if it does not exist, it will be created.
    # Leave name empty to use the default request queue.
    request_queue = await RequestQueue.open(name='my-request-queue')

    # Interact with the request queue directly, e.g. add a batch of requests.
    await request_queue.add_requests(['https://apify.com/', 'https://crawlee.dev/'])

    # Create a new crawler (it can be any subclass of BasicCrawler) and pass the request
    # queue as request manager to it. It will be managed by the crawler.
    crawler = HttpCrawler(request_manager=request_queue)

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: HttpCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

    # And execute the crawler.
    await crawler.run()


if __name__ == '__main__':
    asyncio.run(main())
```

### Request-related helpers[​](#request-related-helpers "Direct link to Request-related helpers")

Crawlee provides helper functions to simplify interactions with the [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md):

* The [`add_requests`](https://crawlee.dev/python/python/api/class/AddRequestsFunction.md) function allows you to manually add specific URLs to the configured request storage. In this case, you must explicitly provide the URLs you want to be added to the request storage. If you need to specify further details of the request, such as a `label` or `user_data`, you have to pass instances of the [`Request`](https://crawlee.dev/python/python/api/class/Request.md) class to the helper.
* The [`enqueue_links`](https://crawlee.dev/python/python/api/class/EnqueueLinksFunction.md) function is designed to discover new URLs in the current page and add them to the request storage. It can be used with default settings, requiring no arguments, or you can customize its behavior by specifying link element selectors, choosing different enqueue strategies, or applying include/exclude filters to control which URLs are added. See [Crawl website with relative links](https://crawlee.dev/python/python/docs/examples/crawl-website-with-relative-links.md) example for more details.

- Add requests
- Enqueue links

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKClcXG5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG4gICAgICAgICMgaGlnaGxpZ2h0LW5leHQtbGluZVxcbiAgICAgICAgYXdhaXQgY29udGV4dC5hZGRfcmVxdWVzdHMoWydodHRwczovL2FwaWZ5LmNvbS8nXSlcXG5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2NyYXdsZWUuZGV2LyddKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.4rFaFsp9XGKyiA76XDIx-l3KyakGJNmwby76ONNhDZU\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


async def main() -> None:
    crawler = BeautifulSoupCrawler()

    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')
        await context.add_requests(['https://apify.com/'])

    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKClcXG5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG4gICAgICAgICMgaGlnaGxpZ2h0LW5leHQtbGluZVxcbiAgICAgICAgYXdhaXQgY29udGV4dC5lbnF1ZXVlX2xpbmtzKClcXG5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2NyYXdsZWUuZGV2LyddKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.OW2BLGkoerVrkHQB5rtTqivd31CJ132twgCKmAA8aqA\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


async def main() -> None:
    crawler = BeautifulSoupCrawler()

    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')
        await context.enqueue_links()

    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

### Request manager[​](#request-manager "Direct link to Request manager")

The [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md) implements the [`RequestManager`](https://crawlee.dev/python/python/api/class/RequestManager.md) interface, offering a unified API for interacting with various request storage types. This provides a unified way to interact with different request storage types.

If you need custom functionality, you can create your own request storage by subclassing the [`RequestManager`](https://crawlee.dev/python/python/api/class/RequestManager.md) class and implementing its required methods.

For a detailed explanation of the [`RequestManager`](https://crawlee.dev/python/python/api/class/RequestManager.md) and other related components, refer to the [Request loaders guide](https://crawlee.dev/python/python/docs/guides/request-loaders.md).

## Dataset[​](#dataset "Direct link to Dataset")

The [`Dataset`](https://crawlee.dev/python/python/api/class/Dataset.md) is designed for storing structured data, where each entry has a consistent set of attributes, such as products in an online store or real estate listings. Think of a [`Dataset`](https://crawlee.dev/python/python/api/class/Dataset.md) as a table: each entry corresponds to a row, with attributes represented as columns. Datasets are append-only, allowing you to add new records but not modify or delete existing ones. Every Crawlee project run is associated with a default dataset, typically used to store results specific to that crawler execution. However, using this dataset is optional.

The following code demonstrates basic operations of the dataset:

* Basic usage
* Usage with Crawler
* Explicit usage with Crawler

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLnN0b3JhZ2VzIGltcG9ydCBEYXRhc2V0XFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICAjIE9wZW4gdGhlIGRhdGFzZXQsIGlmIGl0IGRvZXMgbm90IGV4aXN0LCBpdCB3aWxsIGJlIGNyZWF0ZWQuXFxuICAgICMgTGVhdmUgbmFtZSBlbXB0eSB0byB1c2UgdGhlIGRlZmF1bHQgZGF0YXNldC5cXG4gICAgZGF0YXNldCA9IGF3YWl0IERhdGFzZXQub3BlbihuYW1lPSdteS1kYXRhc2V0JylcXG5cXG4gICAgIyBQdXNoIGEgc2luZ2xlIHJvdyBvZiBkYXRhLlxcbiAgICBhd2FpdCBkYXRhc2V0LnB1c2hfZGF0YSh7J2Zvbyc6ICdiYXInfSlcXG5cXG4gICAgIyBQdXNoIG11bHRpcGxlIHJvd3Mgb2YgZGF0YSAoYW55dGhpbmcgSlNPTi1zZXJpYWxpemFibGUgY2FuIGJlIHB1c2hlZCkuXFxuICAgIGF3YWl0IGRhdGFzZXQucHVzaF9kYXRhKFt7J2Zvbyc6ICdiYXIyJywgJ2NvbDInOiAndmFsMid9LCB7J2NvbDMnOiAxMjN9XSlcXG5cXG4gICAgIyBGZXRjaCBhbGwgZGF0YSBmcm9tIHRoZSBkYXRhc2V0LlxcbiAgICBkYXRhID0gYXdhaXQgZGF0YXNldC5nZXRfZGF0YSgpXFxuICAgICMgRG8gc29tZXRoaW5nIHdpdGggaXQuLi5cXG5cXG4gICAgIyBSZW1vdmUgdGhlIGRhdGFzZXQuXFxuICAgIGF3YWl0IGRhdGFzZXQuZHJvcCgpXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.O__n073jB5cW-yuSD3Knh1D3RcjEKGbDOHhkmvQIuXg\&asrc=run_on_apify)

```
import asyncio

from crawlee.storages import Dataset


async def main() -> None:
    # Open the dataset, if it does not exist, it will be created.
    # Leave name empty to use the default dataset.
    dataset = await Dataset.open(name='my-dataset')

    # Push a single row of data.
    await dataset.push_data({'foo': 'bar'})

    # Push multiple rows of data (anything JSON-serializable can be pushed).
    await dataset.push_data([{'foo': 'bar2', 'col2': 'val2'}, {'col3': 123}])

    # Fetch all data from the dataset.
    data = await dataset.get_data()
    # Do something with it...

    # Remove the dataset.
    await dataset.drop()


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBDcmVhdGUgYSBuZXcgY3Jhd2xlciAoaXQgY2FuIGJlIGFueSBzdWJjbGFzcyBvZiBCYXNpY0NyYXdsZXIpLlxcbiAgICBjcmF3bGVyID0gQmVhdXRpZnVsU291cENyYXdsZXIoKVxcblxcbiAgICAjIERlZmluZSB0aGUgZGVmYXVsdCByZXF1ZXN0IGhhbmRsZXIsIHdoaWNoIHdpbGwgYmUgY2FsbGVkIGZvciBldmVyeSByZXF1ZXN0LlxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiByZXF1ZXN0X2hhbmRsZXIoY29udGV4dDogQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm9jZXNzaW5nIHtjb250ZXh0LnJlcXVlc3QudXJsfSAuLi4nKVxcblxcbiAgICAgICAgIyBFeHRyYWN0IGRhdGEgZnJvbSB0aGUgcGFnZS5cXG4gICAgICAgIGRhdGEgPSB7XFxuICAgICAgICAgICAgJ3VybCc6IGNvbnRleHQucmVxdWVzdC51cmwsXFxuICAgICAgICAgICAgJ3RpdGxlJzogY29udGV4dC5zb3VwLnRpdGxlLnN0cmluZyBpZiBjb250ZXh0LnNvdXAudGl0bGUgZWxzZSBOb25lLFxcbiAgICAgICAgfVxcblxcbiAgICAgICAgIyBQdXNoIHRoZSBleHRyYWN0ZWQgZGF0YSB0byB0aGUgKGRlZmF1bHQpIGRhdGFzZXQuXFxuICAgICAgICBhd2FpdCBjb250ZXh0LnB1c2hfZGF0YShkYXRhKVxcblxcbiAgICAjIFJ1biB0aGUgY3Jhd2xlciB3aXRoIHRoZSBpbml0aWFsIFVSTHMuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9jcmF3bGVlLmRldiddKVxcblxcbiAgICAjIEV4cG9ydCB0aGUgZGF0YXNldCB0byBhIGZpbGUuXFxuICAgIGF3YWl0IGNyYXdsZXIuZXhwb3J0X2RhdGEocGF0aD0nZGF0YXNldC5jc3YnKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.MJZr5dPsoPf4RBsnbhXayhzuMf0IkqEXu6W35dBDYGY\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


async def main() -> None:
    # Create a new crawler (it can be any subclass of BasicCrawler).
    crawler = BeautifulSoupCrawler()

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Extract data from the page.
        data = {
            'url': context.request.url,
            'title': context.soup.title.string if context.soup.title else None,
        }

        # Push the extracted data to the (default) dataset.
        await context.push_data(data)

    # Run the crawler with the initial URLs.
    await crawler.run(['https://crawlee.dev'])

    # Export the dataset to a file.
    await crawler.export_data(path='dataset.csv')


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBCZWF1dGlmdWxTb3VwQ3Jhd2xlciwgQmVhdXRpZnVsU291cENyYXdsaW5nQ29udGV4dFxcbmZyb20gY3Jhd2xlZS5zdG9yYWdlcyBpbXBvcnQgRGF0YXNldFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBPcGVuIHRoZSBkYXRhc2V0LCBpZiBpdCBkb2VzIG5vdCBleGlzdCwgaXQgd2lsbCBiZSBjcmVhdGVkLlxcbiAgICAjIExlYXZlIG5hbWUgZW1wdHkgdG8gdXNlIHRoZSBkZWZhdWx0IGRhdGFzZXQuXFxuICAgIGRhdGFzZXQgPSBhd2FpdCBEYXRhc2V0Lm9wZW4obmFtZT0nbXktZGF0YXNldCcpXFxuXFxuICAgICMgQ3JlYXRlIGEgbmV3IGNyYXdsZXIgKGl0IGNhbiBiZSBhbnkgc3ViY2xhc3Mgb2YgQmFzaWNDcmF3bGVyKS5cXG4gICAgY3Jhd2xlciA9IEJlYXV0aWZ1bFNvdXBDcmF3bGVyKClcXG5cXG4gICAgIyBEZWZpbmUgdGhlIGRlZmF1bHQgcmVxdWVzdCBoYW5kbGVyLCB3aGljaCB3aWxsIGJlIGNhbGxlZCBmb3IgZXZlcnkgcmVxdWVzdC5cXG4gICAgQGNyYXdsZXIucm91dGVyLmRlZmF1bHRfaGFuZGxlclxcbiAgICBhc3luYyBkZWYgcmVxdWVzdF9oYW5kbGVyKGNvbnRleHQ6IEJlYXV0aWZ1bFNvdXBDcmF3bGluZ0NvbnRleHQpIC0-IE5vbmU6XFxuICAgICAgICBjb250ZXh0LmxvZy5pbmZvKGYnUHJvY2Vzc2luZyB7Y29udGV4dC5yZXF1ZXN0LnVybH0gLi4uJylcXG5cXG4gICAgICAgICMgRXh0cmFjdCBkYXRhIGZyb20gdGhlIHBhZ2UuXFxuICAgICAgICBkYXRhID0ge1xcbiAgICAgICAgICAgICd1cmwnOiBjb250ZXh0LnJlcXVlc3QudXJsLFxcbiAgICAgICAgICAgICd0aXRsZSc6IGNvbnRleHQuc291cC50aXRsZS5zdHJpbmcgaWYgY29udGV4dC5zb3VwLnRpdGxlIGVsc2UgTm9uZSxcXG4gICAgICAgIH1cXG5cXG4gICAgICAgICMgUHVzaCB0aGUgZXh0cmFjdGVkIGRhdGEgdG8gdGhlIGRhdGFzZXQuXFxuICAgICAgICBhd2FpdCBkYXRhc2V0LnB1c2hfZGF0YShkYXRhKVxcblxcbiAgICAjIFJ1biB0aGUgY3Jhd2xlciB3aXRoIHRoZSBpbml0aWFsIFVSTHMuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9jcmF3bGVlLmRldiddKVxcblxcbiAgICAjIEV4cG9ydCB0aGUgZGF0YXNldCB0byB0aGUga2V5LXZhbHVlIHN0b3JlLlxcbiAgICBhd2FpdCBkYXRhc2V0LmV4cG9ydF90byhrZXk9J2RhdGFzZXQnLCBjb250ZW50X3R5cGU9J2NzdicpXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.S7QloNdJjL1jFG-OB6DV1XEDtPAtjk1K2DiEuY50_rs\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext
from crawlee.storages import Dataset


async def main() -> None:
    # Open the dataset, if it does not exist, it will be created.
    # Leave name empty to use the default dataset.
    dataset = await Dataset.open(name='my-dataset')

    # Create a new crawler (it can be any subclass of BasicCrawler).
    crawler = BeautifulSoupCrawler()

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Extract data from the page.
        data = {
            'url': context.request.url,
            'title': context.soup.title.string if context.soup.title else None,
        }

        # Push the extracted data to the dataset.
        await dataset.push_data(data)

    # Run the crawler with the initial URLs.
    await crawler.run(['https://crawlee.dev'])

    # Export the dataset to the key-value store.
    await dataset.export_to(key='dataset', content_type='csv')


if __name__ == '__main__':
    asyncio.run(main())
```

### Dataset-related helpers[​](#dataset-related-helpers "Direct link to Dataset-related helpers")

Crawlee provides the following helper function to simplify interactions with the [`Dataset`](https://crawlee.dev/python/python/api/class/Dataset.md):

* The [`push_data`](https://crawlee.dev/python/python/api/class/PushDataFunction.md) function allows you to manually add data to the dataset. You can optionally specify the dataset ID or its name.

## Key-value store[​](#key-value-store "Direct link to Key-value store")

The [`KeyValueStore`](https://crawlee.dev/python/python/api/class/KeyValueStore.md) is designed to save and retrieve data records or files efficiently. Each record is uniquely identified by a key and is associated with a specific MIME type, making the [`KeyValueStore`](https://crawlee.dev/python/python/api/class/KeyValueStore.md) ideal for tasks like saving web page screenshots, PDFs, or tracking the state of crawlers.

The following code demonstrates the usage of the [`KeyValueStore`](https://crawlee.dev/python/python/api/class/KeyValueStore.md):

* Basic usage
* Usage with Crawler
* Explicit usage with Crawler

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLnN0b3JhZ2VzIGltcG9ydCBLZXlWYWx1ZVN0b3JlXFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICAjIE9wZW4gdGhlIGtleS12YWx1ZSBzdG9yZSwgaWYgaXQgZG9lcyBub3QgZXhpc3QsIGl0IHdpbGwgYmUgY3JlYXRlZC5cXG4gICAgIyBMZWF2ZSBuYW1lIGVtcHR5IHRvIHVzZSB0aGUgZGVmYXVsdCBLVlMuXFxuICAgIGt2cyA9IGF3YWl0IEtleVZhbHVlU3RvcmUub3BlbihuYW1lPSdteS1rZXktdmFsdWUtc3RvcmUnKVxcblxcbiAgICAjIFNldCBhIHZhbHVlIGFzc29jaWF0ZWQgd2l0aCAnc29tZS1rZXknLlxcbiAgICBhd2FpdCBrdnMuc2V0X3ZhbHVlKGtleT0nc29tZS1rZXknLCB2YWx1ZT17J2Zvbyc6ICdiYXInfSlcXG5cXG4gICAgIyBHZXQgdGhlIHZhbHVlIGFzc29jaWF0ZWQgd2l0aCAnc29tZS1rZXknLlxcbiAgICB2YWx1ZSA9IGt2cy5nZXRfdmFsdWUoJ3NvbWUta2V5JylcXG4gICAgIyBEbyBzb21ldGhpbmcgd2l0aCBpdC4uLlxcblxcbiAgICAjIERlbGV0ZSB0aGUgdmFsdWUgYXNzb2NpYXRlZCB3aXRoICdzb21lLWtleScgYnkgc2V0dGluZyBpdCB0byBOb25lLlxcbiAgICBhd2FpdCBrdnMuc2V0X3ZhbHVlKGtleT0nc29tZS1rZXknLCB2YWx1ZT1Ob25lKVxcblxcbiAgICAjIFJlbW92ZSB0aGUga2V5LXZhbHVlIHN0b3JlLlxcbiAgICBhd2FpdCBrdnMuZHJvcCgpXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjEwMjQsInRpbWVvdXQiOjE4MH19.qceedpqh_DGXE7XIm7nm2VuVj3pWpczUEAWoO04mTrA\&asrc=run_on_apify)

```
import asyncio

from crawlee.storages import KeyValueStore


async def main() -> None:
    # Open the key-value store, if it does not exist, it will be created.
    # Leave name empty to use the default KVS.
    kvs = await KeyValueStore.open(name='my-key-value-store')

    # Set a value associated with 'some-key'.
    await kvs.set_value(key='some-key', value={'foo': 'bar'})

    # Get the value associated with 'some-key'.
    value = kvs.get_value('some-key')
    # Do something with it...

    # Delete the value associated with 'some-key' by setting it to None.
    await kvs.set_value(key='some-key', value=None)

    # Remove the key-value store.
    await kvs.drop()


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQbGF5d3JpZ2h0Q3Jhd2xlciwgUGxheXdyaWdodENyYXdsaW5nQ29udGV4dFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBDcmVhdGUgYSBuZXcgUGxheXdyaWdodCBjcmF3bGVyLlxcbiAgICBjcmF3bGVyID0gUGxheXdyaWdodENyYXdsZXIoKVxcblxcbiAgICAjIERlZmluZSB0aGUgZGVmYXVsdCByZXF1ZXN0IGhhbmRsZXIsIHdoaWNoIHdpbGwgYmUgY2FsbGVkIGZvciBldmVyeSByZXF1ZXN0LlxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiByZXF1ZXN0X2hhbmRsZXIoY29udGV4dDogUGxheXdyaWdodENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm9jZXNzaW5nIHtjb250ZXh0LnJlcXVlc3QudXJsfSAuLi4nKVxcblxcbiAgICAgICAgIyBDYXB0dXJlIHRoZSBzY3JlZW5zaG90IG9mIHRoZSBwYWdlIHVzaW5nIFBsYXl3cmlnaHQncyBBUEkuXFxuICAgICAgICBzY3JlZW5zaG90ID0gYXdhaXQgY29udGV4dC5wYWdlLnNjcmVlbnNob3QoKVxcbiAgICAgICAgbmFtZSA9IGNvbnRleHQucmVxdWVzdC51cmwuc3BsaXQoJy8nKVstMV1cXG5cXG4gICAgICAgICMgR2V0IHRoZSBrZXktdmFsdWUgc3RvcmUgZnJvbSB0aGUgY29udGV4dC4gIyBJZiBpdCBkb2VzIG5vdCBleGlzdCxcXG4gICAgICAgICMgaXQgd2lsbCBiZSBjcmVhdGVkLiBMZWF2ZSBuYW1lIGVtcHR5IHRvIHVzZSB0aGUgZGVmYXVsdCBLVlMuXFxuICAgICAgICBrdnMgPSBhd2FpdCBjb250ZXh0LmdldF9rZXlfdmFsdWVfc3RvcmUoKVxcblxcbiAgICAgICAgIyBTdG9yZSB0aGUgc2NyZWVuc2hvdCBpbiB0aGUga2V5LXZhbHVlIHN0b3JlLlxcbiAgICAgICAgYXdhaXQga3ZzLnNldF92YWx1ZShcXG4gICAgICAgICAgICBrZXk9ZidzY3JlZW5zaG90LXtuYW1lfScsXFxuICAgICAgICAgICAgdmFsdWU9c2NyZWVuc2hvdCxcXG4gICAgICAgICAgICBjb250ZW50X3R5cGU9J2ltYWdlL3BuZycsXFxuICAgICAgICApXFxuXFxuICAgICMgUnVuIHRoZSBjcmF3bGVyIHdpdGggdGhlIGluaXRpYWwgVVJMcy5cXG4gICAgYXdhaXQgY3Jhd2xlci5ydW4oWydodHRwczovL2NyYXdsZWUuZGV2J10pXFxuXFxuXFxuaWYgX19uYW1lX18gPT0gJ19fbWFpbl9fJzpcXG4gICAgYXN5bmNpby5ydW4obWFpbigpKVxcblwifSIsIm9wdGlvbnMiOnsiYnVpbGQiOiJsYXRlc3QiLCJjb250ZW50VHlwZSI6ImFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLTgiLCJtZW1vcnkiOjQwOTYsInRpbWVvdXQiOjE4MH19.ynGvfEYEOs1Xt3Jci9yYB-LjftmK1kaIg_yjhIuz3IA\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext


async def main() -> None:
    # Create a new Playwright crawler.
    crawler = PlaywrightCrawler()

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Capture the screenshot of the page using Playwright's API.
        screenshot = await context.page.screenshot()
        name = context.request.url.split('/')[-1]

        # Get the key-value store from the context. # If it does not exist,
        # it will be created. Leave name empty to use the default KVS.
        kvs = await context.get_key_value_store()

        # Store the screenshot in the key-value store.
        await kvs.set_value(
            key=f'screenshot-{name}',
            value=screenshot,
            content_type='image/png',
        )

    # Run the crawler with the initial URLs.
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNyYXdsZXJzIGltcG9ydCBQbGF5d3JpZ2h0Q3Jhd2xlciwgUGxheXdyaWdodENyYXdsaW5nQ29udGV4dFxcbmZyb20gY3Jhd2xlZS5zdG9yYWdlcyBpbXBvcnQgS2V5VmFsdWVTdG9yZVxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBPcGVuIHRoZSBrZXktdmFsdWUgc3RvcmUsIGlmIGl0IGRvZXMgbm90IGV4aXN0LCBpdCB3aWxsIGJlIGNyZWF0ZWQuXFxuICAgICMgTGVhdmUgbmFtZSBlbXB0eSB0byB1c2UgdGhlIGRlZmF1bHQgS1ZTLlxcbiAgICBrdnMgPSBhd2FpdCBLZXlWYWx1ZVN0b3JlLm9wZW4obmFtZT0nbXkta2V5LXZhbHVlLXN0b3JlJylcXG5cXG4gICAgIyBDcmVhdGUgYSBuZXcgUGxheXdyaWdodCBjcmF3bGVyLlxcbiAgICBjcmF3bGVyID0gUGxheXdyaWdodENyYXdsZXIoKVxcblxcbiAgICAjIERlZmluZSB0aGUgZGVmYXVsdCByZXF1ZXN0IGhhbmRsZXIsIHdoaWNoIHdpbGwgYmUgY2FsbGVkIGZvciBldmVyeSByZXF1ZXN0LlxcbiAgICBAY3Jhd2xlci5yb3V0ZXIuZGVmYXVsdF9oYW5kbGVyXFxuICAgIGFzeW5jIGRlZiByZXF1ZXN0X2hhbmRsZXIoY29udGV4dDogUGxheXdyaWdodENyYXdsaW5nQ29udGV4dCkgLT4gTm9uZTpcXG4gICAgICAgIGNvbnRleHQubG9nLmluZm8oZidQcm9jZXNzaW5nIHtjb250ZXh0LnJlcXVlc3QudXJsfSAuLi4nKVxcblxcbiAgICAgICAgIyBDYXB0dXJlIHRoZSBzY3JlZW5zaG90IG9mIHRoZSBwYWdlIHVzaW5nIFBsYXl3cmlnaHQncyBBUEkuXFxuICAgICAgICBzY3JlZW5zaG90ID0gYXdhaXQgY29udGV4dC5wYWdlLnNjcmVlbnNob3QoKVxcbiAgICAgICAgbmFtZSA9IGNvbnRleHQucmVxdWVzdC51cmwuc3BsaXQoJy8nKVstMV1cXG5cXG4gICAgICAgICMgU3RvcmUgdGhlIHNjcmVlbnNob3QgaW4gdGhlIGtleS12YWx1ZSBzdG9yZS5cXG4gICAgICAgIGF3YWl0IGt2cy5zZXRfdmFsdWUoXFxuICAgICAgICAgICAga2V5PWYnc2NyZWVuc2hvdC17bmFtZX0nLFxcbiAgICAgICAgICAgIHZhbHVlPXNjcmVlbnNob3QsXFxuICAgICAgICAgICAgY29udGVudF90eXBlPSdpbWFnZS9wbmcnLFxcbiAgICAgICAgKVxcblxcbiAgICAjIFJ1biB0aGUgY3Jhd2xlciB3aXRoIHRoZSBpbml0aWFsIFVSTHMuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9jcmF3bGVlLmRldiddKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5Ijo0MDk2LCJ0aW1lb3V0IjoxODB9fQ.PapAL9WCy3Ht2SILQ4hVbFsAjBaY3WN1scODkUMFuCM\&asrc=run_on_apify)

```
import asyncio

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext
from crawlee.storages import KeyValueStore


async def main() -> None:
    # Open the key-value store, if it does not exist, it will be created.
    # Leave name empty to use the default KVS.
    kvs = await KeyValueStore.open(name='my-key-value-store')

    # Create a new Playwright crawler.
    crawler = PlaywrightCrawler()

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

    # Run the crawler with the initial URLs.
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

To see a real-world example of how to get the input from the key-value store, see the [Screenshots](https://crawlee.dev/python/python/docs/examples/capture-screenshots-using-playwright.md) example.

### Key-value store-related helpers[​](#key-value-store-related-helpers "Direct link to Key-value store-related helpers")

Crawlee provides the following helper function to simplify interactions with the [`KeyValueStore`](https://crawlee.dev/python/python/api/class/KeyValueStore.md):

* The [`get_key_value_store`](https://crawlee.dev/python/python/api/class/GetKeyValueStoreFunction.md) function retrieves the key-value store for the current crawler run. If the KVS does not exist, it will be created. You can also specify the KVS's ID or its name.

## Cleaning up the storages[​](#cleaning-up-the-storages "Direct link to Cleaning up the storages")

By default, Crawlee cleans up all unnamed storages (including the default one) at the start of each run, so every crawl begins with a clean state. This behavior is controlled by [`Configuration.purge_on_start`](https://crawlee.dev/python/python/api/class/Configuration.md#purge_on_start) (default: True). In contrast, named storages are never purged automatically and persist across runs. The exact behavior may vary depending on the storage client implementation.

### When purging happens[​](#when-purging-happens "Direct link to When purging happens")

The cleanup occurs as soon as a storage is accessed:

* When opening a storage explicitly (e.g., [`RequestQueue.open`](https://crawlee.dev/python/python/api/class/RequestQueue.md#open), [`Dataset.open`](https://crawlee.dev/python/python/api/class/Dataset.md#open), [`KeyValueStore.open`](https://crawlee.dev/python/python/api/class/KeyValueStore.md#open)).
* When using helper functions that implicitly open storages (e.g., [`push_data`](https://crawlee.dev/python/python/api/class/PushDataFunction.md)).
* Automatically when [`BasicCrawler.run`](https://crawlee.dev/python/python/api/class/BasicCrawler.md#run) is invoked.

### Disabling automatic purging[​](#disabling-automatic-purging "Direct link to Disabling automatic purging")

To disable automatic purging, set `purge_on_start=False` in your configuration:

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLmNvbmZpZ3VyYXRpb24gaW1wb3J0IENvbmZpZ3VyYXRpb25cXG5mcm9tIGNyYXdsZWUuY3Jhd2xlcnMgaW1wb3J0IEh0dHBDcmF3bGVyLCBIdHRwQ3Jhd2xpbmdDb250ZXh0XFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICAjIFNldCB0aGUgcHVyZ2Vfb25fc3RhcnQgZmllbGQgdG8gRmFsc2UgdG8gYXZvaWQgcHVyZ2luZyB0aGUgc3RvcmFnZSBvbiBzdGFydC5cXG4gICAgIyBoaWdobGlnaHQtbmV4dC1saW5lXFxuICAgIGNvbmZpZ3VyYXRpb24gPSBDb25maWd1cmF0aW9uKHB1cmdlX29uX3N0YXJ0PUZhbHNlKVxcblxcbiAgICAjIFBhc3MgdGhlIGNvbmZpZ3VyYXRpb24gdG8gdGhlIGNyYXdsZXIuXFxuICAgIGNyYXdsZXIgPSBIdHRwQ3Jhd2xlcihjb25maWd1cmF0aW9uPWNvbmZpZ3VyYXRpb24pXFxuXFxuICAgIEBjcmF3bGVyLnJvdXRlci5kZWZhdWx0X2hhbmRsZXJcXG4gICAgYXN5bmMgZGVmIHJlcXVlc3RfaGFuZGxlcihjb250ZXh0OiBIdHRwQ3Jhd2xpbmdDb250ZXh0KSAtPiBOb25lOlxcbiAgICAgICAgY29udGV4dC5sb2cuaW5mbyhmJ1Byb2Nlc3Npbmcge2NvbnRleHQucmVxdWVzdC51cmx9IC4uLicpXFxuXFxuICAgIGF3YWl0IGNyYXdsZXIucnVuKFsnaHR0cHM6Ly9jcmF3bGVlLmRldi8nXSlcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6MTAyNCwidGltZW91dCI6MTgwfX0.GVr3HNPv6I6LpxZUxHyKGma--cGMGCt36pK266_G-hM\&asrc=run_on_apify)

```
import asyncio

from crawlee.configuration import Configuration
from crawlee.crawlers import HttpCrawler, HttpCrawlingContext


async def main() -> None:
    # Set the purge_on_start field to False to avoid purging the storage on start.
    configuration = Configuration(purge_on_start=False)

    # Pass the configuration to the crawler.
    crawler = HttpCrawler(configuration=configuration)

    @crawler.router.default_handler
    async def request_handler(context: HttpCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

### Manual purging[​](#manual-purging "Direct link to Manual purging")

Purge on start behavior just triggers the storage's `purge` method, which removes all data from the storage. If you want to purge the storage manually, you can do so by calling the `purge` method on the storage instance. Or if you want to delete the storage completely, you can call the `drop` method on the storage instance, which will remove the storage, including metadata and all its data.

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlLnN0b3JhZ2VzIGltcG9ydCBEYXRhc2V0XFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICAjIENyZWF0ZSBzdG9yYWdlIGNsaWVudCB3aXRoIGNvbmZpZ3VyYXRpb25cXG4gICAgZGF0YXNldCA9IGF3YWl0IERhdGFzZXQub3BlbihuYW1lPSdteS1kYXRhc2V0JylcXG5cXG4gICAgIyBQdXJnZSB0aGUgZGF0YXNldCBleHBsaWNpdGx5IC0gcHVyZ2luZyB3aWxsIHJlbW92ZSBhbGwgaXRlbXMgZnJvbSB0aGUgZGF0YXNldC5cXG4gICAgIyBCdXQga2VlcHMgdGhlIGRhdGFzZXQgaXRzZWxmIGFuZCBpdHMgbWV0YWRhdGEuXFxuICAgIGF3YWl0IGRhdGFzZXQucHVyZ2UoKVxcblxcbiAgICAjIE9yIHlvdSBjYW4gZHJvcCB0aGUgZGF0YXNldCBjb21wbGV0ZWx5LCB3aGljaCB3aWxsIHJlbW92ZSB0aGUgZGF0YXNldFxcbiAgICAjIGFuZCBhbGwgaXRzIGl0ZW1zLlxcbiAgICBhd2FpdCBkYXRhc2V0LmRyb3AoKVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.XvBVIcni8HiJw5cUVNYMWsT63unemXiUhQ_x4v7601g\&asrc=run_on_apify)

```
import asyncio

from crawlee.storages import Dataset


async def main() -> None:
    # Create storage client with configuration
    dataset = await Dataset.open(name='my-dataset')

    # Purge the dataset explicitly - purging will remove all items from the dataset.
    # But keeps the dataset itself and its metadata.
    await dataset.purge()

    # Or you can drop the dataset completely, which will remove the dataset
    # and all its items.
    await dataset.drop()


if __name__ == '__main__':
    asyncio.run(main())
```

Note that purging behavior may vary between storage client implementations. For more details on storage configuration and client implementations, see the [Storage clients guide](https://crawlee.dev/python/python/docs/guides/storage-clients.md).

## Conclusion[​](#conclusion "Direct link to Conclusion")

This guide introduced you to the different storage types available in Crawlee and how to interact with them. You learned about the distinction between named storages (persistent across runs) and unnamed storages with aliases (temporary and purged on start). You discovered how to manage requests using the [`RequestQueue`](https://crawlee.dev/python/python/api/class/RequestQueue.md) and store and retrieve scraping results using the [`Dataset`](https://crawlee.dev/python/python/api/class/Dataset.md) and [`KeyValueStore`](https://crawlee.dev/python/python/api/class/KeyValueStore.md). You also learned how to use helper functions to simplify interactions with these storages and how to control storage cleanup behavior.

If you have questions or need assistance, feel free to reach out on our [GitHub](https://github.com/apify/crawlee-python) or join our [Discord community](https://discord.com/invite/jyEM2PRvMU). Happy scraping!

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/guides/storages.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/guides/storage-clients.md)

[Storage clients](https://crawlee.dev/python/python/docs/guides/storage-clients.md)

[Next](https://crawlee.dev/python/python/docs/guides/trace-and-monitor-crawlers.md)

[Trace and monitor crawlers](https://crawlee.dev/python/python/docs/guides/trace-and-monitor-crawlers.md)


---

* [](https://crawlee.dev/python/python)
* [Guides](https://crawlee.dev/python/python/docs/guides.md)
* Trace and monitor crawlers

Version: 1.6

On this page

# Trace and monitor crawlers

[OpenTelemtery](https://opentelemetry.io/) is a collection of APIs, SDKs, and tools to instrument, generate, collect, and export telemetry data (metrics, logs, and traces) to help you analyze your software’s performance and behavior. In the context of crawler development, it can be used to better understand how the crawler internally works, identify bottlenecks, debug, log metrics, and more. The topic described in this guide requires at least a basic understanding of OpenTelemetry. A good place to start is [What is open telemetry](https://opentelemetry.io/docs/what-is-opentelemetry/).

In this guide, it will be shown how to set up OpenTelemetry and instrument a specific crawler to see traces of individual requests that are being processed by the crawler. OpenTelemetry on its own does not provide out of the box tool for convenient visualisation of the exported data (apart from printing to the console), but there are several good available tools to do that. In this guide, we will use [Jaeger](https://www.jaegertracing.io/) to visualise the telemetry data. To better understand concepts such as exporter, collector, and visualisation backend, please refer to the [OpenTelemetry documentation](https://opentelemetry.io/docs/collector/).

## Set up the Jaeger[​](#set-up-the-jaeger "Direct link to Set up the Jaeger")

This guide will show how to set up the environment locally to run the example code and visualize the telemetry data in Jaeger that will be running locally in a [docker](https://www.docker.com/) container.

To start the preconfigured Docker container, you can use the following command:

```
docker run -d --name jaeger -e COLLECTOR_OTLP_ENABLED=true -p 16686:16686 -p 4317:4317 -p 4318:4318 jaegertracing/all-in-one:latest
```

For more details about the Jaeger setup, see the [getting started](https://www.jaegertracing.io/docs/2.7/getting-started/) section in their documentation. You can see the Jaeger UI in your browser by navigating to <http://localhost:16686>

## Instrument the Crawler[​](#instrument-the-crawler "Direct link to Instrument the Crawler")

Now you can proceed with instrumenting the crawler to send the telemetry data to Jaeger and running it. To have the Python environment ready, you should install either **crawlee\[all]** or **crawlee\[otel]**, This will ensure that OpenTelemetry dependencies are installed, and you can run the example code snippet. In the following example, you can see the function `instrument_crawler` that contains the instrumentation setup and is called before the crawler is started. If you have already set up the Jaeger, then you can just run the following code snippet.

```
import asyncio

from opentelemetry.exporter.otlp.proto.grpc.trace_exporter import OTLPSpanExporter
from opentelemetry.sdk.resources import Resource
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import SimpleSpanProcessor
from opentelemetry.trace import set_tracer_provider

from crawlee.crawlers import BasicCrawlingContext, ParselCrawler, ParselCrawlingContext
from crawlee.otel import CrawlerInstrumentor
from crawlee.storages import Dataset, KeyValueStore, RequestQueue


def instrument_crawler() -> None:
    """Add instrumentation to the crawler."""
    resource = Resource.create(
        {
            'service.name': 'ExampleCrawler',
            'service.version': '1.0.0',
            'environment': 'development',
        }
    )

    # Set up the OpenTelemetry tracer provider and exporter
    provider = TracerProvider(resource=resource)
    otlp_exporter = OTLPSpanExporter(endpoint='localhost:4317', insecure=True)
    provider.add_span_processor(SimpleSpanProcessor(otlp_exporter))
    set_tracer_provider(provider)
    # Instrument the crawler with OpenTelemetry
    CrawlerInstrumentor(
        instrument_classes=[RequestQueue, KeyValueStore, Dataset]
    ).instrument()


async def main() -> None:
    """Run the crawler."""
    instrument_crawler()

    crawler = ParselCrawler(max_requests_per_crawl=100)
    kvs = await KeyValueStore.open()

    @crawler.pre_navigation_hook
    async def pre_nav_hook(_: BasicCrawlingContext) -> None:
        # Simulate some pre-navigation processing
        await asyncio.sleep(0.01)

    @crawler.router.default_handler
    async def handler(context: ParselCrawlingContext) -> None:
        await context.push_data({'url': context.request.url})
        await kvs.set_value(key='url', value=context.request.url)
        await context.enqueue_links()

    await crawler.run(['https://crawlee.dev/'])


if __name__ == '__main__':
    asyncio.run(main())
```

## Analyze the results[​](#analyze-the-results "Direct link to Analyze the results")

In the Jaeger UI, you can search for different traces, apply filtering, compare traces, view their detailed attributes, view timing details, and more. For the detailed description of the tool's capabilities, please refer to the [Jaeger documentation](https://www.jaegertracing.io/docs/1.47/deployment/frontend-ui/#trace-page).

![Jaeger search view](/python/assets/images/jaeger_otel_search_view_example-0df5ae38961f2bca04b111a66a4bf3c7.png "Example visualisation of search view in Jaeger") ![Jaeger trace view](/python/assets/images/jaeger_otel_trace_example-0d47251f36e4adb58600b108e66d8e42.png "Example visualisation of crawler request trace in Jaeger")

You can use different tools to consume the OpenTelemetry data that might better suit your needs. Please see the list of known Vendors in [OpenTelemetry documentation](https://opentelemetry.io/ecosystem/vendors/).

## Customize the instrumentation[​](#customize-the-instrumentation "Direct link to Customize the instrumentation")

You can customize the [`CrawlerInstrumentor`](https://crawlee.dev/python/python/api/class/CrawlerInstrumentor.md). Depending on the arguments used during its initialization, the instrumentation will be applied to different parts of the Crawlee code. By default, it instruments some functions that can give quite a good picture of each individual request handling. To turn this default instrumentation off, you can pass `request_handling_instrumentation=False` during initialization. You can also extend instrumentation by passing `instrument_classes=[...]` initialization argument that contains classes you want to be auto-instrumented. All their public methods will be automatically instrumented. Bear in mind that instrumentation has some runtime costs as well. The more instrumentation is used, the more overhead it will add to the crawler execution.

You can also create your instrumentation by selecting only the methods you want to instrument. For more details, see the [`CrawlerInstrumentor`](https://crawlee.dev/python/python/api/class/CrawlerInstrumentor.md) source code and the [Python documentation for OpenTelemetry](https://opentelemetry.io/docs/languages/python/).

If you have questions or need assistance, feel free to reach out on our [GitHub](https://github.com/apify/crawlee-python) or join our [Discord community](https://discord.com/invite/jyEM2PRvMU).

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/guides/trace_and_monitor_crawlers.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/guides/storages.md)

[Storages](https://crawlee.dev/python/python/docs/guides/storages.md)

[Next](https://crawlee.dev/python/python/docs/deployment.md)

[Deployment](https://crawlee.dev/python/python/docs/deployment.md)


---

* [](https://crawlee.dev/python/python)
* Introduction

Version: 1.6

On this page

