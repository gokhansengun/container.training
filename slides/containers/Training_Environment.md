
class: title

# Our training environment

![SSH terminal](images/title-our-training-environment.jpg)

---

## Our training environment

- If you are attending a tutorial or workshop:

  - a VM has been provisioned for each student

- If you are doing or re-doing this course on your own, you can:

  - install Docker locally (as explained in the chapter "Installing Docker")

  - install Docker on e.g. a cloud VM

  - use http://www.play-with-docker.com/ to instantly get a training environment

---

## Our Docker VM

*This section assumes that you are following this course as part of
a tutorial, training or workshop, where each student is given an
individual Docker VM.*

- The VM is created just before the training.

- It will stay up during the whole training.

- It will be destroyed shortly after the training.

- It comes pre-loaded with Docker and some other useful tools.

---

## What *is* Docker?

- "Installing Docker" really means "Installing the Docker Engine and CLI".

- The Docker Engine is a daemon (a service running in the background).

- This daemon manages containers, the same way that an hypervisor manages VMs.

- We interact with the Docker Engine by using the Docker CLI.

- The Docker CLI and the Docker Engine communicate through an API.

- There are many other programs, and many client libraries, to use that API.

---

## Why don't we run Docker locally?

- We are going to download container images and distribution packages.

- This could put a bit of stress on the local WiFi and slow us down.

- Instead, we use a remote VM that has a good connectivity

- In some rare cases, installing Docker locally is challenging:

  - no administrator/root access (computer managed by strict corp IT)

  - 32-bit CPU or OS

  - old OS version (e.g. CentOS 6, OSX pre-Yosemite, Windows 7)

- It's better to spend time learning containers than fiddling with the installer!

---

## Connecting to your Virtual Machine

You need an SSH client.

* On OS X, Linux, and other UNIX systems, just use `ssh`:

```bash
$ ssh <login>@<ip-address>
```

* On Windows, if you don't have an SSH client, you can download:

  * Putty (www.putty.org)

  * Git BASH (https://git-for-windows.github.io/)

  * MobaXterm (http://moabaxterm.mobatek.net)

---

## Checking your Virtual Machine

Once logged in, make sure that you can run a basic Docker command:

.small[
```bash
$ docker version
Client: Docker Engine - Community
 Version:           19.03.11
 API version:       1.40
 Go version:        go1.13.10
 Git commit:        42e35e61f3
 Built:             Mon Jun  1 09:12:22 2020
 OS/Arch:           linux/amd64
 Experimental:      false

Server: Docker Engine - Community
 Engine:
  Version:          19.03.11
  API version:      1.40 (minimum version 1.12)
  Go version:       go1.13.10
  Git commit:       42e35e61f3
  Built:            Mon Jun  1 09:10:54 2020
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.2.13
  GitCommit:        7ad184331fa3e55e52b890ea95e65ba581ae3429
 runc:
  Version:          1.0.0-rc10
  GitCommit:        dc9208a3303feef5b3839f4323d9beb36df0a9dd
```
]

If this doesn't work, raise your hand so that an instructor can assist you!
