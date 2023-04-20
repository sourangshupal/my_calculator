# Calculator Project

# Calculator App Deployment on AWS EC2 using Flask and Gunicorn

In this tutorial, we will be deploying a Flask Calculator app on AWS EC2 instance. We will clone the repository, update the system, install the requirements and run the app using a public IP.

## Prerequisites

Before we start, you should have the following:

-   An AWS account
-   Basic knowledge of AWS EC2 instances
-   Basic knowledge of the command line interface

## Step 1: Launch an EC2 instance

1.  Log in to your AWS account and go to the EC2 dashboard.
2.  Click on the "Launch Instance" button.
3.  Choose an Amazon Machine Image (AMI) that is compatible with your application. For instance, select an Ubuntu Server AMI.
4.  Choose an instance type according to your needs.
5.  Configure the instance details, such as the number of instances, network settings, and storage.
6.  Add tags to your instance for better identification.
7.  Configure the security group to allow HTTP and SSH traffic.
8.  Review and launch the instance.

## Step 2: Connect to the instance

1.  Open your terminal and navigate to the directory where your private key is stored.
2.  Run the following command to change the permissions of your private key file:

```
chmod 400 {path_to_private_key}

```

1.  Connect to the instance using SSH with the following command:

```
ssh -i {path_to_private_key} ubuntu@{public_ip_address}

```

## Step 3: Clone the repository

1.  Install Git on your instance with the following command:

```
sudo apt-get update
sudo apt-get install git

```

1.  Navigate to the directory where you want to clone the repository.
2.  Clone the repository with the following command:

```
git clone {repository_url}

```

**Repository** - [https://github.com/sourangshupal/my_calculator](https://github.com/sourangshupal/my_calculator)

## Step 4: Update the system

1.  Update the system with the following command:

```
sudo apt-get update
sudo apt-get upgrade

```

## Step 5: Install the requirements

1.  Navigate to the directory where the Flask Calculator app is located.
2.  Create a virtual environment with the following command:

```
python3 -m venv venv

```

1.  Activate the virtual environment with the following command:

```
source venv/bin/activate

```

1.  Install the requirements with the following command:

```
pip install -r requirements.txt

```

## Step 6: Run the app

1.  Run the app with the following command:

```
python3 app.py
```

1.  Access the app using the public IP address of your instance in your web browser.

**Output**

![[output/image.png]]

## Conclusion

In this tutorial, we have covered the steps to deploy a Flask Calculator app on AWS EC2 instance. You can now clone your repository, update the system, install the requirements, and run the app using the public IP address of your instance.

## Now run the app using gunicorn3 and Nginx.

## Step 1: Install gunicorn3

1.  Install gunicorn3 with the following command:

```
sudo apt-get install gunicorn3

```

## Step 2: Create the Nginx configuration file

1.  Create the Nginx configuration file with the following command:

```
sudo nano /etc/nginx/sites-available/flask_app

```

1.  Paste the following configuration into the file:

```
server {
    listen 80;
    server_name {public_ip_address};

    location / {
        proxy_pass <http://localhost:8000>;
    
    }
}

```

1.  Replace `{public_ip_address}` with the public IP address of your instance.
2.  Save and close the file.

## Step 3: Enable the Nginx configuration

1.  Enable the Nginx configuration with the following command:

```
sudo ln -s /etc/nginx/sites-available/flask_app /etc/nginx/sites-enabled/flask_app

```

## Step 4: Restart Nginx

1.  Restart Nginx with the following command:

```
sudo systemctl restart nginx

```

## Step 5: Run the app

1.  Go to the **`my_calculator`** directory and run the app with the following command:

```
gunicorn3 --bind localhost:8000 app:app.py

```

1.  Access the app using the public IP address of your instance in your web browser.

**Output**

![[output/image.png]]
## Conclusion

In this tutorial, we have covered the steps to deploy a Flask Calculator app on AWS EC2 instance using gunicorn3 and Nginx. You can now clone your repository, update the system, install the requirements, and run the app using the public IP address of your instance.
