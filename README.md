#Custom IAM Policies for Developer Access

EXPERIENCE:

My organization needed to grant different levels of access to a group of developers working on a critical application. However, standard AWS managed policies don't exactly fit my requirements. I crafted custom IAM policies tailored to the developers' specific tasks and resource requirements. This project will involve specifying fine-grained permissions, using conditions to control access based on IP ranges and resource tags, and testing the policies extensively to ensure they grant the right level of access while maintaining security.
Define Requirements

- Before crafting custom IAM policies, you need to clearly define the requirements of the developers' access. What AWS services and resources do they need access to, and what actions should they be able to perform? Are there any specific IP ranges they should access from? Document these requirements.

 -  Developers' Roles and Responsibilities: The organization had developers with different roles and responsibilities within the critical application. These roles included front-end developers, back-end developers, and database administrators.

  - Fine-Grained Permissions: Custom IAM policies were crafted for each role. For example, front-end developers were given permissions to access specific S3 buckets containing web assets, while back-end developers were granted access to EC2 instances hosting the application's server.

  - IP Range Controls: To enhance security, IP range controls were implemented. Access to certain resources was restricted to specific IP ranges or office locations to prevent unauthorized access from outside the organization's network.

- Resource Tags: Resource tagging was used extensively. AWS resources were tagged based on their purpose and sensitivity level. IAM policies were configured to grant access to resources with specific tags, allowing developers to work only with resources relevant to their tasks.

  - Extensive Testing: Before deploying the custom IAM policies, extensive testing was conducted. This involved creating sandbox environments, simulating various developer scenarios, and verifying that the policies granted access as intended. Testing ensured that there were no over-permissive policies and that developers couldn't escalate their privileges.

  - Access Revocation: IAM policies were designed with the principle of least privilege. Access was provisioned based on what was needed for developers to perform their roles effectively. Additionally, there were mechanisms in place to promptly revoke access when a developer's role or project changed.

  - Regular Review: The organization committed to periodic reviews of IAM policies to align them with changing requirements and ensure ongoing security and compliance.
 
STEPS
CREATE AWS RESOURCES TO EMULATE AN ENVIRONMENT

For the sake of simplicity, simulate a workforce environment containing S3 buckets and EC2 instances. 


![image](https://github.com/lucien95/IAM-POLICIES-4-DEV/assets/120702469/ccd4b136-aacc-4e0d-b067-3b39ee9ee6d1)


- Create 2 EC2 instances for a production environment with the following parameters

    Instance 1:
        name : webServerProd
        tags:
            environment : production
            application : webserver

    Instance 2:
        name : dbServerProd
        tags:
            environment : production
            application : databaseserver

  - Create 2 EC2 instances for a dev environment with the following parameters

    Instance 1:
        name : webServerDev
        tags:
            environment : development
            application : webserver

    Instance 2:
        name : dbServerProd
        tags:
            environment : development
            application : databaseserver

  - Create an S3 bucket for a production environment with the following parameters

    Bucket 1:
        name : thisvaluehastobegloballyuniqueprod
        tags:
            environment : production
            application : webserver
            security : public

  - Create an S3 buckets for a production environment with the following parameters

    Bucket 1:
        name : thisvaluehastobegloballyuniquedev
        tags:
            environment : development
            application : webserver
            security : confidential

- Create Users and Groups in the IAM Portal

    Create user groups
        name : Developers-Prod
        name : Developers-Dev

    Create users

- Create group policy

This policy grants full access to EC2 instances with the specified tags while still restricting access to only the allowed IP addresses. Adjust the IP addresses as needed for your use case. Checkout the file on this repository called, "DeveloperAccess.json"






