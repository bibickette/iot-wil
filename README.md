# Sub-Project presentation - `inception-of-things-gcaptari`
 
> GitOps repository monitored by Argo CD : part of the [Inception-of-Things](https://github.com/bibickette/inception-of-things) project.
 
This repository contains the Kubernetes manifests for the `wil42/playground` application deployed automatically by Argo CD into a K3d cluster.
 
---
 
## How it works
 
Argo CD watches this repository continuously. Any change pushed here is automatically applied to the cluster within minutes : no manual `kubectl apply` needed.
 
```
git push → Argo CD detects change → pulls new image → redeploys pod
```
 
## Repository structure
 
```
├── application.yaml   ← change the image tag here to switch versions
├── ingress.yaml
└── README.md
```
 
## Switching versions
 
To update the running application, edit `application.yml` and change the image tag:
 
```bash
# Switch from v1 to v2
sed -i 's/playground:v1/playground:v2/' application.yml
git add application.yml
git commit -m "update to v2"
git push
```
 
Argo CD will detect the change and redeploy automatically. Verify with:
 
```bash
curl http://localhost:8888/
# {"status":"ok", "message": "v2"}
```
 
## Available versions
 
| Tag | Image |
|---|---|
| `v1` | `wil42/playground:v1` |
| `v2` | `wil42/playground:v2` |
 
---
 
*Part of [Inception-of-Things](https://github.com/bibickette/inception-of-things) project.*
 
