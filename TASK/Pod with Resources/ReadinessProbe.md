# Create a Deployment with a ReadinessProbe

Create a Deployment named space-alien-welcome-message-generator of image httpd:alpine with one replica.
It should've a ReadinessProbe which executes the command stat /tmp/ready . This means once the file exists the Pod should be ready.
The initialDelaySeconds should be 10 and periodSeconds should be 5 .
Create the Deployment and observe that the Pod won't get ready.