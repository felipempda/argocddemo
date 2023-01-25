# Demo argoCD

Simple projet for testing argocd.

# Creating app

kubectl create namespace testapp

argocd app create myapp --repo https://github.com/felipempda/argocddemo.git --path app --dest-server https://kubernetes.default.svc --dest-namespace testapp


# View app details

argocd app get myapp

```yaml
Name:               argocd/myapp
Project:            default
Server:             https://kubernetes.default.svc
Namespace:          testapp
URL:                https://xxxxxxxxx/applications/myapp
Repo:               https://github.com/felipempda/argocddemo.git
Target:
Path:               app
SyncWindow:         Sync Allowed
Sync Policy:        <none>
Sync Status:        OutOfSync from  (f355f0f)
Health Status:      Missing

GROUP  KIND        NAMESPACE  NAME   STATUS     HEALTH   HOOK  MESSAGE
apps   Deployment  testapp    myapp  OutOfSync  Missing
```

# Sync app

argocd app sync myapp

```yaml
TIMESTAMP                  GROUP        KIND   NAMESPACE                  NAME    STATUS    HEALTH        HOOK  MESSAGE
2023-01-25T02:12:30+00:00   apps  Deployment     testapp                 myapp  OutOfSync  Missing
2023-01-25T02:12:31+00:00   apps  Deployment     testapp                 myapp  OutOfSync  Missing              deployment.apps/myapp created
2023-01-25T02:12:31+00:00   apps  Deployment     testapp                 myapp    Synced  Progressing              deployment.apps/myapp created

Name:               argocd/myapp
Project:            default
Server:             https://kubernetes.default.svc
Namespace:          testapp
URL:                https://xxxxxxxxx/applications/myapp
Repo:               https://github.com/felipempda/argocddemo.git
Target:
Path:               app
SyncWindow:         Sync Allowed
Sync Policy:        <none>
Sync Status:        Synced to  (f355f0f)
Health Status:      Progressing

Operation:          Sync
Sync Revision:      f355f0f2e3d6c629be90dd6929281788b13136dc
Phase:              Succeeded
Start:              2023-01-25 02:12:30 +0000 UTC
Finished:           2023-01-25 02:12:31 +0000 UTC
Duration:           1s
Message:            successfully synced (all tasks run)

GROUP  KIND        NAMESPACE  NAME   STATUS  HEALTH       HOOK  MESSAGE
apps   Deployment  testapp    myapp  Synced  Progressing        deployment.apps/myapp created
```