
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
