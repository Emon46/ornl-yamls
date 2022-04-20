1. Upgrade kubedb operator

```bash
helm upgrade -i kubedb-operator appscode/kubedb \
  -n kubedb-operator \
  --version v2022.03.28 \
  --reuse-values \
  --set kubedb-provisioner.operator.registry=kubedb \
  --set kubedb-provisioner.operator.repository=operator \
  --set kubedb-provisioner.operator.tag=raft-metrics-exporter_linux_amd64
```

```bash
helm install kubedb appscode/kubedb \
  --version v2022.03.28 \
  --namespace kubedb --create-namespace \
  --set kubedb-provisioner.enabled=true \
  --set kubedb-ops-manager.enabled=true \
  --set kubedb-autoscaler.enabled=true \
  --set kubedb-dashboard.enabled=true \
  --set kubedb-schema-manager.enabled=true \
  --set-file global.license=kubedb-enterprise-license-579bb78c-b616-49ce-af34-768c27f402fd.txt \
  --set kubedb-provisioner.operator.registry=kubedb \
  --set kubedb-provisioner.operator.repository=operator \
  --set kubedb-provisioner.operator.tag=raft-metrics-exporter_linux_amd64
```

2. Add new test PostgresVersions

```bash
kubectl create -f pg-0.10.0-raft-new.yaml
kubectl create -f pg-0.10.0-raft-old.yaml
kubectl create -f pg-0.6.0-raft-new.yaml
kubectl create -f pg-0.6.0-raft-old.yaml
```

3. create demo namespace

```
kubectl create ns demo
```

4. create test postgres instancces

```bash
kubectl create -f pg-r34-wfix.yaml
kubectl create -f pg-r34-wofix.yaml
kubectl create -f pg-r35-wfix.yaml
kubectl create -f pg-r35-wofix.yaml
```

5. Port forward and open Grafana Dashboard

```
kubectl port-forward sts/prometheus-kube-prometheus-stack-prometheus 9090:9090 -n monitoring

kubectl port-forward deploy/kube-prometheus-stack-grafana 3000:3000 -n monitoring
```

6. Install panopticon

```
helm upgrade -i panopticon appscode/panopticon \
    -n kubedb-operator --create-namespace \
    --set-file license=/path/to/license.txt
```

7. Install grafana-dashboard.json
