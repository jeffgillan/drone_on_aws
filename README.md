# drone_on_aws

Launch VM in AWS EC2

install docker on Vm with shell script

## Restrict private key permissions
chmod 400 /Users/jgillan/Downloads/container_test.pem

## move data from local machine to VM scp parallel

`cd ~/Documents/aerial_projects/test_images`

`ls | parallel -j 4 scp -i /Users/jgillan/Downloads/container_test.pem -r {} ubuntu@54.209.130.223:/home/ubuntu`

declare metashape floating license

pull and run automate-metashape container on VM


