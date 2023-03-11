# Pod with Resources
1. 
Create a new Namespace limit .
In that Namespace create a Pod named resource-checker of image httpd:alpine .
The container should be named my-container .
It should request 30m CPU and be limited to 300m CPU.
It should request 30Mi memory and be limited to 30Mi memory.

>> k -n limit run resource-checker --image=httpd:alpine -oyaml --dry-run=client > pod.yaml

