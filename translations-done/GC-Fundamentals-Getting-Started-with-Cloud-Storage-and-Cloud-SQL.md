### Google Cloud Fundamentals: Getting Started with Cloud Storage and Cloud SQL

#### Objectives:
    - In this lab, you learn how to perform the following tasks:
    
    - Create a Cloud Storage bucket and place an image into it.
    
    - Create a Cloud SQL instance and configure it.
    
    - Connect to the Cloud SQL instance from a web server.
    
    - Use the image in the Cloud Storage bucket on a web page.
    
#### Steps:
1. Show the list of machine type
    gcloud sql tiers list
    
2. Create instance
    gcloud sql instances create bloghost --tier=db-n1-standard-2 --region=us-central1-b --database-version=MYSQL_5_7
    
3. Set password
    gcloud sql users set-password root --host=% --instance bloghost --password blog@20