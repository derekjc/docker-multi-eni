# docker-multi-eni

## Assumptions
- You are running Amazon Linux
- You have docker installed
- You have 2 ENIs and what to host 1 docker container behind each ENI.

## How to use these files

* Copy docker to /etc/rc.d/init.d
* Copy the remaining files to /etc/sysconfig/network-scripts. This will overwrite ec2net-functions.
* Create the required symlinks:
```    
ln -s /etc/sysconfig/network-scripts/ifup-local /sbin/
ln -s /etc/sysconfig/network-scripts/ifdown-pre-local /sbin
```
* Ensure that the above scripts are executable.
* Restart docker. This will add some iptable rules. See diff of the docker script for details.
* Attach an ENI to the instance. If the first above steps were done correctly, you should have additional iptable rules as well as route table lookups.
* Launch your containers as usual with individual ENI private IPs and ports.
