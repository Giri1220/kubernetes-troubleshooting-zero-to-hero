# kubernetes-troubleshooting-zero-to-hero
Learn how to troubleshoot the most common Kubernetes Issues

## Day-01

### ImagePullBackOff

Video Link - https://youtu.be/vGab4v3RWEw

When a kubelet starts creating containers for a Pod using a container runtime, it might be possible the container is in Waiting state because of ImagePullBackOff.

The status ImagePullBackOff means that a container could not start because Kubernetes could not pull a container image for reasons such as 

- Invalid image name or 
- Pulling from a private registry without imagePullSecret. 

The BackOff part indicates that Kubernetes will keep trying to pull the image, with an increasing back-off delay.

Kubernetes raises the delay between each attempt until it reaches a compiled-in limit, which is 300 seconds (5 minutes).


## Day-02

### CrashLoopBackOff

When you see "CrashLoopBackOff," it means that kubelet is trying to run the container, but it keeps failing and crashing. After crashing, Kubernetes tries to restart the container automatically, but if the container keeps failing repeatedly, you end up in a loop of crashes and restarts, thus the term "CrashLoopBackOff." 

This situation indicates that something is wrong with the application or the configuration that needs to be fixed.

## Day-03

### Pods not schedulable

In Kubernetes, the scheduler is responsible for assigning pods to nodes in the cluster based on various criteria. Sometimes, you might encounter situations where pods are not being scheduled as expected. This can happen due to factors such as node constraints, pod requirements, or cluster configurations.

1. Node Selector
2. Node Affinity
3. Taints
4. Tolerations
<img width="529" alt="image" src="https://github.com/user-attachments/assets/8453004c-4337-42a8-a0cf-5a54c75e2e5c" />
<img width="508" alt="image" src="https://github.com/user-attachments/assets/4377afdd-cb5c-4632-a7de-9f35ca01c553" />
<img width="524" alt="image" src="https://github.com/user-attachments/assets/47aa4ba6-7f49-4ddc-88d5-0ace856cf33b" />
<img width="519" alt="image" src="https://github.com/user-attachments/assets/9171a256-0a3c-4fc4-88d3-f172c72be433" />
<img width="521" alt="image" src="https://github.com/user-attachments/assets/c5aca69e-d6fa-40a8-aa1b-5143e578f593" />




