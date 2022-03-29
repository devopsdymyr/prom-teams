
Reference: https://www.youtube.com/watch?v=sh8e_HyKtK0&ab_channel=zzTALK

helm repo add stable https://charts.helm.sh/stable
helm repo update

helm install demo stable/prometheus-operator -n monitoring
kubectl get po -n monitoring

helm repo add prometheus-msteams https://prometheus-msteams.github.io/prometheus-msteams/
helm repo update
helm install msteams prometheus-msteams/prometheus-msteams -n monitoring
kubectl get po -n monitoring
kubectl get secret -n monitoring
kubectl edit secret <alertmanage.yaml> -n monitoring

configSecret

kubectl create secret generic myalertmanager --from-file=alertmanager.yaml=alertmanager-teams.yaml -n monitoring

kubectl get secret -n monitoring 

helm upgrade demo -f values-alertmanager.yaml stable/prometheus-operator -n monitoring