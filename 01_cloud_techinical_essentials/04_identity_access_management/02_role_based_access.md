# Role based access

Each API call in AWS has to be signed, however in practice the app will have multiple tools interacting with one another, these interactions also need to be signed and authenticated. This can be done by setting a IAM role, similar to a user it has a secret key and secret password. However, it does not have a static login credential, the roles are programmatically assigned, and credentials are temporary.