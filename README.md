# General instructions

## How to start Rstudio container with volume

This will start a docker container with a local volume `/tmp/r-libs`
attached to the container.

	docker run -p 8001:8001
		-v /tmp/r-libs:/usr/local/lib/R/host-site-library 
		-e USER=rstudio bioconductor/anvil-rstudio-bioc3.8:latest

	docker run -p 8001:8001
		-v /tmp/r-libs:/usr/local/lib/R/host-site-library 
		-e USER=rstudio bioconductor/anvil-rstudio-bioc3.9:latest

