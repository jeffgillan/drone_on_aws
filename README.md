# Drone Imagery Processing on AWS

## Login into [AWS Management Console](https://aws.amazon.com/console/) 

Sign-in using root user email. 

Launch VM in AWS EC2. Use Amazon Machine Image (AMI) Ubuntu 22.04 and instance type `g4dn.2xlarge` for a GPU. 


## Restrict private key permissions
chmod 400 /Users/jgillan/Downloads/container_test.pem


## From local machine, connect to EC2 VM through SSH
`ssh -i "/Users/jgillan/Downloads/container_test.pem" ubuntu@44.223.46.46`

You have to first connect via ssh in order to get the VM listed on the `known hosts` file on your local machine. 

When you have demonstrated the connection to the VM, you can close the ssh connection with `exit`. 

## Storage on EC2 VMs

EC2 VMs have two types of storage: Elastic Block Storage (EBS) and Local NVMe Instance Storage (Temporary). When you launch the `g4dn.2xlarge` instance, it will come with a relatively small EBS (8GB) mounted at `/`. That means your home directory on the VM (/home/ubuntu) is on this storage. This is not enough storage for drone imagery. The `g4dn.2xlarge` instance also comes with a 225 GB NVMe storage that works better for drone imagery. This is temporary and will disappear when the VM is shutdown. 

To use the NVMe storage, we need to mount it. On the VM command line type: `lsblk`. This will list the storage volumes and if they are mounted. Look for the device that has 225 GB. If the mountpoint is blank, it is not mounted and not yet usable. 

Make it useable:

`sudo mkfs.ext4 /dev/nvme1n1`

`sudo mkdir -p /mnt/instance-store`

`sudo mount /dev/nvme1n1 /mnt/instance-store`

Check the available and used storage 

`df -h /mnt/instance-store`

Change ownership so we can transfer data into the directory 

`sudo chown -R ubuntu:ubuntu /mnt/instance-store`


## move data from local machine to VM using scp parallel

`cd ~/Documents/aerial_projects/test_images`

`ls | parallel -j 4 scp -i /Users/jgillan/Downloads/container_test.pem -r {} ubuntu@54.209.130.223:/mnt/instance-store`

## declare metashape floating license
`export AGISOFT_FLS=<IP_address>:<port_number>`

## Run automate-metashape container on VM
`docker run -v </host/data/dir>:/data -e AGISOFT_FLS=$AGISOFT_FLS --gpus all ghcr.io/open-forest-observatory/automate-metashape --config_file /data/config.yml`

## Move metashape files back to local machine
`scp -i /Users/jgillan/Downloads/container_test.pem -r ubuntu@3.95.255.230:/home/ubuntu/ /Users/jgillan/Documents`


ssh -i "container_test.pem" ubuntu@ec2-3-235-20-137.compute-1.amazonaws.com





