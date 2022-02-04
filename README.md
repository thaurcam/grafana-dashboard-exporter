# Grafana Dashboard Exporter
Putting together the gists from **crisidev/grafana-dashboard-exporter**, **kosuke-/grafana-dashboard-exporter** and 
**IAmStoxe/loop-json.sh**

This script exports all grafana dashboards to a local folder and maintains the folder structure of grafana

Change the following vars according to your environment:
- BACKUP_DIR (base directory to place the subfolders and dashboards in)
- HOST (URL to your grafana instance inlcuding port if other than 443)
- KEY (grafana API key with read permissions)