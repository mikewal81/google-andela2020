# LAB: Google Cloud Fundamentals - Getting Started with GKE

## Objectives
   In this lab, you learn how to perform the following tasks:
   
    - Provision a Kubernetes cluster using Kubernetes Engine.
   
    - Deploy and manage Docker containers using kubectl.

## Steps
1. Confirm that needed APIs are enabled       

    i. Check for the enabled cloud services in this project         
    
        gcloud services list      
         
    ii. If Kubernetes Engine API and Container Registry API are not enabled, enable them with these commands       
    
        gcloud services enable container.googleapis.com       
        
        gcloud services enable containerregistry.googleapis.com          
        
        OR             
        
        gcloud services enable container.googleapis.com containerregistry.googleapis.com     

2. Start a Kubernetes Engine cluster           

    i. Place the zone that Qwiklabs assigned you to into an environment variable called MY_ZONE:         
        (Currently My Zone is us-central1-a. You can replace my zone with the zone your poroject is in)        
        
        export MY_ZONE=us-central1-a
        
    ii. Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster webfrontend and configure it to run 2 nodes:             
    
        gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2
        
    iii. Check your installed version of Kubernetes using the kubectl version command:           
    
        kubectl version
        
    iv. List all the VM instances in the current project          
    
        gcloud compute instances list

3. Run and deploy a container    

    i. Launch a single instance of the nginx container:        
    
        kubectl create deploy nginx --image=nginx:1.17.10
    
    ii. View the pod running the nginx container:         
    
        kubectl get pods
        
    iii.  Expose the nginx container to the Internet:        
    
        kubectl expose deployment nginx --port 80 --type LoadBalancer
        
    iv. View the new service:       
    
        kubectl get services
        
    v. Open a new web browser tab and paste your cluster's external IP address into the address bar:        
    
        RESULT : The default home page of the Nginx browser is displayed.
        
    vi. Scale up the number of pods running on your service:       
    
        kubectl scale deployment nginx --replicas 3
        
    vii. Confirm that Kubernetes has updated the number of pods:      
    
        kubectl get pods
        
    viii. Confirm that your external IP address has not changed:       
    
        kubectl get services
        
    ix. Return to the web browser tab in which you viewed your cluster's external IP address. Refresh the page to confirm that the nginx web server is still responding:       
    
        RESULT : The default home page of the Nginx browser is displayed.
