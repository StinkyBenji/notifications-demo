# argocd-notifications hands-on 

This repo deploys argocd-notifications as an argocd application. In `argocd-notifications/base`, the manifest of `argocd-notifications` is defined.

We used HashiCorp Vault to store our secret (Slack token), by installing argocd-vault-plugin on the argocd repo server (Refer to [README.me](https://github.com/StinkyBenji/openshift-gitops-setup/blob/master/argocd-server/README.md)), we can retrieve the token by creating secret object as shown in the following:

```
---
apiVersion: v1
kind: Secret
metadata:
  name: argocd-notifications-secret
  annotations:
    avp.kubernetes.io/path: "secret/data/vplugin/slacktoken"
stringData: 
  slack-token: <slack-token>
type: Opaque
```

`notifications-app/base` is the definition of an argocd application which deploys the notification controller. We referred this repository in [OpenShift-GitOps-Setup](https://github.com/StinkyBenji/openshift-gitops-setup). 