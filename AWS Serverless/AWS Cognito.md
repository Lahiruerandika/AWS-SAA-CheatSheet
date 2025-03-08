# AWS Cognito

- Cognito is used for givin users an identity in oder to being able to communicate with a system
- Cognito offers 3 products:
    - **Cognito User Pools:**
        - Sign in functionality for the app users
        - Integrates with API Gateway
    - **Cognito Identity Pool (Federated Identity):**
        - Provides AWS credentials to users which want to access AWS resources directly
        - Integrates with Cognito User Pools as an identity provider
    - **Cognito Sync:**
        - Used for synchronize data from a device to Cognito
        - Deprecated, replaced by AppSync
