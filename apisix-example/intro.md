# Getting Started

This article is a quick start guide for Apache APISIX. The Quick Start is divided into the following three steps:

1. Install Apache APISIX via Docker Compose.
2. Create a route and bind it with a Upstream.
3. Use curl command to verify that the results returned after binding are as expected.

In addition, this article provides some advanced operations on how to use Apache APISIX, including adding authentication, prefixing Route, using the APISIX Dashboard, and troubleshooting.

We will use the following echo endpoint as an example, which will return the parameters we passed.

### Request

The request URL consists of these components:
![requesturl](https://cdn.jsdelivr.net/gh/apache/apisix@release/2.11/docs/assets/images/requesturl.jpg)

- Protocol: the network transport protocol, HTTP protocol is used in our example.
- Port: The port, 80 is used in our example.
- Host: The host, httpbin.org is used in our example.
- Path: The path, /get is used in our example.
- Query Parameters: the query string, two strings foo1 and foo2 are listed in our example.

### Response

<pre>
<code class="language-json hljs">
{
  "args": { "foo1": "bar1", "foo2": "bar2" },
  "headers": {
    "Accept": "*/*",
    "Host": "httpbin.org",
    "User-Agent": "curl/7.29.0",
    "X-Amzn-Trace-Id": "Root=1-6088fe84-24f39487166cce1f0e41efc9"
  },
  "origin": "58.152.81.42",
  "url": "http://httpbin.org/get?foo1=bar1&foo2=bar2"
}
</code>
</pre>

## Pre-requisites

For this particular tutorial you don't need to install any pre-requisites. However the following are required when using on your local machine.

- Installed Docker and Docker Compose component.
- We use the curl command for API testing. You can also use other tools such as Postman for testing.
