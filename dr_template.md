# Infrastructure

## AWS Zones
| Region | Availability Zones   |
|--------|----------------------|
| us-east-2|us-east-2a, us-east-2b, us-east-2c|
| us-west-1|us-west-1b, us-west-1c|

## Servers and Clusters

### Table 1.1 Summary
| Asset      | Purpose           | Size                                                                   | Qty                                                             | DR                                                                                                           |
|------------|-------------------|------------------------------------------------------------------------|-----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| Asset name | Brief description | AWS size eg. t3.micro (if applicable, not all assets will have a size) | Number of nodes/replicas or just how many of a particular asset | Identify if this asset is deployed to DR, replicated, created in multiple locations or just stored elsewhere |
| Ubuntu-Web | EC2 | t3.micro | 3 instances | Deployed to two regions, us-east-2 and us-west-1 |
| udacity-project | VPC | NA | 1 | IPs in multiple AZs |
| udacity-cluster | EKS Cluster | NA | 2 nodes | 2 node replica set |
| udacity-lb-tf | ALB Load Balancer | NA | One in each zone  |  |
| udacity-db-cluster | Aurora MySQL DB Cluster | db.t2.small | 2 clusters in 2 regions | geo replication is configured between the cluster in zone1 and zone2, each cluster has 2 nodes in the appropriate AZs |
| ec2_sg | Security Group | NA | One for each zone | Ensure this security group is identical in each zone in case a failover is needed |
| Prometheus | Monitoring stack | NA | One for us-east-2 |Collect metrics and visualize data to Grafana dashboard, running on EKS |

### Descriptions
| Asset     | Description                                              |
|-----------|----------------------------------------------------------|
| Ubuntu-Web (EC2) | EC2s are AWS services that run and manage virtual machines in the AWS cloud. EC2 instances are the main VMs that are running our application.|
| udacity-project (VPC) | VPCs enables a logically isolated area of AWS cloud.  This VPC will be used to launch AWS resources, including our EC2s in this virtual network |
| udacity-cluster (EKS) | EKS is the AWS managed Kubernetes control plane.  This cluster is used to run a Highly Available and scalable cluster of services |
| udactiy-lb-tf (ALB)| Load balancers are used to automatically scale capacity based on traffic.  This load balancer is used to balance the load between our EC2 intances |
| udacity-db-cluster (rds) | RDS is an AWS managed database service. Our db cluster is based a postgres database platform and is being used to store our application data | 
| ec2_sg (Security Group) | AWS Security Groups control inbound and outbound traffic to AWS resources.  This security group will be used to control access to our VPC and EC2 instances to ensure only the proper access is occurring |

## DR Plan
### Pre-Steps:
1) Ensure that our infrastructure is setup and working in the DR site.
2) Both site are same configuration
3) Enable database replication to DR site
4) Configure backup and retention


## Steps:
1) Point the DNS to load balancer in DR site
2) Perform database failover by AWS console
