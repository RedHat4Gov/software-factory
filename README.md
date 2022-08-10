# A Software Factory

This repository contains the various demonstration for software factory features.

Visit the [Software Factory](https://redhat4gov.github.io/software-factory/) documentation page.

## Partner Demonstrations

### Software Bill of Material

First, clone this repo. Then, from a fresh cluster:

1. Install the OpenShift Pipelines Operator into all namespaces
1. Install Sonatype Nexus IQ Operatore
    1. Install the Nexus IQ namespace ``` oc apply -f components/sonatype/sonatype-namespace.yml ```
    1. Insall the Nexus IQ Operator Subscription ``` oc apply -f components/sonatype/nexus-iq-sever/nexus-iq-server-subscription.yml ```
    1. Insall an Nexus IQ Operator instance ``` oc apply -f components/sonatype/nexus-iq-sever/nexus-iq-server-instance.yml ```
    1. Insall an Nexus IQ Operator route ``` oc apply -f components/sonatype/nexus-iq-sever/nexus-iq-server-route.yml ```
1. Access the Nexus IQ Server via your route
    1. Login with default credentials [un: admin, pw: admin123]
    1. Upload the Not For Resale (NFR) License
1. Install Tekton task for Nexus IQ Scan ``` oc apply -f https://raw.githubusercontent.com/tektoncd/catalog/main/task/nexus-lifecycle-scan/0.1/nexus-lifecycle-scan.yml ```
1. Install WebGoat Sample Pipeline (components/sonatype/tekton-pipelines-samples/web-goat-pipeline)
    1. First, the two parameters in the pipeline CRD
        1. [REPLACE-WITH-NEXUS-IQ_SERVER] - Replace with the route created earlier
        1. [USER:PASSWORD] - Use the default of ```admin:admin123```
    1. Invoke the updated pipline CRD ``` oc apply -f components/sonatype/tekton-pipelines-samples/web-goat-pipeline ```
1. Invoke a pipeline run. Make sure to selevt the VolumeClaimTemplate for the storage option

