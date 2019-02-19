# Leonardo Initial test

Setting up a leonardo standalone instance.

## Initial tests / failures

The IP address and alias need to be added to /etc/hosts, so that the
API can be accessed as intended.

```
130.211.229.19 	leonardo-dev.anvilproject.org
```

My /etc/hosts file looks like this,

```
##
# Host Database
#
# localhost is used to configure the loopback interface
# when the system is booting.  Do not change this entry.
##
130.211.229.19  leonardo-dev.anvilproject.org
127.0.0.1	localhost
255.255.255.255	broadcasthost
::1             localhost
```

This allows me to access the API on Swagger. 

NOTE: This is not possible via Roswell Internet yet. 

## Testing the API

Test different API functions

### Install gcloud

https://cloud.google.com/sdk/docs/downloads-interactive

This is needed if you want to test the API, without Swagger.

### Get a list of clusters

For each session you'd need to authenticate with Google.

```
gcloud auth login
```

Then run the API `GET` command to get a list of clusters as json

```
curl -k -X GET 
	--header 'Content-Type: application/json' 
	--header 'Accept: application/json'
	--header "Authorization: Bearer `gcloud auth print-access-token`" 
	'https://leonardo-dev.anvilproject.org/api/clusters'
```

List of clusters as json

```
[{"autopauseThreshold":30,"stagingBucket":"leostaging-ea-leo181206r2-390d6787-2cbb-41d2-9f93-4570f389296a","clusterImages":[],"scopes":[],"instances":[],"errors":[],"machineConfig":{"numberOfWorkers":0,"masterMachineType":"n1-standard-2","masterDiskSize":200},"creator":"afgane@gmail.com","googleProject":"anvil-leo-dev","id":3,"labels":{"creator":"afgane@gmail.com","clusterName":"ea-leo181206r2","googleProject":"anvil-leo-dev"},"dateAccessed":"2018-12-07T03:39:50.200Z","stopAfterCreation":false,"status":"Stopped","clusterUrl":"https://130.211.229.19/notebooks/anvil-leo-dev/ea-leo181206r2","clusterName":"ea-leo181206r2","operationName":"projects/anvil-leo-dev/regions/us-west1/operations/b050149f-c59d-4999-acdf-a7226085bb9f","serviceAccountInfo":{},"googleId":"8593f34c-8095-4bf0-a3a7-a06088b6467b","createdDate":"2018-12-07T02:46:03.323Z"},{"autopauseThreshold":30,"stagingBucket":"leostaging-rt-test-19b9ee45-597d-49cb-b7f3-8046cfe67d82","clusterImages":[],"scopes":[],"instances":[],"errors":[],"machineConfig":{"numberOfWorkers":0,"masterMachineType":"n1-standard-2","masterDiskSize":200},"creator":"rtitle@broadinstitute.org","googleProject":"anvil-leo-dev","id":1,"labels":{"creator":"rtitle@broadinstitute.org","clusterName":"rt-test","googleProject":"anvil-leo-dev"},"dateAccessed":"2018-12-06T17:29:37.960Z","stopAfterCreation":false,"status":"Stopped","clusterUrl":"https://130.211.229.19/notebooks/anvil-leo-dev/rt-test","clusterName":"rt-test","operationName":"projects/anvil-leo-dev/regions/us-west1/operations/e5b3de74-f5e2-4fde-b043-11220cc6e822","serviceAccountInfo":{},"googleId":"68710807-08c3-44ca-8bd7-8591889781e0","createdDate":"2018-12-
```


### Start a cluster


```
curl -X PUT \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header "Authorization: Bearer `gcloud auth print-access-token`" \
-d '{ \ 
   		"jupyterDockerImage": "us.gcr.io/leo-standalone/leonardo-jupyter:rt-galaxy-dev", \ 
   		"rstudioDockerImage": "us.gcr.io/leo-standalone/leonardo-rstudio:rt-galaxy-dev"}' \ 
'https://leonardo-dev.anvilproject.org/api/cluster/v2/anvil-leo-dev/bioc-test-cluster'
```

Once the cluster is started,

	https://console.cloud.google.com/compute/instances?project=anvil-leo-dev&duration=PT1H

Shows that an instance is active. 


### Get all active once the status is "RUNNING"

https://leonardo-dev.anvilproject.org/#!/cluster/getCluster


### Stop a cluster

Same process as above but tried it out with Swagger.


### Image for Rstudio which needs to be changed

Image for Rstudio
https://github.com/DataBiosphere/leonardo/tree/rt-galaxy-dev/docker/rstudio.

Dockerfile:
https://github.com/DataBiosphere/leonardo/blob/rt-galaxy-dev/docker/rstudio/Dockerfile

This can be replaced with one of the Bioconductor images, or we can
add to it, since it's based on the `rocker` images as well.

##  Questions / TODO

1. Once a cluster is started, how do I access the RStudio instance ?

1. Update with latest Bioconductor version, and get `library(BiocManager)` functional.

1. API for launching a Leonardo instance from R?

1. Configure Rstudio image with correct dependencies from Bioconductor,
   
   - Correct version of R
   
   - BiocManager
   
   - List of packages which are "Bioconductor basic" ?
   
0. What if someone wants to build a custom image, how to make this
   easy? Can "bioconda-multi-container" be leveraged?



## Start a custom image

Start anvil-bioc-image custom image,

```
curl -X PUT 
	--header 'Content-Type: application/json' 
	--header 'Accept: application/json' 
	--header 'Authorization: Bearer ya29.GlxyBkiZ2amlfNlkWn2cdM_vvh0SuzO4b2HCyZOlNWBOZczenfk9lsqnkpCF8qI3amkuLHXVQT60yXn-UtCrXQhMWjWjzm0vi5eCLM2eD7FSW0vQ6zrdkZvFU0l2YA' 
	-d '{ \ 
    		"bioconductorImage": "us.gcr.io/anvil-leo-dev/anvil_bioc_image:test-bioc" \ 
	}' 
 'https://leonardo-dev.anvilproject.org/api/cluster/v2/anvil-leo-dev/anvil-bioc-image-test'
```

Response body,

```
{
  "autopauseThreshold": 30,
  "clusterImages": [
    {
      "tool": "Jupyter",
      "dockerImage": "gcr.io/anvil-leo-dev/leonardo-notebooks:rt-galaxy-dev",
      "timestamp": "2018-12-14T21:05:45.218Z"
    }
  ],
  "scopes": [
    "https://www.googleapis.com/auth/userinfo.email",
    "https://www.googleapis.com/auth/userinfo.profile",
    "https://www.googleapis.com/auth/bigquery",
    "https://www.googleapis.com/auth/source.read_only"
  ],
  "instances": [],
  "errors": [],
  "machineConfig": {
    "numberOfWorkers": 0,
    "masterMachineType": "n1-standard-2",
    "masterDiskSize": 200
  },
  "creator": "nitesh.turaga@gmail.com",
  "googleProject": "anvil-leo-dev",
  "id": 12,
  "labels": {
    "clusterName": "anvil-bioc-image-test",
    "googleProject": "anvil-leo-dev",
    "creator": "nitesh.turaga@gmail.com"
  },
  "dateAccessed": "2018-12-14T21:05:45.218Z",
  "stopAfterCreation": false,
  "status": "Creating",
  "clusterUrl": "https://130.211.229.19/notebooks/anvil-leo-dev/anvil-bioc-image-test",
  "clusterName": "anvil-bioc-image-test",
  "serviceAccountInfo": {},
  "createdDate": "2018-12-14T21:05:45.218Z"
}
```

Run locally with 

```
docker run -p 8001:8001 -e USER=rstudio nitesh1989/anvil_bioc_docker
```
