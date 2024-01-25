# AWS cloud practioner exam practice notes 

### AWS Lightsail and AWS Batch
Amazon Lightsail is designed to be the easiest way to launch and manage a virtual private server with AWS. Lightsail plans include everything you need to
jumpstart your project – a virtual machine, SSD-based storage, data transfer, DNS management, and a static IP address – for a low, predictable price.
AWS Batch enables developers, scientists, and engineers to easily and efficiently run hundreds of thousands of batch computing jobs on AWS. AWS Batch
dynamically provisions the optimal quantity and type of compute resources (e.g., CPU or memory-optimized instances) based on the volume and specific resource
requirements of the batch jobs submitted.

### AWS Well-Architected Framework
- __Operational Excellence__: The ability to support development and run workloads
  effectively, gain insight into their operations, and to continously improve
  supporting processes and procedures to deliver business value.
- __Security__: The security pillar describes how to take advantage of cloud tech to protect
  data, systems, and assets in a way that can improve your security posture.
- __Reliability__: The reliability pillar encompasses the ability of a workload to perform its
  intended function correctly and consistently when its expected to. This
  includes the ability to operate and test the workload through its total
  lifecycle.
- __Performance Efficiency__: The ability to use computing resources efficiently
  to meet systems requirments, and to maintain that efficency as demand
  changes and tech evoles.
- __Cost Optimization__: The ability to run systems to deliver business value at
  the lowest price point.
- __Sustainability__: The ability to continually improve sustainability impacts
  by reducing energy consumption and increasing efficiency across all
  components of a workload by maximizing the benefits from the benefits from
  the provisioned resources and minimizing the total resources required. 


## AWS CAF
- __Business__ The Business perspective helps ensure that your cloud investments accelerate your digital transformation ambitions and business outcomes. Common stakeholders include chief executive officer (CEO), chief financial officer (CFO), chief operations officer (COO), chief information officer (CIO), and chief technology officer (CTO).
- __People__ The People perspective serves as a bridge between technology and business, accelerating the cloud journey to help organizations more rapidly evolve to a culture of continuous growth, learning, and where change becomes business-as-normal, with focus on culture, organizational structure, leadership, and workforce. Common stakeholders include CIO, COO, CTO, cloud director, and cross-functional and enterprise-wide leaders.
- __Governance__ The Governance perspective helps you orchestrate your cloud initiatives while maximizing organizational benefits and minimizing transformation-related risks. Common stakeholders include chief transformation officer, CIO, CTO, CFO, chief data officer (CDO), and chief risk officer (CRO).
- __Platform__ The Platform perspective helps you build an enterprise-grade, scalable, hybrid cloud platform, modernize existing workloads, and implement new cloud-native solutions. Common stakeholders include CTO, technology leaders, architects, and engineers.
- __Security__ The Security perspective helps you achieve the confidentiality, integrity, and availability of your data and cloud workloads. Common stakeholders include chief information security officer (CISO), chief compliance officer (CCO), internal audit leaders, and security architects and engineers.
- __Operations__ The Operations perspective helps ensure that your cloud services are delivered at a level that meets the needs of your business. Common stakeholders include infrastructure and operations leaders, site reliability engineers, and information technology service managers.

## Notes from youtube aws ccp cert course
AWS Macie is a machine learning service that helps detect sensitive data stored
in aws.

AWS GuardDuty is a service that helps monitor aws accounts for potential
security threats.

AWS coginto: Implement secure, frictionless customer identity and access management that scales. This essentially means that it is a service for customers or users of a platform to login etc into some kind of a UI, but this service manages the accounts of those users. 

AWS Storage Gateway provides on-premise application with access to cloud storage
through. This is usually used together with direct connect since customers using
this need a higher level of security.

AWS Transit Gateway enables customers to connect thousands of VPCs. You can
attach your hybrid connectivity (VPN and Direct Connect connections) to a single
Transit Gateway instance, consolidating and controlling your organizations
entire AWS routing confugration in one place.

Amazon Connect is an omnichannel cloud contact center. You can set up a contact center in a few steps, add agents who are located anywhere, and start engaging with your customers.You can create personalized experiences for your customers using omnichannel communications. For example, you can dynamically offer chat and voice contact, based on such factors as customer preference and estimated wait times. Agents, meanwhile, conveniently handle all customers from just one interface. For example, they can chat with customers, and create or respond to tasks as they are routed to them.

AWS Fargate is a serverless compute engine for containes that works with both
ECS and EKS. Fargate makes it easy to focus on building your applications.
Fargate eliminates the need to provision and manage servers, lets you specify
and pay for resources per application, and improves security through application
isolation by design.

AWS Concierge Team are AWS billing and account experts that specoalize in
working with enterprise accounts and are included as part of the enterprise
support plan. 

AWS Local zones, support reducing latency for end users by enabling a limited
number of compute and storage services locally to users. 

S3 different pricing for different storage and access levels need to get a good
grip on it before the exam.

Differences between aws direct connect and aws site to site vpn.

Differences and when to use the different service which is aws kms and aws
secret manager.

13
