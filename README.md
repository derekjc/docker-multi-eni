# docker-multi-eni

# Assumptions
- You are running Amazon Linux
- You have docker installed
- You have 2 ENIs and what to host 1 docker container behind each ENI.

1. Copy docker to /etc/init.d
2. Copy the remaining files to /etc/sysconfig/network-scripts. This will overwrite ec2net-functions.
3. Create the required symlinks:
```    
ln -s /etc/sysconfig/network-scripts/ifup-local /sbin/
ln -s /etc/sysconfig/network-scripts/ifdown-pre-local /sbin
```
4. Ensure that the above scripts are executable.
5. Restart docker. This will add some iptable rules. See diff of the docker script for details.
6. Attach an ENI to the instance. If the first above steps were done correctly, you should have additional iptable rules as well as route table lookups.
7. Launch your containers as usual with individual ENI private IPs and ports.
