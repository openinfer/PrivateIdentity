# Private Identity
Private Identity artifacts

# Deploy new cluster on AWS
## Install AWSCLI
  pip install awscli
## Configure AWS
  aws configure 
Note: setup awscli on your system with credentials using ACCESS-KEY-ID and SECRET-ACCESS-KEY
## Install eksctl 
  curl --silent --location "https://github.com/weaveworks/eksctl/releases/download/latest_release/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
  sudo mv /tmp/eksctl /usr/local/bin
## Create Cluster using eksctl
  eksctl create cluster --name test --version 1.14 --region us-east-2 --nodegroup-name standard-workers-group --node-type m5.xlarge --nodes 2 --nodes-min 2 --nodes-max 3 --node-volume-size 200 --ssh-access --ssh-public-key my-public-key.pub --managed

  Note: Replace my-public-key.pub with your system public key that will help you to login into nodes and rest parameters you can choose as per your new requirements.


  
