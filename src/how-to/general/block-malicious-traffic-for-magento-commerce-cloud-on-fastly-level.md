---
title: Block malicious traffic for Magento Commerce Cloud on Fastly level
labels: 2.3.x,ACL,Fastly,Magento Commerce Cloud,block traffic,how to,robots.txt,security
---

This article provides the steps you could take to block malicious traffic, when you suspect that your Magento Commerce Cloud store is experiencing a DDoS attack. 

## Affected products and versions:

* Magento Commerce Cloud 2.3.x

In this article we assume that you already have the malicious IPs and/or their country and userAgents. Magento Commerce Cloud users would typically get this information from Magento Support. The following sections provide steps for blocking traffic based on this information. All the changes should be done in the Production environment.

## Get access to Admin Panel

If your website is overloaded by DDoS, you might not be able to log in to your Magento Admin (and perform all the steps described further in this article).

To get access to Admin, put your website into maintenance mode as described in [Enable or disable maintenance mode](https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/install-cli-subcommands-maint.html#instgde-cli-maint) and whitelist your IP address. Disable the maintenance mode after this is done.

## Block traffic by IP

For the Magento Commerce Cloud store, the most effective way to block traffic by specific IP addresses and subnets is adding an ACL for Fastly in the Magento Admin. Following are the steps with links to more detailed instructions: 

1. In the Magento Admin, navigate to Stores > Configuration > Advanced > System > Full Page Cache > Fastly Configuration.
1. [Create a new ACL](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/ACL.md) with a list of IP addresses or subnets you're going to block.
1. Add it to the ACL list and block as described in the [Blocking](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BLOCKING.md) guide for the Fastly\_Cdn Magento module. 

## Block traffic by country 

For the Magento Commerce Cloud store, the most effective way to block traffic by country(s) is adding an ACL for Fastly in the Magento Admin.  

1. In the Magento Admin, navigate to Stores > Configuration > Advanced > System > Full Page Cache > Fastly Configuration.
1. Select the countries and configure blocking using ACL as described in the [Blocking](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BLOCKING.md) guide for the Fastly\_Cdn Magento module. 

## Block traffic by user agent

To establish blocking based on user agent, you need to add a custom VCL snippet to your Fastly configuration. To do this, take the following steps:

1. In the Magento Admin, navigate to Stores > Configuration > Advanced > System > Full Page Cache.
1. Then Fastly Configuration > Custom VCL Snippets.
1. Create the new custom snippet as described in the [Custom VCL snippets](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/CUSTOM-VCL-SNIPPETS.md) guide for the Fastly\_Cdn module. You can use the following code sample as an example. This sample disallows traffic for the `` AhrefsBot `` and `` SemrushBot `` user agents.

<pre><code class="language-json">name: block_bad_useragents
  type: recv
  priority: 5
  VCL:
  ```
  if ( req.http.User-Agent ~ "(AhrefsBot|SemrushBot)" ) {
      error 405 "Not allowed";<br/>
  }
  ```</code></pre>

## Rate Limiting (experimental Fastly functionality)

There is an experimental Fastly functionality for Magento Commerce Cloud which allows you to specify the rate limit for particular paths and crawlers. Please reference the [Fastly module documentation](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/RATE-LIMITING.md) for details.

<p class="warning">The functionality must be extensively tested on staging, before being used on production, because it might block legitimate traffic. </p>

## Recommended: consider updating robot.txt

Updating your `` robots.txt `` file could help to keep certain search engines, crawlers, and robots from crawling certain pages. Examples of pages that should not be crawled are search result pages, checkout, customer information and so on. Keeping robots from crawling these pages could help to decrease the number of requests generated by those robots.

 There are two important considerations when using `` robots.txt ``:

* Robots can ignore your `` robots.txt ``. Especially malware robots, that scan the web for security vulnerabilities, and email address harvesters used by spammers will pay no attention.
* The `` robots.txt `` file is a publicly available file. Anyone can see what sections of your server you don't want robots to use.

The basic information and default Magento `` robots.txt `` configuration can be found in the [Search Engine Robots](https://docs.magento.com/m2/ee/user_guide/marketing/search-engine-robots.html) DevDocs article. 

For general information and recommendations about `` robots.txt ``, see:

* [Create a robots.txt](https://support.google.com/webmasters/answer/6062596?hl=en) file by Google Support
* [About /robots.txt](https://www.robotstxt.org/robotstxt.html) by robotstxt.org

Work with your developer and/or SEO expert to determine what User Agents you want to allow, or those you want to disallow.

 
 