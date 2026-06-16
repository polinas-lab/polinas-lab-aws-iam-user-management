<h1><b>Project Journey</b></h1>

<h1><u>AWS IAM User Management Project</u></h1>

<h2>Why I Started This Project</h2>

After successfully hosting a website using Amazon S3 and CloudFront in my first AWS project, I wanted to learn how AWS manages security and access control.

In real-world organizations, multiple employees use the same AWS account. Administrators, developers, security teams, auditors, and interns all require different levels of access. Granting full administrative permissions to every user would create significant security risks.

To understand how AWS secures cloud environments, I decided to explore AWS Identity and Access Management (IAM) and build a practical project focused on user management, permission control, and access validation.

---

<h2>Project Objective</h2>

The goal of this project was to:

* Understand AWS IAM fundamentals
* Create users and groups
* Assign permissions using AWS Managed Policies
* Implement Role-Based Access Control (RBAC)
* Apply the Principle of Least Privilege
* Validate permissions through real-world testing

---

<h2>Step 1: Exploring AWS IAM</h2>

I started by opening the AWS IAM console and exploring its core components:

* Users
* User Groups
* Policies
* Roles

IAM is the service responsible for controlling who can access AWS resources and what actions they are allowed to perform.

By understanding these components first, I could build a secure access management structure rather than assigning permissions randomly.

<b>AWS IAM Dashboard</b>

The screenshot below shows the IAM service where I explored the different identity and access management components.

```markdown
![IAM Dashboard](screenshots/iam-dashboard.png)
```

<h3>What I Learned</h3>

* IAM is the foundation of AWS security.
* Users represent individual identities.
* Groups simplify permission management.
* Policies define permissions.
* Roles provide temporary access when needed.

---

<h2>Step 2: Creating an Administrator Group</h2>

To manage administrative users efficiently, I created a user group named:

**AdminGroup**

I attached the AWS managed policy:

**AdministratorAccess**

Instead of assigning permissions directly to users, AWS recommends assigning permissions to groups. Any user added to the group automatically inherits its permissions.

<b>Administrator Group Creation</b>

The screenshot below shows the AdminGroup being created and configured.

```markdown
![Admin Group Created](screenshots/admin-group-created.png)
```

<h3>Why This Matters</h3>

Managing permissions at the group level:

* Simplifies administration
* Improves scalability
* Reduces configuration errors
* Follows AWS best practices

---

<h2>Step 3: Creating a Developer Group</h2>

Next, I created a group called:

**DeveloperGroup**

and attached the AWS managed policy:

**PowerUserAccess**

This policy allows developers to create and manage most AWS resources while preventing them from managing IAM security settings.

<b>Developer Group Creation</b>

The screenshot below shows the DeveloperGroup configuration.

```markdown
![Developer Group Created](screenshots/developer-group-created.png)
```

<h3>Why This Matters</h3>

Developers often need access to services such as:

* EC2
* S3
* Lambda
* CloudFront

However, they should not be able to create or modify security credentials and IAM users.

This separation helps protect AWS accounts from accidental or unauthorized security changes.

---

<h2>Step 4: Creating a Read-Only Group</h2>

To provide visibility without modification rights, I created:

**ReadOnlyGroup**

and attached the policy:

**ReadOnlyAccess**

Users in this group can view AWS resources but cannot create, modify, or delete them.

<b>ReadOnly Group Creation</b>

The screenshot below shows the ReadOnlyGroup setup.

```markdown
![ReadOnly Group Created](screenshots/readonly-group-created.png)
```

<h3>Use Cases for Read-Only Access</h3>

This permission level is useful for:

* Auditors
* Managers
* Security Reviewers
* Stakeholders

These users can monitor resources without risking accidental changes.

---

<h2>Step 5: Creating IAM Users</h2>

After creating the groups, I created three IAM users:

* admin-user
* developer-user
* readonly-user

Each user was assigned to its respective group.

<b>Administrator User Creation</b>

```markdown
![Admin User Created](screenshots/admin-user-created.png)
```

<b>Developer User Creation</b>

```markdown
![Developer User Created](screenshots/developer-user-created.png)
```

<b>ReadOnly User Creation</b>

```markdown
![ReadOnly User Created](screenshots/readonly-user-created.png)
```

<h3>What I Learned</h3>

Users inherit permissions automatically from the groups they belong to.

This makes permission management easier because changes only need to be made once at the group level.

---

<h2>Step 6: Testing User Access</h2>

Creating permissions is not enough. Security configurations should always be validated.

To verify that permissions were working correctly, I signed in using each IAM user account and tested different actions.

---

<h3>Testing ReadOnly User Permissions</h3>

I logged in as the ReadOnly user and attempted to create an Amazon S3 bucket.

<b>Result:</b>

❌ Access Denied

This confirmed that the user could view resources but could not make changes.

```markdown
![ReadOnly Access Denied](screenshots/readonly-access-denied.png)
```

---

<h3>Testing Developer User Permissions</h3>

I logged in as the Developer user and attempted to create an S3 bucket.

<b>Result:</b>

✅ Success

This confirmed that the PowerUserAccess policy allowed resource creation.

```markdown
![Developer Bucket Created](screenshots/developer-bucket-created.png)
```

Next, I attempted to create a new IAM user.

<b>Result:</b>

❌ Access Denied

This confirmed that developers could not manage IAM resources.

```markdown
![Developer IAM Not Created](screenshots/developer-iam-notcreated.png)
```

---

<h3>Testing Administrator User Permissions</h3>

Finally, I logged in as the Administrator user and attempted to create a new IAM user.

<b>Result:</b>

✅ Success

This verified that AdministratorAccess provided full AWS permissions.

```markdown
![Admin IAM User Created](screenshots/admin-user-iamcreated.png)
```

---

<h2>Permission Validation Summary</h2>

| User           | Create S3 Bucket | Create IAM User |
| -------------- | ---------------- | --------------- |
| ReadOnly User  | ❌ No             | ❌ No            |
| Developer User | ✅ Yes            | ❌ No            |
| Admin User     | ✅ Yes            | ✅ Yes           |

This testing phase confirmed that each group was receiving the intended permissions.

---

<h2>Key AWS Security Concept Learned</h2>

<h3>Principle of Least Privilege</h3>

The most important security concept I learned during this project was the **Principle of Least Privilege (PoLP)**.

This principle states:

> A user should receive only the permissions required to perform their job and nothing more.

By restricting unnecessary permissions, organizations can significantly reduce security risks.

<h3>Benefits</h3>

* Reduces attack surface
* Prevents accidental changes
* Improves security posture
* Supports compliance requirements
* Protects sensitive AWS resources

This principle is considered one of the most important cloud security best practices.

---

<h2>Project Architecture</h2>

```text
AWS Account
│
├── AdminGroup
│     └── AdministratorAccess
│           └── admin-user
│
├── DeveloperGroup
│     └── PowerUserAccess
│           └── developer-user
│
└── ReadOnlyGroup
      └── ReadOnlyAccess
            └── readonly-user
```

---

<h2>What I Learned</h2>

Through this project, I gained practical experience with:

* AWS Identity and Access Management (IAM)
* IAM Users
* IAM User Groups
* IAM Policies
* AWS Managed Policies
* Permission Inheritance
* Access Control
* Security Best Practices
* Principle of Least Privilege
* Role-Based Access Control (RBAC)
* Permission Validation Testing

---

<h2>Project Outcome</h2>

At the end of this project, I successfully built a secure IAM environment consisting of:

* Multiple IAM Groups
* Different permission levels
* Managed AWS policies
* User-to-group assignments
* Permission validation testing

This project gave me hands-on experience with one of the most important areas of cloud computing: security and access management.

---

<h2>Conclusion</h2>

While my first AWS project focused on hosting a website using Amazon S3 and CloudFront, this project focused on securing AWS environments through proper identity and access management.

By creating users, groups, and permission boundaries, I gained a practical understanding of how organizations manage access across teams while maintaining security. I also learned the importance of validating permissions and applying the Principle of Least Privilege.

This project strengthened my understanding of AWS security fundamentals and serves as an important milestone in my cloud computing journey as I continue exploring services such as EC2, VPC, Route 53, Lambda, DynamoDB, and advanced IAM concepts.
