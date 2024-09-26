# Create a eks cluster dedicated VPC
# Create IAM Role(EksClusterRole) in AWS
      Entity Type->Aws Service, Use Case->EKS->EKS Cluster
      Role Name->EksClusterRole
# Create cluster using created VPC and IAM(EksClusterRole) role
### cluster endpoint access: public and private
# Create Ec2 Instance(k8s client machine) in different vpc
## Install kubectl on EC2 instance
## Install AWS Cli on EC2 instance
## Configure Aws Cli with Credentials
#### Note: we can use root user accesskey and secret key access
#### Note: If ec2(where install kubectl) and cluster not in same vpc so need to update remote machine(ec2 instance) by this command:
########### update kubeconfig file in remote machine from cluster using bellow
######## aws eks update-kubeconfig --name <cluster-name> --region <region_name>
# Create Iam role(EksWorkerNode) for Eks workder nodes(usecase EC2) with bellow polices
###   1. AmazonEKSWorkerNodePolicy
      2. AmazonEKS_CNI_Policy
      3. AmazonEC2ContainerRegistryReadOnly
# Create worker Node Group
      Go ot cluster->Compute->Node Group
      ->Select the Role we have created for workerNodes
      ->Use t2.large
      ->Min 2 and Max 2
# Once Node Group added then check node in k8s_client_machine
      $ kubectl get nodes
      $ kubectl get pods --all-namespaces
# Create POD and expose the POD using NodePort Service/LoadBalancer
### Note: Enable node port in secutriy Group to access than in out browser
      $ kubectl get pods
      $ kubectl get deployment
      $ kubectl get svc
      $ kubectl get pods -o wide
### Try to access from browser by loadbalancer DNS
