---
title: Introduction of IAM
date: 2025-02-25 10:44:25 +0800
categories: [AWS, IAM] 
tags: [iam, cloud]     # TAG names should always be lowercase 
math: true
---

IAM stands for Identity and Access Management—a global service provided by AWS. When we create an AWS account, we automatically start with a root account, even if we are not initially aware of it. However, it is best practice to avoid using the root account for everyday tasks. Instead, we should create individual users and assign them to groups.

Here's how it works:

- **User Creation:** The root account is used only to create new user accounts.
- **Group Assignment:** Users can be added to one or more groups, or they can remain ungrouped.
- **Policies:** We can assign JSON documents, known as policies, to both groups or individual users. These policies define the specific permissions for accessing AWS services.
- **Least Privilege Principle:** In AWS, we apply least privilege principle, that is, we don't give more permission than a user needs.

This approach helps secure our AWS environment by minimizing the risk of accidental or unauthorized actions.

---

> Thank you for reading! Let me know your thoughts and feedback!
{: .prompt-tip }
