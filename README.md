# Alfresco Search Deployment


```
helm install alfresco-content-services-1.1.4.tgz \
--set externalProtocol="https" \
--set externalHost="$EXTERNALHOST" \
--set externalPort="443" \
--set repository.adminPassword="$ALF_ADMIN_PWD" \
--set postgresql.postgresPassword="$ALF_DB_PWD" \
--set alfresco-infrastructure.persistence.efs.enabled=true \
--set alfresco-infrastructure.persistence.efs.dns="$EFS_SERVER" \
--set alfresco-search.common.resources.requests.memory="2500Mi",alfresco-search.common.resources.limits.memory="2500Mi" \
--set alfresco-search.common.environment.SOLR_JAVA_MEM="-Xms2000M -Xmx2000M" \
--set postgresql.persistence.subPath="$DESIREDNAMESPACE/alfresco-content-services/database-data" \
--set persistence.repository.data.subPath="$DESIREDNAMESPACE/alfresco-content-services/repository-data" \
--set alfresco-search.master.persistence.search.data.subPath="$DESIREDNAMESPACE/alfresco-content-services/solr-data" \
--set alfresco-search.slave.persistence.search.data.subPath="$DESIREDNAMESPACE/alfresco-content-services/solr-data-slave" \
--set alfresco-search.common.type="insight-engine" \
--set alfresco-search.common.registryPullSecrets="quay-registry-secret" \
--set alfresco-search.common.ingress.enabled=true \
--set alfresco-search.common.ingress.basicAuth="YWRtaW46JGFwcjEkWVZsY1BhanEkUTNjOTBKZlptYklhZHo5YmZjbmNXLg==" \
--set alfresco-search.common.ingress.whitelist_ips="0.0.0.0/0" \
--set alfresco-insight-zeppelin.enabled=true \
--set alfresco-search.alfresco-insight-zeppelin.registryPullSecrets="quay-registry-secret" \
--set networkpolicysetting.enabled=false \
--namespace=$DESIREDNAMESPACE
```