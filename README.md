Localize.js SEO for Django
===============

Python Django middleware that provides full SEO support for Django apps using [Localize.js](https://localizejs.com). This middleware detects requests from search engine bots and crawlers, and replies with prerendered HTML via our hosted prerendering API.

Questions? We're happy to help. [Email us](https://localizejs.com/?modal=misc/support)!.

Installation
----------

Install via Pip: 

    pip install django_localizejs_seo

you can also install by downloading the repo and run `python setup.py install`

To add the Localize.js SEO middleware to your Django project, first add the app and middleware in your `settings.py` file:
    
    INSTALLED_APPS += ('django_localizejs_seo',)

    MIDDLEWARE_CLASSES = (
        'django_localizejs_seo.prerender.LocalizeSEOMiddleware',
    ) + MIDDLEWARE_CLASSES

Then under `settings.py`, add the following lines to enable Localize SEO and customize prerender url

    LOCALIZE_SEO_PRERENDER_URL = "https://prerender-cdn.localizejs.com/api/prerender/get"
    LOCALIZE_SEO_ENABLED = True

### How it works

When a request is made to your server using this middleware, here's what happens:

1. Middleware checks if request is a GET request. If not, middleware `returns None` is called and the middleware is bypassed.
2. Middleware checks if request is made from a search engine bot or crawler (like Googlebot). If not, `returns None` is called and the middleware is bypassed.
3. When a GET request is made to your website by a search engine bot or crawler, the middleware makes a request to our prerendering API for the prerendered HTML of the page that was requested. 
4. The prerendered HTML is received from the localizejs.com API and delivered to the search engine crawler for indexing.

This is a hosted prerendering service, meaning that the prerendering of your page and caching is offloaded to our servers.

**Performance**:

There are two built in layers of caching. We use Redis on our server to cache your HTML, and the reply is sent through the Amazon Cloudfront CDN to ensure extremely low latency response no matter where your server is (typically less than 20-50ms for a cached request).


# Contribute

Forks and pull requests welcome!

# TODO
* Add request timeout
* Add tests

# Author

[Localize.js](https://localizejs.com). For support, email [support@localizejs.com](mailto:support@localizejs.com).

