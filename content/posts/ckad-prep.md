---
date: '2026-11-25T16:35:10-03:00'
draft: false
title: 'I Booked My CKAD Exam for January. Here’s My Plan'
tags:
- kubernetes
- ckad
- devops
- homelab
- certifications
---
![CKAD exam booking confirmation](/images/booked-ckad.png)

The exam has been purchased with a January 29th test date officially set! Now there’s a deadline that must be met.

I decided to write about this adventure publicly as a way to maintain accountability and to keep a record of what’s learned (along with my Obsidian notes of course).

One may ask, why take the CKAD (Certified Kubernetes Application Developer)?

Well, for a few reasons:

1. Being in tech for over 10 years along with my love of tinkering I have realized a joy in learning new topics such as Kubernetes. It appears there will be many DevOps opportunities for the foreseeable future so this seems like a good way to learn about the topic.
2. My personality is of the type I like to tinker and learn hands-on. Studying for CKAD will allow me to have hands-on exposure by making good use of my 6 node k3s homelab, KodeKloud, and other study material.
3. It’s fun! I view certifications as not necessarily only something to show employers but more so, personally, a guided way to learn the material and have a deeper understanding.

Along with the why, it’s good to elaborate on the exam basics, tips, needed resources and game plan I’ve laid out in order to succeed. In my line of thought, Tasks + Focused Time = Success. Granted you may need more time than others, but generally it’s a good formula to follow. Break things up from your overall goal, into monthly, weekly, and daily attainable goals.

## Exam Basics:

- Online, proctored exam. No multiple choice.
- 2 hours, 15-20 tasks during the test.
- 66% to pass, valid for 2 years, no prerequisites.
- ~$445 includes one retake & 2 sessions on Killer.sh exam simulator.
- Official Kubernetes docs are allowed for use during the exam.

## Exam Tips:

- Skip hard questions and come back later.
- Give medium-hard questions two tries before skipping.
- Practice YAML a lot until the layout and indentation feel natural.
- Personally, with my tech background aiming for 70 hours of study time before exam day. (most people suggest 40-80 hours focused study time)
- Learn short resource names as shown below:

```text
po       Pods
rs       ReplicaSets
deploy   Deployments
svc      Services
ns       Namespaces
netpol   NetworkPolicies
pv       PersistentVolumes
pvc      PersistentVolumeClaims
sa       ServiceAccounts
```

## Exam Resources:

- [KodeKloud](https://kodekloud.com/) - CKAD course & Kubernetes challenges.
- [Killercoda](https://killercoda.com/playgrounds) - Free practice in the browser.
- [labs.iximiuz.com](https://labs.iximiuz.com/) - Deeper knowledge on how Kubernetes works + Answering questions I have in my notes.
- [Killer.sh](https://killer.sh/) - 2 Simulator sessions included with the exam. Saved for the final weeks as recommended.
- KodeKloud’s Discord Group - General questions + They have other communities for Jobs and questions online.

## My Homelab: (Bonus)

- Practice on my own small cluster at home using spare Optiplex 7060s and other small form factor machines

With the game plan laid out I’ll look forward to studying 1-2 hours a day on weekdays, and 3+ on Saturdays for my daily/weekly goals.

## Here’s what I’ve learned so far:

![Summary on K8s Runtime & Pods](/images/kube-summary.png)

### Pods and YAML

Every Kubernetes manifest starts with the same 4 top level fields, which are `apiVersion`, `kind`, `metadata` and `spec` A Pod uses `apiVersion: v1`, while ReplicaSets and Deployments contain `apps/v1`. The `kind` says what you’re creating whether a Pod, Service, ReplicaSet or Deployment. The `metadata` holds its name and labels, and `spec` describes what should actually run. Below is a simple Pod I practiced with which runs a single nginx container.

```YAML
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app: myapp
    type: front-end
spec:
  containers:
    - name: nginx-container
      image: nginx
```

### ReplicaSets, Deployments and namespaces

A `ReplicaSet` keeps a set number of identical Pods running and replaces any that fail. A `Deployment` is on top of that so updates can be rolled out or rolled back when or if something breaks. Namespaces made more sense to me after the analogy was given of last names in different family households. For example, a father calls his son “Mark,” but if he means the Mark in the other household, he says “Mark Smith,” and Kubernetes works the same way with namespaces like `default`, `kube-system`, and `kube-public` which it creates on its own.

```YAML
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: myapp-rs
  labels:
    app: myapp
    type: front-end
spec:
  replicas: 3
  selector:
    matchLabels:
      type: front-end
  template:
    metadata:
      labels:
        app: myapp
        type: front-end
    spec:
      containers:
        - name: nginx-container
          image: nginx
```

Hope this was helpful to others who are thinking of or are preparing for the CKAD currently! Next post could cover containers, my homelab setup, Arch, tmux or dotfiles, plus honest updates on what broke and how I fixed it.

So with all of that mentioned, have you taken the CKAD? If so, reflecting back, what do you wish you would have spent more time on? Let me know!
