# oke-nginx
About
=====

This repository contains steps to deploy Kubernetes cluster on Oracle Cloud Infratstructure.

Prerequisites
=============
1. Create a Free Tier OCI Account
2. Create User, compartment, VCN, Subnet, SSh keys

Steps
=====

1. From the OCI Services menu, click Developer Services > Kubernetes Clusters (OKE).
 
  a. Choose Quick Create and click Launch Workflow
  b. Fill out the dialog box:

      Name: Provide a name (oke-cluster in this example)
      Compartment: Choose your compartment
      Kubernetes Version: Choose the most recent version
      Kubernetes API Endpoint: Public Endpoint
      Kubernetes Worker Nodes: Private Workers
      Shape: VM.Standard.E3.Flex
      Number of nodes: 1
    Click Next
  c. Click "Create Cluster". Wait for cluster to be deploy.
2. Install Kubectl
  a. mkdir -p $HOME/.kube; cd $HOME/.kube; curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.15.0/bin/windows/amd64/kubectl.exe
  b. Run kubectl get nodes, kubectl get namespaces,  kubectl get pods --all-namespaces -o wide to verify cluster is deployed and pods are spin up in kube-  system namespace
3. Run kubectl run nginx  --image=nginx --port=80 to spin nginx pod
  a. Run kubectl get pods -o wide to verify nginx pod is deployed
4. Run kubectl expose pod nginx --port=80 --type=LoadBalancer to expose the service to internet. This will spin up a load balancer on OCI and which in turn will expose the service to internet
5. Go to OCI console, Networking > Load Balancers and fetch the public IP of load balancer. 
  a. Open a new browser tab and enter URL http://<Load-Balancer-Public-IP>. The Nginx welcome screen should be displayed.
