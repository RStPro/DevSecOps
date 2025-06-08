Generally, when discussing DAST, people will refer to implementing automated vulnerability scanning into your development pipeline rather than the manual process we have covered. In this way, the term differs from what you would typically call application pentesting.

Having DAST added to your development process may sound pretty straightforward, but there are some caveats to it:

- We must decide at which stages of the development process we will run scans.
- We must decide what will trigger a scan. We can run scans on each commit made to code or on a scheduled basis.
- We must determine the intensity of each scan. Doing a full vulnerability scan on a medium-sized application will require significant time, and we don't want to slow down the development team.

Since no solution fits all scenarios, determining all of this must be done with the help of the development team so that security requirements are met without actually creating significant disturbances to their established processes.

In this task, we'll examine how we can quickly implement DAST directly into the development pipeline to provide early visibility of vulnerabilities. The scans will run automatically on each commit and will test for a subset of vulnerabilities only to avoid introducing long delays in the pipeline.

## Reviewing our CI/CD Pipeline

Our current machine implements the entire development pipeline for the web application and API you scanned previously. The following two components are in charge of doing that:

- A Gitea repository is running on [http://10.10.182.86:3000/](http://10.10.182.86:3000/), where the code for both applications is stored.
- A Jenkins instance that runs the CI/CD pipeline. You can access Jenkins at [http://10.10.182.86:8080/](http://10.10.182.86:8080/).

Every time a commit is made in Gitea, Jenkins will take the code from the repository and compile it into a Docker instance. These Docker instances are what you have scanned so far.

![[Pasted image 20250607193041.png]]

To access Gitea or Jenkins, you can use the following credentials:

| **Username** | thm |
| ------------ | --- |
| **Password** | thm |
## Running Automated Scans With zap2docker

To integrate ZAP in our pipeline, we will use **zap2docker**, a dockerized version of ZAP proxy built with automation as its primary purpose. The full documentation for zap2docker can be found [here](https://www.zaproxy.org/docs/docker/).

**Note:** The commands in this section are provided for reference only. You don't need to run them manually, as we will have Jenkins do it for us later.

To install zap2docker, you can pull it from Docker Hub using the following command

```Shell
docker pull owasp/zap2docker-stable
```

You can run ZAP from the docker instance using one of the packaged scan scripts, which will allow you to run one of the following scan profiles:  

**Baseline Scan:** ZAP will spider the target website for a maximum time of 1 minute. No active scan will be performed. You can optionally run an AJAX spider if desired.

```Shell
docker run -t owasp/zap2docker-stable zap-baseline.py -t https://www.example.com
```

**Full Scan:** ZAP will run a spider with no time limits, followed by an active scan.


```Shell
docker run -t owasp/zap2docker-stable zap-full-scan.py -t https://www.example.com
```

**API Scan:** ZAP will perform an active scan against an API. You will need to provide a URL to an API description file (OpenAPI, GraphQL or SOAP).

```Shell
docker run -t owasp/zap2docker-stable zap-api-scan.py -t https://www.example.com/swagger.json -f openapi
```

In any of the scans, the results for passive scans will be limited to 10 alerts. In addition to the base commands, you can add the `-j` switch to perform an AJAX scan on the baseline and full scans.

## Integrating ZAP Into the Pipeline

The environment you have access to already has a zap2docker instance ready to use. All we need to do is to tell Jenkins to run zap2docker with the options we need, and that will be it.

Before going into that, let's explore what we have in Jenkins.
When logging into Jenkins, you will find an **organisation** called thm, which contains the two **repositories** for the web application and API.
For each of the repositories, you can see the available **branches**.

![[Pasted image 20250607193658.png]]

You will have a single branch in both projects called `main`.
If you click on the branch, you will be able to see the builds for it. The `simple-webapp` project, for example, has been built two times already:

![[Pasted image 20250607193719.png]]

For each build, we can see there are two stages configured:  

- **Build the Docker image:** This stage will build the Docker container based on the Dockerfile on each project.
- **Deploy the Docker image:** This stage will deploy the Docker container.

Both of these stages are defined in the **Jenkinsfile** in each repository. If we go to Gitea and open the [Jenkinsfile](http://10.10.182.86:3000/thm/simple-webapp/src/branch/main/Jenkinsfile) on the simple-webapp repository, we can see the specific commands run on each of the stages:

![[Pasted image 20250607193805.png]]

In the second stage, you can see how the web application you scanned manually is deployed to port 8082, for example.

If we want to incorporate zap2docker into our pipeline, we can add a third stage that runs the scan for us after building the container. For your convenience, the stage is already defined at the end of the Jenkinsfile, and you can uncomment it to get it running. Feel free to use `git` to send a commit to the repository or use Gitea's built-in editor if you find it easier:

![[Pasted image 20250607194021.png]]

Notice that we are running the **Baseline Scan** only, as this scan will be run for each commit made to the repository, so it isn't sensible to delay the pipeline with a Full Scan that might take hours to finish. This scan intends to find low-hanging fruit only. This means you won't see any SQL injection, Cross Site Scripting, or anything else that requires an active scan. 

Since Jenkins will catch any changes in the repository, it will start the building process immediately after you edit the file. You can switch back to the simple-webapp project in Jenkins to see the progress live:

![[Pasted image 20250607194116.png]]
