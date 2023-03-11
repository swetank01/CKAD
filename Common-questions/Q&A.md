# Common Questions

#### 1. List all namespaces in the cluster and redirect the output to a file

<details><summary>show</summary>
<p>

```bash
k get po -A > list-ns.txt
```
</p>
</details>

#### 2. Create a pod with specified container name, image and labels.

<details><summary>show</summary>
<p>

```bash
k run pod-2 --image=busybox --labels='type=not-common'
```
</p>
</details>


#### 3. Create a secret and mount it as an environment variable into a pod.

<details><summary>show</summary>
<p>

##### Create Secret:
```bash
k create secret generic my-secret \
--from-literal=username=swetank01 \
--from-literal=password=swetank123 
```

##### Create Pod yaml:
```bash
k run secret-pod --image=busybox --dry-run=client -o yaml > secret-pod.yaml
```

##### Edit Yaml:
```bash
vi secret-pod.yaml
```

##### Add Env
```bash
    env:
    - name: USERNAME
      valueFrom:
        secretKeyRef:
          name: my-secret
          key: username
    - name: PASSWORD
      valueFrom:
        secretKeyRef:
          name: my-secret
          key: password
```

##### Validate:
```bash
 k -n common exec secret-pod -- /bin/bash
 echo $USERNAME

 k -n common exec secret-pod -- /bin/echo $USERNAME
 ```

</p>
</details>

#### 4. Create a deployment with X image and Y tag. Change the Y tag to Z and record the changes
- *doc-keyword: 'deployment rollout'*
- nginx:1.14.2-alpine to nginx:1.16.1-alpine 

<details><summary>show</summary>
<p>

##### Create Deployment with Image and Tag:
```bash
k create deploy deploy-1 --image=nginx:1.14.2-alpine
```

##### Check Rollout history:
```bash
k rollout history deployment deploy-1
```

##### Change Tag 1.14.2 to 1.16.1:
```bash
k set image deploy deploy-1 nginx=nginx:1.16.1 --record
```

</p>
</details>



#### 5. Set memory request for a Pod's container to xMi and limit to half of maximum allowed for pods of that namespaces
- *doc-keyword: 'namespace memory / Assign Memory Resources'*

<details><summary>show</summary>
<p>

##### Create Namespace:
```bash
k create namespace quota-mem-cpu
```

##### Create quota into that Namespace: 
```bash
k create quota rq-for-ns-qmc --hard=cpu=1,memory=1G -n quota-mem
```

##### generate pod yaml and edit it with resource limit : 
```bash
k run pod-mem --image=nginx:1.14.2-alpine -n quota-mem --dry-run=client -oyaml > pod-mem.yaml
```

##### Create quota into that Namespace: 
```bash
k create quota rq-for-ns-qmc --hard=cpu=1,memory=1G -n quota-mem
```

</p>
</details>


#### 6.RBAC: ClusterRole, ClusterRoleBindings, Role, RoleBinding, Service Accounts ** NOT COMPLETED
- *doc-keyword: 'namespace memory / Assign Memory Resources'*

<details><summary>show</summary>
<p>

##### Heading:
```bash
k run pod-2 --image=busybox --labels='type=not-common'
```
</p>
</details>


#### 7.Add a sidecar container that prints the logs of the main container. You need to create emptyDir and mount to both the containers. Command to print logs Will be given.
- *doc-keyword: 'sidecar'*

<details><summary>show</summary>
<p>

##### create multipod:
```bash
k run multipod --image=nginx:alpine --dry-run=client -oyaml > multipod.yaml
```

##### create sidecar:logger pod:
```bash
k run logger --image=busybox:alpine --command sleep 4200 --dry-run=client -oyaml >> multipod.yaml
```

##### perform cleanup
```bash
k run logger --image=busybox:alpine --command sleep 4200 --dry-run=client -oyaml >> multipod.yaml
```
</p>
</details>

#### 8.Create a pod with 2 containers. Image names and other info will be provided.
- *doc-keyword: 'namespace memory / Assign Memory Resources'*

<details><summary>show</summary>
<p>

##### Heading:
```bash
k run pod-2 --image=busybox --labels='type=not-common'
```
</p>
</details>

#### 9. Create a network policy that allows all pods with label “key: value” to allow traffic from only Y & Z pods in the same namespace. Allow Egress traffic on Port 53 also.

- *doc-keyword: 'namespace memory / Assign Memory Resources'*

<details><summary>show</summary>
<p>

##### Heading:
```bash
k run pod-2 --image=busybox --labels='type=not-common'
```
</p>
</details>

#### 10. Setting CPU & Mem limits to containers of a Pod
- *doc-keyword: 'namespace memory / Assign Memory Resources'*

<details><summary>show</summary>
<p>

##### Create sample pod :
```bash
k run pod-limit --image=nginx:1.14.2-alpine --dry-run=client -oyaml > pod-with-limit.yaml
```

#### Add the following into resources:
```bash
      requests:
        memory: "64Mi"
        cpu: "250m"
      limits:
        memory: "128Mi"
        cpu: "500m"
```
</p>
</details>
