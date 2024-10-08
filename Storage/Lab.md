# Getting started with Cloud Storage and Cloud SQL

## 1. Deploy a web server VM instance

- In the Google Cloud console, on the Navigation menu (Navigation menu icon), click Compute Engine > VM instances.

- Click Create Instance.

- On the Create an Instance page, for Name, type bloghost

- For Region and Zone, select the region and zone assigned by Qwiklabs.

- For Machine type, accept the default.

- For Boot disk, if the Image shown is not Debian GNU/Linux 11 (bullseye), click Change and select `Debian GNU/Linux 11 (bullseye)`.

- Leave the defaults for Identity and API access unmodified.

- For Firewall, click Allow HTTP traffic.

- Click Advanced options to open that section of the dialog.

- Click Management to open that section of the dialog.

- Scroll down to the Automation section, and enter the following script as the value for Startup script:

```bash
apt-get update
apt-get install apache2 php php-mysql -y
service apache2 restart
```

> Note: Be sure to supply that script as the value of the Startup script field. If you accidentally put it into another field, it won't be executed when the VM instance starts

- Leave the remaining settings as their defaults, and click Create.

## 2. Create a Cloud Storage bucket using the gcloud storage command line


All Cloud Storage bucket `names must be globally unique`.

Cloud Storage buckets can be associated with either a region or a multi-region location: US, EU, or ASIA. In this activity, you associate your bucket with the multi-region closest to the region and zone that Qwiklabs or your instructor assigned you to.

- On the Google Cloud console, on the top right toolbar, click the Activate Cloud Shell Activate Cloud Shell icon. If a dialog box appears, click Continue.

- For convenience, enter your chosen location into an environment variable called LOCATION. Enter one of these commands:

```bash
export LOCATION=US
Or

export LOCATION=EU
Or

export LOCATION=ASIA
```

- In Cloud Shell, the `DEVSHELL_PROJECT_ID` environment variable contains your `project ID`. Enter this command to make a bucket named after your project ID:

```bash
gcloud storage buckets create -l $LOCATION gs://$DEVSHELL_PROJECT_ID
```

- Retrieve a banner image from a publicly accessible Cloud Storage location:

```bash
gcloud storage cp gs://cloud-training/gcpfci/my-excellent-blog.png my-excellent-blog.png
```

- Copy the banner image to your newly created Cloud Storage bucket:

```bash
gcloud storage cp my-excellent-blog.png gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png
```

- Modify the Access Control List of the object you just created so that it's readable by everyone:

```bash
gsutil acl ch -u allUsers:R gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png
```


## 3. Create the Cloud SQL instance

- In the Google Cloud console, on the Navigation menu (Navigation menu icon), click SQL.

- Click Create instance.

- For Choose a database engine, select Choose MySQL.

- For Instance ID, type blog-db, and for Root password type a password of your choice.

> Note: Choose a password that you remember. There's no need to obscure the password because you use mechanisms to connect that aren't open access to everyone.

- For Choose a Cloud SQL edition, click Enterprise and then select Sandbox from the dropdown.

- Select Single zone and set the region and zone assigned by Qwiklabs.

> Note: This is the same region and zone into which you launched the bloghost instance. The best performance is achieved by placing the client and the database close to each other.

- Click Create Instance.

- From the SQL instances details page, copy the Public IP address for your SQL instance to a text editor for use later in this lab.

- Click Users menu on the left-hand side, and then click Add User Account.
    - For User name, type blogdbuser
    - For Password, type a password of your choice. Make a note of it.
    - Click Add to add the user account in the database.

- Click Connections menu on the left-hand side, and then click Networking tab.

- Click Add a Network.

> Note: If you're offered the choice between a Private IP connection and a Public IP connection, choose Public IP for purposes of this lab.

> Note: The Add network button may be unavailable if the user account creation is not yet complete.
For Name, type web front end

- For Network, type the external IP address of your bloghost VM instance, followed by /32
    - The result will look like this : 35.192.208.2/32

> Note: Be sure to use the external IP address of your VM instance followed by /32. 
Do not use the VM instance's internal IP address. Do not use the sample IP address shown here.

- Click Done to finish defining the authorized network.

- Click Save to save the configuration change.

> Note: If the message appears like Another operation is in progress, wait for few minutes until you see the green check for blog-db to save the configuration.


## 4. Configure an application in a Compute Engine instance to use Cloud SQL
- On the Navigation menu (Navigation menu icon), click Compute Engine > VM instances.

- In the VM instances list, click SSH in the row for your VM instance bloghost.

- In your ssh session on bloghost, change your working directory to the document root of the web server:

```cd /var/www/html```

- Use the nano text editor to edit a file called index.php:
```sudo nano index.php```

- Paste the content below into the file:

```html
<html>
<head><title>Welcome to my excellent blog</title></head>
<body>
<h1>Welcome to my excellent blog</h1>
<?php
 $dbserver = "CLOUDSQLIP";
$dbuser = "blogdbuser";
$dbpassword = "DBPASSWORD";
// In a production blog, we would not store the MySQL
// password in the document root. Instead, we would store
//  it in a Secret Manger. For more information see 
// https://cloud.google.com/sql/docs/postgres/use-secret-manager

$conn = new mysqli($dbserver, $dbuser, $dbpassword);

if (mysqli_connect_error()) {
        echo ("Database connection failed: " . mysqli_connect_error());
} else {
        echo ("Database connection succeeded.");
}
?>
</body></html>
```

- Restart the web server:
```bash
sudo service apache2 restart
```

- Open a new web browser tab and paste into the address bar your bloghost VM instance's external IP address followed by /index.php. The URL will look like this:
`35.192.208.2/index.php`

> Note: Be sure to use the external IP address of your VM instance followed by /index.php. Do not use the VM instance's internal IP address. Do not use the sample IP address shown here.

- When you load the page, you will see that its content includes an error message beginning with the words: **Database connection failed: ...**

> Note: This message occurs because you have not yet configured PHP's connection to your Cloud SQL instance.

- Return to your ssh session on bloghost. Use the nano text editor to edit index.php again.
```sudo nano index.php```

- In the nano text editor, replace CLOUDSQLIP with the Cloud SQL instance Public IP address that you noted above. Leave the quotation marks around the value in place.

- In the nano text editor, replace DBPASSWORD with the Cloud SQL database password that you defined above. Leave the quotation marks around the value in place.

- Restart the web server:
```sudo service apache2 restart```

- Return to the web browser tab in which you opened your bloghost VM instance's external IP address. When you load the page, the following message appears:
**Database connection succeeded**.

## 5. Configure an application in a Compute Engine instance to use a Cloud Storage object

- In the Google Cloud console, click Cloud Storage > Buckets.

- Click the bucket that is named after your Google Cloud project.

- In this bucket, there is an object called my-excellent-blog.png. Copy the URL behind the link icon that appears in that object's Public access column, or behind the words **Public link** if shown.

> Note: If you see neither a link icon nor a "Public link", try refreshing the browser. If you still do not see a link icon, return to Cloud Shell and confirm that your attempt to change the object's Access Control list with the gsutil acl ch command was successful.

- Return to your ssh session on your bloghost VM instance.

- Enter this command to set your working directory to the document root of the web server:

```bash
cd /var/www/html
```

- Use the nano text editor to edit index.php:

```bash
sudo nano index.php
```

- Use the arrow keys to move the cursor to the line that contains the h1 element. Press Enter to open up a new, blank screen line, and then paste the URL you copied earlier into the line.

- Paste this HTML markup immediately before the URL:

```html 
<img src='
Place a closing single quotation mark and a closing angle bracket at the end of the URL:
'>
```

The resulting line will look like this:

```html
<img src='https://storage.googleapis.com/qwiklabs-gcp-0005e186fa559a09/my-excellent-blog.png'>
The effect of these steps is to place the line containing <img src='...'> immediately before the line containing <h1>...</h1>
```

- Restart the web server:
```sudo service apache2 restart```

- Return to the web browser tab in which you opened your bloghost VM instance's external IP address. When you load the page, its content now includes a banner image.

