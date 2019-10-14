# Caylent NET Diagram Case

Keeping in mind that the solution should cover the CI / CD ecosystem I divided my solution into two parts. As the proposed case left some details open, in the middle of the explanation I may cite simpler solutions. But because Caylent always delivers the best solution to its customers, I did it the best I could.

- The first diagram discusses the pipeline solution that will deliver a kubernetes object to EKS (AWS).
- The second is 100% focused on cloud infrastructure solution, with services and solution details as a whole.

## CI/CD Solution

My foundation for robust solutions has always been to use Jenkins as the main tool, as I can have the great resilience to develop pipelines for any technology in a centralized and heavily coded way. Thus, I decided to build a scripted pipeline that suited the solution, because I can use varable loads and generate an image for each version of the app. In addition, Jenkins' integration with Kubernetes is excellent, making the job a lot easier.
As such, this jenkins can be easily installed into the EKS cluster via Helm, making each performer a pod leaving the infrastructure resilient and robust.
The entire application solution should be based on Helm, as well as the developer can do manual testing on a test cluster, Helm provides excellent management of Kubernetes objects.

#### Steps
- ** Checkout / Config ** - Checkout the Git repository that may be tied to a web hook to start the pipeline. The config part is to read user-imposed variables in some Git prod or info file;
- ** Build ** - Will build the user's Dockerfile to generate the image and package the helm;
- ** Unit Tests ** - Execution of unit tests of the application to guarantee the quality of the code;
- ** Publish ** - If the application has unit tests with adequate coverage, the pipeline will publish the image and chart to some artifact repository;
- ** Deploy UAT ** - Deploy via helm of a Kuberent object, probably a Pod, in a non-productive environment;
- ** Functional Tests ** - Functional tests to ensure the functioning of the application;
- ** Deploy Prod ** - Deploy via helm of a Kuberent object, probably a Pod, in production after validation of functional tests.

## Infrastructure Solution

The infra solution was developed with resilience and security in mind. The choice of EKS was based on the user's experience to access the application, as the resilience of always leaving the service up and running is always a priority.
The VPC created between the cluster and the databases restricts data access to the application only.
CDN will help to cache user data and sessions.

** Follows diagram below: **

![alt text](./)
