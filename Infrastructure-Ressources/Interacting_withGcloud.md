# Interacting with Google Cloud

There are 4 ways to interact with Google Cloud : 
1. **Google Cloud Console** : 
- Google Cloud’s graphical user interface, or GUI, that helps you deploy, scale, and diagnose production issues in a `simple web-based interface.`
- *What can i do ?*
    - find your resources
    - check their health 
    - have full management control over them
    - set budgets to control how much you spend on them
    -  provides a search facility to quickly find resources and connect to instances via SSH in the browser.

2. **Cloud SDK and Cloud Shell**
    1. Cloud SDK
        - a set of tools that you can use to manage resources and applications hosted on Google Cloud
        - Includes the `Google Cloud CLI` : provides the main command-line interface for Google Cloud products and services
        - Includes also `bq`, a command-line tool for BigQuery.
        - When installed, all of the tools within the Cloud SDK are located under the `bin directory`.
    2. Cloud Shell
        -  a Debian-based virtual machine with a persistent 5 gigabyte home directory, which makes it easy to manage Google Cloud projects and resources.
        - provides command-line access to cloud resources directly from a browser
        - With Cloud Shell, the Cloud SDK gcloud command and other utilities are always installed, available, up to date, and fully authenticated.

3. **APIs**
- The Google Cloud API Explorer shows what APIs is avalaible with its version
- Google provides Cloud Client libraries and Google API Client libraries in many popular languages to take a lot of the drudgery out of the task of calling Google Cloud from your code

4. **Google Cloud App**
- *What can i do ?*
    - start, stop, and use SSH to connect to Compute Engine instances and see logs from each instance.
    - stop and start Cloud SQL instances.
    - administer applications deployed on App Engine by viewing errors, rolling back deployments, and changing traffic splitting.
    - provides up-to-date billing information for your projects and billing alerts for projects that are going over budge
    - set up customizable graphs showing key metrics such as CPU usage, network usage, requests per second, and server errors.
    - offers alerts and incident management.