# Getting Started

- The OpenShift CLI is accessed using the command **oc**.

- The CLI exposes the underlying Kubernetes orchestration system with the enhancements made by OpenShift

---

## First Commands

.exercise[
- Get started by logging in

  ```
  oc login
  ```

- When prompted, enter the following username and password

  ```
  username: developer
  password: developer
  ```

- Check who you actually are. You should be known as `developer` :-)

  ```
  oc whoami
  ```
]

---

## Exploring The Web Console

- While the command line tool is awesome, web console is equally awesome

.exercise[
- Open the web console from `https://cluster-xx.do.gokhansengun.com:8443/console`

- Yes, it has a self-signed certificate and your browsers warns you :-) It is ok, go ahead

- Enter below credentials

  ```
  username: developer
  password: developer
  ```

- You will be landing to the catalog page

]

---

class: pic

## Catalog Page

![Catalog](openshift/images/catalog.jpg)


---

## Create Project

- Let's now create a new project, a playground to try things

.exercise[

- Click `Create Project` button on the upper right corner of the `Catalog Page`

- A pop up will appear, fill the `Name` field as `newproject` and click `Create` button

- Your project is being created now. Click on the link and look around

  - Applications
  - Builds
  - Resources
  - etc

- Do they look familiar to you? :-)

]
