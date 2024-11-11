---
title: "Remote cmd on Openshift"
date: 2024-11-11T08:28:25+02:00
tags: [openshift, devops] 
---
Do you use the graphical interface of Openshift too much ? (like way too much!) I do and I'm guilty because I know command line is always faster as soon as you got the habit.
So this is it for the introduction! 

Lately, I wanted to connect a pod for debugging propuse. So you can connect using the Openshift's GUI.
Or you can also use the `oc` command line tools.

```
# first use oc login and nagivate to your project
oc login <token>
oc project <project_name>
```

Once you are connected, you need to retrieve the pod ID. You are going to use the pod's name to connect to the pod.

```
oc get pods
oc rsh <pod-name>
sh-5.1$  # session to the pods open
```

In my case, I had a problem with a archive file inside the pod. My only way to access was through the pod. So it's possible to download the file in order to analyse it in your local environment.

```
# oc rsync <pod-name>:/<remote-dir> <local-dir> 
oc rsync <pod-name>:/data/faulty.zip /tmp
```

## Reference
[Official documentation](https://docs.openshift.com/container-platform/4.17/nodes/containers/nodes-containers-copying-files.html)
