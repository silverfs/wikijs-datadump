---
title: Identity and Access Management
description: 
published: true
date: 2023-01-10T19:40:14.664Z
tags: 
editor: markdown
dateCreated: 2023-01-10T19:40:10.276Z
---

# Introduction

Identity and Access management is the process of maintaining network users and managing their access rights to networking entities, that can be files, folders, applications, printers, buildings etc. In other words, it is a method of regulating access to computer or network resources based on the roles of individual users within an network environment/enterprise. 
<br />



I'm fairly familiar with setting up a role-based access system using Windows Server Domain Controllers that use Active Directory (AD) for role-based access control (RBAC). Active Directory is a directory service that is included with the Windows Server operating system, and it is used to manage access to network resources, such as user accounts, computers, and other devices.

It's worth to mention that there is different level of broadness when it comes to permissions in AD, such as permissions at the domain level, organizational unit level, or even at the individual objects level. This allows for a fine-grained access control that can be tailored to the specific needs of an organization.
With that being said, let's create a hypothetical scenario!

<br />

# Scenario

Here, we are to design a role structure and policies for a small, made-up virtual company called CloudyTech. 

<br />
<br />

> **Roles:**

- **CEO**: The CEO has complete control over all resources within the company and can make any changes necessary.
- **CTO**: The CTO (Chief Technology Officer) has complete control over all technical resources and can make any necessary changes to the company's infrastructure.
- **IT Admin**: IT Admins are responsible for maintaining the company's servers and network infrastructure. They can make changes to the servers and network equipment, but they cannot make changes to other resources such as company data. 
- **HR Manager**: HR Managers can access and make changes to the company's personnel files, but cannot access other resources.
- **Sales Manager**: Sales Managers can access the company's customer data, but cannot access other resources.
- **Employee**: Regular employees can access the company's shared resources, such as documents and email, but cannot access other resources such as personnel files or customer data.

<br />
---
<br />


> **Policies:**

- All access to company resources is logged and audited on a regular basis.
- Passwords must be changed every 90 days and must meet a minimum length of 10 characters and complexity requirement.
- All employees must use a company VPN to access company resources remotely.
- All company data must be backed up daily and stored in a secure and segmented location.
- The use of personal devices to access company resources is prohibited, unless they are properly configured and managed through a mobile device management (MDM) system.
- In all cases exists the Privacy Law, which ensures that personal identifiable information remains private to all but the individual in question.


<br />

It's important to note that this is just a simple example, and will require adjustments according to the size, and real-world complexity of the organization. As this is an imaginary company, I don't have clear data to work with. These policies are generally acceptable but are of course subject to change.

The role structure, policies and procedures should also be reviewed and updated regularly, as CloudyTech changes overtime.

<br />
<br />