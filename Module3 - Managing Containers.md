# Docker module
Managing Containers

---

## Preparations
```
docker pull dockersamples/static-site
```

## Instructions

 - Run the following containers using dockerhub images:
```
docker run --name my-site-1 -e AUTHOR="<Your Name>" -d -p 8880:80 dockersamples/static-site
```
```
docker run --name my-site-2 -e AUTHOR="<Your friend's Name>" -d -p 8888:80 dockersamples/static-site
```

 - Please validate that your ontainers are running successfully:
```
docker ps
```

 - Stop the first container (site 1):
```
docker stop my-site-1
```

 - Kill the second container (site 2):
```
docker kill my-site-2
```

 - Display running containers:
```
docker ps
```

 - Show all the containers -> including non running containers:
```
docker ps -a
```

 - please start both of containers again:
```
docker start my-site-1 my-site-2
```

 - Restart the first container:
```
docker restart my-site-1
```

 - Display the docker **host** information with:
```
docker info
```

 - Display the resource usage statistics of both running containers (exit with Ctrl + C):
```
docker stats my-site-1 my-site-2
```

 - Retrieve the history of the second container image:
```
docker history dockersamples/static-site
```

 - Inspect the containers image:
```
docker inspect dockersamples/static-site
```

 - Inspect the first container and look for it's internal ip:
```
docker inspect my-site-1
```
```
"Networks": {
    "bridge": {
      "IPAMConfig": null,
      "Links": null,
      "Aliases": null,
      "NetworkID": "42bcf47465456254e4ed2deb04e17076d4f0a82b7edc0de6248a77b287be5b22",
      "EndpointID": "2e00a709dbc81a84fdd608e51722e7a5d3acf063c1f861be3dec1188fc7e9d38",
      "Gateway": "172.17.0.1",
      "IPAddress": "172.17.0.2",
      "IPPrefixLen": 16,
      "IPv6Gateway": "",
      "GlobalIPv6Address": "",
      "GlobalIPv6PrefixLen": 0,
      "MacAddress": "02:42:ac:11:00:02",
      "DriverOpts": null
    }
}
```

 - From your browser, browse to the application and watch The site's name defined by the environment variable:
```
http://localhost:8880
```

 - Show the logs of the second container using the flag --follow:
```
docker logs --follow my-site-2
```

 - From your browser, browse to the application and watch the containers logs changing in the CLI **terminal**:
```
http://localhost:8888
```

## Cleanup

 - Remove used containers:
```
docker rm -f my-site-2 my-site-1
```

