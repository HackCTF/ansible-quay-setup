Instalar Ansible:
```bash
sudo dnf install ansible -y
```

Instalar el ansible-quay-setup:
```bash
git clone https://github.com/HackCTF/ansible-quay-setup.git
cd ansible-quay-setup
python -m pip install -r requirements.txt
ansible-playbook playbooks/setup.yml
```

Entrar al sitio web mediante el navegador web
```bash
localhost:8080
```

##  Robot Access
https://docs.redhat.com/en/documentation/red_hat_quay/3.5/html-single/use_red_hat_quay/index#allow-robot-access-user-repo

https://docs.redhat.com/en/documentation/red_hat_quay/3.13/html-single/use_red_hat_quay/index#creating-robot-account-api

##  Login   

### -  Podman
```sh
podman login localhost:8080
Username: myusername
Password: mypassword
```

execute
```sh
podman login --tls-verify=false localhost:8080
Login Succeeded!
```

#### Create a new container
First we’ll create a container with a single new file based off of the ubuntu base image:
```sh
$ podman run ubuntu echo "fun" > newfile
```
The container will immediately terminate (because its one command is echo), so we’ll use docker ps -l to list it:
```sh
$ podman ps -l
CONTAINER ID        IMAGE               COMMAND             CREATED
07f2065197ef        ubuntu:12.04        echo fun            31 seconds ago
```
Make note of the container id; we’ll need it for the commit command.

#### Tag the container to an image
We next need to tag the container to a known image name

Note that the username must be your Quay username and reponame is the new name of your repository.
```sh
$ podman commit 07f2065197ef localhost:8080/username/reponame
e7050e05a288f9f3498ccd2847fee966d701867bc671b02abf03a6629dc921bb
```
####  Push the image to Quay
```sh
$ podman push localhost:8080/username/reponame
The push refers to a repository [localhost/username/reponame] (len: 1)
Sending image list
Pushing repository quay.io/username/reponame (1 tags)
8dbd9e392a96: Pushing [=======>         ] 21.27 MB/134.1 MB 40s
```
#### Pull the image from Quay
If any changes were made on another machine, a docker pull can be used to update the repository locally
```sh
$ podman pull localhost:8080/username/reponame
```
