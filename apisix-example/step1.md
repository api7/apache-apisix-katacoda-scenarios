# Step 1: Install Apache APISIX#

Run the following commands to install APISIX and start APISIX.

`git clone https://github.com/apache/apisix-docker.git`{{execute}}

`cd apisix-docker/example`{{execute}}

`docker-compose -p docker-apisix up -d`{{execute}}

> Apache APISIX has already supported ARM64 architecture. For ARM64 users, please use `docker-compose -p docker-apisix -f docker-compose-arm64.yml up -d` instead in the last step.

It will take some time to download all required files, please be patient.

Once the download is complete, execute the `curl` command on the host running Docker to access the Admin API, and determine if Apache APISIX was successfully started based on the returned data.

`curl "http://127.0.0.1:9080/apisix/admin/services/" -H 'X-API-KEY: edd1c9f034335f136f87ad84b625c8f1'`{{execute}}

The following data is returned to indicate that Apache APISIX was successfully started:

<pre>
{
  "count": 1,
  "action": "get",
  "node": { "key": "/apisix/services", "nodes": {}, "dir": true }
}
</pre>
