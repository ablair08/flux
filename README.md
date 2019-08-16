# flux


minikube start --cpus 8 --memory 16384 --disk-size 200g



kubectl -n kube-system create sa tiller


kubectl create clusterrolebinding tiller-cluster-rule \
    --clusterrole=cluster-admin \
    --serviceaccount=kube-system:tiller


helm init --skip-refresh --upgrade --service-account tiller --history-max 10


helm repo add fluxcd https://fluxcd.github.io/flux


helm upgrade -i flux --set helmOperator.create=true --set helmOperator.createCRD=false --set git.url=git@github.com:ablair08/flux --namespace flux fluxcd/flux

**once the flux pod comes up** 

  kubectl -n flux logs deployment/flux | grep identity.pub | cut -d '"' -f2

  copy deploy key to github!!

