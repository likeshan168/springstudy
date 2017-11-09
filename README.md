**Messaging with Redis**

for the details, please refer to 

https://spring.io/guides/gs/messaging-redis/me

Note: as we know, PUB/SUB feature already existed in redis

we can do this as the below

1.  start the redis server by running redis-server
2.  open two client and type redis-cli to connect the redis server
3.  in the first client, input SUBSCRIBE first second
4.  in the second client, input PUBLISH second hello
5.  the hello will be seen in the first client