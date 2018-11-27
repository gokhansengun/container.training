# OpenShift Container Platform

- The goal of OpenShift is to provide a great experience for both Developers and System Administrators to develop, deploy, and run containerized applications. 

- Developers should love using OpenShift because it enables them to take advantage of both containerized applications and orchestration without having to the know the details.

- Developers are free to focus on their code instead of spending time writing Dockerfiles and running docker builds.

---

## Composed of ...

- OpenShift is a full platform that incorporates several upstream projects

- Provides additional features and functionality to make those upstream projects easier to consume

- The core of the platform is containers and orchestration

- The platform uses images based upon the docker image format

---

## Access to OpenShift

- CLI (Command Line Interface)

  - The command line tool is called the **oc** tool. This tool is written in the Go programming language and is a single executable that is provided for Windows, macOS, and the Linux Operating Systems.

- Web Console

  - OpenShift also provides a feature rich Web Console that provides a friendly graphical interface for interacting with the platform

- REST API

  - Both the command line tool and the web console actually communicate to OpenShift via the same method, the REST API
  - Having a robust API allows users to create their own scripts and automation depending on their specific requirements
