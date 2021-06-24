# install argo rollouts 

- https://github.com/argoproj/argo-rollouts/releases/latest/download/install.yaml

# install config map with tempalte and trigger

- https://github.com/argoproj/argo-rollouts/releases/latest/download/notifications-install.yaml 

<!-- if above command gave any error  ignore as argorollout is its local version -->


# deploy

 kubectl apply -f argorollout.yaml
 kubectl apply -f secret.yaml

# patch config map

kubectl patch cm argo-rollouts-notification-configmap -n argocd --type merge -p '{"data": {"service.email.gmail": "{ username: tempmail436@gmail.com, password: tempmailpassword, host: smtp.gmail.com, port: 465, from: tempmail436@gmail.com }",
"service.slack": "{ apiURL: <url>, token: xoxb-2219249599776-2228900099952-LoW9o6AN2C3EISnpCdW0VVGC, username: username, icon: icon }"}}'

# deploy rollout and dependency

$ kubectl apply -f services.yaml
$ kubectl apply -f virtualsvc.yaml
$ kubectl apply -f rollout.yaml

# check pod status

$ kubectl argo rollouts get rollout rollouts-demo

# Update image to trigger notification on gmail and slack
  kubectl argo rollouts set image rollouts-demo rollouts-demo=argoproj/rollouts-demo:purple






