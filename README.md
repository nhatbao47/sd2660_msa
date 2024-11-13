# sd2660_msa
MSA application for assignment

Start Jenkins and install following items
Plugins:
- Jenkins suggested
- Docker Pipeline
- Pipeline Utility Steps
- Kubernetes
- Amazon EC2 plugin
- Pipeline: AWS Steps
Tools:
- kubectl cli
- docker

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

Install Trivy
curl -sfL https://github.com/aquasecurity/trivy/releases/download/v0.40.0/trivy_0.40.0_Linux-64bit.tar.gz -o trivy.tar.gz

tar -xvzf trivy.tar.gz

sudo mv trivy /usr/local/bin/

trivy --version

Fix docker
sudo chmod 666 /var/run/docker.sock