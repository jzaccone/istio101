# Exercise 5 - Expose the service mesh with the Istio Ingress Gateway

The components deployed on the service mesh by default are not exposed outside the cluster. External access to individual services so far has been provided by creating an external load balancer or node port on each service.

An Ingress Gateway resource can be created to allow external requests through the Istio Ingress Gateway to the backing services.

![Using istio gateway](../README_images/istio2.jpg)

## Expose the Guestbook app with Ingress Gateway

1. Configure the guestbook default route with the Istio Ingress Gateway. The `guestbook-gateway.yaml` file is in this repository (istio101) in the `workshop/plans` directory.

```shell
cd ../../plans
kubectl create -f guestbook-gateway.yaml
```

1. Get the **EXTERNAL-IP** of the Istio Ingress Gateway.

```shell
kubectl get service istio-ingressgateway -n istio-system
```

Output:

```shell
NAME                   TYPE           CLUSTER-IP      EXTERNAL-IP     PORT(S)                                       AGE
istio-ingressgateway   LoadBalancer   172.21.254.53    169.6.1.1       80:31380/TCP,443:31390/TCP,31400:31400/TCP    1m
2d
```

1. Make note of the external IP address that you retrieved in the previous step, as it will be used to access the Guestbook app in later parts of the course. Create an environment variable called $INGRESS_IP with your IP address.

Example:

```shell
export INGRESS_IP=169.6.1.1
```

Remember this environment variable as we will use it in the next lab.

## References

* [Kubernetes Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/)

* [Istio Ingress](https://istio.io/docs/tasks/traffic-management/ingress.html)

* [Bring your own ALB](https://www.ibm.com/blogs/bluemix/2019/04/bring-your-own-alb-dns-with-health-checks-and-ssl-certificates-beta/)
