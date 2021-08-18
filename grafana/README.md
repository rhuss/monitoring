Import these dashboards to Grafana.

The steps are documented at https://grafana.com/docs/grafana/latest/dashboards/export-import/


For the broker/trigger, run this command on the busybox to generate many requests.


```
for i in `seq 1 200000`; do  curl -s "http://broker-ingress.knative-eventing.svc.cluster.local/event-example/default"   -X POST   -H "Ce-Id: say-hello-goodbye"   -H "Ce-Specversion: 1.0"   -H "Ce-Type: greeting"   -H "Ce-Source: sendoff"   -H "Content-Type: application/json"   -d '{"msg":"Hello Knative! Goodbye Knative!"}'; done

for i in `seq 1 200000`; do  curl -v "http://broker-ingress.knative-eventing.svc.cluster.local/event-example/default"   -X POST   -H "Ce-Id: say-goodbye"   -H "Ce-Specversion: 1.0"   -H "Ce-Type: not-greeting"   -H "Ce-Source: sendoff"   -H "Content-Type: application/json"   -d '{"msg":"Goodbye Knative!"}'; done

```