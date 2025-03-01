# drone_on_aws

Launch VM in AWS EC2

install docker on Vm with shell script

## Restrict private key permissions
chmod 400 /Users/jgillan/Downloads/container_test.pem

## move data from local machine to VM with Rsync
rsync -avz --progress --bwlimit=625 --partial --append -e "ssh -i /Users/jgillan/Downloads/container_test.pem" /Users/jgillan/Documents/aerial_projects/test_images ubuntu@54.209.130.223:/home/ubuntu

declare metashape floating license

pull and run automate-metashape container on VM


