#!/bin/bash
TIMESTAMP=$(date +"%Y.%m.%d-%H.%M.%S")
BACKUP_DIR="."
HOST="https://your-grafana-url:your-port-if-not-443"

# backup grafana dashboards
KEY="your-grafana-api-key-with-read-permissions-to-export-the-dashboards"
if [ ! -d $BACKUP_DIR/dashboards ] ; then
    mkdir -p $BACKUP_DIR/dashboards
fi

for row in $(curl -k -H "Authorization: Bearer $KEY" $HOST/api/search\?query\=\& | jq -r '.[] | @base64'); do
    _jq() {
     echo "${row}" | base64 --decode | jq -r "${1}"
    }
    uri=$(_jq '.uri')
    uid=$(_jq '.uid')
    dashboard=${uri:3}
    folder=$(_jq '.folderTitle' | tr '[:upper:]' '[:lower:]')
    #todo: create all necessary folders one time and not over and over again in the loop
    if [ ! -d $BACKUP_DIR/dashboards/$folder ]; then
      mkdir -p $BACKUP_DIR/dashboards/$folder
    fi
    curl -k -H "Authorization: Bearer $KEY" $HOST/api/dashboards/uid/$uid | jq . > $BACKUP_DIR/dashboards/$folder/$dashboard.json
done