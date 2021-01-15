---
title: Serverless
---

Cautions:  
 If idle, last instances may be shut down, causing higher latency for next requests.  
 Hard to avoid vendor lock-in.  
 Cloud resources are shared operating system, so potential for vulnerabilities.  
 Monitoring can be complicated. Use logs, instead of paying per monitoring hit.  
API Gateway:  
 An API Proxy \(API endpoint\) with features for authentication, validation, monitoring, routing, etc.  
Provider stacks:  
 AWS: Lambda + API Gateway + Amplify \(BaaS: backend\)  
 Azure: \(Python support appears to have begun to be introduced late 2018\)  
  Azure Functions, Azure App Services, Azure Web Apps  
