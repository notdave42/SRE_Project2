# Infrastructure

## AWS Zones
Identify your zones here

The production environment is in us-east-2 and the DR environment is in us-west-1

## Servers and Clusters

### Table 1.1 Summary
| Asset      | Purpose           | Size                                                                   | Qty                                                             | DR                                                                                                           |
|------------|-------------------|------------------------------------------------------------------------|-----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| Asset name | Brief description | AWS size eg. t3.micro (if applicable, not all assets will have a size) | Number of nodes/replicas or just how many of a particular asset | Identify if this asset is deployed to DR, replicated, created in multiple locations or just stored elsewhere |
| VM | Web servers for the site. | t3.micro | 3 instances (EC2) |
| Kubernetes Cluster | Resources for running Grafana and Prometheus monitoring tools. | 2 nodes (EKS) | Created in multiple locations |
| VPC | Allows communication between nodes and externally| One VPC per availablity zone| Created in each region. |
| ALB | Allows connectivity to web servers and allows failover| One ALB per region | Created in each region. |



### Descriptions
More detailed descriptions of each asset identified above.
3 EC2 instances running the website
SSH keys for administering the EC2 instances
GitHub repo for storing the Terraform code
Backend database running on 3 Amazon RDS nodes for the website
Database backups stored in S3 for recovery
Redis backend for caching
Load balancer for the website
Kubernetes cluster for monitoring stack
Monitoring platform (Grafana and Prometheus) for the web application

3 web servers in each region, one in each availablility zone, for serving the web site.
2 Kubernetes clusters one in each region, with 3 nodes each for running the Grafana and Prometheus resources.
2 ALB - load balancers one for each region.  The load balancers will distribute traffic across the 3 web servers in each region. 
2 VPCs - each region will have a vpc to allow traffic between the resources listed above.

## DR Plan
### Pre-Steps:
List steps you would perform to setup the infrastructure in the other region. It doesn't have to be super detailed, but high-level should suffice.

The web servers in the DR region would be built with Terraform using the same image files as the production servers.  The Kubernetes cluster would be built using the Terraform charts with the variables updated for the DR environment.   Grafana and Prometheus will be installed using the Helm charts that were used for the Kubernetes cluster in the production environment.
The ALB load balancers will be configured to distribute the load across the 3 web servers in the DR region.  They will be configured using Terraform with the same templates as were used in production updated with the varibles for the DR environment.
The VPC in the DR region will be set up to allow the same connectivity as the VPC in the production region.  The VPC will be configured using Terraform with variables updated for the DR environment.  

## Steps:
You won't actually perform these steps, but write out what you would do to "fail-over" your application and database cluster to the other region. Think about all the pieces that were setup and how you would use those in the other region

The primary DNS information would be updated to point to the DR ALB IP Address to allow access to web servers in the DR region.  The database cluster would be failed over by promoting the secondary node to primary in the cluster. 