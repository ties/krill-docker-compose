Preparation:
============

1: Create the docker network "web" that should be available to containers from
all docker-compose files.

```
docker network create web
```

2: Create a `.env` file that sets the relevant properties.

Set-up - Publication server:
============================

In the krill publication container, create the krill config file.
```
krillc config repo \
   --token ${KRILL_AUTH_TOKEN} \
   --data /data/ \
   --rrdp "https://rpki.example.net/rrdp/" \
   --rsync "rsync://rpki.example.net/repo/" > krill.conf
```

Set-up - Publication:
=====================

Set up the krill instance (not krill_publish) to publish to the krill_publish
instance. This is [remote publishing](https://rpki.readthedocs.io/en/latest/krill/remote-publishing.html#doc-krill-remote-publishing).

```
krillc publishers add --publisher zz-example-prepdev --rfc8183 ./data/ca-pub-req.xml
krillc repo request --ca zz-example-prepdev
```
