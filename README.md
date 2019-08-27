# flux
FORK github.com:ablair08/flux

minishift start  --memory=16GB  --disk-size=200GB --cpus=6 --vm-driver=virtualbox

oc edit scc restricted


change the following values:
allowHostDirVolumePlugin: true
allowHostNetwork: true
allowPrivilegedContainer: true
runAsUser:
  type: RunAsAny
seLinuxContext:
  type: RunAsAny




{
oc create user ab && oc adm policy add-cluster-role-to-user cluster-admin ab


oc -n kube-system create sa tiller

oc create clusterrolebinding tiller-cluster-rule \
    --clusterrole=cluster-admin \
    --serviceaccount=kube-system:tiller

helm init --skip-refresh --upgrade --service-account tiller --history-max 10 && helm repo add fluxcd https://fluxcd.github.io/flux
}


helm upgrade -i flux \
--set helmOperator.create=true \
--set helmOperator.createCRD=true \
--set git.url=git@github.com:ablair08/flux \
--set syncGarbageCollection.enabled=true \
--set prometheus.enabled=true \
--set memcached.securityContext.runAsUser=null \
--set memcached.securityContext.runAsGroup=null \
--set uid=0 \
--namespace flux \
fluxcd/flux


**once the flux pod comes up** 

  kubectl -n flux logs deployment/flux | grep identity.pub | cut -d '"' -f2

  copy deploy key to github!!