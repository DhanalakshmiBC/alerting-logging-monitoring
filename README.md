## Logging & Monitoring Stack (Prometheus, Grafana, EFK, Node-Exporter)

This Helm chart deploys a complete Kubernetes logging and monitoring solution, including:
	•	Prometheus Operator (Prometheus, Alertmanager, ServiceMonitors, PodMonitors)
	•	Grafana with dashboards
	•	Node Exporter for node-level metrics
	•	EFK (Elasticsearch, Fluentd, Kibana) logging stack
	•	Required CRDs and configuration files


## Components Included
Prometheus Stack
Located in: prometheus/

Includes:
	•	Prometheus Operator manifests
	•	Prometheus deployment & service
	•	Ingress configuration
	•	ServiceMonitor definitions
	•	Tests and helpers

Alertmanager
Located in: templates/alert-manager/

Includes:
	•	Alertmanager Deployment
	•	Alertmanager ConfigMap (alerting rules)
	•	Service definitions
	•	Prometheus alert rules

Node Exporter
Located in: templates/node-exporter/

Provides node-level metrics via:
	•	Node Exporter DaemonSet
	•	Service for scraping via Prometheus

Grafana
Located in: efk/grafana/

Includes:
	•	Grafana Deployment & Service
	•	Dashboards config (optional)
	•	PostgreSQL backend (optional)
	•	PVC for persistence

EFK Logging Stack
Located in: efk/

Includes:
Elasticsearch
	•	StatefulSet
	•	Service
	•	Persistent Volume claims

Fluentd
	•	DaemonSet
	•	ConfigMap
	•	RBAC files

Kibana
	•	Deployment & service (if enabled)

## Folder Structure
logging-monitoring/
├── charts/
├── crds/
│   ├── alertmanagerconfigs.yaml
│   ├── alertmanagers.yaml
│   ├── podmonitors.yaml
│   ├── probes.yaml
│   ├── prometheusagents.yaml
│   ├── prometheuses.yaml
│   ├── prometheusrules.yaml
│   ├── scrapeconfigs.yaml
│   ├── servicemonitors.yaml
│   ├── thanosrulers.yaml
│
├── templates/
│   ├── alert-manager/
│   ├── cert-manager/
│   ├── node-exporter/
│   ├── efk/
│   │   ├── elasticsearch/
│   │   ├── fluentd/
│   │   ├── kibana/
│   │   └── grafana/
│   └── prometheus/
│
├── Chart.yaml
├── values.yaml
└── README.md


## Installation
Add Helm Repo 

If hosting privately, replace the URL:
helm repo add logging-monitoring https://your-repo-url

 Install the Chart
 helm install logmon ./logging-monitoring -n monitoring --create-namespace

 Upgrade Release
 helm upgrade logmon ./logging-monitoring -n monitoring

 Uninstall
 helm uninstall logmon -n monitoring


## Configuration (values.yaml)
Key configurable fields:

prometheus:
  enabled: true
  retention: 15d

grafana:
  adminUser: admin
  adminPassword: admin123
  persistence:
    enabled: true

nodeExporter:
  enabled: true

elasticsearch:
  replicas: 1
  storage: 20Gi

fluentd:
  extraVolumeMounts: []

## Accessing the Dashboards
Grafana UI
grafana.68.233.108.177.nip.io
Default credentials:
	•	Username: admin
	•	Password: ChangeMe123! 

Prometheus UI
prometheus.68.233.108.177.nip.io

Alertmanager UI
alertmanager.68.233.108.177.nip.io

Kibana UI
kibana.68.233.108.177.nip.io


## CRDs
This chart includes Kubernetes CRDs for:
	•	Alertmanager
	•	Prometheus
	•	ServiceMonitor
	•	PodMonitor
	•	PrometheusRule
	•	ThanosRuler

These CRDs are required for the Prometheus Operator to work correctly.


Contributing
Feel free to open issues and submit PRs to enhance the chart.

Grafana dashboard view
<img width="1443" height="739" alt="Screenshot 2025-12-08 at 12 30 22 PM" src="https://github.com/user-attachments/assets/d9096b14-d045-4683-ada4-dae33d5684d4" />



