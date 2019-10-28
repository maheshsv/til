# Amazon VPC

Here is an excellence video explaining the design of Amazon VPC: [A Day in the Life of a Billion Packets](https://www.youtube.com/watch?v=Zd5hsL-JNY4).

Here is the [documentation](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html).

## Key concepts

**VPC**: virtual network dedicated to your AWS account. You can specify IP address range, add subnets, associate security groups, and configure route table.

**subnet**: a range of IP addresses in your VPC. There are public and private subnets. Public subnet has a route to an Internet gateway.

**route table**: a set of rules/routes used to determine where network traffic is directed.

**internet gateway**: highly available VPC component allows communication between instances in VPC and internet.

**VPC endpoint**: enable private connect VPC to supported AWS services.

