# Source-to-Image (S2I)

- In this lab, we are going to deploy a backend service for the ParksMap application

- In a previous lab, we learned how to deploy an application (the ParksMap front end) from a pre-existing Docker-formatted image.

- Here we will learn how to deploy an application direct from source code hosted in a remote Git repository

- Documentation for S2I describes itself in the following way:

  - Source-to-image (S2I) is a tool for building reproducible Docker images.
  - S2I produces ready-to-run images by injecting source code into a Docker image and assembling a new Docker image which incorporates the builder image and built source.
  - The result is then ready to use with docker run. S2I supports incremental builds which re-use previously downloaded dependencies, previously built artifacts, etc.

---

## Deploying the Application Code

.exercise[

- The backend service that you will be deploying in this lab is called `nationalparks-katacoda`

- The source code is available at https://github.com/openshift-roadshow/nationalparks-katacoda 

- Use `Add to Project` button on the `Overview Page` again.

- This time, rather than using `Deploy Image` we will use `Browse Catalog`

]

---

## Deploying the Application Code (cont - 1)

.exercise[

- Select `Python` from the list of supported languages

  ![Catalog](openshift/images/catalog-images.jpg)

- Ensure that the Python version is `3.5` and click on Select

- Fill the form in the popup like it is shown in the following slide

]

---

class: pic

## Deploying the Application Code (cont - 2)

  ![Catalog](openshift/images/nationalparks-katacoda.jpg)

---

## Deploying the Application Code (cont - 3)

.exercise[

- Go to the `Overview` page and observe the image we just dispatched is being built

  ![Catalog](openshift/images/nationalparks-image-build.jpg)

- You should now see that the image has been built and run

- So with the backend we just deployed the original web app should now the National Parks

]

---

class: pic

## Deploying the Application Code (cont - 4)

  ![Catalog](openshift/images/nationalparks-katacoda-w-backend.jpg)