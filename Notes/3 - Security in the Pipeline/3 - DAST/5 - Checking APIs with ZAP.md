Nowadays, web applications depend on APIs to perform some or all of their tasks. The DAST process we have shown so far involves being able to spider a traditional web application, but APIs aren't something that can be spidered easily. The endpoints of an API won't normally expose information about other endpoints, making the discovery process harder. Furthermore, even if we get an endpoint's name, we still need to know what parameters can be passed to it.

Instead of spidering APIs, we will rely on the development team to give us a precise specification of the available endpoints in an API and all of the parameters we can send to them. This way, we don't need to spend time on the discovery process but can focus on testing its security directly.

## API Descriptions

Several standards exist to document APIs, which generally include all the information developers would need to build proper requests and know what to expect as responses for each of the available endpoints. This is also all we need to start testing for security vulnerabilities.

ZAP can import APIs defined by **OpenAPI** (formerly **Swagger**), **SOAP** or **GraphQL**. Depending on the API you are testing, you might get one of these formats from the development team.

To give you a better idea of what these files contain, let's take a look at the one published on [http://10.10.23.83:8081/swagger.json](http://10.10.23.83:8081/swagger.json), which follows the OpenAPI 2.0 standard. Inside the file, you will find a section called `paths`, where every single endpoint of the API is listed. For each of the endpoints, a complete list of the available parameters is presented. For example, here you have the part of the specification on how to interact with `/asciiart/{art_id}`:

![[Pasted image 20250607171900.png]]

The file indicates that you can do calls to `/asciiart/{art_id}` using the GET method by sending the `art_id` parameter in the URL, which is a string. You can find similar definitions for other paths as `/asciiart/generate` or `/asciiart/add`.

API definition files are expected to be processed by machines, so their format might be hard to read. To make it easier for us to understand them, some APIs will also provide a more friendly UI that we can use to run quick tests and explore the available endpoints. You can go to [http://10.10.23.83:8081/swagger-ui/](http://10.10.23.83:8081/swagger-ui/) to check it.

**Note:** Production applications might hide API definitions to prevent external attackers from knowing how to interact with them. Remember, you can always ask the development team for them if needed (if they exist).  

## Importing OpenAPI definitions in ZAP

ZAP supports two methods to import API definitions: you can provide an offline file or a URL from where to download them. Since our API exposes its definition file in [http://10.10.23.83:8081/swagger.json](http://10.10.23.83:8081/swagger.json), let's use the URL option. Go to **Import -> Import an OpenAPI definition from a URL**. Specify the corresponding URL and hit the **Import** button.

![[Pasted image 20250607172207.png]]

You should now see all of the available endpoints and parameters loaded in the Sites tab.

![[Pasted image 20250607172216.png]]

ZAP will also automatically do passive scanning on the endpoints and report some alerts. After importing the API definition, ZAP will treat the API as any other normal web page.

## Scanning the API

Once an API definition is loaded into ZAP, you can use the available tools just as with any other website. To run a scan against the API, right-click its URL and select **Attack -> Active Scan**.

![[Pasted image 20250607172318.png]]

After running the scan, ZAP should have discovered some vulnerabilities in the API. Use the results of the scan to answer the questions at the end of the task.
