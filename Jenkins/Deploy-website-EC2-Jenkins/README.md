# Steps to Deploy Website on EC2 Instence using Jenkins


Step 1:
```sh
1. Create EC2 instence with with Security Groups Rules

2. Security Groups Rules:
    1. SSH  -to can can install the nedded daemon
    2. HTTP: 80  -I need it with wget the files and upgrading  
    3. Custom rule: 8080 -to expose jenkins 
    4. Custom rule:5000 -to expose the website 

```

Step 2:

3.  If you want to ssh locally
    1.  Created Key_Pair and 
    Download the .pem file if you want to ssh locally
    2.  Change <file.pem> permissions
```sh
sudo chmod 400 file.pem
```

Step 4:

Connect to the created EC2 instence:
```sh
sudo ssh -i file.pem ubuntu@PUBLIC_IPv4_DNS_NAME
```

Step 5:

Install Jenkins:
```sh
sudo apt update -y

sudo apt install openjdk-11-jdk -y

java -version

readlink -f $(which java)

JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java

echo $JAVA_HOME

export JAVA_HOME

sudo apt install wget 

wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -

sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \
/etc/apt/sources.list.d/jenkins.list'

sudo apt update -y 

sudo apt-get install jenkins -y
```

Step 6:

Access Jenkins through browser:
```sh
  1. PUBLIC_IPv4_ADDRESS:8080

  2. sudo cat <jenkins_default_password_path>

  3. Fill in user details & Install suggested plugins
```

Step 7:

Create a job:
```sh
  1. Add Repository Link in Source Code Management

  2. Make sure the master branch name is the same as in the repository */main  or */master

  3. Add build setup then Execute Shell 
```

Commands:
```sh
cd Simple-Project/

ansible-playbook file.yml
```

Step 8: 

Install Docker:
```sh
sudo apt-get update

sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io
```

Step 9: 

Add Docker to sudo group:
```sh
sudo groupadd docker

sudo usermod -aG docker $USER

newgrp docker 

sudo chmod 666 /var/run/docker.sock
```

Step 10: 

Install Ansible:
```sh
sudo apt update

sudo apt install ansible -y
```

Step 11: 

Run Job on Jenkins:
```sh
  1. Click on the job from the dashboard

  2. Build Now
```
![log](https://user-images.githubusercontent.com/107524115/228990919-b21b1796-7f7e-4a05-990b-d650bc812668.png)



Step 12: 

Once the job run successfully:

```sh
Go to your browser: PUBLIC_IPv4_ADDRESS:5000
```
![web](https://user-images.githubusercontent.com/107524115/228990943-d7e988ac-01b2-4d3c-9bd7-23d478af01d9.png)
