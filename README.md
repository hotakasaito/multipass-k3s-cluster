# Launch a k3s cluster on MacOS

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

## Usage
```bash
$ ./bootstrap -h
Usage:
  bootstrap -h [-c|-m|-d|-n num] (all|cluster|helm|cert|kong|registry|exlb|test|terminate)

Commands:
  all        all
  cluster    install k3s cluster
  helm       helm setup
  cert       install cert-manager
  kong       load balancer
  registry   private registry
  exlb       external loadbalancer on docker
  test       for private registry
  terminate  purge all vms

Flags: valid only for cluster command
  -c         cpu (default: 2)
  -m         memory (default: 4)
  -d         disk (default: 5)
  -n         node (default: 3)
  -h         show this message
```

# Kubernetes
## Samples
1. echoserver service
> ```bash
> $ export KUBECONFIG=$PWD/run/k3s.yaml
> $ kubectl apply -f samples/echoserver.yaml
> ```

2. docker image push
> ```bash
> $ docker image pull nginx:1.17
> $ DOCKER_REGUSTRY_IP=$(multipass ls --format json | jq -r '[.list[].ipv4[] | select(test("^192\\.168\\."))][0]')
> $ docker image tag nginx:1.17 ${DOCKER_REGUSTRY_IP}:32124/nginx:1.17
> $ docker image push ${DOCKER_REGUSTRY_IP}:32124/nginx:1.17
> ```
