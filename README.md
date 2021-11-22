# Nextcloud Helm Charts

[Helm](https://helm.sh) repo for different charts related to Nextcloud which can be installed on [Kubernetes](https://kubernetes.io)

### Add Helm repository

To install the repo just run:

```bash
helm repo add nextcloud https://nextcloud.github.io/helm/
helm repo update
```

### Helm Charts

* [nextcloud](https://nextcloud.github.io/helm/)

  ```bash
  helm install my-release nextcloud/nextcloud
  ```

## My Configuration

1. Install nextcloud and nginx-ingress-controller

```bash
helm install my-release charts/nextcloud -f custom-apache.yaml
helm install nginx-ingress-controller ingress-nginx/ingress-nginx
```

2. Create tls-secret

```bash
kubectl create secret tls tls-secret --key privkey.pem --cert cert.pem
```

3. Register DNS

Check LoadBalancer's EXTERNAL-IP

```
kubectl get svc nginx-ingress-controller-ingress-nginx-controller
```

And then register it to DNS Record as CNAME in AWS Route 53 console.

4. Restart nginx-ingress-controller pod

```
kubectl delete pod nginx-ingress-controller-ingress-nginx-controller-<XXXX>
```

You can access your dns address after a few minutes later

5. In nextcloud

1) 'Talk' download and enable
2) Use Talk with other people
