1. Upgrade kubedb operator

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
  --set kubedb-provisioner.operator.registry=hremon331046 \
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
