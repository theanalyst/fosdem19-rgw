## RGW
+ Object storage client to the ceph cluster, exposes a RESTFUL S3 & Swift API

![rgw](img/rgw.png)


--

### RGW
+ A RESTful API access to object storage, a la S3 
+ implements user accounts, acls, buckets
+ heavy ecosystem of s3/swift client tooling can be leveraged against RGW

---

### RGW
+ Supports a lot of S3 like features
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

## Sync Modules
+ Built atop of multisite
+ Leverages async metadata and data logs to decide on further actions
+ Multisite itself is a default 'sync module'
+ Currently requires in-tree builds 

---

## ElasticSearch

+ Sends object metadata to elasticsearch
+ Exposes a end-user api to forward queries to ES
+ Also get an overview of interesting object storage trends with ES queries
> How busy is my object storage on friday evenings?

--

<img src="img/rgw-es.svg" width=200%></img>

---

## Archive Sync Module

+ Archives every object (uses object versioning)
+ Allows for only one cluster to be an archive cluster with other clusters free
  to delete the different object versions over time
  
---

## Cloud Sync Module

+ Back up to a different cloud with s3 like apis (S3 itself?)
+ Configurable mapping for buckets/users 

---

## Pub Sub 

+ Subscribe to notifications on modification events

---

- wiki: https://en.opensuse.org/openSUSE:Ceph
- [opensuse-ceph@opensuse.org](mailto:opensuse-ceph@opensuse.org) - Discussion of Ceph specifically on openSUSE related queries
- https://ceph.com/IRC/ - Ceph upstream community mailing lists and IRC channels
- http://lists.suse.com/mailman/listinfo/deepsea-users - DeepSea upstream mailing list. 
- https://groups.google.com/forum/#!forum/openattic-users - openATTIC upstream mailing list. 
- https://github.com/ceph/ceph - upstream Ceph sources 

