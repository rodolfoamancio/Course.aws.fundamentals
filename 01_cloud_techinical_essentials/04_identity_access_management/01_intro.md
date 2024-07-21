# Introduction to AWS identity and access management

You can and should separate the groups which will have access to each part of the application, and each of those could be controlled by login-password access control.

Authentication is different from authorization, the former is associated with the login where the user is verified. The latter is associated with the level of permissions each user has.

IAM handles authentication, while authorization can be handled by IAM policies.