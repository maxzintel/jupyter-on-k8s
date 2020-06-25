# Jupyter Deployment
Given you already have a running kubernetes cluster...
## Steps for deploying:
* `kubectl create namespace jupyter`
* Create deployment manifest.
* `kubectl create -f infrastructure/deploy.yml`
* Once its running, obtain the initial login token:
  * `pod_name=$(kubectl get pods -n jupyter --no-headers | awk '{print $1}')`, then `kubectl logs -n jupyter ${pod_name}`
  * Copy the token following the text: `...?token=...`
* Now we can connect to jupyter with:
  * `kubectl port-forward ${pod-name} 8888:8888 -n jupyter`
  * Once this connection is being handled, navigate to `localhost:8888/?token=${tokenFromBefore}` to access your jupyter container! 