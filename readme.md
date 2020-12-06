# Kubernetes Workflows

(aka as k8s inferno  / skynet / live sharing / one fine sunday / pair)

On [Twitch](https://dashboard.twitch.tv/jz_codingblocks) Outlaw and Joe started with a .NET 5 MVP application then...

- [Converted it to Docker](https://github.com/THEjoezack/k8s-helm-skaffold/blob/main/www/Dockerfile)
- [Converted it to a Kubernetes Deployment/Service](https://github.com/THEjoezack/k8s-helm-skaffold/tree/main/deployment/www)
- [Set up a project for it in Skaffold](https://github.com/THEjoezack/k8s-helm-skaffold/blob/main/skaffold.yaml)
- [Created Kustomize Overlays for it](https://github.com/THEjoezack/k8s-helm-skaffold/tree/main/kustomize)
- [Created Skaffold profiles for Kustomize](https://github.com/THEjoezack/k8s-helm-skaffold/blob/main/skaffold.yaml)

Notes:
- We skimped on some security best practices here, like running the container as root, be warned!)
- These steps are assumed to be independent, so you should reset your Kubernetes cluster between the Kubernetes steps.

## Running Manually

This is your typical pre-Docker development story. It requires dotnet 5 installed on your computer.

```bash
cd www
dotnet run
# Note: Protocol has an "s"
open https://localhost:5001/
```
## Running via Docker

This step only requires Docker, note the url!

```bash
cd www
docker build . -t www:latest
docker run -p 5001:80 www:latest
# Note: No "s" in the protocol - http://localhost:5001/
```

## Running via Kubernetes

Now we're kooking with gas, this requries Docker and that you have kubectl installed and hooked up to a Kubernetes cluster.

This step requires port-forwarding to make the container available to you outside the cluster.

Any changes to these files requires that you apply the file again with kubectl apply.

```bash
cd www
docker build . -t www:latest

cd ../deployment
kubectl apply -f www
kubectl port-forward -5001:5001
# Note: No "s" in the protocol - http://localhost:5001/

```
## Running via Helm

This step requires helm, the primary advantage being the use of overridable variables.

This step also requires port-forwarding to make the container available to you outside the cluster.

Updates and uninstallation is easier too, just use helm update or helm uninstall.

```bash
cd deployment
helm install www www
kubectl port-forward -5001:5001
```

Notes:
- You should probably reset your cluster from the previous step

## Running via Skaffold

We have arrived! Now anybody with Skaffold, Kubernetes and Docker installed can start up, keep updated, and stop this entire project with a single command.

This command will watch the files for changes and redeploy, and any services that skaffold knows about are port-forwarded. Finally, any resources created by Skaffold will be deleted when the program exits.

Sweet, right?

```bash
skaffold dev --port-forward
```

## Running via Kustomize

Woah, just found out about Kustomize...how does that Jive with Helm/Skaffold?

You can render your final Kubernetes like this...

```bash
kustomize build kustomize/production | kubectl apply -f -
```

## Running via Kustomize, via Skaffold Profile

```bash
skaffold dev --port-forward --profile kustomize-prod
```

## Resources


- [.NET Dockerfile (thanks GaProgMan!)](https://github.com/GaProgMan/OnionArch/blob/master/Dockerfile)
- [Skaffold](https://skaffold.dev/)
- [Kustomize (thanks TinFoilSaint!)](https://kustomize.io/)
