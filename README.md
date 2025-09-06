#🔑 How to Login to ArgoCD on Your Local Cluster Using the CLI

1. Install the ArgoCD CLI
If you’re on macOS, install with Homebrew:
```
brew install argocd
```

2. Get the Initial Admin Password
ArgoCD stores the initial admin password in a Kubernetes secret. Retrieve it with:
```
argocd admin initial-password -n argocd
```

3. Login to the ArgoCD Server
Use the username admin and the password from step 2 to login. For example, If port-forwarding is set up on 127.0.0.1:8080, log in with:
```
argocd login 127.0.0.1:8080
```
**Replace 127.0.0.1 with your own local IP address

4. Set the Current Namespace to argocd
This makes CLI commands automatically run in the argocd namespace:
```
kubectl config set-context --current --namespace=argocd
```

5. Create the Guestbook Example Application
Deploy the sample Guestbook app from the official repo:
```
argocd app create guestbook \
  --repo https://github.com/argoproj/argocd-example-apps.git \
  --path guestbook \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace default
```
👉 At this point, you can sync the app with:

argocd app sync guestbook
Do you want me to also include the port-forwarding command so you can actually access the ArgoCD UI in the browser (localhost:8080)?
