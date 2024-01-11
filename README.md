# Spring4Shell Vulnerable Demo App
This repository creates a docker container into GitHub container registry, which is vulnerable by Spring4Shell.  
The container exposes a tomcat based web server on port 8080.

## Deployment
### Manual deployment
```sh
docker run -p 8080:8080 ghcr.io/njannasch/vulnerable-741615656:2849dc93ad178297038e7ce533822f5941a075d3
```

### Kubernetes deployment
```sh
kubectl apply -f deployment.yaml
# Wait until deployment is done, see details with
watch kubectl get pods
```
## Exploit
To exploit the container and initialize the webshell execute:
```sh
./exploit.sh "<HOSTNAME>:<PORT>"
```
Afterwards a webshell is available below **/shell.jsp?cmd=CMD**  where CMD can be anything e.g. like whoami (-> root).  
Further lateral movement is possible on from this point.

## Security Measures
Depending on team responsibilities and company maturity level different security measures are possible like Container Image scanning,  
Container Registry Scanning, Admission Controller, Runtime Protection (e.g. RASP), Agentless Scanning (for Hyperscalers), SAST, DAST, SCA... and many more

### Container
For container runtime visibility and protection different toolings are available on the market like runc or eBPF based.  
Open source solutions for eBPF are e.g. kubearmor, tetragon.
