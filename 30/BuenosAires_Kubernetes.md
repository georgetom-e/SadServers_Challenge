Description: There are two pods: "logger" and "logshipper" living in the default namespace. Unfortunately, logshipper has an issue (crashlooping) and is forbidden to see what logger is trying to say. Could you help fix Logshipper?


Solution: 

1. Check pod states

sudo kubectl get pods
NAME                          READY   STATUS             RESTARTS       AGE
logger-6f7fb76c9f-4jk77       1/1     Running            1 (12m ago)    369d
logshipper-597f84bf4f-6ssjq   0/1     CrashLoopBackOff   11 (83s ago)   369d

2. Investigate logs 

$ sudo kubectl logs logshipper-597f84bf4f-6ssjq
Exception when calling CoreV1Api->read_namespaced_pod_log: (403)
Reason: Forbidden
HTTP response headers: HTTPHeaderDict({'Audit-Id': '262142f5-d5b2-4f21-9593-3b1d74927492', 'Cache-Control': 'no-cache, private', 'Content-Type': 'application/json', 'X-Content-Type-Options': 'nosniff', 'Date': 'Sun, 13 Apr 2025 16:12:42 GMT', 'Content-Length': '352'})
HTTP response body: {"kind":"Status","apiVersion":"v1","metadata":{},"status":"Failure","message":"pods \"logger-6f7fb76c9f-4jk77\" is forbidden: User \"system:serviceaccount:default:logshipper-sa\" cannot get resource \"pods/log\" in API group \"\" in the namespace \"default\"","reason":"Forbidden","details":{"name":"logger-6f7fb76c9f-4jk77","kind":"pods"},"code":403}


3. Check service account permissions --> cluster role binding --> cluster role 

sudo kubectl describe clusterrolebindings log
Name:         logshipper-cluster-role-binding
Labels:       <none>
Annotations:  <none>
Role:
  Kind:  ClusterRole
  Name:  logshipper-cluster-role
Subjects:
  Kind            Name           Namespace
  ----            ----           ---------
  ServiceAccount  logshipper-sa  default


 sudo kubectl describe clusterrole log
Name:         logshipper-cluster-role
Labels:       <none>
Annotations:  descripton: Think about what verbs you need to add.
PolicyRule:
  Resources   Non-Resource URLs  Resource Names  Verbs
  ---------   -----------------  --------------  -----
  namespaces  []                 []              [list]
  pods/log    []                 []              [list]
  pods        []                 []              [list]

 
4. Notice that the ClusterRole does not permit any verb (get, describe, delete...)
   Add verbs 


sudo kubectl edit clusterrole logshipper  --> add verbs 'get' and 'watch' 
Restart the logshipper pod for the changes to take effect. 

