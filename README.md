1)kubectl create -f influxdb-deployment.yaml

2)kubectl create -f influxdb-service.yaml

3)kubectl create -f rbac.yaml

4)kubectl create -f  prometheus-configmap.yaml  

5)kubectl create -f kube-state-metrics.yaml  

6)kubectl create -f node-exporter.yaml

7)kubectl create -f prometheus.yaml

8)kubectl create -f grafana.yaml              

Remplace influxdb-pod  with the name of influxdb created by kubernetes (using kubectl -n kube-system get pods )

kubectl -n kube-system exec -ti influxdb-pod influx

CREATE USER "admin" WITH PASSWORD 'admin' WITH ALL PRIVILEGES;
kubectl -n kube-system exec -ti influxdb-pod bash
influx
auth
CREATE DATABASE prometheus; 
CREATE USER "prom" with password 'prom';
GRANT ALL ON prometheus TO prom;
ALTER RETENTION POLICY "autogen" ON "prometheus" DURATION 1d REPLICATION 1 SHARD DURATION 1d DEFAULT;
SHOW RETENTION POLICIES ON prometheus;
USE prometheus;
SHOW MEASUREMENTS;

