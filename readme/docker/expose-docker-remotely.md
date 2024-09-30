# Expose Docker Remotely

## Theory

Exposing Docker remotely means allowing connections to the Docker daemon from machines other than the one it is running on. This can be useful for managing Docker containers on remote servers, or for exposing Dockerized applications to the public internet.

A remote Docker host is a machine, inside or outside our local network which is running a Docker Engine and has ports exposed for querying the Engine API. The sample application can be deployed on a remote host in several way



***

## Practical

{% hint style="info" %}
Docker must be installed on your system.
{% endhint %}

### Check Docker Process

```
ps -ef | grep docker
```

<figure><img src="../../.gitbook/assets/image (206).png" alt=""><figcaption></figcaption></figure>

### Edit docker.service File

```
vim /lib/systemd/system/docker.service

# add or modify the below line
ExecStart=/usr/bin/dockerd -H=fd:// -H=tcp://0.0.0.0:2375
```

<figure><img src="../../.gitbook/assets/image (207).png" alt=""><figcaption></figcaption></figure>

### Reload and Restart

```
systemctl daemon-reload

sudo service docker restart
```

### Test

```
curl http://localhost:2375/images/json
```

<figure><img src="../../.gitbook/assets/image (208).png" alt=""><figcaption></figcaption></figure>



***

## REFERENCES

* [https://www.youtube.com/watch?v=cjm\_NqteLLA](https://www.youtube.com/watch?v=cjm\_NqteLLA)
* [https://www.docker.com/blog/how-to-deploy-on-remote-docker-hosts-with-docker-compose/#:\~:text=A%20remote%20Docker%20host%20is,remote%20host%20in%20several%20ways.](https://www.docker.com/blog/how-to-deploy-on-remote-docker-hosts-with-docker-compose/)

