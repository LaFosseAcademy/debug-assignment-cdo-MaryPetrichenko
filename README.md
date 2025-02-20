# Instructions

## Repo cloning

Clone the repo from the github locally on your machine:
```bash 
git clone git@github.com:LaFosseAcademy/debug-assignment-cdo-MaryPetrichenko.git 
```

## Create EC2 instance

1. Navigate to the AWS Console, sign in and choose the region **United States (N.Virginia)**
2. Create EC2 instance using default free tier values: 
   - Application and OS Images: Amazon Linux
   - Use your default key pair login or create a new one if needed
   - Instance type: t2.micro
   - Allow  SSH traffic from, HTTPS traffic from the internet, HTTP traffic from the internet

## Terraform 

1. Go to the directory debug-assignment-cdo-MaryPetrichenko/terraform
```bash
cd debug-assignment-cdo-MaryPetrichenko/terraform
```

2. Pass in your credentials running commands:
```bash
export AWS_ACCESS_KEY_ID=<YOUR_ACCESS_KEY>
export AWS_SECRET_ACCESS_KEY=<YOUR_SECRET_ACCESS_KEY>
```
To make sure it works run:
```bash
echo $AWS_ACCESS_KEY_ID
echo $AWS_SECRET_ACCESS_KEY
```
3. Copy the ami id from the aws EC2 instance newly created. Change the following in the main.tf file:
``` bash
ami = "<ami-id-from-aws-instance>"
```
4. To create and start the server run the following commands:
``` bash
terraform init
terraform validate
terraform apply
```

## Ansible

1. Cope the Public IPv4 address from the EC2 instance newly created.

2. Open the ansible/ansible_hosts file and update the IP address of the host:
``` bash
[production]
prod ansible_host=<YOUR_IP_ADDRESS>
```

3. Navigate to the ansible folder and run the following commands:
``` bash
ansible-playbook playbooks/docker-install.yml 
ansible-playbook playbooks/docker-run.yml 
``` 

## Accessing the deployed application

1. Access the app using IPv4 DNS of the EC2 instance and port 3000.

2. The link to acces deployed app can be as following:
    - http://<Your_IPv4_DNS>:3000/tour-de-france/cyclists - to access all cyclists
    - http://<Your_IPv4_DNS>:3000/tour-de-france/cyclists/type/:type - to access cyclists of particular type
    - http://<Your_IPv4_DNS>:3000/tour-de-france/cyclists/:id - to access cyclist by his/her id
    - http://<Your_IPv4_DNS>:3000/tour-de-france/teams - to access information on teams
    - http://<Your_IPv4_DNS>:3000/tour-de-france/teams/:id - to access information on team by its id

# Docker deployment

The application is using two docker images:
- marypetrichenko/tour-de-france-mvc:0.0.1.RELEASE
- marypetrichenko/tour-de-france-db:0.0.1.RELEASE

The images were prebuild and are accessible from the docker hub.
Docker-compose.yml file points the docker images from the hub. The images are downloaded automatically on the first run.

# Access to the current application

Currently deployed application can be accessed via the following link:
http://ec2-100-25-37-10.compute-1.amazonaws.com:3000/tour-de-france/
Other endpoints are given in the previous sections.