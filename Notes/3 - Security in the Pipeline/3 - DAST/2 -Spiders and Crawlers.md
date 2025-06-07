## Spidering an app with ZAP

The first step we'll take is to get a map of all resources in our target web application to identify the scope of our analysis. ZAP provides a spidering module that we can use to that end. A **Spider** will navigate to a starting page you provide and fundamentally explore the website by following all the links it can detect.

![[Pasted image 20250607162402.png]]

To spider a website, we can go to **Tools -> Spider**. This will show us the Spider dialogue, where we only need to specify a website as our starting point. For now, we'll leave the Context and User boxes empty. You can check the following additional options if needed:

- **Recurse:** Spider the website for links recursively.
- **Spider Subtree Only:** Limit the spidering to subfolders of the Starting Point URL.
- **Show Advanced Options:** Enable the Advanced tab, where you can specify additional parameters to tune your spidering.
![[Pasted image 20250607162507.png]]

Point to [http://10.10.23.83:8082/](http://10.10.23.83:8082/) and press Start Scan. After a while, you should see all the URLs that the spider found on the Sites tab:

![[Pasted image 20250607162557.png]]

You should now see the Sites list populated with all URLs found during spidering. Any item outside your starting page's URL is considered out-of-scope and won't be added to the list.

You might notice that if you navigate manually to [http://10.10.23.83:8082/](http://10.10.23.83:8082/), you should see a link in the menu that points to `/nospiders-gallery.php`, but if you expand the sites list on ZAP, you won't see this URL.

![[Pasted image 20250607162645.png]]

This happens because this particular link is not directly embedded in the page's HTML code but is generated on-the-fly by using javascript on your browser (as many modern applications do). Since the regular spider in ZAP doesn't have a javascript engine, it has no way of finding that link.

## More Spiders

To overcome the limitations of ZAP's regular spider, ZAP can leverage a real browser like Firefox or Chrome to process any scripts attached to the website and retrieve the resulting HTML code.
Instead of parsing links directly from HTTP responses, it will do so from the result of a browser processing the website. This can be achieved by using the **AJAX spider**.

![[Pasted image 20250607162743.png]]
Leveraging a real browser is highly advantageous, as ZAP doesn't have to deal with all of the intricacies of current javascript engines but rather delegates this task to a browser, guaranteeing that the result will match what a user will see if they use the same browser.

Using the AJAX spider is a similar process to the regular spider. Just go to **Tools -> AJAX Spider**, configure a URL as a starting point and check the options you see fit. The only new option you have is the Browser selection, where we will choose Firefox this time. The list of browsers also has headless options, which will run the selected browser without showing you its graphical interface, but for now, let's stick to regular Firefox, as it makes it easier to understand how the AJAX spider works. Your configuration should look like this:

![[Pasted image 20250607162811.png]]

Let's hit Start Scan to make it work. You should see Firefox popping up and navigating the website for a bit. When the AJAX spider is done, it will populate the Sites in ZAP, just as the regular spider. Since the AJAX spider leverages the power of Firefox to get better results, you should now see `/nospiders-gallery.php` in your Sites list in ZAP.

![[Pasted image 20250607163227.png]]

