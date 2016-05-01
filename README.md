# javy
A simple java application deployment for a POC.

> Automate evrything, because there is no reason to do it twice.

## Technologies used
* [vagrant](https://www.vagrantup.com/downloads.html)
* [Fedora 23 Cloud Image](https://getfedora.org/cloud/)
* [ansible](https://www.ansible.com/)
* [docker](http://www.docker.com)

Using this technologies I have created 2 docker images (One based on [jetty](https://hub.docker.com/_/jetty/) and the other based on [nginx](https://hub.docker.com/_/nginx/)) which in combination with systemd and nfs in the case of the multivm create a simple deployment POC.

## Usage
For a single vm deployment use:
```bash
cd /path/to/this/repo
vagrant up --provision
```

For a multi vm deployment use:
```bash
cd /path/to/this/repo
VAGRANT_VAGRANTFILE=Vagrantfile-multivm vagrant up --provision
```

After turnning on the vms you will be able to see the page at [http://192.168.33.10](http://192.168.33.10).

> TIP: in a multivm deployment you can see the [haproxy](http://www.haproxy.org/) status page at [http://192.168.33.10/haproxy](http://192.168.33.10/haproxy).

## Cleanup

```bash
cd /path/to/this/repo
vagrant destroy -f
```

For a multi vm deployment use:
```bash
cd /path/to/this/repo
VAGRANT_VAGRANTFILE=Vagrantfile-multivm vagrant destroy -f
```

## Future improvements
Here I'll list some of the improvements that come quickly to my mind right now.
### Without Modifying the application
* Replace NFS by a more cloud friendly distributed filesystem like:
  * [GlusterFS](http://www.gluster.org/)
  * [CephFS](http://ceph.com/)
  * [XtreemFS](http://www.xtreemfs.org/)
  * [Amazon EFS](https://aws.amazon.com/documentation/efs/)
* Replace ansible deployment by:
  * [Docker Swarm Deployment](https://docs.docker.com/swarm/)
  * [Google Kubernetes Deployment](http://kubernetes.io/) / [Openshift Deployment](https://www.openshift.org/)
  * [Mesosphere Deployment](https://mesosphere.com/) / [Apache Aurora Deployment](http://aurora.apache.org/)
  * [CoreOS Deployment](https://coreos.com/)
  * [Amazon ECS](http://docs.aws.amazon.com/AmazonECS/latest/developerguide/Welcome.html)
* Replace haproxy with [Amazon ELB](https://aws.amazon.com/es/elasticloadbalancing/) + [Autoscaling Group](https://aws.amazon.com/autoscaling/)
* Any CDN for static assests
* Replace static assets hosting in nginx with an Amazon S3 Based alternative
* Better versioning for the app. This simplifies rollback in case of needed.
### Modifying the app
* make the app more cloud friendly following the [12factor.net](http://12factor.net/) recommendations.
* Use highly scallable persistence layer like any JDBC compatible database or any NoSQL databases like [Cassandra](http://cassandra.apache.org/), [Hazelcast](https://hazelcast.com/use-cases/application-scaling/), or even [Redis](http://redis.io/). This is more a dev decision than mine.
* Use [Amazon Lambda](https://aws.amazon.com/lambda/details/) in combination with the previuos modifications to create a NoServer deployment restful app.

> Any suggestion is more than Welcome.
