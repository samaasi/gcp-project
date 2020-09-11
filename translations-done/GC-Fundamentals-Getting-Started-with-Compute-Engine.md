# Google Cloud Fundamentals: Getting Started with Compute Engine

## Objectives:

In this lab, you will learn how to perform the following tasks:
    - Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.
    - Create a Compute Engine virtual machine using the gcloud command-line interface.
    - Connect between the two instances.

## Steps:

1. Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.

    gcloud compute instances create my-vm-1 --machine-type "n1-standard-1" --image-project "debian-cloud" --image "debian-9-stretch-v20190213" --subnet "default" --tags http

    gcloud compute firewall-rules create allow-http --action=ALLOW --direction=INGRESS --rules=tcp:80 --target-tags=http

2. Create a Compute Engine virtual machine using the gcloud command-line interface.
Get list of zones and use the grep to filter for just us-central1 `gcloud compute zones list | grep us-central1`

    gcloud config set compute/zone us-central1-b

    gcloud compute instances create "my-vm-2" --machine-type "n1-standard-1" --image-project "debian-cloud" --image "debian-9-stretch-v20190213" --subnet "default"

3. Connect between the two instances.

    1. Use the ping command to confirm that my-vm-2 over the network:

        - Connect to my-vm-2:
            gcloud compute ssh my-vm-2
        - ping my-vm-1 from my-vm-2:
            ping -c 4 my-vm-1
        - Use the ssh command to open a command prompt on my-vm-1 from my-vm-2
            ssh my-vm-1
        - At the command prompt on my-vm-1, install the Nginx web server:
            sudo apt-get install nginx-light -y
        - Use the nano text editor to add a custom message to the home page of the web server:
            sudo nano /var/www/html/index.nginx-debian.html
        - Use the arrow keys to move the cursor to the line just below the h1 header. Add text like this, and replace YOUR_NAME with your name:
            Hi from benson_bariyana
        - Exit the editor using ctrl+X and confirm that the web server is serving your new page. At the command prompt on my-vm-1, execute this command:
            curl http://localhost/
            - Result: The response will be the HTML source of the web server's home page, including your line of custom text.
        - To exit the command prompt on my-vm-1, execute this command:
            exit
        - To confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt on my-vm-2, execute this command:
            curl http://my-vm-1/
            - Result: The response will again be the HTML source of the web server's home page, including your line of custom text.
            
    2. Now get the external IP of my-vm-1 instance from this command:
        gcloud compute instances list --zone us-central1-a
        
    3. Paste the copied IP address of my-vm-1 into a new browser tab and hit enter.
        - Result: You will see your web server's home page, including your custom text 