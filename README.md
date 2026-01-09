# SterlingB2BJenkins

Segue o conteúdo **organizado, estruturado e traduzido para o inglês**, com linguagem **técnica e adequada para proposta de CI/CD**:

---

## Proposed CI/CD Approach for Sterling B2B

### 1. Project Initialization

**a.** Access the Jenkins job and request the creation of a new B2B project.

The pipeline will:

* Create a new Git repository (with a **dev** branch) for the project by checking out a **template project** containing:

  * A basic Business Process (BP)
  * A properties file

* Create two additional Jenkins pipelines:

  * **Project Version Closure**
  * **Code Quality Pre-Validation and Project Deployment** (QA, PROD)

* Import the BP XML into Sterling B2B using:

  ```
  <SI_install>/tp_import/import.sh
  ```

  creating **Resource Tags** for:

  * Business Processes
  * XSLT
  * Service Configurations
  * Other related artifacts

* Create the properties file by invoking the **Sterling B2B Properties REST API**

---

### 2. Development Phase

* The team develops the solution and associates **all components** with the defined **Resource Tag**.

---

### 3. Version Closure and Deployment

#### a. Project Version Closure

* Execute the **Version Closure** pipeline:

  * Extract the **Resource Tag** from Sterling B2B
  * Extract **Properties** from Sterling B2B via REST API
  * Update the Git repository and create a new version tag (e.g., **v1.1**)

#### b. Deployment Pipeline

* Access the Jenkins job that displays:

  * Available Git tags

    * v1.1
    * v1.0
  * Available Sterling B2B target environments

* Select **tag v1.1** and choose the target Sterling B2B environment (QA or PROD)

* The pipeline executes and performs the import into the selected B2B environment using:

  ```
  <SI_install>/tp_import/import.sh
  ```

---

### Benefits

* **Version control** of all B2B artifacts
* Leverages and standardizes the use of **Resource Tags**
* Enables **repeatable and reliable deployments**
* Allows easy redeployment to a new Sterling B2B environment by simply running the pipeline and selecting the desired version tag (e.g., **v1.1**)

---


