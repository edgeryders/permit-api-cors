# permit-api-cors Discourse plugin

Make [Discourse](https://www.discourse.org/) accept the "Api-Key:" HTTP header in CORS requests.


## Description

By default, Discourse does not support authentication with the "`API-Key:`" HTTP header in CORS requests. It only supports that authentication method on non-CORS requests. Non-CORS requests are basically any requests sent by a user agent that is not a browser, for example the default requests sent by `curl` unless you add specific headers to make it a CORS request.

In some circumstances, such as our [tool to post survey responses to Discourse](https://github.com/edgeryders/edgeryders-form), that limitation has to be lifted. That's what this plugin does. Now you can use Discourse's so-called "Admin API" keys with JavaScript applications used inside a web browser.


## Installation

1. Make sure you have a recent Discourse version. In the `stable` branch, only recent (approx. 2019-10-01) Discourse versions support authentication with an `Api-Key:` HTTP header at all. In the `master` branch, this was introduced somewhat earlier. Older versions only support API key authentication as a GET parameter, which is obviously not possible for POST etc. requests.

2. Install the plugin as any other Discourse plugin. In a standalone ("no Docker") installation this is simply:

    ```
    cd plugins/
    git clone https://github.com/edgeryders/permit-api-cors.git
    ```

3. Restart your Discourse web server to enable the plugin.


## Security considerations

**Not a risk per se.** Note that this is not more of a security risk than listing any website as an allowed CORS origin in your Discourse installation. In all cases, the Discourse admin has to make sure before that the site is trustable. The authentication method it uses to connect to Discourse, as such, does not make a site trustable or untrustable.

**Never embed API keys into your application!** This plugin is *not* meant to enable you to put an API key (or even the Discourse master API key) into your JavaScript web application or mobile application. Doing so is a severe security risk, as the key can be extracted from it. Instead, your application has to obtain the API key at runtime, either by letting the user enter their own API key, or by creating a new Discourse account together with an API key.
