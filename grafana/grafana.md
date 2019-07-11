- Get Password

```bash
kubectl get secret grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```
