## Configuration & Terraform  

Now that we know what Terraform is and how it works, let's take a look at how we would define the desired state using Terraform config files.
Terraform config files are written in a declarative language called HCL (HashiCorp Configuration Language), which, as discussed, is easy to understand and human-readable.
The primary purpose of this language is to declare resources; these resources represent infrastructure objects.
The combined definition of these resources makes up the desired infrastructure state.

To give you an example of how, as a DevSecOps engineer, Terraform configuration files might be used, let us consider an example where we want to define a simple VPC (virtual private cloud) using the AWS provider. That would look like this:

```bash
provider "aws" { 
 region = "eu-west-2" 
}

# Create a VPC
resource "aws_vpc" "flynet_vpc" { 
 cidr_block = "10.0.0.0/16" 
 tags = { 
  Name = "flynet-vpc"
 }
}
```

**What does the code do?** After defining our provider (which in this case is AWS), this resource block is used to define a VPC.
We first define the resource by stating the resource type, which in this case is an "aws_vpc", and then what we will call this resource. This example is "flynet_vpc".
Then begins our _resource block,_ where we define our resource arguments.
The arguments given will depend on what type of resource is being defined. For example, an aws_vpc will need a CIDR block (method for allocating IP addresses). We also define tags which can be used in AWS to help with the automation of resources, billing, access control, etc.

## Resource Relationships

Sometimes, resources can depend on other resources. When defining a resource with dependencies, the resources it depends on will be referenced. For example, if you were assigned a task to define an AWS security group ingress rule, allowing SSH access from any source within the VPC, you would add the following code block to your configuration file.

```bash
resource "aws_security_group" "example_security_group" {
 name = "example-security-group"
 description = "Example Security Group"
 vpc_id = aws_vpc.flynet_vpc.id #Reference to the VPC created above (format: resource_type.resource_name.id)

 # Ingress rule allowing SSH access from any source within the VPC
 ingress {
  #Since we are allowing SSH traffic , from port and to port should be set to port 22
  from_port = 22
  to_port = 22
  protocol = "tcp"
  cidr_blocks = [aws_vpc.flynet_vpc.cidr_block]
 }
}
```

**What does the code do?** Here, you can see we have a resource block that defines an AWS security group (helps secure AWS environments by controlling how traffic is allowed into EC2 machines), which allows SSH access from any source within the VPC. You can see in the commented lines how this is configured and how resources can be referenced from within another resource block.

## Infrastructure Modularisation

As a DevSecOps engineer, you will likely work with a large, complex infrastructure.
Another benefit of Terraform is that it allows for the modularization of an infrastructure, that is, for the infrastructure to be broken down and defined as modular components rather than in a single place.
This is common practice in larger organisations as it simplifies the management of complex infrastructure configurations. Let's take a look at what the above example configuration would look like. Below is a representation of a directory `/tfconfig` and the files within it, with a brief comment explaining the purpose of each file:

```bash
tfconfig/
 -flynet_vpc_security.tf #Like mentioned, instead of having all resources defined in one file, resources can be paired up and defined in separate modular files
 -other_module.tf
 -variables.tf #some values will be used across two or many infrastructure modules, so instead of declaring these repeatedly in each .tf file it makes sense to paramaterise them in a file called variables.tf. These variables can then be directly referenced in the .tf file.
 -main.tf #main.tf acts as the central configuration file where the defined modules are all referenced in one place
```

If we consider the example given above, if we were to define a vpc using this structure, it could be configured like so:

![[Pasted image 20250609175357.png]]

We are defining a VPC the same way as we did at the beginning of this task, except now we are storing it in a `variables.tf` file.
We are doing this so we can reuse/reference it.
This could be referenced in any module.tf file, for example, below, we have a code block for a module named `flynet_vpc_security`:

![[Pasted image 20250609175434.png]]

Finally, this module (and all other module tf files) would be collected and referenced in the main.tf file like so:

![[Pasted image 20250609175503.png]]

This level of organisation would be extreme, given how primitive the infrastructure setup is in our example.
However, this was to show you how an infrastructure at scale might be configured in a larger organisation/company.