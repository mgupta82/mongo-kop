# mongo-kop

## Create Kubernetes cluster

https://github.com/kubernetes/kops/blob/master/docs/getting_started/aws.md

aws s3api create-bucket --bucket test-k8s-local-state-store --region ap-southeast-2

For gossip based cluster

export NAME=test.k8s.local
export KOPS_STATE_STORE=s3://test-k8s-local-state-store

aws ec2 describe-availability-zones --region ap-southeast-2

kops create cluster --zones=ap-southeast-2a,ap-southeast-2b,ap-southeast-2c ${NAME}

SSH public key must be specified when running with AWS (create with `kops create secret --name test.k8s.local sshpublickey admin -i ~/.ssh/id_rsa.pub`)

ssh-keygen -b 2048 -t rsa -f ~/.ssh/id_rsa

kops create secret --name test.k8s.local sshpublickey admin -i ~/.ssh/id_rsa.pub

kops edit cluster ${NAME}

kops edit ig nodes --name ${NAME}

kops get ig --name ${NAME}

kops edit ig master-ap-southeast-2a --name ${NAME}

kops update cluster ${NAME} --yes

kops validate cluster

kubectl get nodes --show-labels

kops delete cluster --name ${NAME} --yes

## Deploy on kubernetes cluster

kubectl apply -f .