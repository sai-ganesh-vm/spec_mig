## how to use secrets in EKS or GKS for applications to access them in their environment.
<br>
Applications running in EKS often need access to sensitive data such as database credentials, API keys, or tokens. Secrets can be stored in two primary ways:
<br>
<b>Kubernetes Secrets:</b> A built-in Kubernetes object designed to store and manage sensitive information.<br>
<b>
  AWS Secrets Manager:
</b> A fully managed service to securely store and retrieve secrets, with automatic rotation and fine-grained access control.<br>
