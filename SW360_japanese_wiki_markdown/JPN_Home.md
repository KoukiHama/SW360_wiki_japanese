_SW360 Wiki! へようこそ_

For development, please see the [README.md](https://github.com/eclipse/sw360/blob/master/README.md) file of the project first. Please check also the pages on the right widget of pages. Not every page there has a link on this page!

### Getting started

sw360chat - Slack Channel - https://join.slack.com/t/sw360chat/shared_invite/enQtNjczODE1NjMxNTg4LTU1NDViYTIyOGI2Y2JlZWJhMjFmNDYwY2VkZmVjYmIxZmM4ODU0NjFhNmJlYjgwMDUzNjI2ZTI1NGNkNmI4ZDY

### Naming Policies for this Wiki

Please start every page with a prefix

1. User: topics suitable for admins and end users
1. Admin: for setting up and configure and maintain
1. Dev: All topics for developers

# Using sw360

For using the sw360 as a user, please see the following basic workflows:

* Basic workflows for [creating a component, release and projects](https://github.com/eclipse/sw360/wiki/User-Workflows:-sw360).
* Workflow how [FOSSology and sw360](https://github.com/eclipse/sw360/wiki/User-Workflows:-sw360-and-FOSSology) play together.
* How to [search](https://github.com/eclipse/sw360/wiki/User-Search) in sw360

### General

* Use case description importing projects, releases with licenses [BDP Import](User--BDP-Import)
* Use case description how to [manage vulnerabilities in your project](User-Vulnerability-Management)
* User documentation how to [use the cve-search server](User--Scheduling-CVE-Search-by-Admins)
* User documentation how to [check vulnerabilities for your projects](User-Check-Vulnerabilities-for-Your-Project)
* Documentation about the [handling of vulnerabilities](User-Vulnerability-Management)

### Special

1. Find information about the [role and access model](https://github.com/eclipse/sw360/wiki/Dev-Role-Authorisation-Model)
1. If you are interested in the concept about [moderation requests](https://github.com/eclipse/sw360/wiki/Dev-Moderation-Requests), read the documentation here.
1. Explaining [[enumerations used in SW360|https://github.com/eclipse/sw360/wiki/User-Data-Model-Enumerations]]

# Deploying sw360

In order to install sw360, you can choose between the following ways:

* Use the Vagrant-based installation. Please refer to the [sw360 vagrant project](https://github.com/sw360/sw360vagrant) and the included Readme file. Basic prerequisites are
  * VirtualBox
  * Vagrant
  * Presumeably a git client
* You could install the sw360portal project natively on the machine. This will require more work in order to install the prerequisites. The above mentioned vagrant project documents very precisely what to do in order to install the sw360portal.
* Checkout the docker suite [sw360chores](https://github.com/sw360/sw360chores) and run a docker-based deployment.
* Checkout the docker suite [sw360chores](https://github.com/sw360/sw360chores) and generate a pre-built container where you can deploy the `*.war` files of sw360portal (both frontend and backend)

### General

* [Deployment Requirements](Deploy-requirements)
* [Deployment Authorization Concept](Deploy-authorization-concept)
* sw360.properties explained

### Special

Once the vagrant deployment is ready, a couple of additional steps need to be applied:

1. [Setup liferay / sw360](Deploy-Liferay)
1. [Setup of connection with Fossology](Deploy-FOSSology)
1. [Initial Suggestions for a Secure Deployment](Deploy-Secure-Deployment)
1. [More information on how to user sw360vagrant on Windows](Deploy-sw360-on-Windows-(with-Vagrant))
1. [Again, another description special report](Deploy-vagrant-win7): getting sw360 running using vagrant on Win7 machines

### Very Special

After installing sw360 more topics may include:

1. [How to export data and import it to a new instance](Deploy-Export-and-Import)
1. [How to migrate an existing sw360portal to a new instance](Deploy-Migrating-to-a-new-Server)
1. [Using costco to modify the couchdb database](Dev-Database-Migration-using-Costco)
1. [Special Coverage of Country Codes](Deploy-configuration-country-codes), when countries are displayed, then it uses country codes in the DB 

# Developing sw360

The sw360 is Java-based application consisting of two main parts:

1. A Liferay/based front end application that allows users to work with sw360
1. A Java-based servlet infrastructure Thrift interfaces that allows the Liferay part and other applications to manage and store data
1. In the backend, couchdb is used for storing project, component, release and license information as well as attachments.

### Contributing: Submitting Issues

Please report issues to the issue tracker, but please keep also in mind that someone else has to read them! Issues should include:

* What you intended to do?
* What did you observe?
* Why do you think it is wrong?
* Screenshots of what you have observed presumably gone wrong or link to pages were another person can follow
* Version where you have observed this.
* Common written English and use of line breaks!!! Use the preview function!

Please refer to the following pages for writing issues:

* https://issues.apache.org/bugwritinghelp.html
* https://developer.mozilla.org/en-US/docs/Mozilla/QA/Bug_writing_guidelines
* https://www.joelonsoftware.com/2000/11/08/painless-bug-tracking/

### Workflow

As basic introduction, the dev ops works as following:

1. We are issue-based, please do not hesitate to create issues - also for _questions_ (and set the issue tag)
1. The issues are organised by milestones which [do not represent releases anymore](Dev-Releasing-SW360). Milestone are meant to be useful packages of work done
1. Contributions are made through pull requests
1. We do conversations directly on issues and pull requests

More topics regarding "how" to develop:

1. [Definition of done and code style](Dev-DoD-and-Style)
1. [Creating a sw360 release](Dev-Releasing-SW360)
1. [Brief notes on the jgiven testing](Dev-Testing-Frameworks)
1. [For help with problems, you might want to check that](Dev-Troubleshooting)

### Architecture

sw360 is a server application using Java servlets. It did some faint steps towards micro services (ie. one maintaining licenses, another for vulnerabilities), the front end is a portlet applications using good old JSPs.

1. [Introduction and Scope](Dev-Arch-General)
2. [High Level View](Dev-Arch-View)
3. [Architecture Topics](Dev-Arch-Topics)

### General

1. [How to write a new portlet](https://github.com/eclipse/sw360/wiki/Dev-Adding-a-new-portlet:-Frontend)
1. [Adding a new backend service](https://github.com/eclipse/sw360/wiki/Dev-Adding-a-new-portlet:-Backend)
1. [Changing the data model](Dev-Adding-New-Fields-to-Existing-Classes)
1. [REST API overview](Dev-REST-API)
1. [Migrating to Javascript modules](Dev-Using-RequireJS-for-javascript-modules)

### Special

1. [Filtering in portlets](Dev-Filtering-in-Portlets)
1. [The FOSSology integration](Dev-Fossology-Integration)
1. [How moderation requests work](Dev-Moderation-Requests)
1. [Roles and access rights](Dev-Role-Authorisation-Model)
1. [Attachment Types Description](Dev-Attachment-File-Types)
1. [Our ideas of Google-Summer-of-Code 2019](https://wiki.eclipse.org/Google_Summer_of_Code_2019_Ideas#Eclipse_SW360)
1. [How Friendly URLs work with the Liferay Portlets](Dev-Liferay-Friendly-URL)

### Testing

Generally, all modules have unit tests and these are executed (including deployment of couchdb) at CI times. In addtion, to test the front end, there are defined integration test cases for a manual check, if the sw360 is working properly in general:

1. [Test Cases: Components Functionality](Test-Cases-Components)
1. [Test Cases: Licenses Functionality](Test-Cases-Licenses)
1. [Test Cases: Moderations Functionality](Test-Cases-Moderations)
1. [Test Cases: Projects Functionality](Test-Cases-Projects)
