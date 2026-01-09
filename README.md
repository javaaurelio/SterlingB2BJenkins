# SterlingB2BJenkins


---
## Proposed CI/CD Approach for Sterling B2B

### 1. Project Initialization

1 - Access the Jenkins job and request the creation of a new B2B project.

	The pipeline will:

	a) Create a new Git repository (with a dev branch) for the project by checking out a template project containing:

	  A basic Business Process (BP) +  XSLT + Service ( exemplos ) 
		Ex: Name BP format:  <org>_<nameProject>_Basic  RH_Project_XPT_Basic.bp
		Ex: Name XLST format:  <org>_<nameProject>_Basic_XSLT  RH_Project_XPT_Basic_XSLT.xslt
		etc....
	  A properties file
		Ex: <nameProject>.properties,   Project_XPT.properties

	b) Create two additional Jenkins pipelines:
		Project XPT New Release
		Project XPT Deploy (QA, PROD)

	c) Import the BP XML into Sterling B2B using:

	  <SI_install>/tp_import/import.sh
		Creating "Resource Tags" for:

		  Business Processes
		  XSLT
		  Service Configurations
		  Other related artifacts
		  Create the properties file by invoking the Properties REST API

2. Development Phase

	The team develops the solution and associates all components with the defined Resource Tag.


3. New release Project XPT and Deployment

	a) New release Project XPT

		Execute the "New release Project XPT" pipeline:
		  Optional ( Quality ) : 
				perform validation to ensure that an onFault handler with Session Close exists, that no commented code (//) is present, 
				and that there are not too many Java tasks.
		  
				There is a function source BP "sci-get-property" to check whether a property contains a specific key.
				
				and other...
		  
		  Extract the "Resource Tag" from Sterling B2B
		  Extract "Properties" from Sterling B2B via REST API
		  Update the Git repository and create a new version tag (e.g., "v1.1"  version, the v1.0 is basic Project)

	B) Deployment Pipeline

		Access the Jenkins job that displays:

		  Available Git tags

			* v1.1
			* v1.0
		  Available Sterling B2B target environments

			Select "tag v1.1" and choose the target Sterling B2B environment (QA or PROD)

		 The pipeline executes and performs the import into the selected B2B environment using:

		  ```
		  <SI_install>/tp_import/import.sh
		  ```

---

### Benefits

  Version control of all B2B artifacts
  Leverages and standardizes the use of "Resource Tags"
  Enables "repeatable and reliable deployments"
  Allows easy redeployment to a new Sterling B2B environment by simply running the pipeline and 
  selecting the desired version tag.
  Component naming standardization
  
