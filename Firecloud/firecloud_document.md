# Firecloud Initial test

This document details the firecloud initial exploration and testing.

## Initial login

Using firecloud, this is the entry point for users
	
	https://portal.firecloud.org/ 

You are allowed to sign in with google using Google O-Auth. The
Firecloud engine works with Google Cloud so, it's important to set up
an account of the Google Cloud engine for this.


## Get free credits 

Firecloud gives free credits to test it's service.

It attaches a billing account , "fccredits-niobium-celadon" to my
google account,
https://console.cloud.google.com/home/dashboard?project=fccredits-niobium-celadon-4059&pli=1


## User documentation

https://software.broadinstitute.org/firecloud/documentation/


## Initial test

1. Create a workspace and attach my billing account to it. 

1. Create a new jupyter notebook on my local machine with an R-kernal,
   and a simple command `sessionInfo()` and upload to the 'Notebooks
   BETA' section, to test out R.
   
1. Attach a cluster to the notebook, 'demo-cluster', which starts up
   in my google cloud account.
   
1. R-configuration which exists right now, (Show notebook)

```
R version 3.4.4 (2018-03-15)
Platform: x86_64-pc-linux-gnu (64-bit)
Running under: Debian GNU/Linux 8 (jessie)

Matrix products: default
BLAS: /usr/lib/libblas/libblas.so.3.0
LAPACK: /usr/lib/lapack/liblapack.so.3.0

locale:
 [1] LC_CTYPE=en_US.UTF-8       LC_NUMERIC=C              
 [3] LC_TIME=en_US.UTF-8        LC_COLLATE=en_US.UTF-8    
 [5] LC_MONETARY=en_US.UTF-8    LC_MESSAGES=en_US.UTF-8   
 [7] LC_PAPER=en_US.UTF-8       LC_NAME=C                 
 [9] LC_ADDRESS=C               LC_TELEPHONE=C            
[11] LC_MEASUREMENT=en_US.UTF-8 LC_IDENTIFICATION=C       

attached base packages:
[1] stats     graphics  grDevices utils     datasets  methods   base     

loaded via a namespace (and not attached):
 [1] compiler_3.4.4       IRdisplay_0.6        pbdZMQ_0.3-3        
 [4] tools_3.4.4          htmltools_0.3.6      base64enc_0.1-3     
 [7] crayon_1.3.4         Rcpp_0.12.19         uuid_0.1-2          
[10] IRkernel_0.8.13.9000 jsonlite_1.5         digest_0.6.18       
[13] repr_0.17            evaluate_0.12       
```



## TODO / Comments / Questions

1. Get a billing project for bioconductor at some point? 

	I imagine this project will take some testing on the google cloud
    and for all invloved through Bioconductor, it might make sense to
    get a billing account?
		
1. The R-kernal can be updated on the instance. Which will give us a
   more up to date version of R and Bioconductor.
   
1. Not sure how to import data, when i try to go to data library, I
   get a dbGaP permission dialogue box.
