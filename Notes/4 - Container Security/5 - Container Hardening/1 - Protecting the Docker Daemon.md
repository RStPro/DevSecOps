You may recall from the [Container Vulnerabilities](https://tryhackme.com/room/containervulnerabilitiesDG) room that the Docker daemon is responsible for processing requests such as managing containers and pulling or uploading images to a Docker registry. Docker can be managed remotely and is often done in CI (Continuous Integration) and CD (Continuous Development) pipelines. For example, pushing and running new code in a container on another host to check for errors.

If an attacker can interact with the Docker daemon, they can interact with the containers and images. For example, they launch their own (malicious) containers or gain access to containers running applications with sensitive information (such as databases).

The Docker daemon is not exposed to the network by default and must be manually configured. However, exposing the Docker daemon is a common practice (especially in cloud environments such as CI/CD pipelines).

Implementing secure communication and authentication methods such as those listed below are extremely important in preventing unauthorized access to the Docker daemon.

## SSH

Developers can interact with other devices running Docker using SSH authentication. To do so, Docker uses contexts which can be thought of as profiles. These profiles allow developers to save and swap between configurations for other devices. For example, a developer may have one context for a device with Docker for development and another context for a device with Docker for production.

**Note:** You must have SSH access to the remote device, and your user account on the remote device must have permission to execute Docker commands.

As the developer, you will need to create the Docker context on your device. Please see the code snippet below to create a context within Docker.

![[Pasted image 20250608162330.png]]

Once this has been completed, you can switch to this context, where all Docker-related commands will now be executed on the remote host.

![[Pasted image 20250608162405.png]]

To exit this context and, for example, use your own Docker engine, you can revert to "default" via

```
docker context use default
```

**Note:** This is not entirely secure. For example, a weak SSH password can lead to an attacker being able to authenticate.
Strong password hygiene is strongly recommended.
Some tips for a strong password have been included below:

- A high amount of characters (i.e. 12-22+)
- Special characters such as !, @, #, $
- Capital letters and numbers placed sporadically throughout (i.e. sUp3rseCreT!PaSSw0rd!)

Docker contexts allow you to interact with the Docker daemon directly over SSH, which is a secure and encrypted way of communication.

## TLS Encryption

The Docker daemon can also be interacted with using HTTP/S. This is useful if, for example, a web service or application is going to interact with Docker on a remote device.

To do this securely, we can take advantage of the cryptographic protocol TLS to encrypt the data sent between the devices. When configured in TLS mode, Docker will only accept remote commands from devices that have been signed against the device you wish to execute Docker commands remotely.

**Note**: Creating and managing TLS certificates is out-of-scope for this room, as you will often need to consider factors such as expiry date and strength of encryption for your environment. Once you have created your certificates, you can tell Docker to run in TLS mode with the generated certificate.

On the host (server) that you are issuing the commands from:

![[Pasted image 20250608162613.png]]On 

the host (client) that you are issuing the commands from:

![[Pasted image 20250608162651.png]]

**Note**: It is important to remember that this is not guaranteed to be secure.
For example, anyone with a valid certificate and private key can be a "trusted" device. I have explained the arguments used in generating a TLS certificate and key in the table below:

|   |   |
|---|---|
|**Argument**|**Description**|
|`--tlscacert`|This argument specifies the certificate of the certificate authority. A certificate authority is a trusted entity that issues the certificates used to identify devices.|
|`--tlscert`|This argument specifies the certificate that is used to identify the device.|
|`--tlskey`|This argument specifies the private key that is used to decrypt the communication sent to the device.|