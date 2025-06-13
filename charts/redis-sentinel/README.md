# Redis Sentinel Helm Chart
![redis](https://github.com/user-attachments/assets/193abfcd-1d28-4e42-8d8b-2eb668064e1d)


## Introduction

This guide provides step-by-step instructions to deploy Redis Sentinel on a Kubernetes cluster using Helm. Redis Sentinel provides high availability and monitoring capabilities for Redis. By using Helm, we simplify the deployment process and manage configurations effortlessly.

## Prerequisites

Before you begin, ensure you have the following:
- A Kubernetes cluster (v1.18+)
- Helm (v3.0+)
- The Image Pull Secret of the registry you are using and add the name of the secret in your service account inside values.yaml.

```shell
  serviceAccount:
    imagePullSecrets:
      name1: <name of your Image Pull Secret>
```

## Installation Process

1. **Clone the Helm Repository**

   ```sh
   git clone https://github.com/cyberRuptor/redis-sentinel-helm-chart.git
   ```
   
2. **Make changes inside values.yaml**<br>

   Make the changes if you want to according to your use cases. Like resources, the Password for Redis inside the secret, and the Type of the service whether it is Headless, ClusterIP, or LoadBalancer. You can define your own security contexts also.
   

   -> To change the service type in any of the statefulset Master, Slave, and Sentinel.

   ```shell
    service:
      type: Headless    #set it as LoadBalancer or ClusterIP if you need to create clusterIP service or to use load balancer for external connectivity.
   ```

   just define type as
   Headless for headless service type<br>
   ClusterIP for clusterIP service type<br>
   LoadBalancer for loadBalancer service type<br>

   -> To add the security context in your statefulsets<br>

     1. make the key options true

      ```shell
        securityContext:
           privileged: true  #make it true only when needs root privileges
           allowPrivilegeEscalation: true  #make it true only when needs root privileges
      ```
      
     2. Also uncomment the keys inside the security context from every statefulsets.

      ```shell
      securityContext:
          #privileged: {{ .Values.redisSentinel.securityContext.privileged }}
      ```
3. **Run the command to install helm chart**
   ```sh
       helm install redis-sentinel redis-sentinel-helm-chart
   ```

<br>
If one wants to deploy your Redis Sentinel via statefulset standalone without using Helm Charts then one can follow the below link:-<br>
For documentation, please refer to <br>https://medium.com/@cyberRuptor/deploying-redis-sentinel-as-a-cache-manager-on-k8-ocp-openshift-container-platform-2af64119d911


   
