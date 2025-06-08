Reviewing Docker images is an extremely important habit to practice.
You would be wary of running unknown code on your device, so why would you consider running it in a production environment?

Unfortunately, there are numerous examples of malicious Docker images causing havoc. For instance, in 2020, Palo Alto discovered [cryptomining Docker images](https://unit42.paloaltonetworks.com/cryptojacking-docker-images-for-mining-monero/) that were pulled (and presumably ran) over two million times.

Images on Docker Hub often come with the Dockerfiles attached to the repository. For example, the Docker Hub displays the layers (therefore the commands executed) of the Dockerfile.

![[Pasted image 20250608182217.png]]

In the image above, we can see the various layers of the image on DockerHub.
These layers are the steps that are executed during the building process of the image.

Additionally, open-source code repositories for images on the Docker Hub will often be included, allowing you to review the entire Dockerfile.

![[Pasted image 20250608182237.png]]

In the image above, we can see the code for the Dockerfile.
This allows us to audit the code and understand precisely what actions are being executed in the container. By analysing the code, we can check for vulnerabilities or malicious actions.

Tools such as [Dive](https://github.com/wagoodman/dive) allow you to reverse engineer Docker images by inspecting what is executed and changed at each layer of the image during the build process.

![[Pasted image 20250608182304.png]]

