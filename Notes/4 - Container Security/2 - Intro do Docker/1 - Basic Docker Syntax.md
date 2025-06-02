Docker can seem overwhelming at first. However, the commands are pretty intuitive, and with a bit of practice, you’ll be a Docker wizard in no time.

The syntax for Docker can be categorised into four main groups:

- Running a container
- Managing & Inspecting containers
- Managing Docker images
- Docker daemon stats and information

We will break down each of these categories in this task.

## Managing Docker Images

### **Docker Pull**  

Before we can run a Docker container, we will first need an image. Recall from the “[Intro to Containerisation](https://tryhackme.com/room/introtocontainerisation)” room that images are instructions for what a container should execute. There’s no use running a container that does nothing!  

In this room, we will use the Nginx image to run a web server within a container. Before downloading the image, let’s break down the commands and syntax required to download an image. Images can be downloaded using the `docker pull` command and providing the name of the image.

For example, `docker pull nginx`. Docker must know where to get this image (such as from a repository which we’ll come onto in a later task).

```
docker pull nginx
```

![[Pasted image 20250602155727.png]]

By running this command, we are downloading the latest version of the image titled “nginx”. Images have these labels called _tags_. These _tags_ are used to refer to variations of an image. For example, an image can have the same name but different tags to indicate a different version. I’ve provided an example of how tags are used within the table below:

| **Docker Image** | **Tag** | **Command Example**                                                               | **Explanation**                                                                                                                                                                                                                                                                                                                                                                         |
| ---------------- | ------- | --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ubuntu           | latest  | docker pull ubuntu<br><br>**- IS THE SAME AS -**<br><br>docker pull ubuntu:latest | This command will pull the latest version of the "ubuntu" image. If no tag is specified, Docker will assume you want the "latest" version if no tag is specified.<br><br>It is worth remembering that you do not always want the "latest". This image is quite literally the "latest" in the sense it will have the most recent changes. This could either fix or break your container. |
| ubuntu           | 22.04   | docker pull ubuntu:22.04                                                          | This command will pull version "22.04 (Jammy)" of the "ubuntu" image.                                                                                                                                                                                                                                                                                                                   |
| ubuntu           | 20.04   | docker pull ubuntu:20.04                                                          | This command will pull version "20.04 (Focal)" of the "ubuntu" image.                                                                                                                                                                                                                                                                                                                   |
| ubuntu           | 18.04   | docker pull ubuntu:18.04                                                          | This command will pull version "18.04 (Bionic)" of the "ubuntu" image.                                                                                                                                                                                                                                                                                                                  |

When specifying a tag, you must include a colon `:` between the image name and tag, for example, `ubuntu:22.04` (image:tag). Don’t forget about tags - we will return to these in a future task!

### **Docker Image x/y/z**

The `docker image` command, with the appropriate option, allows us to manage the images on our local system.
To list the available options, we can simply do `docker image` to see what we can do. I’ve done this for you in the terminal below:

```
docker image
```

![[Pasted image 20250602155743.png]]

### **Docker Image ls**

This command allows us to list all images stored on the local system. We can use this command to verify if an image has been downloaded correctly and to view a little bit more information about it (such as the tag, when the image was created and the size of the image).

```
docker image ls
```

![[Pasted image 20250602155923.png]]

For example, in the terminal above, we can see some information for two images on the system:

| **Repository** | **Tag** | **Image ID** | **Created** | **Size** |
| -------------- | ------- | ------------ | ----------- | -------- |
| ubuntu         | 22.04   | 2dc39ba059dc | 10 days ago | 77.8MB   |
| nginx          | latest  | 2b7d6430f78d | 2 weeks ago | 142MB    |

### **Docker Image rm **

If we want to remove an image from the system, we can use `docker image rm` along with the name (or Image ID). In the following example, I will remove the "_ubuntu_" image with the tag "_22.04_". My command will be `docker image rm ubuntu:22.04`:

It is important to remember to include the _tag_ with the image name.

```
docker image rm ubuntu:22.04
```

![[Pasted image 20250602160044.png]]

If we were to run a `docker image ls`, we would see that the image is no longer listed:

![[Pasted image 20250602160106.png]]

