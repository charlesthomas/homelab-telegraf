# homelab-telegraf

This is a mirco-services repo for deploying
[telegraf](https://www.influxdata.com/time-series-platform/telegraf/)
into [my homelab](https://github.com/charlesthomas/homelab).

## cluster access

figuring out permissions was a giant pain with k3s

[this doc](https://github.com/influxdata/telegraf/blob/master/plugins/inputs/kube_inventory/README.md#quickstart-in-k3s) recommends copying the k3s token and cert files to a new location, but even then i couldn't get the permissions correct

instead, on each node i did this even though i'm sure it's a terrible idea:

```bash
sudo chmod 701 /var/lib/rancher/k3s/server
sudo chmod 701 /var/lib/rancher/k3s/server/tls
sudo chmod 604 /var/lib/rancher/k3s/server/token
sudo chmod 604 /var/lib/rancher/k3s/server/tls/client-admin.key
```

the additional resources/rbac.yaml here is because i added permissions based on the `kube-inventory` [plugin docs](https://github.com/influxdata/telegraf/tree/master/plugins/inputs/kube_inventory#kubernetes-permissions).

these docs slightly conflict with the RBAC setup by the helm chart, so i disabled creating rbac in `values.yaml` and the apply is doing a combo of both the one in the chart and the one in the docs

---
This repo is templated via
[homelab-template](https://github.com/charlesthomas/homelab-template)
and automatically updated via
[🤖 Templatron](https://github.com/charlesthomas/templatron).
