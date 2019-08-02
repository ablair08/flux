# flux


Add Secretes 

kubectl -n kube-system create sa tiller

kubectl create clusterrolebinding tiller-cluster-rule \
    --clusterrole=cluster-admin \
    --serviceaccount=kube-system:tiller

helm init --skip-refresh --upgrade --service-account tiller --history-max 10

helm repo add fluxcd https://fluxcd.github.io/flux

helm upgrade -i flux \
--set helmOperator.create=true \
--set helmOperator.createCRD=false \
--set git.url=git@github.com:ablair08/flux \
--namespace flux \
fluxcd/flux

cd /prometheus/examples/
kubectl create secret generic additional-scrape-configs --from-file=prometheus-additional.yaml -n myproject
kubectl create secret generic alertmanager-alertmanager --from-file=alertmanager.yaml -n myproject

