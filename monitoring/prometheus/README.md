### Prometheus gathers the metrics from a K8S cluster. 

Steps (YAML files are in this repo) -

1.) Create namespace

kubectl create namespace monitoring

2.) Create ClusterRole and ClusterRoleBindings

https://github.com/enatech/kubernetes/blob/master/monitoring/prometheus/cluster-role.yaml

3.) Create configmap, deployment and service

https://github.com/enatech/kubernetes/blob/master/monitoring/prometheus/config-map.yaml


4.) Access the Prometheus Dashboard.
