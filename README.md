# Docker Tutorial
Install information etc:
https://docs.docker.com/get-started/

We are following this tutorial: https://docs.docker.com/get-started/part2/#build-the-app

## Underlying Technologies
Namespaces, control groups, and Union File System. 

## Build Image
Build this docker image with the app, giving hellow as its tag running this:
```bash
docker build -t hellow .
```
See result:
```bash
docker image ls
```
## Run container with the image
Run is actually "create + run". Creates *new* container based on image, then runs the *new* container.
This -p flag maps your machine’s port 4000 to the container’s published port 80 :
```bash
docker run -p 4000:80 hellow
```

You visit this link to send request to the app:
```bash
curl http://localhost:4000
```

Running the app in the background, in detached mode:
```bash
docker run -d -p 4000:80 hellow
```
## Manage Containers
List the running containers:
```bash
docker container ls
```

End the process, using the CONTAINER ID from above ls, like so:
```bash
docker container stop <CONTAINER ID>
```
## Upload to a Repo
ex: login to dockerhub
```bash
docker login
```
Then, rename repository with <YOUR_DOCKERHUB_NAME>/image-name:tag (tag used as version)
and upload:
```bash
# ex: docker tag old_image_name username/new_image_name:tag
# ex my dockerhub name is drozturk
docker tag hellow drozturk/hello-ozgur:0.0.1
# check the new tag:
docker image ls
# Publish the image
docker push drozturk/hello-ozgur:0.0.1
```

## Download and run
Now, you can run your app on *any machine* with `docker run` command:
```bash
#docker run -p 4000:80 username/repository:tag
docker run -p 4000:80 drozturk/hello-ozgur:0.0.1
```

## Stop Restart
```bash
docker stop <ContainerId>
docker start <ContainerId>
```

## Update Image with the Changes
Create a new image from container with new apps installed etc.
Don't use this much (maybe for experimenting), rather edit Dockerfile!

```bash
docker commit <ContainerId>  <repoName>/<imageName>:<version>
```
