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

```bash
cd www
docker build . -t www
docker run -p 5001:80 www
# Note: No "s" in the protocol
open http://localhost:5001/
```

## Resources

* [.NET Dockerfile (thanks GaProgMan)](https://github.com/GaProgMan/OnionArch/blob/master/Dockerfile)