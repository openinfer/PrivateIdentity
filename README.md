# Private Identity
Private Identity artifacts

# Deploy new cluster on AWS
## Install AWSCLI
    sudo pip3 install awscli
## Configure AWS
    aws configure 
    AWS Access Key ID [None]: XXXXXXXXXXXXX
    AWS Secret Access Key [None]: XXXXXXXXXXXXXXXX
    Default region name [None]: us-east-2
    Default output format [None]:
Note: Setup awscli on your system with credentials using ACCESS-KEY-ID and SECRET-ACCESS-KEY with default region us-east-2
## Install eksctl 
    curl --location "https://github.com/weaveworks/eksctl/releases/download/latest_release/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
    sudo mv /tmp/eksctl /usr/local/bin
## Create Cluster using eksctl
    eksctl create cluster --name scott --version 1.14 --region us-east-2 --nodegroup-name standard-workers-group --node-type m5.xlarge --nodes 2 --nodes-min 2 --nodes-max 3 --node-volume-size 200 --ssh-access --ssh-public-key /home/scott/.ssh/id_rsa.pub --managed

  Note: Replace my-public-key.pub with your system public key that will help you to login into nodes and rest parameters you can choose as per your new requirements.

## Steps to put apps Into Cluster

#### 1. Import kubeconfig file from AWS
		aws eks --region us-east-2 update-kubeconfig --name scott
		kubectl  config use-context arn:aws:eks:us-east-2:301103197657:cluster/scott
#### 2. Go to location
		export pb_Home=/home/scott/pb/
		cd ${pb_Home}/kubernetes/deployment
		kubectl apply -f mandatory.yaml
		kubectl apply -f deploy_nlb.yml
        	kubectl apply -f ingress-aws.yml
		kubectl create secret tls privateidentity.org --key ./certs/privateidentity.org/privateidentity.org.key --cert ./certs/privateidentity.org/privateidentity.org.crt
        	kubectl get ing

Note: You need to change Route53 rules in aws for new nlb [network load balancer]
 
#### 3. Go to location 
		export pb_Home=/home/scott/pb
		cd ${pb_Home}/kubernetes/code/pbapp/aws
		./cluster-run.sh devel v1.2
		cd ${pb_Home}/kubernetes/code/jobscheduler/aws
		./cluster-run.sh devel v1.2

### Steps to put pbweb application Into Cluster
   
#### Go to location
		pbweb_Home=/home/scott/pb-web
		cd ${pbweb_Home}/kubernetes/aws
		kubectl apply -f ingress-devel.yml
		./cluster_run.sh devel v1.2

