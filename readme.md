# k8s inferno  / skynet / live sharing / one fine sunday / pair

## Up next

- Stateful set
- Separate www to front-end/back-end
- Prometheus/Grafana
- 1 metric, 1 trace, and get that visualixed in prom jager and grafana.

## Running Manually

```bash
# requires dotnet 5
cd www
dotnet run
# Note: Protocol has an "s"
open https://localhost:5001/
```
## Running via Docker

Notes:
- we skimped on some security best practices here, like running as root, be warned!)

```bash
cd www
docker build . -t www:latest
docker run -p 5001:80 www:latest
# Note: No "s" in the protocol - http://localhost:5001/
```

## Running via Kubernetes

```bash
cd www
docker build . -t www:latest

cd ../deployment
kubectl apply -f www
# Note: No "s" in the protocol - http://localhost:5001/
```
## Running via Helm

Notes:
- You should probably reset your cluster from the previous step

## Running via skaffold

```bash
skaffold run --port-forward
```

## Resources

```bash
cd charts
helm install www www
```

* [.NET Dockerfile (thanks GaProgMan)](https://github.com/GaProgMan/OnionArch/blob/master/Dockerfile)