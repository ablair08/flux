# flux


Add Secretes 

cd /prometheus/examples/
kubectl create secret generic additional-scrape-configs --from-file=prometheus-additional.yaml -n myproject
kubectl create secret generic alertmanager-alertmanager --from-file=alertmanager.yaml -n myproject

