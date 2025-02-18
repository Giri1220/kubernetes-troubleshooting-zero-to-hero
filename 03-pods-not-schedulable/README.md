In Kubernetes, the scheduler is responsible for assigning pods to nodes in the cluster based on various criteria. Sometimes, you might encounter situations where pods are not being scheduled as expected. This can happen due to factors such as node constraints, pod requirements, or cluster configurations.

1. Node Selector

Node Selector is a simple way to constrain pods to nodes with specific labels. It allows you to specify a set of key-value pairs that must match the node's labels for a pod to be scheduled on that node.
Usage: Include a nodeSelector field in the pod's YAML definition to specify the required labels.
We can add labels to the node by using the command.
""kubectl edit node node_name""
we get below error if label doesn't match![image](https://github.com/user-attachments/assets/b30a181e-c6b6-4355-879b-2965df279439)
![image](https://github.com/user-attachments/assets/12bdbefb-d235-4df7-b759-547b7e6328d8)



```
spec:
    containers:
    - name: my-app
    image: my-image
    nodeSelector:
    disktype: ssd
```

2. Node Affinity

Node Affinity is a more expressive way to specify rules about the placement of pods relative to nodes' labels. It allows you to specify rules that apply only if certain conditions are met.
Usage: Define nodeAffinity rules in the pod's YAML definition, specifying required and preferred node selectors.
![image](https://github.com/user-attachments/assets/dbe22010-e35f-4bf0-b99c-0b34c87c9365)

```
spec:
    containers:
    - name: my-app
    image: my-image
    affinity:
    nodeAffinity:
        requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
            - key: disktype
            operator: In
            values:
            - ssd
```

3. Taints

Taints are applied to nodes to repel certain pods. They allow nodes to refuse pods unless the pods have a matching toleration.
Usage: Use kubectl taint command to apply taints to nodes. Include tolerations field in the pod's YAML definition to tolerate specific taints.

```
kubectl taint nodes node1 disktype=ssd:NoSchedule
```
![image](https://github.com/user-attachments/assets/41e9e2f3-1d39-400a-8611-9a5df4e25c72)
![image](https://github.com/user-attachments/assets/154acc01-d123-4e21-b220-c44cd1cd044f)
![image](https://github.com/user-attachments/assets/675d0b24-35fc-4e11-9719-270cb91cc196)

```
spec:
    containers:
    - name: my-app
    image: my-image
    tolerations:
    - key: disktype
      operator: Equal
      value: ssd
      effect: NoSchedule
```

4. Tolerations

Tolerations are applied to pods and allow them to schedule onto nodes with matching taints. They override the effect of taints.

Usage: Include tolerations field in the pod's YAML definition to specify which taints the pod tolerates.
![image](https://github.com/user-attachments/assets/cad41a03-cf16-49ea-8801-9c5bafa78b3d)
![image](https://github.com/user-attachments/assets/c6c5d8d5-9d68-440c-822a-b60884d816bf)
![image](https://github.com/user-attachments/assets/b027a7cb-b97f-465c-a0fc-c6779d12a3c0)

```
spec:
  containers:
  - name: my-app
    image: my-image
  tolerations:
  - key: disktype
    operator: Equal
    value: ssd
    effect: NoSchedule
```
