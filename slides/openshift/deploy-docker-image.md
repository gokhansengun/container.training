# Deploying a Docker Image

- We are going to deploy a web app called `ParksMap` which shows National Parks around the globe.

- Deploying an existing Docker Image is the easiest

.exercise[
  
- On the upper-right of the screen click `Add to Project` button 

- Select `Deploy Image` from the dropdown list to deploy a Docker-formatted image

- Put the name of image `openshiftroadshow/parksmap-katacoda:1.0.0` on the `Image Name` box and press `Enter`

- Following slide has a screenshot

]

---

class: pic

## Deploy Image Dialog

![Catalog](openshift/images/deploy-docker-image.jpg)

---

class: pic

## Your First Pod

![Catalog](openshift/images/first-pod.jpg)

---

## Scaling the Application

.exercise[

- Click the "up" arrow next to the pod to scale the application

  ![Catalog](openshift/images/scale-arrow.png)

- To verify that we changed the number of replicas, click the pods number in the circle next to the arrows. You should see a list with your pods similar to the following

  ![Catalog](openshift/images/scaled-pods.png)
]

---

## Application "Self Healing"

- OpenShift's DeploymentConfigs are constantly monitoring to see that the desired number of Pods is actually running

- Let's "accidentally" kill a pod and see what happens

.exercise[

- Click on one of the pods

- Select `delete` from the `Actions` menu

  ![Catalog](openshift/images/delete-pod.jpg)

]

---

## Application "Self Healing" (Cont)

.exercise[

- You will see that while one pod is `terminating`, another one is created and in `running` state

  ![Catalog](openshift/images/pod-recreated.jpg)

- Before moving forward, go ahead and scale your application down to a single pod

]

---

## Routing HTTP Requests

- Services provide internal abstraction and load balancing **within** an OpenShift environment

- What about external service?

- The way that external clients are able to access applications running in OpenShift is through the OpenShift routing layer. The data object behind that layer is a Route.


---

## Creating a Route

.exercise[

- Creating a Route is pretty straight-forward. 

- Just click the "Create Route" link displayed against the application on the `Overview` page.

  ![Catalog](openshift/images/create-route.jpg)

- Confirm the dialog

- The route will be created and displayed in the overview page

]

---

class: pic

## Created Route

![Catalog](openshift/images/created-route.jpg)

---

class: pic

## 

![Catalog](openshift/images/reach-app-via-route.jpg)
