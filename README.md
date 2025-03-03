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
`export AGISOFT_FLS=<IP_address>:<port_number>`

## Run automate-metashape container on VM
`docker run -v </host/data/dir>:/data -e AGISOFT_FLS=$AGISOFT_FLS --gpus all ghcr.io/open-forest-observatory/automate-metashape --config_file /data/config.yml`

## Move metashape files back to local machine
`scp -i /Users/jgillan/Downloads/container_test.pem -r ubuntu@3.95.255.230:/home/ubuntu/ /Users/jgillan/Documents`







