# Tushar_Microservice_Monitoring_Setup
This project sets up a complete **Kubernetes monitoring stack** using Prometheus, Grafana, and Node Exporter with external access via domain.

## 📊 Prometheus + Grafana + Node Exporter (Kubernetes_Single Cluster)
---

## 🧩 Architecture Overview

![Monitoring Architecture](Microservice_Monitoring1.gif)

---

## ⚙️ Tech Stack

- Kubernetes
- Prometheus
- Grafana
- Node Exporter (DaemonSet)
- Helm

---

## 🚀 Step-by-Step Implementation

# 🚀 Kubernetes Monitoring Setup (Prometheus + Grafana)

### 1) Create Namespace

kubectl create namespace monitoring

---

### 2) Add Helm Repo & Install Monitoring Stack

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm repo update

helm install monitoring prometheus-community/kube-prometheus-stack -n monitoring

---

### 3) Verify Pods & DaemonSets

kubectl get pods -n monitoring  
kubectl get daemonsets -n monitoring

---

### 4) Check Services & Expose Grafana

kubectl get svc -n monitoring  

kubectl edit svc monitoring-grafana -n monitoring  

👉 Convert ClusterIP service to LoadBalancer:

type: LoadBalancer  

(AGIC ingress rule also can be used)

---

### 5) Map External IP to Custom Domain

Once External IP is assigned:

kubectl get svc -n monitoring  

👉 Map domain with IP (DNS):

grafana.tushardevops.online → <EXTERNAL-IP>  

👉 Access Grafana:

http://grafana.tushardevops.online/

---

### 6) Generate Grafana Admin Password

PowerShell command:

[System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String((kubectl get secret monitoring-grafana -n monitoring -o jsonpath="{.data.admin-password}")))

---

### 7) Login to Grafana

Username: admin  
Password: (generated above)  
update email address

👉 Change password after login

---

### 8) Explore Grafana

- Prometheus data source already configured  
- Node Exporter already configured  
- Dashboards available  

👉 Explore:
- Monitoring  
- Alerting  
- Metrics visualization  

---

## 📊 Commands Summary

kubectl get pods -n monitoring  
kubectl get daemonsets -n monitoring  
kubectl get svc -n monitoring  

---

## 🌐 Output Example

monitoring-grafana   LoadBalancer   10.x.x.x   20.xx.xx.xx   80:xxxxx/TCP  

---

## 🎯 Result

Grafana accessible via:

http://grafana.tushardevops.online/

![Grafana_Dashboard](4dashboard.png)


![Grafana_Dashboard](3dashboard.png)
---

## 🔥 Notes 

- Can use LoadBalancer OR Ingress (AGIC)  
- Prometheus + Node Exporter auto-configured  
- Ready-to-use monitoring dashboards  
