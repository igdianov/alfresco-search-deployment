# Alfresco Search Deployment

This Helm chart will deploy Search Services.

It offers you the posibility of setting affinity and tolerations for the search pod:

```bash
# Define Affinity and Tolerations used for scheduling SOLR on Pod and PV level

affinity: |
  nodeAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
      nodeSelectorTerms:
        - matchExpressions:
          - key: "SolrMasterOnly"
            operator: In
            values:
            - "true"

tolerations:
- key: "SolrMasterOnly"
  operator: "Equal"
  value: "true"
  effect: "NoSchedule"
```

It creates its own PVC to store indexes if no other existingPVC is given with persistence.existingClaim

```bash
persistence:
  existingClaim: #Only define if you have a pvc already defined
```

It offers the posibility of attaching a specific AWS EBS

```bash
persistence:
  EbsPvConfiguration:
    fsType: ext4
    volumeID: volumeEC2
```

And also gives you the option of setting affinity for the persistent volume.

```bash
PvNodeAffinity:
  required:    
    nodeSelectorTerms:
    - matchExpressions:
      - key: "SolrMasterOnly"
        operator: In
        values:
        - "true"
```
