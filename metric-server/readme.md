# Metric Server

Metric Server allows you to monitor resource using in a kubernetes cluster. You can get idea of pod resource usage so you can set correct resource limits in your application's kubernetes pod configuration file.

## Commands

```sh
kubectl top nodes
```

```sh
kubectl get pods
```

## Troubleshooting

If you got an error (x509) in logs that looks like this:

```sh
"Failed to scrape node" err="Get \"https://192.168.200.13:10250/stats/summary?only_cpu_and_memory=true\": x509: cannot validate certificate for 192.168.200.13 because it doesn't contain any IP SANs" node="k8s-worker-01.example.com"
```

You can fix it as described below:

```json
containers:
      - name: mtrics-server
        image: k8s.gcr.io/metrics-server-amd64:v0.3.7
        args:
          - --cert-dir=/tmp
          - --secure-port=4443
          - --kubelet-insecure-tls
          - --kubelet-preferred-address-types=InternalIP,ExternalIP,Hostname
```
