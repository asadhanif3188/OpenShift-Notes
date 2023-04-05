# Red Hat OpenShift Notes

## Description
Red Hat OpenShift is an open-source container application platform for developing and hosting enterprise-grade applications. OpenShift is Red Hat's Platform as a Service (PaaS) offering. Once deployed, OpenShift takes care of managing the underlying infrastructure components, thereby enabling the developers to do what they do best: code. 

OpenShift has **four** different flavors:
1. **OpenShift Origin**: Open source application container platform. 
2. **OpenShift Online**: It is Red Hat's publically hosted version of OpenShift Origin, available for application development and hosting purposes. 
3. **OpenShift Dedicated**: It is a managed private cluster on cloud platforms like AWS and Google.  
4. **OpenShift Enterprise**: OpenShift Enterprise is on-premise, private PaaS offering of OpenShift. 

**OpenShift Origin** is based on top of **Docker** containers and the **Kubernetes** cluster manager, with added developer and operational centric **Tools** that enable rapid application development, deployment and lifecycle management. 

**Docker**: Docker in the fundamental technology that powers the development of containerized applications in the form of resuable images. Docker enables us to create an image of our application, with all the required dependencies prepackaged into images that can be instantly deployed in any environment.  

**Kubernetes**: Kubernetes powers deployment and management of these Docker images across large clusters by providing *self-healing* and *autoscaling* features. 

**Tools**: OpenShift builds on these technologies by providing a layer of tools that abstract the underlying Kubernetes and infrastructure management tasks to help developers easily deploy and manage their applications on the Kubernetes-based infrastructure. 
- OpenShift adds support for developer tools such are built-in integration of with source code management (SCM) software lke GitHub. 
- OpenShift has built-in integration with build pipelines that helps developers rapidly and consistently develop, build, test and deploy applications. 
- OpenShift helps manage Docker images of your application by providing a built-in registry. 
- OpenShift comes with support for software-defined network (SDN) that provides networking capabilities out of the box. 
- OpenShift is API-centric and has a rich and well documneted set of APIs that helps us easily integrate OpenShift with our existing infrastructure. 
- OpenShift provides out-of-box support for projects, teams, and users to organiza and manage access to applications.

## Getting Started with OpenShift

### Installation Methods - OpenShift
First of all create RedHat [account](https://www.redhat.com/wapps/ugc/register.html?_flowId=register-flow&_flowExecutionKey=e1s1). 

### Install - Single Node using CRC 
Got to [console.redhat.com/openshift](http://console.redhat.com/openshift), and install code-ready containers (CRC). It is just like Docker Desktop. It just sits locally, it's in task bar, we can open it up. We can use OpenShift locally just on like a dev style cluster, e.g. Docker Desptop, Minikube, etc. Click on create cluster, from the poratl, and choose local option and follow the steps of installation. 

To install the pre-req for code-ready container, run following command. 

`crc setup`

### Install - Multi-Node CLuster 
The portal has two sections, the **developer** and the **administrator**. There is the observability piece of OpenShift wher we can see metrics, alerts, events, etc. 

There is a **Project** section, we can think of a project like a namespace in Kubernetes.  

There is OpenShift Command Line Interface, i.e. known as `oc`, option avaliable to run different commands. 
To see list of Pods, run the command:

`oc get pods`

**Note:** In OpenShift `oc` mimics the `kubectl` of K8s. 
