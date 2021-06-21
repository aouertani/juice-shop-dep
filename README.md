# juice-shop

![Version: latest](https://img.shields.io/badge/Version-latest-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: v12.0.2](https://img.shields.io/badge/AppVersion-v12.0.2-informational?style=flat-square)

OWASP Juice Shop: Probably the most modern and sophisticated insecure web application

**Homepage:** <https://mambudemo.com>

**Grafana:** <https://grafana.mambudemo.com>

## Maintainers

| Name | Email |
| ---- | ------ |
| Ahmed Ouertani | elouertani.ahmed@gmail.com |

## Source Code

* <https://github.com/aouertani/juice-shop-dep.git>
* <https://github.com/bkimminich/juice-shop>

## Prerequisites

In order to be able to run Juice Shop in GkE the following tools and configuration need to be set:
* cert-manager : https://aouertani.atlassian.net/l/c/zFeku5dD
* Ingress Ngnix Controller: https://aouertani.atlassian.net/l/c/VqJaAWKe
* Ingress Cluster Issuer: https://aouertani.atlassian.net/l/c/qigL8ZM9
* Google Cloud Domain Name: https://aouertani.atlassian.net/l/c/eWR7NcGV

## Deploy Juice Shop in GKE

* Clone and Deploy Juice Shop
```
$ git clone https://github.com/aouertani/juice-shop-dep.git
$ cd juice-shop-dep
$ helm install demo .
```
* Check that all the application’s components are up and running:
```
kubectl get svc,pods,ingress,deployments -n default
```
* Get the Ingress external IP (ADDRESS)
```
$ kubectl get ingress -n default 
NAME              CLASS    HOSTS           ADDRESS          PORTS     AGE
demo-juice-shop   <none>   mambudemo.com   34.116.180.176   80, 443   2d16h
```
* Create a record set in your DNS zone to point the DNS created to the ingress IP, here 34.116.180.176
* Access the application web interface at this address you set. Here : https://mambudemo.com/

## Set Prometheus and Grafana dashboard
The detailed procedure here: https://aouertani.atlassian.net/l/c/EjpAmRUn

## Deploy Juice Shop in Minikube 

* If you installed Minikube locally, run the following command:
```
minikube start
```
* Enable the Ingress controller
```
minikube addons enable ingress
```
* Verify that the NGINX Ingress controller is running
```
kubectl get pods -n kube-system
```
* Clone and deploy Juice Shop
```
$ git clone https://github.com/aouertani/juice-shop-dep.git
$ cd juice-shop-dep
$ git checkout master
$ helm install demo .
```
* Verify the IP address is set:
```
kubectl get ingress
```
* Get the Minikube IP adress and add the following line to the bottom of the /etc/hosts file.
```
$ IP=$(minikube ip)
$ echo "${IP} chart-example.local" | sudo tee -a /etc/hosts
```
* Verify that the Ingress controller is directing traffic:
```
$ curl chart-example.local
```

## Chart Configuration

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| annotations | object | `{}` | add annotations to the deployment, service and pods |
| fullnameOverride | string | `""` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"docker.io/bkimminich/juice-shop"` | Container Image containing the juice-shop |
| image.tag | string | defaults to the appVersion | The image tag |
| imagePullSecrets | list | `[]` |  |
| ingress.annotations | object | `{}` |  |
| ingress.enabled | bool | `false` |  |
| ingress.hosts[0].host | string | `"chart-example.local"` |  |
| ingress.hosts[0].paths | list | `[]` |  |
| ingress.tls | list | `[]` |  |
| labels | object | `{}` | add labels to the deployment, service and pods |
| nameOverride | string | `""` |  |
| nodeSelector | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| replicaCount | int | `1` |  |
| resources | object | `{}` |  |
| securityContext | object | `{}` |  |
| service.port | int | `3000` |  |
| service.type | string | `"ClusterIP"` |  |
| tolerations | list | `[]` |  |
