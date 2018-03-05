vpc subnet

reserved address, use 10.0.00/24 as an example

* `10.0.0.0`: Network address.

* `10.0.0.1`: Reserved by AWS for the VPC router.

* `10.0.0.2`: Reserved by AWS. The IP address of the DNS server is always the base of the VPC network range plus two; however, we also reserve the base of each subnet range plus two. For VPCs with multiple CIDR blocks, the IP address of the DNS server is located in the primary CIDR. For more information, see[Amazon DNS Server](https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_DHCP_Options.html#AmazonDNS).

* `10.0.0.3`: Reserved by AWS for future use.

* `10.0.0.255`: Network broadcast address. We do not support broadcast in a VPC, therefore we reserve this address.

![](/assets/vpc_diagram.png)



ACL

ACL is stateless

block IP addresses using ACL not security group

