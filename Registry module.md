# Docker module
Local Registry

---

## Preparations

- Uninstall old versions
```
 sudo apt-get remove docker docker-engine docker.io containerd runc
```
- Update the apt
```
 sudo apt-get update
```
- install packages  to use a repository over HTTPS
```
 sudo apt-get install ca-certificates curl gnupg lsb-release
```
- Add Docker’s official GPG key
```
 sudo mkdir -p /etc/apt/keyrings
 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
- set up the repository
```
echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
- Install Docker Engine
```
sudo chmod a+r /etc/apt/keyrings/docker.gpg
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```
- Pull docker registry and ubuntu
```
docker pull registry:2
docker pull ubuntu:22.04
```

## Instructions

 - Run the following containers using dockerhub images:
```
docker run -d -p 5000:5000 --restart=always --name registry registry:2
```

 - Please validate that your ontainers are running successfully:
```
docker ps
```

 - Lets tag and push to our local registry:
 
```
docker tag ubuntu:22.04 localhost:5000/my-ubuntu
docker push localhost:5000/my-ubuntu
```

 - Lets clear the image lacal cach :
```
docker image remove ubuntu:22.04
docker image remove localhost:5000/my-ubuntu
```

 - Pull image from local registry :
```
docker pull localhost:5000/my-ubuntu
```

 - Lets see what repositories we have in our registry :
```
curl -X GET http://localhost:5000/v2/_catalog
```
   Expected result:
```
{"repositories":["my-ubuntu"]}
```
 - Lets see what tags we have in specific repository :
```
curl -X GET http://localhost:5000/v2/my-ubuntu/tags/list
```
   Expected result:
```
{"name":"my-ubuntu","tags":["latest"]}
```
