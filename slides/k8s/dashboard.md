# The Kubernetes dashboard

- Kubernetes resources can also be viewed with a web dashboard

- We are going to deploy that dashboard with *three commands:*

  1) actually *run* the dashboard

  2) bypass SSL for the dashboard

  3) bypass authentication for the dashboard

--

There is an additional step to make the dashboard available from outside (we'll get to that)

--

.footnote[.warning[Yes, this will open our cluster to all kinds of shenanigans. Don't do this at home.]]

---

## 1) Running the dashboard

- We need to create a *deployment* and a *service* for the dashboard

- But also a *secret*, a *service account*, a *role* and a *role binding*

- All these things can be defined in a YAML file and created with `kubectl apply -f`

.exercise[

- Create all the dashboard resources, with the following command:
  ```bash
  kubectl apply -f ~/container.training/k8s/kubernetes-dashboard.yaml
  ```

]

---


## 2) Bypassing SSL for the dashboard

- The Kubernetes dashboard uses HTTPS, but we don't have a certificate

- Recent versions of Chrome (63 and later) and Edge will refuse to connect

  (You won't even get the option to ignore a security warning!)

- We could (and should!) get a certificate, e.g. with [Let's Encrypt](https://letsencrypt.org/)

- ... But for convenience, for this workshop, we'll forward HTTP to HTTPS

.warning[Do not do this at home, or even worse, at work!]

---

## Running the SSL unwrapper

- We are going to run [`socat`](http://www.dest-unreach.org/socat/doc/socat.html), telling it to accept TCP connections and relay them over SSL

- Then we will expose that `socat` instance with a `NodePort` service

- For convenience, these steps are neatly encapsulated into another YAML file

.exercise[

- Apply the convenient YAML file, and defeat SSL protection:
  ```bash
  kubectl apply -f ~/container.training/k8s/socat.yaml
  ```

]

.warning[All our dashboard traffic is now clear-text, including passwords!]

---

## Connecting to the dashboard

.exercise[

- Check which port the dashboard is on:
  ```bash
  kubectl -n kube-system get svc socat
  ```

]

You'll want the `3xxxx` port.


.exercise[

- Connect to http://oneofournodes:3xxxx/

<!-- ```open http://master-0:3xxxx/``` -->

]

The dashboard will then ask you which authentication you want to use.

---

## Dashboard authentication

- We have three authentication options at this point:

  - token (associated with a role that has appropriate permissions)

  - kubeconfig (e.g. using the `~/.kube/config` file from `master-0`)

  - "skip" (use the dashboard "service account")

- Let's use "skip": we get a bunch of warnings and don't see much

---

## 3) Bypass authentication for the dashboard

- The dashboard documentation [explains how to do this](https://github.com/kubernetes/dashboard/wiki/Access-control#admin-privileges)

- We just need to load another YAML file!

.exercise[

- Grant admin privileges to the dashboard so we can see our resources:
  ```bash
  kubectl apply -f ~/container.training/k8s/grant-admin-to-dashboard.yaml
  ```

- Reload the dashboard and enjoy!

]

--

.warning[By the way, we just added a backdoor to our Kubernetes cluster!]

---

## Exposing the dashboard over HTTPS

- We took a shortcut by forwarding HTTP to HTTPS inside the cluster

- Let's expose the dashboard over HTTPS!

- The dashboard is exposed through a `ClusterIP` service (internal traffic only)

- We will change that into a `NodePort` service (accepting outside traffic)

.exercise[

- Edit the service:
  ```
  kubectl edit service kubernetes-dashboard
  ```

]

--

`NotFound`?!? Y U NO WORK?!?

---

## Editing the `kubernetes-dashboard` service

- If we look at the [YAML](https://github.com/jpetazzo/container.training/blob/master/k8s/kubernetes-dashboard.yaml) that we loaded before, we'll get a hint

--

- The dashboard was created in the `kube-system` namespace

--

.exercise[

- Edit the service:
  ```bash
  kubectl -n kube-system edit service kubernetes-dashboard
  ```

- Change type `type:` from `ClusterIP` to `NodePort`, save, and exit

<!--
```wait Please edit the object below```
```keys /ClusterIP```
```keys ^J```
```keys cwNodePort```
```keys ^[ ``` ]
```keys :wq```
```keys ^J```
-->

- Check the port that was assigned with `kubectl -n kube-system get services`

- Connect to https://oneofournodes:3xxxx/ (yes, https)

]

---

## Running the Kubernetes dashboard securely

- The steps that we just showed you are *for educational purposes only!*

- If you do that on your production cluster, people [can and will abuse it](https://blog.redlock.io/cryptojacking-tesla)

- For an in-depth discussion about securing the dashboard,
  <br/>
  check [this excellent post on Heptio's blog](https://blog.heptio.com/on-securing-the-kubernetes-dashboard-16b09b1b7aca)

---

# Security implications of `kubectl apply`

- When we do `kubectl apply -f <URL>`, we create arbitrary resources

- Resources can be evil; imagine a `deployment` that ...

--

  - starts bitcoin miners on the whole cluster

--

  - hides in a non-default namespace

--

  - bind-mounts our nodes' filesystem

--

  - inserts SSH keys in the root account (on the node)

--

  - encrypts our data and ransoms it

--

  - ☠️☠️☠️

---

## `kubectl apply` is the new `curl | sh`

- `curl | sh` is convenient

- It's safe if you use HTTPS URLs from trusted sources

--

- `kubectl apply -f` is convenient

- It's safe if you use HTTPS URLs from trusted sources

- Example: the official setup instructions for most pod networks

--

- It introduces new failure modes (like if you try to apply yaml from a link that's no longer valid)

