Initially, Infrastructure has been created with relevant IAM roles andVPC
with EC2 (pre-installed Jenkins) using Main.tf file in Terraform. 

In Jenkins, Application has been successfully build and pushed into the Docker respository as per
Project requirements. 

Using Jenkinsfile, Build image has been successfully deployed into EKS
Cluster with application Load balancer ARN.

Configured Setup for monitoring system to check the health of the cluster.  
