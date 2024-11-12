# sd2660_msa
MSA application for assignment

Jenkins 
Install plugins
- Docker Pipeline
- Pipeline Utility Steps
- Kubernetes
- Amazon EC2 plugin
- Pipeline: AWS Steps

Credentials
- aws-credential
- ubuntu-user

Add Amazon EC2 to Jenkins clouds

Amazon EC2
Install unzip first
sudo apt install unzip

Install aws cli
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

Fix docker
sudo chmod 666 /var/run/docker.sock