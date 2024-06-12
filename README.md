# dify-kubernetes

Deploy Dify on Kubernetes

## How to use

### Clone the repository

```shell
git clone https://github.com/Winson-030/dify-kubernetes.git

kubectl apply -f dify-kubernetes.yaml

```

### Apply Directly

```shell

kubectl apply -f https://raw.githubusercontent.com/Winson-030/dify-kubernetes/main/dify-deployment.yaml

```

After Deployed, you can visit the dify web site via nodeport at 'http://$(PUBLIC_IP):30000', or you can deploy a ingress to your cluster.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: dify-ingress
  namespace: dify
spec:
  ingressClassName: 'traefik'
  rules:
    - host: dify.example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: dify-nginx
                port:
                  number: 80
          - path: /api
            pathType: Prefix
            backend:
              service:
                name: dify-nginx
                port:
                  number: 80
          - path: /console/api
            pathType: Prefix
            backend:
              service:
                name: dify-nginx
                port:
                  number: 80
          - path: /v1
            pathType: Prefix
            backend:
              service:
                name: dify-nginx
                port:
                  number: 80
          - path: /files
            pathType: Prefix
            backend:
              service:
                name: dify-nginx
                port:
                  number: 80
  tls:
    - secretName: dify-tls
    
```
