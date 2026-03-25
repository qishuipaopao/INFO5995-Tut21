# Task 3: Find at Least One Vulnerability Related to Randomness and Crypto

For Assignment 1, we focused on one strong and well-validated randomness-related issue rather than broad bug hunting, because the assignment scope is limited to vulnerabilities related to randomness and cryptography.

Using static analysis in JADX, we searched for values treated as tokens or other security-relevant random-looking identifiers. We identified a session-related value, `sessionToken`, in the login and profile logic. The relevant code locations include the `Login` activity, especially the methods `createSession()` and `generateSessionToken()`, and the `Profile` activity, which accesses the same stored session token.

The core issue is that the application generates the session token using `java.util.Random`. Based on our code inspection, `generateSessionToken()` creates a 16-character alphanumeric token by selecting characters from an uppercase/lowercase/digit character set. This token is then stored in `SharedPreferences` under the preference file `SessionPrefs` with the key `sessionToken`, which indicates that it is part of the app’s session-management mechanism rather than a harmless UI-only random value.

We assessed this pattern as security-relevant because the token is created after successful login and is intended to represent authenticated session state. A session token should have strong unpredictability. However, `java.util.Random` is a general-purpose pseudo-random number generator rather than a cryptographically secure random source. Therefore, it is unsuitable for generating security-sensitive values such as authentication or session tokens.

Based on this analysis, we selected **weak session token generation using `java.util.Random`** as our core vulnerability for Assignment 1. This is the strongest randomness-related issue we identified in the APK, and it directly matches the assignment requirement to focus on a validated randomness/cryptography weakness.

As a supplementary observation, the session mechanism also appears to be weakly enforced. From our code inspection, the `Profile` activity initializes the session-related `SharedPreferences`, but we did not observe a clear token-validation step before loading the UI. In addition, the logout logic only removes the token and applies the update, without an obvious redirect back to the login screen or termination of the current activity. We do not use this as the main vulnerability, but it suggests that session validation may be incomplete.
