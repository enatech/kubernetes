**CKAD Exam Prep**

To run all yaml files, a minimum kubernetes cluster is requried (one master, or one master and two workers)

# Deployments
### simple nginx with 2 replicas

kubectl apply -f [https://github.com/enatech/kubernetes/blob/master/ckad/nginx-deployment.yaml](nginx-deployment.yaml)

**Check the deployment and pod; test the pod via IP -**

kubectl get deploy --show-labels

kubectl get deploy -l app=nginx

kubectl get pods -l app=nginx

kubectl describe pod <podname> | grep IP

curl IP:80

**Now scale the deployment with 5 replicas**

kubectl scale deploy nginx --replicas=5

**Test some rollout and update scenarios; then autoscale**

kubectl set image deploy/nginx nginx=nginx:1.17.4

kubectl rollout history deploy nginx

kubectl rollout undo deploy nginx

kubectl autoscale deploy nginx --min=2 --max=5 --cpu-percent=85

### Multicontainer deployment, add an alpine container to the existing yaml and exec into the pod/container nginx

[https://github.com/enatech/kubernetes/blob/master/ckad/nginx-multicontainer-deploy.yaml](nginx-multicontainer-deploy.yaml)

kubectl exec -it <podname> sh -c nginx-multi
  
# Service

**Create a service for the above nginx simple deployment. Using a service, the application can be accessed via ClusterIP within any node of the cluster; changing the type to NodePort, the app can be accessed on any node on targetPort via outside the cluster also**

kubectl apply -f [https://github.com/enatech/kubernetes/blob/master/ckad/nginx-service.yaml](nginx-service.yaml)

kubectl get svc --all-namespaces

curl <ClusterIp>:8080
  
For NodePort

curl nodeName:nodePort

# Persistent Volumes and PVCs

**Create a PV with 10GB storage and RW access using host's /tmp/data folder to store data

kubectl apply -f [https://github.com/enatech/kubernetes/blob/master/ckad/pv.yaml](pv.yaml)

kubectl apply -f [https://github.com/enatech/kubernetes/blob/master/ckad/pvc.yaml](pvc.yaml)
  
**Create similar PV using NFS

kubectl apply -f [https://github.com/enatech/kubernetes/blob/master/ckad/pv-nfs.yaml](pv-nfs.yaml)

**Use the newly created PVC in a Deployment, then write any file in worker host where the pod is running (not discussing NFS at the moment) on the hostPath and exec inside the pod to see the new file on mountPath

kubectl apply -f [https://github.com/enatech/kubernetes/blob/master/ckad/busybox-deploy-pvc.yaml](busybox-deploy-pvc.yaml)

kubectl exec -it <podname> sh OR kubectl exec -it <podname> -- ls -l /tmp
 
# Secrets and Deploy using secret

**Create a secret for username and password (example) and then create a deploy for busybox that uses the username env variable and loads the value from secret via the key. Secret can also be loaded via envFrom->secretRef in spec.containers.envFrom.secretRef.

kubectl apply -f [https://github.com/enatech/kubernetes/blob/master/ckad/secrets.yaml] (secrets.yaml)

kubectl apply -f [https://github.com/enatech/kubernetes/blob/master/ckad/busybox-load-secret.yaml] busybox.yaml
