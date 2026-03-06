# Node Backup/Restore

{% stepper %}
{% step %}
### Access Backup Functionality

Users can manage backups for their nodes by navigating to the specific node’s backup page at `nodes/{nodeId}/backup`.
{% endstep %}

{% step %}
### Create a Backup

* If no backup has been previously created, the page will display a "Create Backup" button in the "Backup Node" section.
* To initiate the backup process, the user clicks the "Create Backup" button.
* Clicking the button triggers an AWS Lambda function that communicates with the RGB node's `/backup` API endpoint to start the backup process on the node.
* Once the backup is successfully created, it is automatically uploaded to an Amazon S3 bucket. The bucket is structured to organize backups based on `userId` and `nodeId`, ensuring backups are easy to manage and retrieve.
{% endstep %}

{% step %}
### Download

A pre-signed URL is generated and provided to the user. This URL allows the user to download the backup directly from the S3 bucket. For security purposes, the URL is time-limited and expires 30 minutes after being issued.
{% endstep %}
{% endstepper %}

***

#### Node Restore

{% stepper %}
{% step %}
### Access Restore Functionality

Users can manage backups for their nodes by navigating to the specific node’s backup page and find the "Restore node" section at `nodes/{nodeId}/backup`.
{% endstep %}

{% step %}
### Uploading the Backup File

* Click "Upload" — this button will generate an S3 upload URL.
* Once the S3 upload URL is generated, users are prompted to select the backup file from their local device.
* After selecting the file, the upload begins automatically, securely transferring the backup file to the designated S3 bucket.
{% endstep %}

{% step %}
### Restoring Node

* After the upload is successfully completed, a "Restore" button becomes active on the interface.
* Users click the "Restore" button to start the restoration process. It triggers the node’s `/restore` API.
* The `/restore` API facilitates the restoration by taking the backup data from S3 and applying it to the node.
{% endstep %}
{% endstepper %}
