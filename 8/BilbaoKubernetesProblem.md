Description: There's a Kubernetes Deployment with an Nginx pod and a Load Balancer declared in the manifest.yml file. The pod is not coming up. Fix it so that you can access the Nginx container through the Load Balancer.

Solution: Describe the problematic pod and notice the node selector label, missing on the node. 


 Warning  FailedScheduling  433d  default-scheduler  0/2 nodes are available: 1 node(s) didn't match Pod's node affinity/selector, 1 node(s) had untolerated taint {node.kubernetes.io/unreachable: }. preemption: 0/2 nodes are available: 2 Preemption is not helpful for scheduling..


label the node: kubectl label node disk=ssd

Warning  FailedScheduling  37s   default-scheduler  0/2 nodes are available: 1 Insufficient memory, 1 node(s) had untolerated taint {node.kubernetes.io/unreachable: }. preemption: 0/2 nodes are available: 1 No preemption victims found for incoming pod, 1 Preemption is not helpful for scheduling..

descrease memory request in manifest.yaml, as the node doesn't have sufficient memory, k apply -f manifest --force


