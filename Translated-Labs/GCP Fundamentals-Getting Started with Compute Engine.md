# LAB: Google Cloud Fundamentals - Getting Started with Compute Engine

## Objectives
   In this lab, you will learn how to perform the following tasks:
   
    - Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.
   
    - Create a Compute Engine virtual machine using the gcloud command-line interface.
   
    - Connect between the two instances.
    
## Steps 
1. Create a virtual machine using the GCP Console. 
    gcloud compute instances create my-vm-1 --tags http
    gcloud compute firewall-rules create allow-http --destination=INGRESS --rules=http:80 --target-tags=http

2. Create a virtual machine using the gcloud command line.
    gcloud compute zones list | grep us-central1
    gcloud config set compute/zone us-central1-b
    gcloud compute instances create "my-vm-2" --machine-type "n1-standard-1" --image-project "debian-cloud" --image "debian-9-stretch-v20190213" --subnet "default"

3. Connect between VM instances.
    i. Use the ping command to confirm that my-vm-2 can reach my-vm-1 over the network:
        - connect to my-vm-2: 
            gcloud compute ssh my-vm-2
        - ping my-vm-1 from my-vm-2: 
            ping my-vm-1
        - Use the ssh command to open a command prompt on my-vm-1:
            ssh my-vm-1
        - At the command prompt on my-vm-1, install the Nginx web server:
            sudo apt-get install nginx-light -y
        - Use the nano text editor to add a custom message to the home page of the web server:
            sudo nano /var/www/html/index.nginx-debian.html
        - Add text like this, and replace YOUR_NAME with your name:
            Hi from YOUR_NAME
        - Exit Text Editor and Confirm that the web server is serving your new page.
            curl http://localhost/
        - exit command prompt on my-vm-1
            exit
        - Confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt on my-vm-2, execute this command:
            curl http://my-vm-1/
    ii. Get IP of my-vm-1 instance
        gcloud compute instances list
    iii. Copy the External IP address for my-vm-1 and paste it into the address bar of a new browser tab. 
        - Result : Home page including Custom Text will be in the browser