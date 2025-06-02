## **Cluster Architecture**

Okay, so we've learned what Kubernetes is, why it's needed and how it can benefit us in DevSecOps.
Now, it's time to deepen our understanding by looking under the hood and analyzing how it can do what it does. That's right! It's architecture time! We will go through each key component that makes up Kubernetes architecture, one by one, before putting it all together at the end and showing how all these components connect. Let's get into it!
### **Kubernetes Pod**

Pods are the smallest deployable unit of computing you can create and manage in Kubernetes.

When you work in DevSecOps with Kubernetes, you'll hear a lot of this word.
You can think of a pod as a group of one or more containers. These containers share storage and network resources. Because of this, containers on the same pod can communicate easily as if they were on the same machine whilst maintaining a degree of isolation.

Pods are treated as a unit of replication in Kubernetes; if a workload needs to be scaled up, you will increase the number of pods running.

![[Pasted image 20250602180111.png]]

## **Kubernetes Nodes**

Kubernetes workloads (applications) are run inside containers, which are placed in a pod. These pods run on nodes. When talking about node architecture, there are two types to consider. The **control plane** (also known as "master node") and **worker nodes**. Both of these have their own architecture/components, so let's take a look at them. Nodes can either be a virtual or physical machine. Think of it this way: if applications run in containers which are placed in a pod, nodes contain all the services necessary to run pods.

## **Kubernetes Cluster** 

At the highest level, we have our Kubernetes Cluster; put simply, a Cluster is just a set of nodes.


# **The Kubernetes Control Plane**

The control plane manages the worker nodes and pods in the cluster. It does this with the use of various components. Take a look at each of the components and what they are responsible for. Then see them all put together in a control plane architecture diagram.

## **Kube-apiserver** 

The API server is the front end of the control plane and is responsible for exposing the Kubernetes API. The kube-apiserver component is scalable, meaning multiple instances can be created so traffic can be load-balanced.

## **Etcd** 

Etcd is a key/value store containing cluster data / the current state of the cluster.

It is highly available and consistent. If a change is made in the cluster, for example, another pod is spun up, this will be reflected in the key/value store, etcd. The other control plane components rely on etcd as an information store and query it for information such as available resources.

## **Kube-scheduler** 

The kube-scheduler component actively monitors the cluster. Its job is to catch any newly created pods that have yet to be assigned to a node and make sure it gets assigned to one. It makes this decision based on specific criteria, such as the resources used by the running application or available resources on all worker nodes.

## **Kube-controller-manager** 

This component is responsible for running the controller processes. There are many different types of controller processes, but one example of a controller process is the **node controller** process, which is responsible for noticing when nodes go down. The controller manager would then talk to the scheduler component to schedule a new node to come up.

## **Cloud-controller-manager**

This component enables communication between a Kubernetes cluster and a cloud provider API. The purpose of this component is to allow the separation of components that communicate internally within the cluster and those that communicate externally by interacting with a cloud provider. This also allows cloud providers to release features at their own pace.

![[Pasted image 20250602180651.png]]

# **Kubernetes Worker Node**

Worker nodes are responsible for maintaining running pods. Let's take a look at the components, which are present on every worker node, and what they are responsible for:  

## **Kubelet** 

Kubelet is an agent that runs on every node in the cluster and is responsible for ensuring containers are running in a pod. Kubelet is provided with pod specifications and ensures the containers detailed in this pod specification are running and healthy! It executes actions given to it by the controller manager, for example, starting the pod with a container inside.

## **Kube-proxy** 

Kube-proxy is responsible for network communication within the cluster. It makes networking rules so traffic can flow and be directed to a pod (from inside or outside of the cluster). Traffic won't hit a pod directly but instead hit something called a Service (which would be associated with a group of pods), and then gets directed to one of the associated pods. More on services in the next task!

## **Container runtime**

Pods have containers running inside of them. A container runtime must be installed on each node for this to happen. So far, we have covered one example of this in this module, which is probably the most popular choice, Docker. However, some alternatives can be used, such as rkt or runC.

![[Pasted image 20250602180940.png]]

# **Communication Between Components**

Okay, so we've covered a lot there. Let's take a step and look at how all those individual components we've just covered work together to make up Kubernetes architecture. A Kubernetes cluster contains nodes and Kubernetes runs a workload by placing containers into pods that run on these nodes. Take a look at the graphic below to see how all these components come together.

![[Pasted image 20250602181042.png]]

