## Phase One: Explore

![[Pasted image 20250602191342.png]]

Okay, let's get going, shall we? The first thing we want to do is start our Minikube cluster. You can do this by running the following command in the terminal (the cluster will take a couple of minutes to start up):  

```
minikube start
```

Once the cluster has started up, you're ready to go! This guided walkthrough will take you through this cluster, reinforcing knowledge taught in the room. That being said, you have a Kubernetes cluster at your disposal, so feel free to explore the cluster and experiment with the different commands you have learned so far!

Let's see what's running already, shall we? We can do this using the following command (`-A` for all namespaces)

```
kubectl get pods -A
```

After running this, you should see a few pods running. These are the default pods present when you first start a Kubernetes cluster (you may recognise some of these names as they represent some of the control plane and worker node processes). Exciting stuff! But how about we make it more exciting by adding a deployment and service into the mix? On the VM you will be able to find some config YAML files located here:

```
~/Desktop/configuration
```

There are two config YAMLs here of interest to us: **nginx-deployment.yaml** and **nginx-service.yaml**. Check these configuration files out using the cat command:

```
cat filename
```

Let's break down what we see in each of these files:

**nginx-deployment.yaml**

This is a relatively simple deployment; we can see the desired state has been defined as a single replica pod, inside of which will be a container running an nginx image. From the other lines, we can determine that this pod will be used to run some kind of web app.

**nginx-service.yaml**

This, again, is a straightforward nginx NodePort service being defined here. The eagle-eyed among you may have noticed that the 'selector: -> app: ' field matches the app label defined in the deployment, as well as the 'targetPort' matching the 'containerPort' outlined in the deployment. This service exposes the web application running in the pod, which the deployment controls. To apply the configuration outlined in these YAML files, we use the kubectl apply command. Remember to apply the service file first! Like so:

```
kubectl apply -f nginx-service.yaml
```

```
kubectl apply -f nginx-deployment.yaml
```

Verify the replica pod is running by using the following command (not providing any namespace flag will get all the pods in the default namespace, which is where our pod should be):

```
kubectl get pods -A
```

You should now see a pod with 'nginx-deployment' in its name! Our deployment has been started!

## Phase Two: Interact

![[Pasted image 20250602191420.png]]

Okay, now we have a web application running in a pod, which is being exposed by a service. If you recall the nginx-service.yaml, the service connects to the web application using the target port of port 80 (the port where the container is exposed). However, the service's port itself is set to 8080. We want to access this service. We will do this by using the kubectl port-forward command, which allows us to forward a port on our localhost to the Kubernetes service port (8080). Here is the full command to do so: 

```
kubectl port-forward service/nginx-service 8090:8080
```

After running this command, open a web browser (Firefox) and access the web application at the following address:

```
http://localhost:8090/
```

Looks like a simple login terminal, but it needs credentials. Why don't we see if there are any Kubernetes secrets on the cluster that can help us log in to the terminal? Open another terminal window (so the previous window continues to port-forward) and run the following command to see if there are any secrets (in the default namespace):

```
kubectl get secrets
```

Ahh, there is! "terminal-creds" sounds like we are onto a winner! Using the kubectl describe command, we can get more details on this secret to see what is being stored here:

```
kubectl describe secret terminal-creds
```

In the description, we can see that two pieces of "Data" are being stored: a username and a password. While Kubernetes secrets **are** stored in plaintext and not encrypted by default, they are base64 encoded, so we pipe this command and base64 decode the output to get it in plain text. To access this data, we can use the following command:

To get the username, run:

```
kubectl get secret terminal-creds -o jsonpath='{.data.username}'| base64 --decode
```

To get the password, run:

```
kubectl get secret terminal-creds -o jsonpath='{.data.password}'| base64 --decode
```

Use these credentials to access the login terminal. That's a bingo! We're in, and you have retrieved the flag!

**Bonus Task:** For those curious enough, you can use an alternate method to get this flag. It will require some Kubernetes investigation on your part, but the first breadcrumb lies in the nginx-deployment.yaml!

## Phase Three: Secure

![[Pasted image 20250602191449.png]]

It's great that we could access the terminal using the credentials stored in the Kubernetes secret, but as a DevSecOps engineer, this is where our alarm bells should be going off. Time for us to get to work with some Kubernetes secret management. With these credentials being sensitive information, we want to restrict access to the Kubernetes secret they are stored in. We can do this by configuring RBAC (Role-Based Access Control).

First things first, let's decide who it is we want to be able to access this secret. Your DevSecOps manager has suggested that you restrict access to a service account, which is essentially an identity a pod can assume to interact with the Kubernetes API/cluster. By doing this, we can maybe even set it up so that in the future, our daily terminal tasks can be run by an application in a pod. Let's use the kubectl create serviceaccount (can be abbreviated to 'sa') command to make two service accounts, the 'terminal-user' for non-admin terminal activities (should not have access to secret) and the 'terminal-admin' for admin terminal activities (should have access to secret). Run these two commands to make those service accounts:   

```
kubectl create sa terminal-user
```

```
kubectl create sa terminal-admin
```

With those service accounts created, it's time to restrict access to the 'terminal-creds' secret so that only the 'terminal-admin' service account can access it. We are going to do this by defining and applying two configurations. First of all, a Role YAML that defines the role and what it can do (get the 'terminal-creds' secret). Then, a Role Binding YAML that binds the role we have defined to the 'terminal admin' service account. Navigate to the following directory and cat the two YAMLs to examine how these are defined:

```
~/Desktop/configuration/rbac
```

**role.yaml**

Here, you can see we define a role named "secret-admin". In the rules section, we define what it is this role can do. We define the resource (secrets), what verbs are being restricted (we are restricting the 'get' verb, but you could restrict others) and finally, the name of our secret (terminal-creds).

**role-binding.yaml**

In this YAML, we bind the 'terminal-admin' service account (in the 'subjects' section) with the 'secret-admin' role defined above (in the roleRef section).

Lets now apply these configurations the same way we applied the deployment and service (using kubectl apply):  

```
kubectl apply -f role.yaml
```

```
kubectl apply -f role-binding.yaml
```

You have now configured RBAC for this Kubernetes secret! The only thing left to do is test whether our RBAC is working. We can do this using the kubectl auth command, which tells us if a service account has sufficient permission to perform a specific action. Let us first verify that the regular 'terminal-user' service account CAN NOT access the secret:  

```
kubectl auth can-i get secret/terminal-creds --as=system:serviceaccount:default:terminal-user
```

It looks like we expected. This "no" response confirms that this service account can no longer access the terminal-creds secret. Now, finally, let us verify that our 'terminal-admin' service account CAN access it:

```
kubectl auth can-i get secret/terminal-creds --as=system:serviceaccount:default:terminal-admin
```

With this "yes" output, you have confirmed RBAC is in place and fulfilled your duty as a DevSecOps engineer, fortifying the cluster and taking a good first step into hardening this cluster.