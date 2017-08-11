# Tech Stack

[minikube](https://github.com/kubernetes/minikube)  Minikube is a tool that makes it easy to run Kubernetes locally. Minikube 
runs a single-node Kubernetes cluster inside a VM on your laptop for users looking to try out Kubernetes or develop with it day-to-day.  
kubectrl    
[kops](https://github.com/kubernetes/kops) The easiest way to get a production grade Kubernetes cluster up and running.  
[helm](https://helm.sh/) The package manager for Kubernetes. Think of it as kubectl for clusters.    
[ingress](https://github.com/kubernetes/ingress) Provides services with externally-reachable urls, load balancing, 
terminate SSL, offer name based virtual hosting etc.          

## Installing and configuring kops
    
    # Installing OSX using brew
    brew update && brew install kops
    
    # Create an access key using the aws console
    # aws.amazon.com -> IAM -> Users -> you -> Security Credentials
    
    # Create a ~/.aws/credentials file with the following contents
    [default]
    aws_access_key_id=<your id here>
    aws_secret_access_key=<your key here>
    
    kops export kubecfg dev.wesbank.ekyc.co.za --state s3://wesbank-kyc-clusterconfig
       