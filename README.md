<!-- <style>
.hover_img a span { position: absolute; display: none; z-index: 99; }
.hover_img a:hover span { display: block; left: 25%; }

.hover_gif a span { position: absolute; display: none; z-index: 99; }
.hover_gif a:hover span { display: block; left: 5%; }
</style> -->

<p>
  <img src="img/kuber-black.png#gh-dark-mode-only" alt="image" height="100" style="margin-bottom: 15px"/>
  <img src="img/kuber-white.png#gh-light-mode-only" alt="image" height="100" style="margin-bottom: 15px"/>
</p>


# Annotation <!-- omit in toc -->
Let me be honest from the start, this repo is a collection of Kubernetes recipes and quick solutions to issues which I face daily in my job. 
You don't find here any explanations how things work under the hood. If you need one of those better read some book, watch the video
or refer to the official documentation. Fortunately, nowdays we have a real lot info about Kuber so whenever you want to
you always have an opportunity to go [deeper](./img/mike.png).
<!-- <span class="hover_img">
  <a href="#">
    deeper.
    <span>
      <img src="img/mike.png" alt="mike" height="100"/>
    </span>
  </a>
</span> -->


But if you are trying to figure out how to do something in no time or just decide to get your hands dirty, you are welcome. Hope, 
you will find what you seek in here. From my side, I commit to update this repo with new info and new recipes during my career. 


[Have fun!](./img/party.gif)
<!-- <span class="hover_gif">
  <a href="#">
    Have fun!
    <span>
      <img src="img/party.gif" alt="party" height="100"/>
    </span>
  </a>
</span> -->



## Table of Contents <!-- omit in toc -->
- [Notes](#notes)
- [Basic Commands](#basic-commands)
  - [Switch to another access context](#switch-to-another-access-context)
  - [List available pods](#list-available-pods)
  - [Get pod logs](#get-pod-logs)
  - [Delete pod](#delete-pod)
  - [Map localhost port to pod port](#map-localhost-port-to-pod-port)
  - [Copy data between pod and localhost](#copy-data-between-pod-and-localhost)
  - [Execute shell command in the pod container](#execute-shell-command-in-the-pod-container)
  - [List all available type of Kubernetes resources](#list-all-available-type-of-kubernetes-resources)
  - [Get documentation for resource](#get-documentation-for-resource)
  - [List all resources of specific type that exist in a cluster](#list-all-resources-of-specific-type-that-exist-in-a-cluster)
  - [Describe Kubernetes resource](#describe-kubernetes-resource)
  - [Get manifest for Kubernetes resource](#get-manifest-for-kubernetes-resource)
  - [Change resource definition](#change-resource-definition)
  - [Scale Deployment/StatefulSet](#scale-deploymentstatefulset)
  - [Get all available endpoints](#get-all-available-endpoints)
- [Nodes](#nodes)
  - [Get node IP address](#get-node-ip-address)
  - [Add label to node](#add-label-to-node)
  - [Remove label from node](#remove-label-from-node)
  - [Add taints to node](#add-taints-to-node)
  - [Remove taints from node](#remove-taints-from-node)
  - [Get node's available resources](#get-nodes-available-resources)
  - [Get node's conditions](#get-nodes-conditions)
  - [Get node's system info](#get-nodes-system-info)
- [Pods](#pods)
  - [Create pod](#create-pod)
  - [Get pod IP address:](#get-pod-ip-address)
  - [Delete all pods with specific status:](#delete-all-pods-with-specific-status)
  - [Count all pods in the cluster](#count-all-pods-in-the-cluster)
  - [Schedule pod on specific node:](#schedule-pod-on-specific-node)
  - [Run pod on the same node as another pod:](#run-pod-on-the-same-node-as-another-pod)
  - [Force pod to ignore node taints:](#force-pod-to-ignore-node-taints)
  - [Pass pod metadata to container as environment variables](#pass-pod-metadata-to-container-as-environment-variables)
  - [Pas container resource info to container as environment variables](#pas-container-resource-info-to-container-as-environment-variables)
- [Volumes](#volumes)
  - [Use ephemeral volume](#use-ephemeral-volume)
  - [Mount pod metadata as volume](#mount-pod-metadata-as-volume)
  - [Mount container resource info as volume](#mount-container-resource-info-as-volume)
  - [Attach persistent volume to pod](#attach-persistent-volume-to-pod)
- [ConfigMaps \& Secrets](#configmaps--secrets)
  - [Create ConfigMap](#create-configmap)
  - [Mount ConfigMap as volume](#mount-configmap-as-volume)
  - [Pass data from ConfigMap as environment](#pass-data-from-configmap-as-environment)
  - [Make ConfigMap immutable](#make-configmap-immutable)
- [Expose application to network traffic](#expose-application-to-network-traffic)
  - [Create ClusterIP service](#create-clusterip-service)
  - [Create NodePort service](#create-nodeport-service)
  - [Create headless service](#create-headless-service)
- [Jobs](#jobs)
  - [Run some job once](#run-some-job-once)
  - [Get logs of a job](#get-logs-of-a-job)
  - [Run job regularly](#run-job-regularly)
- [RBAC](#rbac)
  - [Create Role](#create-role)
  - [Get existing ServiceAccounts](#get-existing-serviceaccounts)
  - [Create ServiceAccount](#create-serviceaccount)
  - [Bind ServiceAccount to Role](#bind-serviceaccount-to-role)
  - [Combine few ClusterRoles in one](#combine-few-clusterroles-in-one)
  - [Check if service acc has permission to do some action](#check-if-service-acc-has-permission-to-do-some-action)
- [Security](#security)
  - [Prevent container to run with root user](#prevent-container-to-run-with-root-user)
  - [Reduce container capabilities](#reduce-container-capabilities)
  - [Make container root filesystem immutable](#make-container-root-filesystem-immutable)
- [Network Traffic Rules](#network-traffic-rules)
  - [Forbid all ingress traffic to an app](#forbid-all-ingress-traffic-to-an-app)
  - [Restrict ingress traffic to the app](#restrict-ingress-traffic-to-the-app)
  - [Deny all egress traffic from the app (except to kube-system for dns resolution)](#deny-all-egress-traffic-from-the-app-except-to-kube-system-for-dns-resolution)
  - [Allow egress traffic only inside a cluster](#allow-egress-traffic-only-inside-a-cluster)
  - [Forbid egress traffic to specific IP's](#forbid-egress-traffic-to-specific-ips)
- [Resources \& Quotas](#resources--quotas)
  - [Configure default memory usage per container in the namespace](#configure-default-memory-usage-per-container-in-the-namespace)
  - [Configure limit for the requested storage](#configure-limit-for-the-requested-storage)
  - [Configure resource limits for whole namespace](#configure-resource-limits-for-whole-namespace)
  - [Configure how many objects of certains type can be created](#configure-how-many-objects-of-certains-type-can-be-created)
- [Workflows](#workflows)
- [Helm](#helm)
- [Learning Resources](#learning-resources)
  - [Books](#books)
  - [Articles](#articles)
    - [Resource Usage](#resource-usage)
    - [Scheduling](#scheduling)
    - [App expose](#app-expose)
    - [Aviability](#aviability)
    - [Pods](#pods-1)
    - [Containers](#containers)
    - [Security](#security-1)
  - [Videos](#videos)
  - [Repos](#repos)

## Notes
- Almost all ```kubectl``` commands listed below can be used without namespace flag ```-n```. In this case they will be executed in the default namespace.
- To deploy resource from YAML manifest use ```kubectl apply -f path/to/manifest``` command.
- Obviously, this repo can't cover everything but as I said I'll try to keep it up to life. So more materials will be added in the future.
- Feel free to write me if you face some issues with examples or if you just disagree about something.


## Basic Commands
### Switch to another access context
Get available access contexts:
```sh
kubectl config get-contexts
```

Switch to another context:
```sh
kubectl config use-context <context-name>

# example
kubectl config use-context docker-desktop
```

### List available pods
All pods:
```sh
kubectl get pods -A
```

Pods in specific namespace:
```sh
kubectl get pods 
kubectl get pods -n <namespace>

# example
kubectl get pods -n events
```

Pods matching a selector:
```sh
kubectl get pods -l <key>=<value> 

# example
kubectl get pods -l app=rabbitmq
```

Pods with additional info:
```sh
kubectl get pods -o wide
```

### Get pod logs
By pods name:
```sh
kubectl logs <pod-name>

# example
kubectl logs rabbitmq-0
```

Using selector:
```sh
kubectl logs -l <key>=<value>

# example
kubectl logs -l app=rabbitmq
```

### Delete pod 
Delete gently by name:
```sh
kubectl delete pod <pod-name>

# example
kubectl delete pod event-collector-b7bc87c75-sw2gk
```

Delete gently by selector (all pods matching selector will be deleted): 
```sh
kubectl delete pod -l <key>=<value>

# example
kubectl delete pod -l app=event-collector
```

Delete immediatly:
```sh
kubectl delete pod <pod-name> --grace-period=0 --force

# example
kubectl delete pod event-collector-b7bc87c75-sw2gk --grace-period=0 --force
```

### Map localhost port to pod port
Connect directcly to pod's port:
```sh
kubectl port-forward <pod-name> <localhost-port>:<remote-port>

# example
kubectl port-forward event-collector-b7bc87c75-sw2gk 8000:5672
```

Connect via Service:
```sh
kubectl port-forward service/<service-name> <localhost-port>:<service-port>

# example
kubectl port-forward service/event-collector 8000:5672
kubectl port-forward service/event-collector 8000:metrics
```

Connectt via Deployment:
```sh
kubectl port-forward deployment/<deployment-name> <localhost-port>:<remote-port>

# example
kubectl port-forward deployment/event-collector 8000:5672
```

### Copy data between pod and localhost 
Copy from localhost to pod:
```sh
kubectl cp /local/path <namespace>/<pod>:/remote/path  
kubectl cp /local/path <namespace>/<pod>:/remote/path  -c <container-name>

# example
```

Copy from pod to localhost:
```sh
kubectl cp <namespace>/<pod>:/remote/path /local/path

# example
```

### Execute shell command in the pod container
Single command:
```sh
kubectl exec <pod>  -- <command> 
```

Get into container's shell:
```sh
kubectl exec -it <pod> -- sh
kubectl exec -it <pod> -c <container> -- sh
```

### List all available type of Kubernetes resources
```sh
kubectl api-resources
```

### Get documentation for resource 
For resource in common:
```sh
kubectl explain <resource>

# example
kubectl explain service
```

Explain specific field in resource definition:
```sh
kubectl explain <resource>.<field>.<nested-field>

# example
kubectl explain service.spec.ports
```

### List all resources of specific type that exist in a cluster
```sh
kubect get <resource-type> -n <namespace>

# example
kubectl get services 
kubectl get services -n eventes
```

### Describe Kubernetes resource
```sh
kubect decribe <resource-type> <resource-name> -n <namespace>

# example
kubectl describe service kube-dns -n kube-system
```

### Get manifest for Kubernetes resource
In YAML:
```sh
kubectl get <resource-type> <resource-name> -n <namespace> -o yaml

# example
kubectl get service kube-dns -n kube-system -o yaml
```

In JSON:
```sh
kubectl get <resource-type> <resource-name> -n <namespace> -o json

# example
kubectl get service kube-dns -n kube-system -o json
```

### Change resource definition 
```sh
kubectl patch <resource-type> <resource-name> -p <new-data>'{"spec":{"containers":[{"name":"kubernetes-serve-hostname","image":"new image"}]}}'

# example 
kubectl patch pod api-proxy -p '{"spec":{"containers":[{"name":"nginx","image":"nginx:stable-alpine"}]}}'
```

### Scale Deployment/StatefulSet 
```sh
kubectl scale <deploy/sts>/<resource-name> --replicas=<number>

# example
kubectl scale deploy/event-service --replicas=0
kubectl scale sts/datanode --replicas=4
```


### Get all available endpoints
```sh
kubectl get endpoints -A
```


## Nodes
### Get node IP address
```sh
kubectl get node <node-name> -o jsonpath="{.status.addresses[?(@.type == 'ExternalIP')].address}"
kubectl get node <node-name> -o jsonpath="{.status.addresses[?(@.type == 'InternalIP')].address}"
```

### Add label to node
```sh
kubectl label nodes <node-name> <label>=<value>
```

### Remove label from node
From single node:
```sh
kubectl label nodes <node-name> <label>- 
```

From all nodes:
```sh
kubectl label nodes --all <label>-
```

### Add taints to node
```sh
kubectl taint nodes <node-name> key=value:NoSchedule
```

### Remove taints from node
```sh
kubectl taint nodes <node-name> key=value:NoSchedule-
```

### Get node's available resources
```sh
kubectl describe nodes <node-name> | grep -i "Capacity:\|Allocatable:" -A 6

# example
kubectl describe nodes gke-staging-de795cfc-mtfr | grep -i "Capacity:\|Allocatable:" -A 6
```

### Get node's conditions
```sh
kubectl describe nodes <node-name> | grep -i "Conditions:" -A 15

# example
kubectl describe nodes gke-staging-reports-de795cfc-mtfr | grep -i "Conditions:" -A 15
```

### Get node's system info
```sh
kubectl describe nodes <node-name> | grep -i "System Info:" -A 10

# example
kubectl describe nodes gke-staging-reports-de795cfc-mtfr | grep -i "System Info:" -A 10
```

## Pods
### Create pod 
Using CLI:
```sh
kubectl run --image=<image> <pod-name> --labels="key1=value1,key2=value2" -- <command-to-execute>

# example
kubectl run --image=busybox:latest busybox --labels="env=prod,app=busy" -- sleep 3600
```

From YAML:
```yaml
apiVersion: v1 
kind: Pod 
metadata:
  name: busybox
  labels:
    env: prod
    app: busy
spec:
  containers:
  - name: busybox
    image: busybox:latest
    args:
    - /bin/sh
    - -c
    - sleep 3600
  restartPolicy: Never
``` 

### Get pod IP address:
```sh
kubectl get pod <pod-name> -o jsonpath="{.status.podIP}"

# example
kubectl get pods busybox -o jsonpath="{.status.podIP}"
```

### Delete all pods with specific status:
```sh
kubectl delete pods --field-selector status.phase=<status:Pending,Failed,Unknown,Running,Succeeded>

# exmaple
kubectl delete pods --field-selector status.phase=Failed
```

### Count all pods in the cluster
```sh
kubectl get pods --field-selector=status.phase!=Succeeded,status.phase!=Failed --output json | jq -j '.items | length'
```

### Schedule pod on specific node: 
Via nodeSelector:
```yaml
spec:
  nodeSelector:
    nodeLabel: value
```

Via nodeAffinity:
```yaml
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution: #hard requirement
        nodeSelectorTerms: 
        - matchExpressions: 
          - key: NumberOfCores
            operator: Gt
            values: [ "3" ]
      preferredDuringSchedulingIgnoredDuringExecution: #soft requirement 
      - weight: 1
        preference:
          matchField:
          - key: metadata.name
            operator: In
            values: [ "temporary-node" ]
```

### Run pod on the same node as another pod:
```yaml
spec:
  affinity:
    podeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        labelSelector:
        - matchExpression:
          - key: destination
            operator: In
            values: [ "data", "ml" ]
```

### Force pod to ignore node taints:
```yaml
spec:
  tolerations:
  - key: "key"
    operator: "Exists"
    effect: "NoSchedule"
---
spec:
  tolerations:
  - key: "key"
    operator: "Equal"
    value: "value"
    effect: "NoSchedule"
```

### Pass pod metadata to container as environment variables
```yaml
spec:
  containers:
  - name: busybox
    image: busybox:latest
    env:
    - name: NODE_NAME
      valueFrom:
        fieldRef:
          fieldPath: spec.nodeName
    - name: NAMESPACE
      valueFrom:
        fieldRef:
          fieldPath: metadata.namespace
    - name: IP
      valueFrom:
        fieldRef: 
          fieldpath: status.podIP     
```

### Pas container resource info to container as environment variables
```yaml
spec:
  containers:
  - name: busybox
    image: busybox:latest
    env:
    - name: MEMORY_LIMIT
      valueFrom:
        resourceFieldRef:
          containerName: busybox
          resource: limits.memory  
    - name: CPU_REQUEST
      valueFrom:
        resourceFieldRef:
          containerName: busybox
          resource: requests.cpu    
```


## Volumes
### Use ephemeral volume
```yaml
spec:
  containers:
  - name: busybox
    image: busybox:latest
    volumeMounts:
    - mountPath: /app/cache
      name: local
  volumes:
  - name: local
    emptyDir:
      sizeLimit: 1Gi
```

### Mount pod metadata as volume
```yaml
spec:
  containers:
  - name: busybox
    image: busybox:latest
    args: |
      cat labels
      cat annotations
    volumeMounts:
    - name: pod-meta
  volumes:
  - name: pod-meta
    downardAPI:
      items:
      - path: labels
        fieldRef:
          fieldPath: metadata.labels
      - path: annotations
        fieldRef:
          fieldPath: metadata.annotations
```

### Mount container resource info as volume
```yaml
spec:
  containers:
  - name: busybox
    image: busybox:latest
    args: |
      cat limits
      cat requests
    volumeMounts: container-info
  volumes:
  - name: container-info:
    downardAPI:
      items:
        - path: limits
          resourceFieldRef: 
            containerName: busybos
            resource: limits
        - path: requests
          resourceFieldRef: 
            containerName: busybos
            resource: requests
```

### Attach persistent volume to pod
Get available storage classes:
```sh
kubectl get storageclass
```

Create Persisten Volume Claim:
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: random-log
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: standard
  resources:
    requests:
      storage: 50Gi
```

Attach Persisten Volume Claim as a volume:
```yaml
apiVersion: v1 
kind: Pod 
metadata:
  name: busybox
  labels:
    env: prod
    app: busy
spec:
  containers:
  - name: busybox
    image: busybox:latest
    args:
    - /bin/sh
    - -c
    - sleep 3600
    volumeMounts:
    - name: log-volume
      mountPath: "/logs"
  restartPolicy: Never
  volumes:
  - name: log-volume 
    persistentVolumeClaim:
      claimName: random-log
```

## ConfigMaps & Secrets

### Create ConfigMap 
Using CLI and manual entered data:
```sh
kubectl create configmap <configmap-name> --from-literal=key1=value1 --from-literal=key2=value2

# example
kubectl create configmap db-config --from-literal=service=postgres --from-literal=port=5432
```

Using CLI and the whole content of a file as a value for a key:
```sh
kubectl create configmap <configmap-name> --from-file=key1=/path/to/some --from-file=key2=/path/to/another

# example
kubectl create configmap monitoring-config --from-file=metrics=/user/config.xml 
```

Using ClI and key=value pairs in file as a source data:
```sh
kubectl create configmap <configmap-name> --from-file=path/to/some

# exmaple
kubectl create configmap db-config --from-file=db/props
```

From YAML:
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: db-config
data:
  service: "postgres"
  port: "5432"
  migration.properties: |
    user=mike
    source.env=dev
    target.env=staging
```

### Mount ConfigMap as volume
Add all the data from a ConfigMap to a volume:
```yaml
spec:
  containers:
    - name: busybox
      image: busybox:latest
      command: [ "/bin/sh", "-c", "ls /etc/config/" ]
      volumeMounts:
      - name: config
        mountPath: /etc/config
  volumes:
    - name: config
      configMap:
        name: config-map-name
```

Add data by key and make it available on specific path:
```yaml
spec:
  containers:
    - name: busybox
      image: busybox:latest
      command: [ "/bin/sh","-c","cat /etc/config/keys" ]
      volumeMounts:
      - name: config
        mountPath: /etc/config
  volumes:
    - name: config
      configMap:
        name: config-map-name
        items:
        - key: key
          path: keys
```

### Pass data from ConfigMap as environment
Specify a key from ConfigMap which value will be used as env variable:
```yaml
spec:
  containers:
    - name: busybox
      image: busybox:latest
      command: [ "/bin/sh", "-c", "env" ]
      env:
        - name: ENV_FROM_CONFIGMAP
          valueFrom:
            configMapKeyRef:
              name: config-map-name
              key: some-key
```

Read all ConfigMap's key-value pairs as env variables:
```yaml
spec:
  containers:
    - name: busybox
      image: busybox:latest
      command: [ "/bin/sh", "-c", "env" ]
      envFrom:
      - configMapRef:
          name: config-map-name
```

### Make ConfigMap immutable
Obviously you can't change configmap after creation:
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: hero-config
data:
  user: Invincible
  strength: 500
immutable: true
```

## Expose application to network traffic 

### Create ClusterIP service
Using CLI
```sh
kubectl expose pod <pod-name> --port=<svc-port-number> --taget-port=<target-port-number> --name=<svc-name>
kubectl expose deployment <deploy-name> --port=<svc-port-number> --taget-port=<target-port-number> --name=<svc-name>

# example
kubectl expose pod nginx --port=80 --taget-port=80 --name=api-proxy
kubectl expose deployment api-proxy --port=80 --taget-port=80 --name=api-proxy
```

From YAML:
```yaml
apiVersion: v1
kind: Service
metadata:  
  name: api-proxy
spec:
  selector:    
    app: nginx
  type: ClusterIP
  ports:  
  - name: http
    port: 80
    targetPort: 80
    protocol: TCP
```

### Create NodePort service 
```yaml
apiVersion: v1
kind: Service
metadata:  
  name: api-proxy
spec:
  selector:    
    app: nginx
  type: NodePort
  ports:  
  - name: http
    port: 80
    targetPort: 80
    nodePort: 30036
    protocol: TCP
```

### Create headless service 
```yaml
apiVersion: v1
kind: Service
metadata:  
  name: kafka
spec:
  selector:    
    app: kafka
  type: ClusterIP
  clusterIP: None
  ports:  
  - name: http
    port: 9092
    targetPort: 9092
    protocol: TCP
```

## Jobs
### Run some job once
```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: migrate-job
spec:
  template:
    spec:
      containers:
      - name: migration
        image: eu.gcr.io/org/backend:stable
        command: ["bash", "-c", "python manage.py migrate --fake-initial"]
        env:
          - name: DATABASE_URL
            valueFrom:
              secretKeyRef:
                key: DATABASE_URL
                name: backend-env
      restartPolicy: Never
  backoffLimit: 2
```

### Get logs of a job
```sh
kubectl logs <job-pod-name>
kubectl logs jobs/<job-name>

# example
kubectl logs migrate-job-7f6cc7cdc8-rqldg
kubectl logs jobs/migrate-job
```

### Run job regularly
```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: duck
spec:
  schedule: "*/30 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: duck-says
            image: busybox:stable
            imagePullPolicy: IfNotPresent
            command:
            - /bin/sh
            - -c
            - echo "Kuber quack-quack-quack"
          restartPolicy: OnFailure
```

## RBAC

### Create Role 
Create role which control resource access within one namespace:
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: spy
  namespace: default
rules:
- apiGroups: [""]
  resources: ["secrets"]
  verbs: ["get", "watch", "list"]
```

Create role which control resource access within whole cluster:
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: spy
rules:
- apiGroups: [""]
  resources: ["secrets"]
  verbs: ["get", "watch", "list"]
```

### Get existing ServiceAccounts
```sh
kubectl get serviceaccounts -n <namespace>

# example
kubectl get serviceaccounts -n events
```

### Create ServiceAccount 
Using CLI:
```sh
kubectl create serviceaccount <service_acc_name> -n <namespace>

# example 
kubectl create serviceaccount spy
kubectl create serviceaccount spy -n events 
```

From YAML:
```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: spy
  namespace: default
```

### Bind ServiceAccount to Role 
Create binding for the role in specific namespace:
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: secret-reader
  namespace: default
subjects:
- kind: ServiceAccount
  name: spy
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: spy
  apiGroup: rbac.authorization.k8s.io
```

Create binding for the cluster-wide role:
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: secret-reader
subjects:
- kind: ServiceAccount
  name: spy
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: spy
  apiGroup: rbac.authorization.k8s.io
```

**Notes**: Role Binding can reference a Cluster Role as well. If it so all permissions from Cluster Role work only for resources in namespace of Role Binding

### Combine few ClusterRoles in one
You can combine few Cluster Roles into the one. To do this add a labels for Cluster Roles which permissions you want to aggregate and then create new role with aggreagtionRule option. Just likes this:
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: admin
aggregationRule:
  clusterRoleSelectors:
  - matchLabels:
      aggregate-to-admin: "true"
rules: [] # rules list must be empty. It will be filled from Cluster Roles that match the label
```

### Check if service acc has permission to do some action
```sh
kubectl auth can-i <verb> <resource> --as=system:serviceaccount:<namespace>:<service_acc_name>

# example
kubectl auth can-i create pod --as=system:serviceaccount:default:watchdog
```

## Security
### Prevent container to run with root user
Ensure that container doesn't start up with root user in charge:
```yaml
kind: Pod
metadata:
  name: web 
spec:
  securityContext: 
    runAsNonRoot: true 
  containers: 
  - name: web
    image: nginx:stable-alpine
```

Explicitly define which user and group to use in container:
```yaml
kind: Pod
metadata:
  name: web 
spec:
  securityContext: 
    runAsUser: 1000 
    runAsGroup: 2000
  containers: 
  - name: web
    image: nginx:stable-alpine
```

**Note**: you can define ```securityContext``` both at the pod level and at the container level. In first case it will be applied
to all containers in the pod if they don't have their own ```securityContext```.

### Reduce container capabilities 
```yaml
kind: Pod
metadata:
  name: web 
spec:
  containers: 
  - name: web
    image: nginx:stable-alpine
    securityContext:
      capabilities:
        drop: [ 'ALL' ]
        add: ['NET_BIND_SERVICE']
```

### Make container root filesystem immutable 
```yaml
kind: Pod
metadata:
  name: backend 
spec:
  containers: 
  - name: web
    image: eu.gcr.io/org/backend:stable
    securityContext:
      readOnlyRootFilesystem: true
```

## Network Traffic Rules 
### Forbid all ingress traffic to an app
```yaml
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
  name: web-deny-all
spec:
  podSelector:
    matchLabels:
      app: web
  ingress: []
```

### Restrict ingress traffic to the app
```yaml
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
  name: db-allow
spec:
  podSelector:
    matchLabels: # to pods
      app: gameshop 
      id: db
  ingress:
  - from:
      - podSelector:
          matchLabels: # from pods
            app: gameshop
            id: backend

```


### Deny all egress traffic from the app (except to kube-system for dns resolution)
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-egress
spec:
  podSelector:
    matchLabels:
      app: db
  policyTypes:
  - Egress
  egress:
  - to:
    - namespaceSelector:
        matchLabels:
          kubernetes.io/metadata.name: kube-system
      podSelector:
        matchLabels:
          k8s-app: kube-dns
    ports:
      - port: 53
        protocol: UDP
      - port: 53
        protocol: TCP
```

### Allow egress traffic only inside a cluster
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: egress-within-cluster
spec:
  policyTypes:
  - Egress
  podSelector:
    matchLabels:
      app: events
  egress: []
```

### Forbid egress traffic to specific IP's
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: test-network-policy
  namespace: default
spec:
  podSelector:
    matchLabels:
      role: db
  policyTypes:
  - Egress
  egress:
  - to:
    - ipBlock:
        cidr: 0.0.0.0/0
        except:
          - 172.17.0.0/16
          - 172.23.42.0/24

```

## Resources & Quotas

### Configure default memory usage per container in the namespace
Define just default values:
```yaml
apiVersion: v1
kind: LimitRange
metadata:
  name: memory-limit
  namespace: namespace
spec:
  limits:
  - type: Container
    default:
      memory: 512Mi
    defaultRequest:
      memory: 256Mi 
```

Define default, min and max values:
```yaml
apiVersion: v1
kind: LimitRange
metadata:
  name: memory-limit
  namespace: namespace
spec:
  limits:
  - type: Container
    default:
      memory: 512Mi
    defaultRequest:
      memory: 256Mi
    min:
      memory: 100Mi
    max:
      memory: 1028Mi
```

### Configure limit for the requested storage
```yaml
apiVersion: v1
kind: LimitRange
metadata:
  name: storage-limit
  namespace: namespace
spec:
  limits:
  - type: PersistentVolumeClaim
    max:
      storage: 20Gi
    min:
      storage: 10Gi
```

### Configure resource limits for whole namespace
```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: namespace-resource-limit
  namespace: namespace
spec:
  hard:
    requests.cpu: "10"
    requests.memory: 10Gi
    limits.cpu: "20"
    limits.memory: 20Gi
```

### Configure how many objects of certains type can be created
Via CLI:
```sh
kubectl create quota <quota-name> --hard=pods=300,limits.memory=300Gi --namespace=<namespace>
```

In YAML:
```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: namespace-objects-quota
  namespace: namespace
spec:
  hard:
    pods: 100
    services: 10
    secrets: 10
    configmaps: 10
    persistentvolumeclaims: 20
    services.nodeports: 0
    services.loadbalancers: 0
    count/roles.rbac.authorization.k8s.io: 10
```

## Workflows
In progress...

## Helm 
In progress...
<!-- ### Install Helm Chart to Cluster 
From repo:
```sh
```

From local machine:
```sh
```

### Upgrade existing Helm Chart 
### Validate Chart  

### Reusable templates  -->

## Learning Resources 

### Books
1. [Kubernetes Patterns by Bilgin Ibryam and Roland Huss](https://amzn.eu/d/0dqK7xD)
2. [Kubernetes Operators by Jason Dobies and Joshua Wood](https://amzn.eu/d/4JkmoeT)

### Articles
#### Resource Usage
1. [What Everyone Should Know About Kubernetes Memory Limits](https://home.robusta.dev/blog/kubernetes-memory-limit) 
2. [For the Love of God, Stop Using CPU Limits on Kubernetes](https://home.robusta.dev/blog/stop-using-cpu-limits) 
   
#### Scheduling
1. [Advanced Kubernetes pod to node scheduling](https://www.cncf.io/blog/2021/07/27/advanced-kubernetes-pod-to-node-scheduling/)
   
#### App expose
1. [Kubernetes NodePort vs LoadBalancer vs Ingress](https://medium.com/google-cloud/kubernetes-nodeport-vs-loadbalancer-vs-ingress-when-should-i-use-what-922f010849e0)

#### Aviability
1. [Keep your Kubernetes cluster balanced](https://itnext.io/keep-you-kubernetes-cluster-balanced-the-secret-to-high-availability-17edf60d9cb7)

#### Pods
1. [What are Kubernetes Pods Anyway?](https://www.ianlewis.org/en/what-are-kubernetes-pods-anyway)

#### Containers
1. [The Almighty Pause Container](https://www.ianlewis.org/en/almighty-pause-container)


#### Security
1. [10 Kubernetes Security Context settings you should understand](https://snyk.io/blog/10-kubernetes-security-context-settings-you-should-understand)

### Videos
1. [Building a Container from sratch in Go](https://youtu.be/Utf-A4rODH8?si=6jIt3xnWNlu7c7XN)
2. [Role Based Access Control in Kubernetes](https://youtu.be/CnHTCTP8d48?si=8h68TXDmKT0ykWhd)
3. [Init Container Examples: Learn Kubernetes Pod Spec Features](https://youtu.be/Ezz03l2JDmE?si=ZfdkameL_qhranwf)
4. [10 Ways to Shoot Yourself in the Foot with Kubernetes](https://youtu.be/QKI-JRs2RIE?si=p0yDqPHz_Lgs4uPb)

### Repos
1. [Kubernetes Network Policy Recipes](https://github.com/ahmetb/kubernetes-network-policy-recipes)
  







