# Tech Stack

[minikube](https://github.com/kubernetes/minikube)  Minikube is a tool that makes it easy to run Kubernetes locally. Minikube 
runs a single-node Kubernetes cluster inside a VM on your laptop for users looking to try out Kubernetes or develop with it day-to-day.  
kubectrl    
[kops](https://github.com/kubernetes/kops) The easiest way to get a production grade Kubernetes cluster up and running.  
[helm](https://helm.sh/) The package manager for Kubernetes. Think of it as kubectl for clusters.    
[ingress](https://github.com/kubernetes/ingress) Provides services with externally-reachable urls, load balancing, 
terminate SSL, offer name based virtual hosting etc.          

## View logs of a pod

    kubctrl log -f <podName>

## Useful aliases for working with kubernetes

    # Spin up a box which allows you to run curl to test things from within the cluster      
    alias busybox='kubectl delete deploy/busybox; kubectl run -i --rm --tty busybox --image=radial/busyboxplus:curl -- sh'

## Installing and configuring kops
    
    # Installing OSX using brew
    brew update && brew install kops
    
    # Create an access key using the aws console
    # aws.amazon.com -> IAM -> Users -> you -> Security Credentials
    
    # Create a ~/.aws/credentials file with the following contents
    [default]
    aws_access_key_id=<your id here>
    aws_secret_access_key=<your key here>
    
    kops export kubecfg <CLUSTER_DOMAIN> --state s3://<KOPS_CLUSTER_CONFIG_BUCKET>
    
    ## Ingress
    
    # Configure DNS
    Add a wildcard route53 entry as a CNAME of the AWS ELB that was created for the ingress gateway (i.e. Kong in the infrastructure namespace).
    
    # Create API in Kong for a service ingress
    kubectl port-forward $(kubectl get po -o name | grep inggw-kong | sed 's/.*\///g') 8001
    curl -X POST http://localhost:8001/apis -H 'Content-Type: application/json' -d '{"name": "<SERVICE_NAME>", "hosts": "<FULLY_QUALIFIED_INGRESS_HOSTNAME>", "upstream_url": "http://<SERVICE_NAME>"}'
    curl -X POST http://localhost:8001/upstreams -H 'Content-Type: application/json' -d '{"name": "<SERVICE_NAME>"}'
    curl -X POST http://localhost:8001/upstreams/<SERVICE_NAME>/targets -H 'Content-Type: application/json' -d '{"target": "<SERVICE_IP>:<SERVICE_PORT>"}'
    
    
    # Get a password from a secret
    kubectl get secret -n infra metricviz-grafana -o yaml
    
    # Decode the password
    echo -n "<USERNAME>" | base64 -D
    echo -n "<PASSWORD>" | base64 -D
    
## Installing Elasticsearch 

    Steps to install Elasticsearch into
    
    https://github.com/elastic/rally 