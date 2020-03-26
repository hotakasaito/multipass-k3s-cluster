# Launch k3s cluster on MacOS

## Preparing
```bash
$ git clone git@github.com:hotakasaito/multipass-k3s-cluster.git
$ cd multipass-k3s-cluster
```

## Launch cluster
```bash
$ ./bootstrap cluster
```

## Set KUBECONFIG
```bash
$ export KUBECONFIG=$PWD/run/k3s.yaml
```

## Show cluster
### Example
```bash
$ kubectl cluster-info
Kubernetes master is running at https://192.168.64.3:6443
CoreDNS is running at https://192.168.64.3:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
Metrics-server is running at https://192.168.64.3:6443/api/v1/namespaces/kube-system/services/https:metrics-server:/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```

## Terminate clsuter

```bash
$ ./bootstrap terminate
```
