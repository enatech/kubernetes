**CKAD Exam Prep**

To run all yaml files, a minimum kubernetes cluster is requried (one master, or one master and two workers)

# Deployments
### simple nginx with 2 replicas

kubectl apply -f [https://github.com/enatech/kubernetes/blob/master/ckad/nginx-deployment.yaml]nginx-deployment.yaml

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

[https://github.com/enatech/kubernetes/blob/master/ckad/nginx-multicontainer-deploy.yaml]nginx-multicontainer-deploy.yaml

kubectl exec -it <podname> sh -c nginx-multi
  
