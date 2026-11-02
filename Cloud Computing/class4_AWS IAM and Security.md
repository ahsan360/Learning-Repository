# AWS IAM and Security – Beginner's Guide

## 1. What is AWS IAM?

**IAM (Identity and Access Management)** is an AWS service that helps you manage access to your AWS account and resources.

It allows you to control:

- Who can access your AWS account.
- Which AWS services they can access.
- What actions they can perform.
- Which resources they can use.

### Real-world example

Imagine you own a software company with three employees:

- A developer
- A tester
- A system administrator

You do not want everyone to have complete access to your AWS account.

Using IAM, you can:

- Allow the developer to access EC2 and S3.
- Allow the tester to view testing resources.
- Give the administrator broader permissions.

This is why IAM is important.

---

# 2. Protecting the AWS Root User

## What is the Root User?

When you create an AWS account, AWS automatically creates a **root user**.

The root user is the original account owner and has complete access to the AWS account.

Think of it as the owner of a company who has the highest level of authority.

### What can the Root User do?

The root user can:

- Access all AWS services.
- Manage billing information.
- Change account settings.
- Manage IAM users and permissions.
- Close the AWS account.
- Perform certain tasks that require root-user access.

### Why should you protect it?

If someone gets access to your root user credentials, they may gain complete control over your AWS account.

This could result in:
- Unauthorised access to your resources.
- Deletion of important infrastructure.
- Exposure of sensitive information.
- Unexpected AWS charges.

## Root User Security Best Practices

### 1. Enable MFA

MFA stands for **Multi-Factor Authentication**.

It adds another layer of security when you sign in.

For example:

1. Enter your root email address.
2. Enter your password.
3. Provide an additional verification code or approval.

Even if someone knows your password, they may not be able to access your account without the additional authentication factor.

### 2. Use a Strong Password

Create a unique password that you do not use on other websites.

### 3. Never Share Root Credentials

Do not share your root email address and password with developers or other employees.

### 4. Avoid Using Root for Daily Activities

Use an IAM identity with appropriate permissions for everyday AWS tasks.

### 5. Do Not Create Root Access Keys

Avoid creating access keys for the root user. Use IAM roles or other appropriate identities instead.

**Remember:** The root user should be used only for tasks that specifically require it.

---

# 3. IAM Users

## What is an IAM User?

An **IAM user** is an identity that you create inside your AWS account for an individual or workload that needs access to AWS resources.

An IAM user can have:

- A username.
- A password for console access, if configured.
- Access keys for programmatic access, if required.
- Permissions that determine what it can do.

### Real-world example

Suppose you have two developers:

- Developer A: Rahim
- Developer B: Karim

You can create two separate IAM users:

- `rahim`
- `karim`

You can then assign different permissions to each user.

For example:

| IAM User | Permission |
|---|---|
| rahim | Access to EC2 |
| karim | Access to S3 |

Rahim cannot automatically access S3, and Karim cannot automatically access EC2.

Their actual access depends on the permissions they receive.

## How to Create an IAM User

1. Open the AWS Management Console.
2. Search for IAM.
3. Open the IAM service.
4. Select Users.
5. Click Create user.
6. Enter a username.
7. Configure the required access method.
8. Assign permissions.
9. Review and create the user.

### Important Security Point

Avoid creating long-term access keys unless necessary.

For human users, prefer federation or IAM Identity Center where appropriate. For applications running on AWS, prefer IAM roles.

---

# 4. IAM Groups

## What is an IAM Group?

An **IAM group** is a collection of IAM users.

It allows you to manage permissions for multiple users more efficiently.

Instead of assigning the same permissions to every user individually, you can assign permissions to a group.

### Real-world example

Suppose your company has five developers.

You want all developers to have permission to access specific EC2 resources.

Without IAM groups:

- Assign permissions to Developer 1.
- Assign permissions to Developer 2.
- Assign permissions to Developer 3.
- Repeat for every developer.

With IAM groups:

1. Create a group named `Developers`.
2. Attach the required permissions to the group.
3. Add all five developers to that group.

Now the users receive the group's permissions.

## Example of IAM Groups

| Group | Purpose |
|---|---|
| Developers | Access development resources |
| Testers | Access testing resources |
| Administrators | Administrative permissions |
| Support | Access required for support tasks |

### Important Points

- An IAM group can contain multiple IAM users.
- An IAM user can belong to multiple groups.
- Groups cannot contain other groups.
- A group is not an identity that can sign in.
- Permissions assigned to a group apply to its users.

**Remember:** IAM groups make permission management easier when multiple users need similar access.

---

# 5. IAM Policies

## What is an IAM Policy?

An **IAM policy** is a document that defines permissions.

It tells AWS what actions an identity is allowed or denied to perform on particular resources.

For example:

You have a developer who needs to view EC2 instances but should not be allowed to delete them.

You can create a policy that allows viewing EC2 instances without granting deletion permissions.

## Important Elements of an IAM Policy

An IAM policy commonly contains these elements:

| Element | Meaning |
|---|---|
| Version | Policy language version |
| Statement | Contains permission rules |
| Effect | Allow or Deny |
| Action | Operation being allowed or denied |
| Resource | AWS resource affected |
| Condition | Optional conditions for applying the rule |

### Understanding Each Element

**1. Effect**

Defines whether an action is allowed or denied.

Possible values:

- `Allow`
- `Deny`

**2. Action**

Defines which AWS operation the user can perform.

Examples:

- `s3:GetObject`
- `s3:PutObject`
- `ec2:DescribeInstances`

**3. Resource**

Defines which AWS resource the policy applies to.

For example, you can allow access to a particular S3 bucket rather than every bucket in your account.

**4. Condition**

Defines additional requirements for permission.

For example, you can restrict access based on an IP address or other supported conditions.

## Example of an IAM Policy

The following policy allows a user to view EC2 instances.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:DescribeInstances",
      "Resource": "*"
    }
  ]
}
```

### Understanding This Policy

- `Version`: Defines the policy language version.
- `Statement`: Contains the permission rule.
- `Effect`: Allows the action.
- `Action`: Allows viewing EC2 instance information.
- `Resource`: Applies to all resources supported by this action.

Notice that this policy does not grant permission to delete or modify EC2 instances.

## Types of IAM Policies

### 1. AWS Managed Policies

These are policies created and maintained by AWS.

Example:

`AmazonS3ReadOnlyAccess`

This AWS-managed policy provides read-only access to S3.

### 2. Customer Managed Policies

These are policies that you create and manage yourself.

For example, you can create a policy that allows developers to access only a particular S3 bucket.

### 3. Inline Policies

These are policies directly attached to an individual IAM user, group, or role.

They are useful for permissions that are specifically intended for one identity.

### How IAM Policies Work

You can attach identity-based policies to:

- IAM users.
- IAM groups.
- IAM roles.

AWS evaluates applicable policies when an identity attempts to perform an action.

**Important:** An explicit Deny overrides an Allow.

---

# 6. IAM Roles

## What is an IAM Role?

An **IAM role** is an identity that provides a set of permissions to a trusted entity.

Unlike a typical IAM user, a role does not have permanent passwords or access keys.

When an entity assumes a role, AWS provides temporary security credentials.

### Real-world example: EC2 accessing S3

Imagine you have built a web application and deployed it on an EC2 instance.

Your application needs to upload images to an S3 bucket.

One approach would be to store AWS access keys inside your application.

However, this is dangerous because someone could discover those credentials.

A better approach is to use an IAM role.

### How It Works

1. Create an IAM role.
2. Configure EC2 as the trusted service.
3. Attach an IAM policy that allows the required S3 actions.
4. Assign the role to your EC2 instance.
5. Your application obtains temporary credentials automatically.
6. Your application can access the permitted S3 resources.

This approach avoids storing long-term access keys inside your application.

## Two Important Parts of an IAM Role

### 1. Trust Policy

A trust policy defines **who or what is allowed to assume the role**.

For example, it can allow the EC2 service to assume a particular role.

### 2. Permissions Policy

A permissions policy defines **what the role is allowed to do** after it is assumed.

For example, it can allow the role to upload files to a specific S3 bucket.

### Example

Suppose you create a role named:

`EC2-S3-Access-Role`

Its configuration might look like this:

| Configuration | Purpose |
|---|---|
| Trusted entity | EC2 service |
| Permissions | Upload files to a specific S3 bucket |
| Assigned to | EC2 instance |

**Remember:**

- Trust policy = Who can use the role?
- Permissions policy = What can the role do?

---

# 7. AWS IAM Security Best Practices

These are important practices you should follow when managing AWS access.

## 1. Enable MFA

Enable MFA for the root user and other human identities.

## 2. Follow the Principle of Least Privilege

Give users only the permissions they need to perform their jobs.

For example:

If a developer only needs to read files from S3, do not give them full S3 access.

## 3. Avoid Using the Root User

Use an appropriate IAM identity for everyday activities.

## 4. Prefer IAM Roles

Use IAM roles instead of storing long-term access keys in applications.

## 5. Never Expose Access Keys

Never upload AWS access keys to GitHub or include them in publicly accessible source code.

## 6. Review Permissions Regularly

Remove unnecessary permissions and review unused identities.

## 7. Use IAM Groups

Organise users into groups based on their responsibilities.

## 8. Use IAM Access Analyzer

IAM Access Analyzer helps identify potential access risks, such as resources shared with external entities.

## 9. Monitor Account Activity

Use AWS CloudTrail to record and review account activity.

## 10. Use Strong Authentication

Use secure authentication methods and avoid sharing credentials between employees.

---

# 8. Quick Comparison

| IAM Component | Main Purpose |
|---|---|
| Root User | Complete account ownership and access |
| IAM User | Represents an individual or workload |
| IAM Group | Organises users with similar permissions |
| IAM Policy | Defines permissions |
| IAM Role | Provides temporary permissions to trusted entities |

# 9. Important Interview Questions

**Q1. What is AWS IAM?**

AWS IAM is a service that allows you to manage access to AWS resources securely.

**Q2. What is the difference between the root user and an IAM user?**

The root user is the original account owner with full account access, whereas an IAM user is a separately created identity with assigned permissions.

**Q3. Why should we enable MFA?**

MFA adds an additional authentication layer and reduces the risk of unauthorised access.

**Q4. What is the difference between an IAM user and an IAM group?**

An IAM user represents an individual identity, while an IAM group is a collection of users that share permissions.

**Q5. What is an IAM policy?**

An IAM policy is a JSON document that defines which actions are allowed or denied on AWS resources.

**Q6. What is an IAM role?**

An IAM role provides temporary permissions to a trusted entity without requiring permanent credentials.

**Q7. What is the principle of least privilege?**

It means granting only the minimum permissions necessary to perform a particular task.

**Q8. What is the difference between a trust policy and a permissions policy?**

A trust policy defines who can assume a role, while a permissions policy defines what the role can do.

---

# 10. Final Summary

Remember these five concepts:

1. **Root User:** The owner of your AWS account.
2. **IAM User:** An individual identity with assigned permissions.
3. **IAM Group:** A collection of users with shared permissions.
4. **IAM Policy:** A document that defines permissions.
5. **IAM Role:** An identity that provides temporary permissions to trusted entities.

The most important security principle is:

**Never give more permissions than necessary. Follow the Principle of Least Privilege.**

## Official AWS Documentation

- [AWS IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/)
- [IAM Security Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
- [IAM Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html)
- [IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html)
