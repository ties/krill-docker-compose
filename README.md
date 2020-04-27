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

In the krill publication container, create the krill config file. Make sure that
you copy it outside the container and update `krill_publish/krill.conf` with it.
```
krillc config repo \
   --token ${KRILL_AUTH_TOKEN} \
   --rrdp "https://${KRILL_FQDN}/rrdp/" \
   --rsync "rsync://${KRILL_FQDN}/repo/" \
   --data /data/ > krill_config.conf
```

Set-up - Publication:
=====================

Set up the krill instance (not krill_publish) to publish to the krill_publish
instance. This is [remote publishing](https://rpki.readthedocs.io/en/latest/krill/remote-publishing.html#doc-krill-remote-publishing).

```
krillc publishers add --publisher zz-example-prepdev --rfc8183 ./data/ca-pub-req.xml
krillc repo request --ca zz-example-prepdev
```
