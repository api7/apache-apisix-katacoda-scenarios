# Step 3: Validation

We have created the route and the Upstream service and bound them. Now let's access Apache APISIX to test this route.

`curl -i -X GET "http://127.0.0.1:9080/get?foo1=bar1&foo2=bar2" -H "Host: httpbin.org"`{{execute}}

It returns data from our Upstream service (actually httpbin.org) and the result is as expected.
