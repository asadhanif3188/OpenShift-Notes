# Red Hat OpenShift Notes

## Description
Red Hat OpenShift is an open-source container application platform for developing and hosting enterprise-grade applications. OpenShift is Red Hat's Platform as a Service (PaaS) offering. Once deployed, OpenShift takes care of managing the underlying infrastructure components, thereby enabling the developers to do what they do best: code. 

One of the key features of OpenShift is its ability to simplify the process of deploying and scaling applications. With OpenShift, developers can easily create application images and deploy them to the platform, which will automatically manage the container environment, including scaling and load balancing.

OpenShift also provides a number of tools for managing the container environment, including monitoring and logging tools, as well as tools for managing access and security. Additionally, OpenShift supports a wide range of programming languages and frameworks, making it a flexible platform for building and deploying applications.

Some of the other features of OpenShift include:
- Self-service application deployment: Developers can easily deploy applications to OpenShift without needing to go through a centralized IT team.
- Built-in security: OpenShift includes a number of security features, including secure container images and integrated authentication and authorization.
- Multi-cloud support: OpenShift can be deployed on a variety of infrastructure, including on-premises data centers, public clouds, and hybrid clouds.
- Community support: OpenShift has a large and active community of users and contributors, providing a wealth of resources and support for developers.

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

# Openshift Concepts

## Projects and Users
A large Kubernetes cluster can host lots of Pods in hundreds of deployments with various services and endpoints configured. The same large infrastructure can be shared by various teams working on different applications. Sharing the same infrastructure with different teams, however, may not be a good idea as there are no restrictions as to who can access what resources since the entire platform is shared between different teams. Users will also need to coordinate on the names they use for their applications, as this setup does not allow for two users to create a deployment or serice with the same name. 

A project in OpenShift allow users to organize and manage their contents in the OpenShift environment. It helps teams isolate their work from other teams sharing the same infratructure. It allows us to manage access to resources for various users. Projects are built on top of Kubernetes constructs known as namespaces. Using namespaces, K8s automatically prefixes a name of our choice to the objects we create in our namespace, thereby providing some basic grouping functionality for resources. OpenShift projects builds on this functionality to provide complete grouping and isolation of resources that is seamless to users. The user simple creates a project and deploys the application and no longer worry about managing namespaces underneath. All of that is taken care by OpenShift automatically. 

OpenShift comes with built-in user management features. There are three types of users available:
1. Regular User
2. System User
3. Service Accounts

#### 1. Regular User

Regular user are developers and others who interact with OpenShift for developing and deploying applications on a regular basis. They so simple by the name of the users, such as *`developer`*. 

#### 2. System User

System useras are used for interacting with the inftrastructure, such as cluster administrator or a user created for each node in the cluster. OpenShift creates some of these users by default, such as the *`system admin`* and *`system master`* users. 
Note that system users can be identified by a system prefix on the usernames. 

#### 3. Service Accounts
They are created as needed for each project. These user accounts are for enabling communication between various services within our application, for example, an account used by the web server for accessing the database. 

Service accounts have a prefix of system service account on the usernames, e.g. `system:serviceaccount:projj1:db_user`. OpenShift master includes a built-in OAuth server that is responsible for authenticating and authorizating users into the OpenShift cluster. For All in One mode of setup, such as the one we deployed with minishift, the default OAuth configuration is set to an *Allow All* identity provider, that allows any user to log in with any password. If the user doesn't exist with the system, it is automatically created when the user tries to log in for the first time. The password is never varified in this setup. In case of advanced installation, the *Deny All* provider is used, and this denies access for all users. The administrator then needs to manually create and enable new users. This behavior can be changed by modifying the master configuration file, located at `/etc/openshift/master/master-config.yaml`. 

### Creating Users 
Log into the CLI using the `OC login` command. 

`oc login -u system:admin` 

**Note:** `system:admin` is the username. 

To see the list of project, use following command. 

`oc get projects`

To see the list of user, use following command. 

`oc get users`

To assign `cluster-admin` role to `administrator` user, use following command. 

`oc adm policy add-cluster-role-to-user cluster-admin administrator`

