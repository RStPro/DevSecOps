Let's start with the big question, shall we? What is Kubernetes? In the previous rooms in this module, we discussed containers and Docker, so let's use that as our jumping-off point.

Imagine you have a Docker container that is running an app that can be accessed externally. Suddenly, this application starts receiving a lot of traffic, so a new container with this application needs to be spun up so the traffic can be distributed between the two. This is where Kubernetes comes in as a container orchestration system.

The term "orchestration" conjures up images of a literal orchestra. This metaphor does have some traction, with the containers being like instruments and Kubernetes being the conductor in control of the flow. It would just be a very strange orchestra where the conductor tells the players to leave when they're no longer needed for the song and brings new ones on when they are.

## **The Many Benefits of Kubernetes**

Now that we've established what Kubernetes is and why it’s needed, let's look at how this technology can benefit the DevSecOps space.

- Kubernetes makes an application **highly available and scalable**. It does this by, for example, duplicating an application (and its db component) and load balancing external requests to this application to an available resource, therefore removing a single point of failure from the architecture and removing bottlenecks, which can slow down application response times. As mentioned earlier, scalability is a big concern for many companies; Kubernetes allows workloads to be scaled up or down to match demand.
- Kubernetes is also **highly portable** in that it can be run anywhere with nearly any type of infrastructure and can be used with a single or multi-cloud set, making it a very flexible tool.
- Another benefit of Kubernetes is its popularity; because of this, many technologies are compatible with it and can be used to make each tool more powerful.

These are just a few ways Kubernetes benefits the DevSecOps space, and it explains why that word is thrown around so much!

