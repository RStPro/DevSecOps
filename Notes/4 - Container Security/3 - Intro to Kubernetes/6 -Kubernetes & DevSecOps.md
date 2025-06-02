## **Kubernetes and Security **

Before we dive into what a DevSecOps engineer would be responsible for in a Kubernetes cluster, let's consider Kubernetes from a security perspective to give some context. Kubernetes is, relatively speaking, new on the block. That is to say, it is an emerging technology. It's emerging but very popular, with many companies adopting Kubernetes, especially young tech and start-up companies. 

Introducing any tool into a system is considered an increased security risk as a new tool means a new potential way into that system. These risks are amplified when dealing with a tool like Kubernetes, where you have a network of pods that can communicate with each other. The default setting allows any pod to communicate with another. This implies all kinds of security considerations. As a DevSecOps engineer, it is your responsibility to ensure these channels are secure.

![[Pasted image 20250602190400.png]]

## **Kubernetes Hardening**

Container hardening is one way in which DevSecOps engineers can secure these channels, and we will dive into that later in this module with the [Container Hardening](https://tryhackme.com/room/containerhardening) room. It is the process of using container scanning tools to detect CVEs present in a cluster and remediate them to ensure minimal security breach risk.

Kubernetes hardening is precisely that, ensuring these channels are secure by fortifying your cluster following best container security practices that you would perform as a DevSecOps engineer. Various companies and government agencies have defined these best practices; let's go over each area in which we can strengthen our container security and how this can be done.

## **Secure your Pods!** 

Let's begin with a few ways to secure the pods themselves. Some best practices for pod security include:

- Containers that run applications should not have root privileges
- Containers should have an immutable filesystem, meaning they cannot be altered or added to (depending on the purpose of the container, this may not be possible) 
- Container images should be frequently scanned for vulnerabilities or misconfigurations 
- Privileged containers should be prevented  
- [Pod Security Standards](https://kubernetes.io/docs/concepts/security/pod-security-standards/) and [Pod Security Admission](https://kubernetes.io/docs/concepts/security/pod-security-admission/)

## **Hardening and Separation of your Network!**

In the introduction to this task, one thing especially was flagged as a big security risk: communication. That communication happens over a network, and it's your job as a DevSecOps engineer to ensure this communication is secure. This can be done using the following best practices: 

- Access to the control plane node should be restricted using a firewall and role-based access control in an isolated network
- Control plane components should communicate using Transport Layer Security (TLS) certificates
- An explicit deny policy should be created
- Credentials and sensitive information should not be stored as plain text in configuration files. Instead, they should be encrypted and in Kubernetes secrets

## **Using Authentication and Authorization Optimally** 

It wouldn't be a security lesson if we didn't talk about authentication and authorization, of course! Kubernetes is no different. Here are some best practices which can help make sure you are making efficient use of Kubernetes authentication and authorization features: 

- Anonymous access should be disabled 
- Strong user authentication should be used 
- RBAC policies should be created for the various teams using the cluster and the service accounts utilised 

## **Keeping an Eye Out**

You can't rest easy knowing your Kubernetes cluster is secure if you don't know what's going on in your Kubernetes cluster. Here are some logging best practices to ensure you know exactly what is going on in your cluster and can detect threats when they appear: 

- Audit logging should be enabled 
- A log monitoring and alerting system should be implemented

## **Security Never Sleeps**

This is in no way an endorsement of a sleepless lifestyle; DevSecOps engineers do, in fact, need to sleep! Being secure is one thing, staying secure is another. Here are some best practices to ensure your cluster stays a safe haven: 

- Security patches and updates should be applied quickly
- Vulnerability scans and penetration tests should be done semi-regularly 
- Any obsolete components in the cluster should be removed

# **Kubernetes Security Best Practices in Action**

![[Pasted image 20250602190719.png]]

The above information tells us there are **a lot** of ways to harden a Kubernetes infrastructure. There are so many, in fact, that breaking down each practice would turn this room into a self-published e-book. With the opportunity to get your hands on Kubernetes just a task away, let's finish this one by breaking down just three of them.

## **RBAC** 

RBAC (Role-Based Access Control) in Kubernetes regulates access to a Kubernetes cluster and its resources based on defined roles and permissions. These permissions (permission to create/delete x resource, etc.) are assigned to users, groups or service accounts. RBAC is a good way to ensure the resources in your cluster can only be accessed by those who **need** to access it. RBAC can be configured using a YAML file (same as defining a resource) where specific rules can be defined by declaring the resource type and verbs. Verbs are the actions being restricted, such as 'create' and 'get'.  

## **Secrets Management**

A Kubernetes secret is an object used to store sensitive information (like credentials, OAuth tokens or SSH keys). Secrets are a good way to ensure that sensitive data isn't leaked and allow for more control over how this information is used. Secrets are stored as a base64 encoded string, unencrypted by default. For security, it is best to configure encryption at rest. Another way to promote secure secrets management in your Kubernetes cluster is to configure the least privilege access to secrets using RBAC.  

## **PSA (Pod Security Admission) and PSS (Pod Security Standards)**

Pod Security Standards are used to define security policies at 3 levels (privileged, baseline and restricted) at a namespace or cluster-wide level. What these levels mean: 

- Privileged: This is a near unrestricted policy (allows for known privilege escalations)
- Baseline: This is a minimally restricted policy and will prevent known privilege escalations (allows deployment of pods with default configuration)
- Restricted: This heavily restricted policy follows the current pod hardening best practices

Pod Security Admission (using a Pod Security Admission controller) enforces these Pod Security Standards by intercepting API server requests and applying these policies.

**Note:** Previously, the roles of PSA and PSS were fulfilled using PSPs (Pod Security Policies); however, as of Kubernetes v1.25, these have been removed. Just to save any confusion if you stumble across PSPs doing some extracurricular Kubernetes security study!

As you can see, a lot goes into fortifying a Kubernetes cluster and plenty to keep a DevSecOps engineer busy. These are some of the best practices involved in Kubernetes hardening. DevSecOps engineers, while following these practices and utilising techniques such as automated security checks, can ensure their Kubernetes environment is safeguarded against cyber threats.