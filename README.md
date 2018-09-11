# local-kafka

Start your own single broker kafka cluster locally making it accessible to other
local services via sharing the network "local-kafka"

```
docker-compose up -d
```
(!) Make sure to start the kafka cluster before starting your app service, or the network will not be found and you see this error:
```
ERROR: Network local-kafka declared as external, but could not be found.
```
---
To access the cluster, just modify your docker-compose.yml:

* Declare the network at the bottom of your docker-compose.yml

So a full example docker-compose.yml would look like:
```
version: '3'

services:
  producer:
    image: alpine:latest
    command: ping kafka

networks:
  default:
    external:
      name: local-kafka
```
Then you can access the cluster from inside your service via dns name "kafka", e.g.:
```
docker-compose run producer ping kafka
```
