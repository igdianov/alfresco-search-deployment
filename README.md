# Alfresco Search Deployment

## Contents of this repository
a) Alfresco Content Services deployed via [docker-compose](docker-compose/docker-compose.yml)
1. Alfresco Repository
2. Alfresco Share
3. A Postgres DB  
4. Alfresco Insight Engine (under Quay.io repository)
5. Insight Zeppelin (under Quay.io repository)

b) Alfresco Search (`alfresco-search`) helm charts used as a requirement under [acs-deployment/helm/alfresco-content-services](https://github.com/Alfresco/acs-deployment/tree/master/helm/alfresco-content-services) Chart


## Alfresco Search - Helm Chart

### Deployment options
* [Deploying with Helm charts on AWS using Kops](https://github.com/Alfresco/acs-deployment/tree/master/docs/helm-deployment-aws_kops.md)
* [Deploying with Helm charts on AWS using EKS](https://github.com/Alfresco/acs-deployment/tree/master/docs/helm-deployment-aws_eks.md)

### Configurations
a) setting affinity and tolerations for the search pod:

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

b) creates its own PVC to store indexes if no other existingPVC is given with persistence.existingClaim

```bash
persistence:
  existingClaim: #Only define if you have a pvc already defined
```

c) offers the posibility of attaching a specific AWS EBS

```bash
persistence:
  EbsPvConfiguration:
    fsType: ext4
    volumeID: volumeEC2
```

d) gives you the option of setting affinity for the persistent volume.

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

## Contributing guide
Please use [this guide](CONTRIBUTING.md) to make a contribution to the project and information to report any issues.

This project contains the code for starting the entire Alfresco Content Services (Enterprise) product with **Docker** or **Kubernetes**.

## Other Information
Checkout [acs-deployment](https://github.com/Alfresco/acs-deployment/blob/master/README.md#other-information) readme.