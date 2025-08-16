Initially, Infrastructure has been created with relevant 
IAM roles and VPC with EC2 (pre-installed Jenkins) using Main.tf file in Terraform. 

In Jenkins, Application has been successfully build. 
it has been pushed into the Docker respository. 

Using Jenkinsfile, Build image has been successfully deployed into EKS
Cluster with application Load balancer ARN.

Configured Setup for monitoring system to check the health of the cluster.  
