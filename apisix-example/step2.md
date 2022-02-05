# Step 2: Create a Route#

Now we have a running instance of Apache APISIX! Next, let's create a Route.

## How it works

Apache APISIX provides users with a powerful Admin API and APISIX Dashboard. In this article, we use the Admin API to walk you through the procedures of creating a Route.

We can create a Route and connect it to an Upstream service(also known as the Upstream). When a Request arrives at Apache APISIX, Apache APISIX knows which Upstream the request should be forwarded to.

Because we have configured matching rules for the Route object, Apache APISIX can forward the request to the corresponding Upstream service. The following code is an example of a Route configuration:

<pre>
{
  "methods": ["GET"],
  "host": "example.com",
  "uri": "/services/users/*",
  "upstream": { "type": "roundrobin", "nodes": { "httpbin.org:80": 1 } }
}
</pre>

This routing configuration means that all matching inbound requests will be forwarded to the Upstream service httpbin.org:80 when they meet all the rules listed below:

- The HTTP method of the request is GET.
- The request header contains the host field, and its value is example.com.
- The request path matches /services/users/_, _ means any subpath, for example /services/users/getAll?limit=10.

Once this route is created, we can access the Upstream service using the address exposed by Apache APISIX.

`curl -i -X GET "http://{APISIX_BASE_URL}/services/users/getAll?limit=10" -H "Host: example.com"`{{execute}}

This will be forwarded to `http://httpbin.org:80/services/users/getAll?limit=10` by Apache APISIX.

## Create an Upstream

After reading the previous section, we know that we must set up an Upstream for the Route. An Upstream can be created by simply executing the following command:

`curl "http://127.0.0.1:9080/apisix/admin/upstreams/1" -H "X-API-KEY: edd1c9f034335f136f87ad84b625c8f1" -X PUT -d '{ "type": "roundrobin", "nodes": { "httpbin.org:80": 1 }}'`{{execute}}

We use roundrobin as the load balancing mechanism, and set httpbin.org:80 as our upstream target (Upstream service) with an ID of 1. For more information on the fields, see Admin API.

> Creating an Upstream service is not actually necessary, as we can use Plugin to intercept the request and then respond directly. However, for the purposes of this guide, we assume that at least one Upstream service needs to be set up.

## Bind the Route to the Upstream

We've just created an Upstream service (referencing our backend service), now let's bind a Route for it!

`curl "http://127.0.0.1:9080/apisix/admin/routes/1" -H "X-API-KEY: edd1c9f034335f136f87ad84b625c8f1" -X PUT -d '{ "uri": "/get", "host": "httpbin.org", "upstream_id": "1"}'`{{execute}}
