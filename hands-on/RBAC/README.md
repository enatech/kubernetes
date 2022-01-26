### Create a ServiceAccount, ClusterRole and RoleBinding specific to namespaces so that only actions defined in the CLusterRole are allowed on the namespaces

kubectl create ns ns1 ns2

kubectl apply -f nginx.yaml

kubectl apply -f sa.yaml

kubectl apply -f cluster-role.yaml

kubectl apply -f role-binding.yaml

### Now check the access

kubectl auth can-i get pods -n kube-system --as system:serviceaccount:default:sa

kubectl auth can-i get pods -n ns1 --as system:serviceaccount:default:sa

kubectl auth can-i delete pods -n ns1 --as system:serviceaccount:default:sa



