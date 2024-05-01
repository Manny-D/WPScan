# WPScan

![WPScan Header Image](https://github.com/Manny-D/WPScan/assets/99146530/c6d3ea0c-6b13-4b00-b906-37804102c49d)


## Description

This lab was part of an online course that presented an overview of [WPScan](https://wpscan.com), a free tool to identify security weaknesses in WordPress websites. It scans plugins, themes, and users for vulnerabilities. This will be an overview of its functionality.

<b>Remember</b>, ethical hacking requires consent!

<br>

## What is WordPress

[WordPress](https://wordpress.com) is a popular website creation tool used by over a third of all websites. It allows users to easily build and manage websites with features like plugins, themes, and user accounts, but these features can also introduce security vulnerabilities.

Plugins:

- Enhance WordPress with functionalities like editors, forms, security monitoring, etc.
- Free plugins from small teams or with infrequent updates can introduce security risks.
- WPScan identifies vulnerabilities in plugins that could be exploited by attackers.

Themes:

- Control the look and feel of your WordPress site.
- Similar to plugins, themes can have vulnerabilities that attackers can exploit.
- Update or remove vulnerable themes to fix the issue.
- Popular, frequently updated themes are generally safer.

Users:

- WordPress allows user registration for specific site access (e.g., purchasing courses).
- Attackers might try to gain access through brute-forcing passwords or social engineering.
- Leaked usernames make attacks easier. WPScan helps identify username leaks.

<br>

## WPScan: Intro

In this demonstration / walkthrough, a vulnerability scan was conducted against the securityred[.]team site that is hosted within an Amazon Web Services Virtual Private Cloud (AWS VPC). 

<b>Important note</b>: <b>DO NOT</b> scan site(s) unless you have permission, as this would be considered <b>illegal</b>!

<br>

### Basic Security Scan

No specific parameters will be specified. Generic security issues can be identified here. <br>

The command begins with: <b>wpscan --url [enter URL here]</b>

![Basic Scan](https://github.com/Manny-D/WPScan/assets/99146530/ee42184f-b1dc-4f11-b325-46c51fd4305f)

As seen above, after the tool updates it will start the scan against the target URL. Results are visible in real-time:

![Interesting Findings 1](https://github.com/Manny-D/WPScan/assets/99146530/2174a5cc-2531-4ce5-ae9e-56bddb3fde16)

First finding results: <b>securityred[.]team</b> <br>
WPScan performs basic checks by analyzing HTTP headers from the target website's root domain. This reveals the server software (Apache) and PHP version (7.2.17).

Second finding results: <b>securityred[.]team/robots[.]txt</b> <br>
WPScan also searches for common URLs and performed reconnaissance on the specified '.txt' file, which search engine spiders 'crawl' and list any related pages. <br>

Here's an example of what you'd see when visiting <b>securityred[.]team/robots[.]txt</b>:

![Crawl Result](https://github.com/Manny-D/WPScan/assets/99146530/75a1bde9-be51-44ef-ae61-62eff4be1826)

In the abobe screenshot, WPScan finds the default admin login page at /wp-admin/, highlighting a potential security risk (e.g. brute force attacks). To mitigate this, admins should change this URL and use strong admin account passwords.

<br/>

![Interesting Findings 2](https://github.com/Manny-D/WPScan/assets/99146530/7b5b7dc8-c915-45cd-ac94-c335f5be62be)

Third finding results: <b>securityred[.]team/xmlrpc[.]php</b> <br>
WPScan detects xmlrpc.php, a feature for remote content management. While convenient, it has vulnerabilities: attackers can bypass login defenses and launch denial-of-service attacks. WPScan also includes references for further testing with Metasploit.

Fourth finding results: <b>securityred[.]team/readme[.]html</b> <br>
WPScan shows the existence of a readme.html page, which may disclose private information. 

<br/>

![Interesting Findings 3](https://github.com/Manny-D/WPScan/assets/99146530/e6035039-a8ac-4c99-8e00-b48dbf92a0e0)

Fifth finding results: <b>WordPress version</b> <br>
WPScan fingerprinted the current version as 5.3.2 along with its release date. Expliots may be employed by threat actors, as this is an older / outdated version. 

<br/>

![Interesting Findings 4](https://github.com/Manny-D/WPScan/assets/99146530/6be2bb44-07f1-4be6-b493-36af6fbc02b7)

Sixth finding results: WordPress Theme: <b>mesmerize-pro</b> <br>
WPScan has identified a CSS (cascading style sheet) theme the page is using. 

<br/>

![Interesting Findings 5](https://github.com/Manny-D/WPScan/assets/99146530/41041c2c-42c6-4893-a2b4-456679253e2f)

Seventh finding results: Plugin(s): <b>mesmerize companion</b> <br>
WPScan passively identified "mesmerize-companion" plugin working with "mesmerize-pro" theme on the site.

<br/>

## End Scan Details

![Completed](https://github.com/Manny-D/WPScan/assets/99146530/ab7ea4f7-3f36-4c80-8522-4f9f13f4571b)

WPScan ends with some basic details about the scan. Its power lies in its ability to identify vulnerabilities, even on seemingly simple websites. 

<br>

### Other Parameters

To fine tune the information you may be looking for in future scan, related to vulnerable themes, vulnerable plugins, and user enumeration, the following can be used:
- wpscan –url [enter URL here] –enumerate vp
- wpscan –url [enter URL here] –enumerate vt
- wpscan –url [enter URL here] –enumerate u

<br/>

## Conclusion 

WPScan is a valuable tool for WordPress security. It can scan for vulnerabilities in WordPress plugins, themes, and user configurations. This empowers website owners to take corrective actions and harden their WordPress sites against potential attacks.
