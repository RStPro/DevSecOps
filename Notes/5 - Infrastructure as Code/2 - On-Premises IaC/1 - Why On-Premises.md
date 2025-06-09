## Reasons for On-Prem IaC

In the modern world, where we have several cloud providers, using on-prem IaC may seem counter-intuitive.
However, there are some cases where on-prem IaC will suit your needs much better. The biggest benefit is that it allows you much better control of your entire IaC pipeline. Let's use another popular example, GitHub vs self-hosted GitLab, as a case study.

GitHub and GitLab are two popular source code management platforms, backed by the popular versioning software Git, that are used by organisations.
However, deciding between the two often becomes a question of control.

If you self-host the solution using GitLab, you fully control the entire stack. You are ultimately not only responsible for the management of the GitLab platform, but also the underlying infrastructure. While this is a lot more work, it also allows you to lock down access significantly. For example, you could only allow access to your GitLab instance via VPN, meaning it is not exposed to the internet for everyone.

Conversely, using GitHub means you are shifting some of that security responsibility. It is important to remember that GitHub is a Software-as-a-Service (SaaS) solution. That means that if you use GitHub, you have no control over the infrastructure hosting your source code. Instead, you are transferring the security responsibility of infrastructure management to GitHub, which becomes a third party of your organisation. While these organisations take security measures seriously, their security is not without flaws, which can leave your organisation's source code [exposed](https://thehackernews.com/2023/01/github-breach-hackers-stole-code.html). This is a risk that you have to accept whenever you use a third party.

Extrapolating from this case study, you should see why some organisations still prefer on-prem IaC, especially in heavily regulated sectors, such as the financial or governmental sectors. While on-prem IaC is definitely more effort, it provides an organisation with full control and customization of their IaC pipeline.

## Benefits and Drawbacks

To summarize why one would use on-prem IaC and determine if it is the correct solution for your specific problem, let's look at the benefits and drawbacks.

**On-prem IaC has the following benefits:**

- Allows full control of the IaC pipeline
- The IaC pipeline can be fully customized for your exact needs
- Data protection and regulation is easier to perform as the IaC pipeline does not host resources on third-party systems
- While the initial investment cost of the infrastructure is high, there are no monthly fees for hosting the IaC pipeline
- It is often easier to do small deployments

**On-prem IaC has the following drawbacks:**

- As you are hosting your own IaC pipeline, you are fully responsible for its security and configuration
- Scalability of deployments is not as flexible as cloud-based IaC, which can lead to either not having sufficient resources for the deployment or an over-investment in resources
- The initial investment for on-prem IaC is significantly higher than cloud-based IaC

Now that you understand why on-prem IaC can be used, let's dive into some of the tooling that can be used to create your very own on-prem IaC. While there are many different tools and software that can be used, for this room, we will focus on Vagrant and Ansible as examples.