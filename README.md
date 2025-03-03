# Drone Imagery Processing on AWS

## Login into [AWS Management Console](https://aws.amazon.com/console/) 

Sign-in using root user email. 

Launch VM in AWS EC2

install docker on Vm with shell script

## Restrict private key permissions
chmod 400 /Users/jgillan/Downloads/container_test.pem

## move data from local machine to VM using scp parallel

`cd ~/Documents/aerial_projects/test_images`

`ls | parallel -j 4 scp -i /Users/jgillan/Downloads/container_test.pem -r {} ubuntu@54.209.130.223:/home/ubuntu`

## declare metashape floating license

## Run automate-metashape container on VM

## Move metashape files back to local machine







