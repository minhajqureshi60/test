# test
#!/bin/bash

echo "installing python"
sudo apt-get update && sudo apt-get upgrade -y
sudo apt install build-essential checkinstall -y
sudo apt install libreadline-gplv2-dev libncursesw5-dev libssl-dev tk-dev libgdbm-dev libc6-dev libbz2-dev libffi-dev
cd /opt && sudo wget https://www.python.org/ftp/python/3.9.10/Python-3.9.10.tar.xz
sudo tar -xvf Python-3.9.10.tar.xz
cd Python-3.9.10/
sudo ./configure
sudo make && sudo make install
cd /home/ubuntu/
python3 -V
python3.9 -m venv .
source bin/activate

# Install dependencies
echo "Installing dependencies"
sudo apt update
sudo apt install -y \ ca-certificates curl gnupg lsb-release
echo "Adding Docker source"
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - 

sudo add-apt-repository "https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

echo "Installing Docker Engine"
sudo apt update && sudo apt install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin

echo "Adding user to docker group"
sudo gpasswd -a $USER docker

echo "Docker is installed; log out and log in to run Docker without sudo!"

pip3 install django
# created a django project in which I have created dockerfile and docker-compose.yaml file and started a project and pushed to github
docker-compose build
docker-compose up

echo "installing jenkins"
sudo apt update
sudo apt install openjdk-11-jre -y
java -version
sudo apt install curl
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io.key | sudo tee \   /usr/share/keyrings/jenkins-keyring.asc > /dev/null
sudo apt-get install jenkins

# created a freestyle project in jenkins and integrated with github then clicked on build now and copied Building in workspace from console output of project from jenkins
cd /var/lib/jenkins/workspace/aqsquare
docker-compose build
docker-compose up
# configured the build step in jenkins by:
echo minhaj00 | sudo -S docker-compose build

# Start the Docker container
echo minhaj00 | sudo -S docker-compose up -d

added jenkins to the docker group, run command in the terminal:
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
# run the project in jenkins 
