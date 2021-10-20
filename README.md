# Geoserver Helm Chart

Deploy a geoserver instance using helm. Optionally with periodic backups to an S3-compatible storage.
[GeoServer is an open source server for sharing geospatial data.](http://geoserver.org/)

## Install

```sh
    helm repo add iits-geoserver https://iits-consulting.github.io/geoserver-chart/
    helm repo update
    helm install geoserver iits-geoserver/geoserver
```

## Migrate geoserver to this chart

To migrate your existing geoserver instance, back up your $GEOSERVER_DATA_DIR (typically /data/) and copy it to this
chart's [/data/](/charts/geoserver/data/) directory. All configuration within [/data/](/charts/geoserver/data/) is
automatically applied. Then install the chart like you normally would. For example, at the root of this git repo, run:

```sh
helm upgrade --install geoserver charts/geoserver
```

## Configuration

Upon upgrade, this chart always overrides the $GEOSERVER_DATA_DIR with what's inside
the [/data/](/charts/geoserver/data/) directory. This enables a standardized GitOps workflow. Thus, at the time of
deployment, all configuration is represented within this chart. If you change any configs via Geoserver's GUI, make sure
to fetch your live data via:

```sh
kubectl cp -n geoserver $(kubectl -n geoserver get pods -l app=geoserver -o jsonpath='{.items[0].metadata.name}'):/data/ charts/geoserver/data
```

### Routing

Because routing is such a custom matter, no default ingress is provided in this helm chart.
