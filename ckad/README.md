CKAD Exam Prep

To run all yaml files, a minimum kubernetes cluster is requried (one master, or one master and two workers)

- Deployment - simple nginx with 2 replicas

kubectl apply -f <deploment.yaml>

Check the deployment -

kubectl get deploy --show-labels

Now scale the deployment with 5 replicas

kubectl scale deploy <deployment> --replicas=5
