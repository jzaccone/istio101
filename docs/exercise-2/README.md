# Exercise 2 - Installing Istio on IBM Cloud Kubernetes Service

We will be installing Istio using the Istio Operator. The Istio operator will manage the installation for you instead of you manually installing, upgrading, and uninstalling Istio on your cluster.

1. Download the `istioctl` CLI and add it to your PATH:

   ```shell
   curl -L https://istio.io/downloadIstio | ISTIO_VERSION=1.5.6 sh -
   ```

   ```shell
   export PATH=$PWD/istio-1.5.6/bin:$PATH
   ```

1. Deploy the Istio operator:

    ```shell
    istioctl operator init
    ```

1.  Install the Istio `demo` configuration profile using the operator:

    ```shell
    $ kubectl create ns istio-system
    $ kubectl apply -f - <<EOF 
    apiVersion: install.istio.io/v1alpha1
    kind: IstioOperator
    metadata:
        namespace: istio-system
        name: example-istiocontrolplane
        spec:
            profile: demo
    EOF
    ```

1. The install will take just a couple minutes. Give the operator a few minutes to start installing the pods in the following command. Verify the installation is complete by checking for the pods in the `istio-system` namespace.

    ```shell
    $ kubectl get pods -n istio-system
    NAME                                   READY   STATUS    RESTARTS   AGE
    grafana-5cc7f86765-xzrxj               1/1     Running   0          17m
    istio-egressgateway-866795b5d7-s8dlp   1/1     Running   0          17m
    istio-ingressgateway-f476fdd5-pwnrz    1/1     Running   0          17m
    istio-tracing-8584b4d7f9-54rxg         1/1     Running   0          16m
    istiod-6684498666-ptktr                1/1     Running   0          17m
    kiali-696bb665-bcbv8                   1/1     Running   0          16m
    prometheus-b665549dc-h69cd             2/2     Running   0          16m
    ```

    Before you continue, make sure all the pods are deployed and either in the **`Running`** state. 

2. Check the version of your Istio:
    ```shell
    istioctl version
    ```
    Sample output:
    ```shell
    client version: 1.5.6
    control plane version: 1.5.6
    data plane version: 1.5.6 (4 proxies)
    ```
    Congratulations! You successfully installed Istio into your cluster.