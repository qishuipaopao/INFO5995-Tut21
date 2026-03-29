PoC Description

This proof of concept demonstrates a vulnerability in the application’s session token generation.

The application uses java.util.Random to generate session tokens, which is not secure for authentication purposes.

Steps:
1. Launch the application
2. Log in with valid credentials
3. A session token is generated after login
4. Due to the predictability of java.util.Random, the token can potentially be guessed or reproduced

Impact:
An attacker may exploit this vulnerability to hijack user sessions or impersonate legitimate users.

Conclusion:
The use of java.util.Random in security-sensitive contexts introduces a significant risk and should be replaced with a secure random generator such as SecureRandom.
