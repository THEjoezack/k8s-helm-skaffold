# k8s inferno  / skynet / live sharing / one fine sunday / pair

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
# Note: No "s" in the protocol
open http://localhost:5001/
```

# Running via Kubernetes

```bash
cd www
docker build . -t www:latest
docker run -p 5001:80 www:latest
# Note: No "s" in the protocol
open http://localhost:5001/
```

## Resources

* [.NET Dockerfile (thanks GaProgMan)](https://github.com/GaProgMan/OnionArch/blob/master/Dockerfile)