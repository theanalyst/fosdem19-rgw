## Index

+ RGW 
  - Introduction
+ Multisite
+ Sync Modules
  - Basic Idea
  - ES
  - Cloud Sync
  - Archive
  - Pub/Sub

---

## RGW
+ Object storage client to the ceph cluster, exposes a RESTFUL S3 & Swift API

![rgw](img/rgw.png)


--

+ A RESTful API access to object storage
+ Immutable objects, not 1:1 mapped to rados objects
+ Implements user accounts, acls, buckets
+ heavy ecosystem of s3/swift client tooling can be leveraged against RGW

--

+ Supports a lot of S3/swift like features
  - Multipart uploads
  - Object Versioning
  - torrents
  - lifecycle
  - encryption
  - compression
  - static websites
  - metadata search...
+ From Jewel we support multisite which allows geographical redundancy

---

## Multisite

+ Geographical redundancy with async data replication*
+ Data is replicated across zones, within zonegroups. Realms can
  partition data in to namespaces.
+ There is a master zone which will be the source of truth for all
  metadata
+ Built on principle that data changes are frequent, metadata changes
  not so much
+ Data CP in local cluster, AP in remote

--

+ Under the hood, done via logs for data, metadata changes and then
  the remote zone syncs the objects.
+ Since we have the ability to notify the remote zone on data changes,
  can we utilize this for further external services?


---

## Sync Modules
+ Built atop of multisite
+ Leverages async metadata and data logs to decide on further actions
+ Modules can define whether they export data or only consume data.
+ Multisite itself is a default 'sync module'
+ Currently requires in-tree builds {C++} 

--

+ Require their own zone 
+ Allows for integrating external services based on data/metadata in
  RGW
+ For getting started writing one look at the log sync module

---

### ElasticSearch

+ Sends object metadata to elasticsearch
+ Exposes a end-user api to forward queries to ES
+ Also get an overview of interesting object storage trends with ES queries

--

<img src="img/rgw-es.svg" width=200%></img>

---

### Cloud Sync Module

+ Back up to a different cloud with s3 like apis (S3 itself?)
+ A cloud provider redundancy of sorts, useful for critical data backups
+ Configurable mapping for buckets/users

---

### Archive Sync Module

+ Archives every object (uses object versioning)
+ Allows for only one cluster to be an archive cluster with other
  clusters free to delete the different object versions over time

---

### Pub Sub 

+ Subscribe to notifications on modification events for a topic
+ Object create/delete [marker] events supported
+ Push Notifications (HTTP & AQMP) coming soon

---

- https://github.com/ceph/ceph - upstream Ceph project
- https://ceph.com/IRC/ - Ceph upstream community mailing lists and IRC channels `#ceph`, `#ceph-devel` on OFTC

