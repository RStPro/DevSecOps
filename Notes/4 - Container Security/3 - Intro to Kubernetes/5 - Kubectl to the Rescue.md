We've just covered how to define the desired state of your cluster using YAML config files, but currently, those exist only as files.

To take these from configurations to running processes, we need to interact with the cluster. We can do this by interacting with the apiserver component of the control plane using different methods: UI if using the Kubernetes dashboard, API if using some sort of script or command line using a tool called kubectl.

This task focuses on the last of these. Simply put, kubectl is a command line tool provided by Kubernetes that allows us to communicate with a Kubernetes cluster's control plane and is a great addition to your DevSecOps arsenal. This task will show you how to take the config files outlined in the previous task and apply them, as well as give you some boot camp training for this tool, teaching you some of the basic commands so you can navigate a Kubernetes cluster like it's your back garden!

## **Kubectl apply** 

Once you have defined your deployment and service configurations in the YAML file, the next step would be to apply them so Kubernetes can take the desired configuration and turn it into a running process(s). This is done using the aptly named apply command. For example, if applying the service YAML mentioned in the previous task, that would look like this:

```
kubectl apply -f example-deployment.yaml
```

## **Kubectl get** 

Once both configurations have been applied, you'll want to check the status of both to ensure things are running as expected. This would be done using the Kubectl get command. This is a very versatile command, and you will be using it a lot in your time with Kubernetes. The get command can be used to check the state of resources. The resource type will follow 'get', then `-n` or `--namespace` followed by the namespace (unless you are checking a cluster-level resource like a node). For example, to check the state of a deployment, you would use:

```
kubectl get pods -n example-namespace
```

The output for this command would look something like this:

![[Pasted image 20250602185008.png]]

As mentioned, this command can be used to check on a variety of resources such as deployments, services, pods, and ReplicaSets.

## **Kubectl describe** 

This command can be used to show the details of a resource (or a group of resources). These details can help in troubleshooting or analysis situations. For example, say one of the pods in your cluster has started erroring out, and you want to get more information about the pod to try to determine why it has crashed. You would run the following command:

```
kubectl describe pod example-pod -n example-namespace
```

This would give you back some details about the erroring pod. For example:

![[Pasted image 20250602185613.png]]

You can see here that the describe command details contain some "events". These events can help shine a light on what the issue is. For more details surrounding this event, Kubernetes captures logs from each container in a running pod. These logs can be viewed using our next command.

## **Kubectl logs** 

Say you want to view the application logs of the erroring pods. Maybe you want to view the logs surrounding the event error. For this, we would use the kubectl logs command. Here is an example of how this would be used:

```
kubectl logs example-pod -n example-namespace
```

These logs can provide valuable insight not just for troubleshooting but for security analysis as well.  

## **Kubectl exec**

Now, let's say the log information was helpful, but there are still some unanswered questions, and you want to dig deeper and access the container's shell. The kubectl exec command will allow you to get inside a container and do this! If a pod has more than one container, you can specify a container using the `-c` or `--container` flag. The command for this is (the `-it` flag runs the command in interactive mode, everything after `--` will be run inside the container): 

```
kubectl exec -it example-pod -n example-namespace -- sh
```

From here, you can run any command you want from within the container itself. Maybe you want to snoop around for your security analysis or run a command to test connectivity from the container.

## **Kubectl port-forward** 

Another handy command is kubectl port-forward. This command allows you to create a secure tunnel between your local machine and a running pod in your cluster. An example of when this might be useful is when testing an application.

Let's imagine we have an nginx web application running across 3 pods which are exposed by a web application service. If you remember, a service makes a pod externally accessible. We take the port that is used to expose these pods and map it to one of our local ports. For example, matching the target port (the port the service is exposed on, which in our configuration example was 8080) to local port 8090 would make this web application accessible on our local machine at `http://localhost:8090`. The resources specified are `resource-type/resource-name`. This would be done using the kubectl port-forward command with the following syntax : 

```
kubectl port-forward service/example-service 8090:8080
```

There are, of course, plenty more kubectl commands that can be used to navigate and interact with a Kubernetes cluster, but the ones covered give you a solid foundation, and you can perform some day-to-day DevSecOps tasks using only these.