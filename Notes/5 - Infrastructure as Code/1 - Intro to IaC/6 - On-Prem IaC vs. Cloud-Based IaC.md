Infrastructure as code has two use cases. On-premises IaC and cloud-based IaC.

Going forward, this module will go in-depth and give practical examples of both of these. Let’s first establish the key differences between the two. Here, we outline key differences between on-prem IaC and cloud-based IaC across five categories: Location, Tech, Resources, Scalability and Cost.

## Comparison

![[Pasted image 20250609112736.png]]

**On-prem:** As the name implies, if your infrastructure is on-prem, then the code written will configure servers, network devices, storage and software located on your premises. This can mean physical infrastructure in a premises owned by an organisation or rented in a data center.

**Cloud-based:** This means provisioning and configuring infrastructure resources in a cloud environment using cloud resources. This is done using a cloud service provider (CSP) such as AWS, Microsoft Azure, GCP, etc.

![[Pasted image 20250609112751.png]]

**On-prem:** Typically, when working with an on-premises infrastructure, IaC tools like Ansible, Chef and Puppet would be used (although others can be configured to do so) to manage and provision infrastructure on physical servers or virtual machines in an on-prem data centre. 

**Cloud-based:** There are many tools available to provision and manage cloud infrastructure designed to leverage the elastic nature of cloud computing, with some cloud service providers having their own IaC tool/service. Some examples of tools that can be used for cloud-based IaC are Terraform, AWS CloudFormation, Azure Resource Manager (ARM) templates and Google Cloud Deployment Manager.

![[Pasted image 20250609112824.png]]

**On-prem:** When using on-prem IaC, you’ll likely be dealing with physical hardware, which comes with the caveats of hardware compatibility, physical upkeep and limited physical resources. This will mean setting up and configuring those physical resources (physical servers, storage devices, network equipment, etc.). On-prem IaC may be used by companies who rely on their on-premises infrastructure due to legacy systems and require assistance in the efficient management of this infrastructure. 

**Cloud-based:** In the cloud, you interact with virtual resources provided by the cloud service provider (AWS, GCP, Azure, etc.). These resources can be provisioned/managed by cloud-based IaC tools. The underlying infrastructure is handled by the CSP and not the user. Cloud-based IaC would be perfect for companies that offer video streaming services. Due to the nature of this service, it can lead to a fluctuating demand on computing resources, which can peak. Cloud-based IaC makes it easy to gain access to additional cloud-based virtual machines or storage depending on resource consumption to ensure consistent performance during these peaks.

![[Pasted image 20250609112902.png]]

**On-prem:** Scaling resources using on-prem IaC can be a slow and cumbersome process. This can involve manual/physical changes and procurement. Because scalability is such a slow process, consideration is required, and hardware limitations must be enough to handle peak load. This can prove challenging in situations where an on-premises infrastructure starts receiving increased traffic (think enrolment or exam season at a university/college).

**Cloud-based:** Due to the cloud’s elastic nature, scaling resources is far more flexible than on-premises. Cloud-based IaC tools can define scaling policies so resources can be scaled up or down based on demand and resource consumption, leveraging auto-scaling features. This ensures that only the resources needed are paid for. Cloud-based IaC can streamline the process of scaling infrastructure to meet demands during peak seasons. Imagine an infrastructure that supports an online game. This infrastructure would see increased traffic when the game releases a new update, or an event is underway.

![[Pasted image 20250609112954.png]]

**On-prem:** On-premises infrastructure expenses mean having to pay for physical hardware (or leasing a server from a third-party data centre - depending on the use case); this also comes with the costs of physical upkeep (fault repairs/part replacements, etc.), operational costs and expenses involved in upgrading the infrastructure. An on-premises infrastructure and the use of on-prem IaC doesn't boast any cost benefits per se. If choosing on-prem, it would likely be due to a combination of other factors rather than cost.

**Cloud-based:** When using cloud-based IaC, you’ll deal with infrastructure that cloud service providers bill for on a pay-as-you-go basis. This means you only need to pay for what you use (which can be made more cost-effective by the efficient use of auto-scaling). Cloud-based IaC tools are an ideal and cost-effective solution for scenarios where infrastructure needs to be automatically scaled up and down on demand. For example, if an online retailer is expecting an increase in traffic over Black Friday weekend or over the holiday period, they may want to scale up their resources but not have to pay for those resources when traffic returns to an average rate.

When comparing cloud-based infrastructure as code with on-premises infrastructure as code, it primarily comes down to the **location** of the **infrastructure** and what tools are used in their management and provisioning. Cloud-based IaC uses virtual elastic resources, which are charged on a pay-as-you-go basis and provided by a CSP, whereas on-prem IaC deals with physical hardware.

## Benefits 

Let’s examine how the above-mentioned differences translate into benefits depending on specific use cases. Here are some of the benefits of each to give you an idea of when you might use on-prem IaC and Cloud based IaC:

**On-prem IaC:** The main advantage of on-premises infrastructure as code is that it allows complete control. This complete control is sometimes required due to regulations/security and compliance requirements. This is common in bigger banking corporations or businesses that deal with customer-sensitive or government data. These regulations can call for data sovereignty (meaning the data has to be stored and processed within the country). Whilst cloud providers offer specialized government cloud environments for some of these cases (e.g. us gov cloud in AWS), these offerings are only available in certain regions; for regions like Africa, there is no dedicated government cloud, meaning on-premises infrastructure as code would need to be used to adhere to strict security/compliance requirements. 

**Cloud-based** **IaC:** It has many advantages for fast-paced and growing businesses. The scalability allows infrastructure to be rapidly scaled up or down to meet fluctuating demand without the constraints of physical on-premises infrastructure. Cloud-based infrastructure also allows infrastructure to be deployed globally across different regions, reducing user latency, which can be essential for businesses that need to provide a service to customers worldwide with little to no latency, like online gaming. With cloud providers billing on a pay-as-you-go basis, this can mean that companies can pay only for the infrastructure that they need/use, meaning investment doesn’t need to be made into physical hardware and the maintenance of that hardware.