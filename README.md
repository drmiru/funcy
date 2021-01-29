# funcy

## Description

A framework to run Azure Functions Core Tools Host inside a windows docker container.

## Why funcy

Why would you want to run the azure functions hosting environment locally inside a docker container?
Well the answer is pretty simple. - you want to go hybrid - for several possible reasons.

- Serverless apps which need to communicate with on-premises resources
- Process automation, where Azure Automation Hybrid is not desired or missing functionality

## Options to host/run Azure Functions on-premises

- Functions Azure Stack Hub
- AKS on Azure Stack Hub
- Self-hosted Kubernetes

## Running Azure Function in hybrid environments

Azure Function can execute code on-premises environment using "Hybrid Connections". However, this method has several restrictions and limitations.
Running a function using 
- Mount a drive
- Use UDP
- Access TCP-based services that use dynamic ports, such as FTP Passive Mode or Extended Passive Mode.
- Support LDAP, because it can require UDP.
- Support Active Directory, because you cannot domain join an App Service worker
- Run under a dedicated service account

For more information on "Hybrid Connections" see: https://docs.microsoft.com/en-us/azure/app-service/app-service-hybrid-connections

## The idea

While the existing options to run Azure Functions hybrid are pretty cool and straight forward, they do not cover simple scenarios. Maybe you just need to execute parts of your automation solution on-premies and you do not want to use Azure Automation Hybrid Workers because of the very useful native input/output bindings available with Azure Functions. Purchasing Azure Stack Hub "just" for this use case might be to expensive or not accurate at all.
So while discussing with other fellow MVPs I came up with the idea: "Why not just spin up a container instance on-premises which exposes an Azure Functions host runtime"?
The exposed Function App can then be called using techniques like a web application firewall or even Azure API Management self-hosted gateway.

## The solution
After a few iterations I was able to install .Net core framework and the Azure Function Core Tools as part of the container image build process.
