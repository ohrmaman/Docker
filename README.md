# Docker Workshop
Lab 07: Managing Containers

---

## Preparations

 - Create a new folder for the lab:
```
$ mkdir lab-07
$ cd lab-07
```

## Instructions

 - Run the following containers using dockerhub images:
```
$ docker run -d -p 5002:5002 -e "port=5002" --name python-app1 selaworkshops/python-app:1.0
```
```
$ docker run -d -p 5003:5003 -e "port=5003" --name python-app2 selaworkshops/python-app:2.0
```

 - Ensure the containers are running:
```
$ docker ps
```

 - Stop the first container:
```
$ docker stop python-app1
```

 - Kill the second container:
```
$ docker kill python-app2
```

 - Display running containers:
```
$ docker ps
```

 - Show all the containers (includind non running containers):
```
$ docker ps -a
```

 - Let's start both containers again:
```
$ docker start python-app1 python-app2
```

 - Restart the second container:
```
$ docker restart python-app2
```

 - Display the docker host information with:
```
$ docker info
```

 - Show the running processes in the first container using:
```
$ docker top python-app1
```

 - Display the resource usage statistics of both containers (exit with Ctrl + C):
```
$ docker stats python-app1 python-app2
```

 - Retrieve the history of the second container image:
```
$ docker history selaworkshops/python-app:2.0
```

 - Inspect the second container image:
```
$ docker inspect selaworkshops/python-app:2.0
```

 - Inspect the first container and look for the internal ip:
```
$ docker inspect python-app1
```
```
"Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "822cb66790c6358d9decab874916120f3bdeff7193a4375c94ca54d50832303d",
                    "EndpointID": "9aa96dc29be08eddc6d8f429ebecd2285c064fda288681a3611812413cbdfc1f",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.3",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:03",
                    "DriverOpts": null
                }
            }
```

 - Show the logs of the second container using the flag --follow:
```
$ docker logs --follow python-app2
```

 - From your browser, browse to the application and watch the containers logs changing in the **terminal**:
```
http://<your-server-ip>:5003
```

 - Stop to tracking logs:
 ```
$ CTRL + C
```

 - Inspect the content of the current directory:
 ```
$ ls -l
```

 - Copy some files from the second container to the host:
 ```
$ docker cp python-app2:/app/index.html .
```

 - Inspect the content of the current directory:
 ```
$ ls -l
```

- Export the **python-app1** container’s filesystem to a tar archive named **FS.tar**: 
 ```
docker export --output="FS.tar" python-app1
 ```
## Cleanup

 - Remove used containers:
```
$ docker rm -f python-app1 python-app2
```

