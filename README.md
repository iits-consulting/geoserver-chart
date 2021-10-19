# Geoserver Helm Chart

Deploy a geoserver instance using helm.

## Install

```shell
    helm repo add iits-geoserver https://iits-consulting.github.io/geoserver-chart/
    helm repo update
    helm install geoserver iits-geoserver/geoserver
```

## Configuration

All configuration within [/data/](/data/) is automatically applied. If you
change any configs via the GUI, you can fetch the live data via:

```sh
kubectl cp -n geoserver $(kubectl -n geoserver get pods -l app=geoserver -o jsonpath='{.items[0].metadata.name}'):/data/ data
```

Because routing is such a custom matter, no default ingress is provided in this helm chart.
