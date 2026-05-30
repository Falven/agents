# Apify platform

Apify is a [platform](https://apify.com) built to serve large-scale and high-performance web scraping and automation needs. It provides easy access to [compute instances (Actors)](#what-is-an-actor), convenient request and result storages, [proxies](https://crawlee.dev/python/python/docs/guides/proxy-management.md), scheduling, webhooks and [more](https://docs.apify.com/), accessible through a [web interface](https://console.apify.com) or an [API](https://docs.apify.com/api).

While we think that the Apify platform is super cool, and it's definitely worth signing up for a [free account](https://console.apify.com/sign-up), **Crawlee is and will always be open source**, runnable locally or on any cloud infrastructure.

note

We do not test Crawlee in other cloud environments such as Lambda or on specific architectures such as Raspberry PI. We strive to make it work, but there are no guarantees.

## Requirements[​](#requirements "Direct link to Requirements")

To run your Crawlee code on Apify platform, you need an Apify account. If you don't have one yet, you can sign up [here](https://console.apify.com/sign-up).

Additionally, you must have the [Apify CLI](https://docs.apify.com/cli/) installed on your computer. For installation instructions, refer to the [Installation guide](https://docs.apify.com/cli/docs/installation).

Finally, ensure that the \[Apify SDK] (<https://docs.apify.com/sdk/python/>) is installed in your project. You can install it using `pip`:

```
pip install apify
```

## Logging into Apify platform from Crawlee[​](#logging-into-apify-platform-from-crawlee "Direct link to Logging into Apify platform from Crawlee")

To access your [Apify account](https://console.apify.com/sign-up) from Crawlee, you must provide credentials - your [API token](https://console.apify.com/account?tab=integrations). You can do that either by utilizing [Apify CLI](https://docs.apify.com/cli/) or with environment variables.

Once you provide credentials to your Apify CLI installation, you will be able to use all the Apify platform features, such as calling Actors, saving to cloud storages, using Apify proxies, setting up webhooks and so on.

### Log in with CLI[​](#log-in-with-cli "Direct link to Log in with CLI")

Apify CLI allows you to log in to your Apify account on your computer. If you then run your crawler using the CLI, your credentials will automatically be added.

```
npm install -g apify-cli
apify login -t YOUR_API_TOKEN
```

### Log in with environment variables[​](#log-in-with-environment-variables "Direct link to Log in with environment variables")

Alternatively, you can always provide credentials to your Actor by setting the [`APIFY_TOKEN`](#apify_token) environment variable to your API token.

> There's also the [`APIFY_PROXY_PASSWORD`](#apify_proxy_password) environment variable. Actor automatically infers that from your token, but it can be useful when you need to access proxies from a different account than your token represents.

### Log in with Configuration[​](#log-in-with-configuration "Direct link to Log in with Configuration")

Another option is to use the [`Configuration`](https://docs.apify.com/sdk/python/reference/class/Configuration) instance and set your api token there.

```
import asyncio

from apify import Actor, Configuration


async def main() -> None:
    # Create a new configuration with your API key. You can find it at
    # https://console.apify.com/settings/integrations. It can be provided either
    # as a parameter "token" or as an environment variable "APIFY_TOKEN".
    config = Configuration(
        token='apify_api_YOUR_TOKEN',
    )

    async with Actor(config):
        Actor.log.info('Hello from Apify platform!')


if __name__ == '__main__':
    asyncio.run(main())
```

## What is an Actor[​](#what-is-an-actor "Direct link to What is an Actor")

When you deploy your script to the Apify platform, it becomes an [Actor](https://apify.com/actors). An Actor is a serverless microservice that accepts an input and produces an output. It can run for a few seconds, hours or even infinitely. An Actor can perform anything from a simple action such as filling out a web form or sending an email, to complex operations such as crawling an entire website and removing duplicates from a large dataset.

Actors can be shared in the [Apify Store](https://apify.com/store) so that other people can use them. But don't worry, if you share your Actor in the store and somebody uses it, it runs under their account, not yours.

**Related links**

* [Store of existing Actors](https://apify.com/store)
* [Documentation](https://docs.apify.com/actors)
* [View Actors in Apify Console](https://console.apify.com/actors)
* [API reference](https://apify.com/docs/api/v2#/reference/actors)

## Running an Actor locally[​](#running-an-actor-locally "Direct link to Running an Actor locally")

First let's create a boilerplate of the new Actor. You could use Apify CLI and just run:

```
apify create my-hello-world
```

The CLI will prompt you to select a project boilerplate template - let's pick "Crawlee + BeautifulSoup". The tool will create a directory called `my-hello-world` with Python project files. You can run the Actor as follows:

```
cd my-hello-world
apify run
```

## Running Crawlee code as an Actor[​](#running-crawlee-code-as-an-actor "Direct link to Running Crawlee code as an Actor")

For running Crawlee code as an Actor on [Apify platform](https://apify.com/actors) you need to wrap the body of the main function of your crawler with `async with Actor`.

NOTE

Adding `async with Actor` is the only important thing needed to run it on Apify platform as an Actor. It is needed to initialize your Actor (e.g. to set the correct storage implementation) and to correctly handle exiting the process.

Let's look at the `BeautifulSoupCrawler` example from the [Quick start](https://crawlee.dev/python/python/docs/quick-start.md) guide:

```
import asyncio

from apify import Actor

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


async def main() -> None:
    # Wrap the crawler code in an Actor context manager.
    async with Actor:
        crawler = BeautifulSoupCrawler(max_requests_per_crawl=10)

        @crawler.router.default_handler
        async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
            context.log.info(f'Processing {context.request.url} ...')
            data = {
                'url': context.request.url,
                'title': context.soup.title.string if context.soup.title else None,
            }
            await context.push_data(data)
            await context.enqueue_links()

        await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

Note that you could also run your Actor (that is using Crawlee) locally with Apify CLI. You could start it via the following command in your project folder:

```
apify run
```

## Deploying an Actor to Apify platform[​](#deploying-an-actor-to-apify-platform "Direct link to Deploying an Actor to Apify platform")

Now (assuming you are already logged in to your Apify account) you can easily deploy your code to the Apify platform by running:

```
apify push
```

Your script will be uploaded to and built on the Apify platform so that it can be run there. For more information, view the [Apify Actor](https://docs.apify.com/cli) documentation.

## Usage on Apify platform[​](#usage-on-apify-platform "Direct link to Usage on Apify platform")

You can also develop your Actor in an online code editor directly on the platform (you'll need an Apify Account). Let's go to the [Actors](https://console.apify.com/actors) page in the app, click *Create new* and then go to the *Source* tab and start writing the code or paste one of the examples from the [Examples](https://crawlee.dev/python/python/docs/examples.md) section.

## Storages[​](#storages "Direct link to Storages")

There are several things worth mentioning here.

### Helper functions for default Key-Value Store and Dataset[​](#helper-functions-for-default-key-value-store-and-dataset "Direct link to Helper functions for default Key-Value Store and Dataset")

To simplify access to the *default* storages, instead of using the helper functions of respective storage classes, you could use:

* [`Actor.set_value()`](https://docs.apify.com/sdk/python/reference/class/Actor#set_value), [`Actor.get_value()`](https://docs.apify.com/sdk/python/reference/class/Actor#get_value), [`Actor.get_input()`](https://docs.apify.com/sdk/python/reference/class/Actor#get_input) for [`Key-Value Store`](https://docs.apify.com/sdk/python/reference/class/KeyValueStore)
* [`Actor.push_data()`](https://docs.apify.com/sdk/python/reference/class/Actor#push_data) for [`Dataset`](https://docs.apify.com/sdk/python/reference/class/Dataset)

### Using platform storage in a local Actor[​](#using-platform-storage-in-a-local-actor "Direct link to Using platform storage in a local Actor")

When you plan to use the platform storage while developing and running your Actor locally, you should use [`Actor.open_key_value_store()`](https://docs.apify.com/sdk/python/reference/class/Actor#open_key_value_store), [`Actor.open_dataset()`](https://docs.apify.com/sdk/python/reference/class/Actor#open_dataset) and [`Actor.open_request_queue()`](https://docs.apify.com/sdk/python/reference/class/Actor#open_request_queue) to open the respective storage.

Using each of these methods allows to pass the `force_cloud` keyword argument. If set to `True`, cloud storage will be used instead of the folder on the local disk.

note

If you don't plan to force usage of the platform storages when running the Actor locally, there is no need to use the [`Actor`](https://docs.apify.com/sdk/python/reference/class/Actor) class for it. The Crawlee variants [`KeyValueStore.open()`](https://crawlee.dev/python/python/api/class/KeyValueStore.md#open), [`Dataset.open()`](https://crawlee.dev/python/python/api/class/Dataset.md#open) and [`RequestQueue.open()`](https://crawlee.dev/python/python/api/class/RequestQueue.md#open) will work the same.

<!-- -->

### Exporting dataset data[​](#exporting-dataset-data "Direct link to Exporting dataset data")

When the [`Dataset`](https://crawlee.dev/python/python/api/class/Dataset.md) is stored on the [Apify platform](https://apify.com/actors), you can export its data to the following formats: HTML, JSON, CSV, Excel, XML and RSS. The datasets are displayed on the Actor run details page and in the [Storage](https://console.apify.com/storage) section in the Apify Console. The actual data is exported using the [Get dataset items](https://apify.com/docs/api/v2#/reference/datasets/item-collection/get-items) Apify API endpoint. This way you can easily share the crawling results.

**Related links**

* [Apify platform storage documentation](https://docs.apify.com/storage)
* [View storage in Apify Console](https://console.apify.com/storage)
* [Key-value stores API reference](https://apify.com/docs/api/v2#/reference/key-value-stores)
* [Datasets API reference](https://docs.apify.com/api/v2#/reference/datasets)
* [Request queues API reference](https://docs.apify.com/api/v2#/reference/request-queues)

## Environment variables[​](#environment-variables "Direct link to Environment variables")

The following describes select environment variables set by the Apify platform. For a complete list, see the [Environment variables](https://docs.apify.com/platform/actors/development/programming-interface/environment-variables) section in the Apify platform documentation.

note

It's important to notice that `CRAWLEE_` environment variables don't need to be replaced with equivalent `APIFY_` ones. Likewise, Crawlee understands `APIFY_` environment variables.

### `APIFY_TOKEN`[​](#apify_token "Direct link to apify_token")

The API token for your Apify account. It is used to access the Apify API, e.g. to access cloud storage or to run an Actor on the Apify platform. You can find your API token on the [Account Settings / Integrations](https://console.apify.com/account?tab=integrations) page.

### Combinations of `APIFY_TOKEN` and `CRAWLEE_STORAGE_DIR`[​](#combinations-of-apify_token-and-crawlee_storage_dir "Direct link to combinations-of-apify_token-and-crawlee_storage_dir")

By combining the env vars in various ways, you can greatly influence the Actor's behavior.

| Env Vars                                | API | Storages         |
| --------------------------------------- | --- | ---------------- |
| none OR `CRAWLEE_STORAGE_DIR`           | no  | local            |
| `APIFY_TOKEN`                           | yes | Apify platform   |
| `APIFY_TOKEN` AND `CRAWLEE_STORAGE_DIR` | yes | local + platform |

When using both `APIFY_TOKEN` and `CRAWLEE_STORAGE_DIR`, you can use all the Apify platform features and your data will be stored locally by default. If you want to access platform storages, you can use the `force_cloud=true` option in their respective functions.

### `APIFY_PROXY_PASSWORD`[​](#apify_proxy_password "Direct link to apify_proxy_password")

Optional password to [Apify Proxy](https://docs.apify.com/proxy) for IP address rotation. Assuming Apify Account was already created, you can find the password on the [Proxy page](https://console.apify.com/proxy) in the Apify Console. The password is automatically inferred using the `APIFY_TOKEN` env var, so in most cases, you don't need to touch it. You should use it when, for some reason, you need access to Apify Proxy, but not access to Apify API, or when you need access to proxy from a different account than your token represents.

## Proxy management[​](#proxy-management "Direct link to Proxy management")

In addition to your own proxy servers and proxy servers acquired from third-party providers used together with Crawlee, you can also rely on [Apify Proxy](https://apify.com/proxy) for your scraping needs.

### Apify proxy[​](#apify-proxy "Direct link to Apify proxy")

If you are already subscribed to Apify Proxy, you can start using them immediately in only a few lines of code (for local usage you first should be [logged in](#logging-into-apify-platform-from-crawlee) to your Apify account.

```
import asyncio

from apify import Actor


async def main() -> None:
    async with Actor:
        # Create a new Apify Proxy configuration. The password can be found at
        # https://console.apify.com/proxy/http-settings and should be provided either
        # as a parameter "password" or as an environment variable "APIFY_PROXY_PASSWORD".
        proxy_configuration = await Actor.create_proxy_configuration(
            password='apify_proxy_YOUR_PASSWORD',
        )

        if not proxy_configuration:
            Actor.log.warning('Failed to create proxy configuration.')
            return

        proxy_url = await proxy_configuration.new_url()
        Actor.log.info(f'Proxy URL: {proxy_url}')


if __name__ == '__main__':
    asyncio.run(main())
```

Note that unlike using your own proxies in Crawlee, you shouldn't use the constructor to create [`ProxyConfiguration`](https://crawlee.dev/python/python/api/class/ProxyConfiguration.md) instances. For using the Apify Proxy you should create an instance using the [`Actor.create_proxy_configuration()`](https://docs.apify.com/sdk/python/reference/class/Actor#create_proxy_configuration) function instead.

### Advanced Apify proxy configuration[​](#advanced-apify-proxy-configuration "Direct link to Advanced Apify proxy configuration")

With Apify Proxy, you can select specific proxy groups to use, or countries to connect from. This allows you to get better proxy performance after some initial research.

```
import asyncio

from apify import Actor


async def main() -> None:
    async with Actor:
        proxy_configuration = await Actor.create_proxy_configuration(
            password='apify_proxy_YOUR_PASSWORD',
            # Specify the proxy group to use.
            groups=['RESIDENTIAL'],
            # Set the country code for the proxy.
            country_code='US',
        )

        # ...


if __name__ == '__main__':
    asyncio.run(main())
```

Now your crawlers will use only Residential proxies from the US. Note that you must first get access to a proxy group before you are able to use it. You can check proxy groups available to you in the [proxy dashboard](https://console.apify.com/proxy).

### Apify proxy vs. own proxies[​](#apify-proxy-vs-own-proxies "Direct link to Apify proxy vs. own proxies")

The [`ProxyConfiguration`](https://docs.apify.com/sdk/python/reference/class/ProxyConfiguration) class covers both Apify Proxy and custom proxy URLs so that you can easily switch between proxy providers. However, some features of the class are available only to Apify Proxy users, mainly because Apify Proxy is what one would call a super-proxy. It's not a single proxy server, but an API endpoint that allows connection through millions of different IP addresses. So the class essentially has two modes: Apify Proxy or Own (third party) proxy.

The difference is easy to remember.

* If you're using your own proxies - you should create a [`ProxyConfiguration`](https://crawlee.dev/python/python/api/class/ProxyConfiguration.md) instance directly.
* If you are planning to use Apify Proxy - you should create an instance using the [`Actor.create_proxy_configuration()`](https://docs.apify.com/sdk/python/reference/class/Actor#create_proxy_configuration) function. The `new_url_function` parameter enables the use of your custom proxy URLs, whereas all the other options are there to configure Apify Proxy.

**Related links**

* [Apify Proxy docs](https://docs.apify.com/proxy)

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/deployment/apify_platform.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/deployment.md)

[Deployment](https://crawlee.dev/python/python/docs/deployment.md)

[Next](https://crawlee.dev/python/python/docs/deployment/aws-lambda.md)

[Deploy on AWS Lambda](https://crawlee.dev/python/python/docs/deployment/aws-lambda.md)


---

* [](https://crawlee.dev/python/python)
* [Deployment](https://crawlee.dev/python/python/docs/deployment.md)
* Deploy on AWS Lambda

Version: 1.6

On this page

# Deploy on AWS Lambda

[AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) is a serverless compute service that lets you run code without provisioning or managing servers. This guide covers deploying [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md) and [`PlaywrightCrawler`](https://crawlee.dev/python/python/api/class/PlaywrightCrawler.md).

The code examples are based on the [BeautifulSoupCrawler example](https://crawlee.dev/python/python/docs/examples/beautifulsoup-crawler.md).

## BeautifulSoupCrawler on AWS Lambda[​](#beautifulsoupcrawler-on-aws-lambda "Direct link to BeautifulSoupCrawler on AWS Lambda")

For simple crawlers that don't require browser rendering, you can deploy using a ZIP archive.

### Updating the code[​](#updating-the-code "Direct link to Updating the code")

When instantiating a crawler, use [`MemoryStorageClient`](https://crawlee.dev/python/python/api/class/MemoryStorageClient.md). By default, Crawlee uses file-based storage, but the Lambda filesystem is read-only (except for `/tmp`). Using `MemoryStorageClient` tells Crawlee to use in-memory storage instead.

Wrap the crawler logic in a `lambda_handler` function. This is the entry point that AWS will execute.

important

Make sure to always instantiate a new crawler for every Lambda invocation. AWS keeps the environment running for some time after the first execution (to reduce cold-start times), so subsequent calls may access an already-used crawler instance.

**TL;DR: Keep your Lambda stateless.**

Finally, return the scraped data from the Lambda when the crawler run ends.

lambda\_function.py

```
import asyncio
import json
from datetime import timedelta
from typing import Any

from aws_lambda_powertools.utilities.typing import LambdaContext

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext
from crawlee.storage_clients import MemoryStorageClient
from crawlee.storages import Dataset, RequestQueue


async def main() -> str:
    # Disable writing storage data to the file system
    storage_client = MemoryStorageClient()

    # Initialize storages
    dataset = await Dataset.open(storage_client=storage_client)
    request_queue = await RequestQueue.open(storage_client=storage_client)

    crawler = BeautifulSoupCrawler(
        storage_client=storage_client,
        max_request_retries=1,
        request_handler_timeout=timedelta(seconds=30),
        max_requests_per_crawl=10,
    )

    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        data = {
            'url': context.request.url,
            'title': context.soup.title.string if context.soup.title else None,
            'h1s': [h1.text for h1 in context.soup.find_all('h1')],
            'h2s': [h2.text for h2 in context.soup.find_all('h2')],
            'h3s': [h3.text for h3 in context.soup.find_all('h3')],
        }

        await context.push_data(data)
        await context.enqueue_links()

    await crawler.run(['https://crawlee.dev'])

    # Extract data saved in `Dataset`
    data = await crawler.get_data()

    # Clean up storages after the crawl
    await dataset.drop()
    await request_queue.drop()

    # Serialize the list of scraped items to JSON string
    return json.dumps(data.items)


def lambda_handler(_event: dict[str, Any], _context: LambdaContext) -> dict[str, Any]:
    result = asyncio.run(main())
    # Return the response with results
    return {'statusCode': 200, 'body': result}
```

### Preparing the environment[​](#preparing-the-environment "Direct link to Preparing the environment")

Lambda requires all dependencies to be included in the deployment package. Create a virtual environment and install dependencies:

```
python3.14 -m venv .venv
source .venv/bin/activate
pip install 'crawlee[beautifulsoup]' 'boto3' 'aws-lambda-powertools'
```

[`boto3`](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html) is the AWS SDK for Python. Including it in your dependencies is recommended to avoid version misalignment issues with the Lambda runtime.

### Creating the ZIP archive[​](#creating-the-zip-archive "Direct link to Creating the ZIP archive")

Create a ZIP archive from your project, including dependencies from the virtual environment:

```
cd .venv/lib/python3.14/site-packages
zip -r ../../../../package.zip .
cd ../../../../
zip package.zip lambda_function.py
```

Large dependencies?

AWS has a limit of 50 MB for direct upload and 250 MB for unzipped deployment package size.

A better way to manage dependencies is by using Lambda Layers. With Layers, you can share files between multiple Lambda functions and keep the actual code as slim as possible.

To create a Lambda Layer:

1. Create a `python/` folder and copy dependencies from `site-packages` into it
2. Create a zip archive: `zip -r layer.zip python/`
3. Create a new Lambda Layer from the archive (you may need to upload it to S3 first)
4. Attach the Layer to your Lambda function

### Creating the Lambda function[​](#creating-the-lambda-function "Direct link to Creating the Lambda function")

Create the Lambda function in the AWS Lambda Console:

1. Navigate to `Lambda` in [AWS Management Console](https://aws.amazon.com/console/).
2. Click **Create function**.
3. Select **Author from scratch**.
4. Enter a **Function name**, for example `BeautifulSoupTest`.
5. Choose a **Python runtime** that matches the version used in your virtual environment (for example, Python 3.14).
6. Click **Create function** to finish.

Once created, upload `package.zip` as the code source in the AWS Lambda Console using the "Upload from" button.

In Lambda Runtime Settings, set the handler. Since the file is named `lambda_function.py` and the function is `lambda_handler`, you can use the default value `lambda_function.lambda_handler`.

Configuration

In the Configuration tab, you can adjust:

* **Memory**: Memory size can greatly affect execution speed. A minimum of 256-512 MB is recommended.
* **Timeout**: Set according to the size of the website you are scraping (1 minute for the example code).
* **Ephemeral storage**: Size of the `/tmp` directory.

See the [official documentation](https://docs.aws.amazon.com/lambda/latest/dg/gettingstarted-limits.html) to learn how performance and cost scale with memory.

After the Lambda deploys, you can test it by clicking the "Test" button. The event contents don't matter for a basic test, but you can parameterize your crawler by parsing the event object that AWS passes as the first argument to the handler.

## PlaywrightCrawler on AWS Lambda[​](#playwrightcrawler-on-aws-lambda "Direct link to PlaywrightCrawler on AWS Lambda")

For crawlers that require browser rendering, you need to deploy using Docker container images because Playwright and browser binaries exceed Lambda's ZIP deployment size limits.

### Updating the code[​](#updating-the-code-1 "Direct link to Updating the code")

As with [`BeautifulSoupCrawler`](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md), use [`MemoryStorageClient`](https://crawlee.dev/python/python/api/class/MemoryStorageClient.md) and wrap the logic in a `lambda_handler` function. Additionally, configure `browser_launch_options` with flags optimized for serverless environments. These flags disable sandboxing and GPU features that aren't available in Lambda's containerized runtime.

main.py

```
import asyncio
import json
from datetime import timedelta
from typing import Any

from aws_lambda_powertools.utilities.typing import LambdaContext

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext
from crawlee.storage_clients import MemoryStorageClient
from crawlee.storages import Dataset, RequestQueue


async def main() -> str:
    # Disable writing storage data to the file system
    storage_client = MemoryStorageClient()

    # Initialize storages
    dataset = await Dataset.open(storage_client=storage_client)
    request_queue = await RequestQueue.open(storage_client=storage_client)

    crawler = PlaywrightCrawler(
        storage_client=storage_client,
        max_request_retries=1,
        request_handler_timeout=timedelta(seconds=30),
        max_requests_per_crawl=10,
        # Configure Playwright to run in AWS Lambda environment
        browser_launch_options={
            'args': [
                '--no-sandbox',
                '--disable-setuid-sandbox',
                '--disable-dev-shm-usage',
                '--disable-gpu',
                '--single-process',
            ]
        },
    )

    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        data = {
            'url': context.request.url,
            'title': await context.page.title(),
            'h1s': await context.page.locator('h1').all_text_contents(),
            'h2s': await context.page.locator('h2').all_text_contents(),
            'h3s': await context.page.locator('h3').all_text_contents(),
        }

        await context.push_data(data)
        await context.enqueue_links()

    await crawler.run(['https://crawlee.dev'])

    # Extract data saved in `Dataset`
    data = await crawler.get_data()

    # Clean up storages after the crawl
    await dataset.drop()
    await request_queue.drop()

    # Serialize the list of scraped items to JSON string
    return json.dumps(data.items)


def lambda_handler(_event: dict[str, Any], _context: LambdaContext) -> dict[str, Any]:
    result = asyncio.run(main())
    # Return the response with results
    return {'statusCode': 200, 'body': result}
```

### Installing and configuring AWS CLI[​](#installing-and-configuring-aws-cli "Direct link to Installing and configuring AWS CLI")

Install AWS CLI following the [official documentation](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) according to your operating system.

Authenticate by running:

```
aws login
```

### Preparing the project[​](#preparing-the-project "Direct link to Preparing the project")

Initialize the project by running `uvx 'crawlee[cli]' create`.

Or use a single command if you don't need interactive mode:

```
uvx 'crawlee[cli]' create aws_playwright --crawler-type playwright --http-client impit --package-manager uv --no-apify --start-url 'https://crawlee.dev' --install
```

Add the following dependencies:

```
uv add awslambdaric aws-lambda-powertools boto3
```

[`boto3`](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html) is the AWS SDK for Python. Use it if your function integrates with any other AWS services.

The project is created with a Dockerfile that needs to be modified for AWS Lambda by adding `ENTRYPOINT` and updating `CMD`:

Dockerfile

```
FROM apify/actor-python-playwright:3.14

RUN apt update && apt install -yq git && rm -rf /var/lib/apt/lists/*

RUN pip install -U pip setuptools \
    && pip install 'uv<1'

ENV UV_PROJECT_ENVIRONMENT="/usr/local"

COPY pyproject.toml uv.lock ./

RUN echo "Python version:" \
    && python --version \
    && echo "Installing dependencies:" \
    && PLAYWRIGHT_INSTALLED=$(pip freeze | grep -q playwright && echo "true" || echo "false") \
    && if [ "$PLAYWRIGHT_INSTALLED" = "true" ]; then \
        echo "Playwright already installed, excluding from uv sync" \
        && uv sync --frozen --no-install-project --no-editable -q --no-dev --inexact --no-install-package playwright; \
    else \
        echo "Playwright not found, installing all dependencies" \
        && uv sync --frozen --no-install-project --no-editable -q --no-dev --inexact; \
    fi \
    && echo "All installed Python packages:" \
    && pip freeze

COPY . ./

RUN python -m compileall -q .

# AWS Lambda entrypoint
ENTRYPOINT [ "/usr/local/bin/python3", "-m", "awslambdaric" ]

# Lambda handler function
CMD [ "aws_playwright.main.lambda_handler" ]
```

### Building and pushing the Docker image[​](#building-and-pushing-the-docker-image "Direct link to Building and pushing the Docker image")

Create a repository `lambda/aws-playwright` in [Amazon Elastic Container Registry](https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html) in the same region where your Lambda functions will run. To learn more, refer to the [official documentation](https://docs.aws.amazon.com/AmazonECR/latest/userguide/getting-started-cli.html).

Navigate to the created repository and click the "View push commands" button. This will open a window with console commands for uploading the Docker image to your repository. Execute them.

Example:

```
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin {user-specific-data}
docker build --platform linux/amd64 --provenance=false -t lambda/aws-playwright .
docker tag lambda/aws-playwright:latest {user-specific-data}/lambda/aws-playwright:latest
docker push {user-specific-data}/lambda/aws-playwright:latest
```

### Creating the Lambda function[​](#creating-the-lambda-function-1 "Direct link to Creating the Lambda function")

1. Navigate to `Lambda` in [AWS Management Console](https://aws.amazon.com/console/).
2. Click **Create function**.
3. Select **Container image**.
4. Browse and select your ECR image.
5. Click **Create function** to finish.

Configuration

In the Configuration tab, you can adjust resources. Playwright crawlers require more resources than BeautifulSoup crawlers:

* **Memory**: Minimum 1024 MB recommended. Browser operations are memory-intensive, so 2048 MB or more may be needed for complex pages.
* **Timeout**: Set according to crawl size. Browser startup adds overhead, so allow at least 5 minutes even for simple crawls.
* **Ephemeral storage**: Default 512 MB is usually sufficient unless downloading large files.

See the [official documentation](https://docs.aws.amazon.com/lambda/latest/dg/gettingstarted-limits.html) to learn how performance and cost scale with memory.

After the Lambda deploys, click the "Test" button to invoke it. The event contents don't matter for a basic test, but you can parameterize your crawler by parsing the event object that AWS passes as the first argument to the handler.

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/deployment/aws_lambda.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/deployment/apify-platform.md)

[Deploy on Apify](https://crawlee.dev/python/python/docs/deployment/apify-platform.md)

[Next](https://crawlee.dev/python/python/docs/deployment/gcp-cloud-run-functions.md)

[Cloud Run functions](https://crawlee.dev/python/python/docs/deployment/gcp-cloud-run-functions.md)


---

* [](https://crawlee.dev/python/python)
* [Deployment](https://crawlee.dev/python/python/docs/deployment.md)
* Deploy to Google Cloud
* Cloud Run

Version: 1.6

On this page

# Cloud Run

[Google Cloud Run](https://cloud.google.com/run) is a container-based serverless platform that allows you to run web crawlers with headless browsers. This service is recommended when your Crawlee applications need browser rendering capabilities, require more granular control, or have complex dependencies that aren't supported by [Cloud Functions](https://crawlee.dev/python/python/docs/deployment/gcp-cloud-run-functions.md).

GCP Cloud Run allows you to deploy using Docker containers, giving you full control over your environment and the flexibility to use any web server framework of your choice, unlike Cloud Functions which are limited to [Flask](https://flask.palletsprojects.com/en/stable/).

## Preparing the project[​](#preparing-the-project "Direct link to Preparing the project")

We'll prepare our project using [Litestar](https://litestar.dev/) and the [Uvicorn](https://www.uvicorn.org/) web server. The HTTP server handler will wrap the crawler to communicate with clients. Because the Cloud Run platform sees only an opaque Docker container, we have to take care of this bit ourselves.

info

GCP passes you an environment variable called `PORT` - your HTTP server is expected to be listening on this port (GCP exposes this one to the outer world).

```
import os

import uvicorn
from litestar import Litestar, get

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext
from crawlee.storage_clients import MemoryStorageClient


@get('/')
async def main() -> str:
    """The crawler entry point that will be called when the HTTP endpoint is accessed."""
    # Disable writing storage data to the file system
    storage_client = MemoryStorageClient()

    crawler = PlaywrightCrawler(
        headless=True,
        max_requests_per_crawl=10,
        browser_type='firefox',
        storage_client=storage_client,
    )

    @crawler.router.default_handler
    async def default_handler(context: PlaywrightCrawlingContext) -> None:
        """Default request handler that processes each page during crawling."""
        context.log.info(f'Processing {context.request.url} ...')
        title = await context.page.query_selector('title')
        await context.push_data(
            {
                'url': context.request.loaded_url,
                'title': await title.inner_text() if title else None,
            }
        )

        await context.enqueue_links()

    await crawler.run(['https://crawlee.dev'])

    data = await crawler.get_data()

    # Return the results as JSON to the client
    return json.dumps(data.items)


# Initialize the Litestar app with our route handler
app = Litestar(route_handlers=[main])

# Start the Uvicorn server using the `PORT` environment variable provided by GCP
# This is crucial - Cloud Run expects your app to listen on this specific port
uvicorn.run(app, host='0.0.0.0', port=int(os.environ.get('PORT', '8080')))  # noqa: S104 # Use all interfaces in a container, safely
```

tip

Always make sure to keep all the logic in the request handler - as with other FaaS services, your request handlers have to be **stateless.**

## Deploying to Google Cloud Platform[​](#deploying-to-google-cloud-platform "Direct link to Deploying to Google Cloud Platform")

Now, we’re ready to deploy! If you have initialized your project using `uvx crawlee create`, the initialization script has prepared a Dockerfile for you.

All you have to do now is run `gcloud run deploy` in your project folder (the one with your Dockerfile in it). The gcloud CLI application will ask you a few questions, such as what region you want to deploy your application in, or whether you want to make your application public or private.

After answering those questions, you should be able to see your application in the GCP dashboard and run it using the link you find there.

tip

In case your first execution of your newly created Cloud Run fails, try editing the Run configuration - mainly setting the available memory to 1GiB or more and updating the request timeout according to the size of the website you are scraping.

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/deployment/google_cloud_run.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/deployment/gcp-cloud-run-functions.md)

[Cloud Run functions](https://crawlee.dev/python/python/docs/deployment/gcp-cloud-run-functions.md)

[Next](https://crawlee.dev/python/python/docs/examples.md)

[Examples](https://crawlee.dev/python/python/docs/examples.md)


---

* [](https://crawlee.dev/python/python)
* [Deployment](https://crawlee.dev/python/python/docs/deployment.md)
* Deploy to Google Cloud
* Cloud Run functions

Version: 1.6

On this page

# Cloud Run functions

[Google Cloud Run Functions](https://cloud.google.com/functions) is a serverless execution environment for running simple HTTP-based web scrapers. This service is best suited for lightweight crawlers that don't require browser rendering capabilities and can be executed via HTTP requests.

## Updating the project[​](#updating-the-project "Direct link to Updating the project")

For the project foundation, use [BeautifulSoupCrawler](https://crawlee.dev/python/python/api/class/BeautifulSoupCrawler.md) as described in this [example](https://crawlee.dev/python/python/docs/examples/beautifulsoup-crawler.md).

Add [`functions-framework`](https://pypi.org/project/functions-framework/) to your dependencies file `requirements.txt`. If you're using a project manager like `poetry` or `uv`, export your dependencies to `requirements.txt`.

Update the project code to make it compatible with Cloud Functions and return data in JSON format. Also add an entry point that Cloud Functions will use to run the project.

```
import json
from datetime import timedelta

import functions_framework
from flask import Request, Response

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext
from crawlee.storage_clients import MemoryStorageClient


async def main() -> str:
    # Disable writing storage data to the file system
    storage_client = MemoryStorageClient()

    crawler = BeautifulSoupCrawler(
        storage_client=storage_client,
        max_request_retries=1,
        request_handler_timeout=timedelta(seconds=30),
        max_requests_per_crawl=10,
    )

    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        data = {
            'url': context.request.url,
            'title': context.soup.title.string if context.soup.title else None,
            'h1s': [h1.text for h1 in context.soup.find_all('h1')],
            'h2s': [h2.text for h2 in context.soup.find_all('h2')],
            'h3s': [h3.text for h3 in context.soup.find_all('h3')],
        }

        await context.push_data(data)
        await context.enqueue_links()

    await crawler.run(['https://crawlee.dev'])

    # Extract data saved in `Dataset`
    data = await crawler.get_data()
    # Serialize to json string and return
    return json.dumps(data.items)


@functions_framework.http
def crawlee_run(request: Request) -> Response:
    # You can pass data to your crawler using `request`
    function_id = request.headers['Function-Execution-Id']
    response_str = asyncio.run(main())

    # Return a response with the crawling results
    return Response(response=response_str, status=200)
```

You can test your project locally. Start the server by running:

```
functions-framework --target=crawlee_run
```

Then make a GET request to `http://127.0.0.1:8080/`, for example in your browser.

## Deploying to Google Cloud Platform[​](#deploying-to-google-cloud-platform "Direct link to Deploying to Google Cloud Platform")

In the Google Cloud dashboard, create a new function, allocate memory and CPUs to it, set region and function timeout.

When deploying, select **"Use an inline editor to create a function"**. This allows you to configure the project using only the Google Cloud Console dashboard.

Using the `inline editor`, update the function files according to your project. **Make sure** to update the `requirements.txt` file to match your project's dependencies.

Also, make sure to set the **Function entry point** to the name of the function decorated with `@functions_framework.http`, which in our case is `crawlee_run`.

After the Function deploys, you can test it by clicking the "Test" button. This button opens a popup with a `curl` script that calls your new Cloud Function. To avoid having to install the `gcloud` CLI application locally, you can also run this script in the Cloud Shell by clicking the link above the code block.

[Edit this page](https://github.com/apify/crawlee-python/edit/master/website/versioned_docs/version-1.6/deployment/google_cloud.mdx)

Last updated

<!-- -->

on **Apr 28, 2026** by **github-actions\[bot]**

[Previous](https://crawlee.dev/python/python/docs/deployment/aws-lambda.md)

[Deploy on AWS Lambda](https://crawlee.dev/python/python/docs/deployment/aws-lambda.md)

[Next](https://crawlee.dev/python/python/docs/deployment/gcp-cloud-run.md)

[Cloud Run](https://crawlee.dev/python/python/docs/deployment/gcp-cloud-run.md)


---

## [📄️<!-- --> <!-- -->Add data to dataset](https://crawlee.dev/python/python/docs/examples/add-data-to-dataset.md)

[This example demonstrates how to store extracted data into datasets using the context.pushdata helper function. If the specified dataset does not already exist, it will be created automatically. Additionally, you can save data to custom datasets by providing datasetid or datasetname parameters to the pushdata function.](https://crawlee.dev/python/python/docs/examples/add-data-to-dataset.md)


---

* [](https://crawlee.dev/python/python)
* [Examples](https://crawlee.dev/python/python/docs/examples.md)
* Adaptive Playwright crawler

Version: 1.6

