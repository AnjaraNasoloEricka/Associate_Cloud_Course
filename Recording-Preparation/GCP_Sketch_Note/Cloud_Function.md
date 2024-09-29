# Cloud Function

## What is Cloud Function ?
- It is a small piece of code that runs `in response to an event`. Because it is fully managed, developers can just write the code and deploy it without worrying about managing the servers or scaling up/down with traffic spikes.

## Use cases 
- Integration with third-party services and APIs
- Asynchronous workloads like lightweight ETL
- Lightweight APIs and webhooks
- IoT processing and update of the sensors/devices in the field
- Real-time file processing for use cases such as media transcoding or resizing as soon as the file is uploaded in Google Cloud Storage.
- Real-time ML solutions for use cases such as media translation or image recognition for files uploaded in GCS.
- Backend for chat applications and mobile apps.


## Difference between Firebase Function and Cloud Function 
- Both Cloud Functions and Firebase Functions can do the same things, they just have slightly different signatures and slightly different ways of deploying. 

- Firebase Functions have a local emulator, which Cloud Functions uses the Functions Framework