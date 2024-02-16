# Docker Container

{% embed url="https://linuxhandbook.com/create-custom-docker-image/" %}

## Creating a Docker File

### Create a Html file

```
echo "Hello World" > index.html
```

### Create a Dockerfile

```
touch Dockerfile
```

### Edit the Dockerfile

```
FROM nginx
COPY index.html /usr/share/nginx.html
```

{% hint style="info" %}
A Dockerfile is a text file with instructions to build a Docker image

\
When we run a Dockerfile, Docker image is created\
\
When we run the docker image, containers are created
{% endhint %}

### Start docker & Build docker image from Dockerfile

```
sudo service docker start
```

```
docker build -t <folder-name> .
```

{% hint style="info" %}
The folder should have the Dockerfile
{% endhint %}

### List docker images

```
docker images
```

### Run docker container from the image

```
docker run -p 8080:80 <image-name>
```

## Access the app

```
http://localhost:8080
```

