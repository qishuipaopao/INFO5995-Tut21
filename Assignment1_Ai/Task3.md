Vulnerability:

The core reason is the use of java.util.Random to generate session tokens.

Part of Login.java code is as follows:

private String generateSessionToken() {
    Random random = new Random();
    StringBuilder sb = new StringBuilder(16);
    for (int i = 0; i < 16; i++) {
        sb.append("ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789".charAt(random.nextInt(62)));
    }
    return sb.toString();
}
# This method is used to generate session tokens stored in SharedPreferences.

Random() is insecure because it generates pseudo-random numbers based on a time seed, and the output is predictable. Tokens, on the other hand, are security-sensitive data. The Session Token in this app is used to identify the user and can also be considered a login credential. If an attacker guesses it, they can directly log into someone else's account, creating a vulnerability.

In summary, this software has a security impact. This vulnerability allows attackers to:

1. Predict valid session tokens
2. Inject arbitrary tokens into local storage
3. Completely bypass authentication
4. Impersonate legitimate users