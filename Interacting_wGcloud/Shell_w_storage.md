# Google cloud Shell with Google Cloud Storage 

## 1. Use the Cloud Console to create a bucket


- In the Cloud Console, on the Navigation menu (Navigation menu), click Cloud Storage > Bucket.

- Click Create.

- For Name, type a globally unique bucket name; leave all other values as their defaults.

- Click Create.
    - If prompted Public access will be prevented click Confirm.

- Explore features in the Cloud Console
    - The Google Cloud menu contains a Notifications icon. Sometimes, feedback from the underlying commands is provided there. If you are not sure what is happening, check Notifications for additional information and history.

    - Click Check my progress to verify the objective.

## 2. Access Cloud Shell

In this section, you explore Cloud Shell and some of its features.

- You can use the Cloud Shell to manage projects and resources via command line without having to install the Cloud SDK and other tools on your computer.

- **Cloud shell provides the following:**

    - Temporary Compute Engine VM
    - Command-line access to the instance via a browser
    - 5 GB of persistent disk storage ($HOME dir)
    - Pre-installed Cloud SDK and other tools
    - gcloud: for working with Compute Engine and many Google Cloud services
    - gcloud storage: for working with Cloud Storage
    - kubectl: for working with Google Kubernetes Engine and Kubernetes
    - bq: for working with BigQuery
    - Language support for Java, Go, Python, Node.js, PHP, and Ruby
    - Web preview functionality
    - Built-in authorization for access to resources and instances

> Note: After 1 hour of inactivity, the Cloud Shell instance is recycled. Only the /home directory persists. Any changes made to the system configuration, including environment variables, are lost between sessions.

- Open Cloud Shell and explore features
    - In the Google Cloud menu, click Activate Cloud Shell (Activate Cloud Shell icon). If prompted, click Continue. Cloud Shell opens at the bottom of the Cloud Console window.



## 3. Use Cloud Shell to create a Cloud Storage bucket
Create a second bucket and verify in the Cloud Console
- Open Cloud Shell again.
- Use the gcloud storage command to create another bucket. Replace [BUCKET_NAME] with a globally unique name (you can append a 2 to the globally unique bucket name you used previously):

```gcloud storage buckets create gs://[BUCKET_NAME]```

- If prompted, click Authorize.
- In the Cloud Console, on the Navigation menu (Navigation menu icon), click Cloud Storage > Bucket, or click Refresh if you are already in the Storage browser. The second bucket should be displayed in the Buckets list.

> Note: You have performed equivalent actions using the Cloud Console and Cloud Shell. You created a bucket using the Cloud Console and another bucket using Cloud Shell.

## 4. Explore more Cloud Shell features
**Upload a file**

- Open Cloud Shell.
- Click the More button (More button) in the Cloud Shell toolbar to display further options.
- Click Upload. Upload any file from your local machine to the Cloud Shell VM. This file will be referred to as [MY_FILE].
- In Cloud Shell, type ls to confirm that the file was uploaded.
- Copy the file into one of the buckets you created earlier in the lab. Replace [MY_FILE] with the file you uploaded and [BUCKET_NAME] with one of your bucket names:
```bash
gcloud storage cp [MY_FILE] gs://[BUCKET_NAME]
```

    - If your filename has whitespaces, be sure to place single quotes around the filename. For example, gcloud storage cp ‘my file.txt' gs://[BUCKET_NAME]


## 5. Create a persistent state in Cloud Shell
In this section you will learn a `best practice for using Cloud Shell`. 

- The gcloud command often requires you to specify values such as a Region, Zone, or Project ID. Entering them repeatedly increases the chance of making typing errors. If you use Cloud Shell frequently, you may want to `set common values in environment variables` and use them instead of typing the actual values.

    - Identify available regions : Open Cloud Shell from the Cloud Console. Note that this allocates a new VM for you. To list available regions, execute the following command:

    ```bash
    gcloud compute regions list
    ```

    - Select a region from the list and note the value in any text editor. This region will now be referred to as [YOUR_REGION] in the remainder of the lab.
    - Create an environment variable and replace [YOUR_REGION] with the region you selected in the previous step:
    ```bash
    INFRACLASS_REGION=[YOUR_REGION]
    ```
    - Verify it with echo:
    ```bash
    echo $INFRACLASS_REGION
    ```

    - You can use environment variables like this in gcloud commands to reduce the opportunities for typos and so that you won't have to remember a lot of detailed information.

> Note: Every time you close Cloud Shell and reopen it, a new VM is allocated, and the environment variable you just set disappears. In the next steps,`you create a file to set the value so that you won't have to enter the command each time Cloud Shell is reset`.

- Append the environment variable to a file
- Create a subdirectory for materials used in this lab:
```bash
mkdir infraclass
```

- Create a file called config in the infraclass directory:
```bash
touch infraclass/config
```

- Append the value of your Region environment variable to the config file:
```bash
echo INFRACLASS_REGION=$INFRACLASS_REGION >> ~/infraclass/config
```

- Create a second environment variable for your Project ID, replacing [YOUR_PROJECT_ID] with your Project ID. You can find the project ID on the Cloud Console Home page.

- Use the source command to set the environment variables, and use the echo command to verify that the project variable was set:
```bash
source infraclass/config
echo $INFRACLASS_PROJECT_ID
```


- In the next step, you modify the .profile file so that the source command is issued automatically every time a terminal to Cloud Shell is opened.

- Modify the bash profile and create persistence
```bash
nano .profile
```

- Add the following line to the end of the file:
```bash
source infraclass/config
```

- Close and then re-open Cloud Shell to reset the VM.
    - Use the echo command to verify that the variable is still set:
        ```echo $INFRACLASS_PROJECT_ID```
    - You should now see the expected value that you set in the config file.

> Note: If your Cloud Shell environment is ever corrupted, instructions on resetting it are in the Cloud Shell Documentation article titled Disabling or Resetting Cloud Shell. This will cause everything in your Cloud Shell environment to be set back to its original default state.

