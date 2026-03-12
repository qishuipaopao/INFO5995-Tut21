System Model (a1_case1.apk)

Key components
- Activities: MainActivity (launcher), Login, Profile.
- Storage: internal file `credentials.txt` (plaintext), SharedPreferences `SessionPrefs` key `sessionToken`.
- UI: registration + login forms; profile screen with WebView and logout button (no WebView logic found).

Data flows and behavior
1) App launch
   - `MainActivity` is the launcher activity.

2) Register path (MainActivity -> Login)
   - User enters username/password in `activity_main.xml` inputs.
   - `MainActivity$1.onClick` reads both fields, writes a plaintext line to internal `credentials.txt` using `openFileOutput(..., MODE_APPEND)`.
   - After saving, it starts `Login` activity.

3) Login path (MainActivity -> Login)
   - `MainActivity$2.onClick` starts `Login` activity directly.

4) Credential check (Login)
   - `Login$1.onClick` reads username/password, calls `checkCredentials`.
   - `checkCredentials` parses `credentials.txt` lines formatted as `Username: <u> Password: <p>` and compares with input.
   - On failure, shows `Toast("Wrong Credential")`.
   - On success: calls `createSession()` then starts `Profile`.

5) Session creation and storage
   - `createSession()` generates a 16-char token via `java.util.Random` (A–Z, a–z, 0–9).
   - Stores the token in `SharedPreferences` `SessionPrefs` under `sessionToken`.

6) Profile / logout
   - `Profile` loads layout with a WebView and logout button.
   - `Profile$1.onClick` calls `clearSession()` which removes `sessionToken` from `SessionPrefs`. No navigation occurs.

System model (text diagram)
User
 -> MainActivity (register/login UI)
    - Register: write credentials.txt (internal storage, plaintext) -> Login
    - Login: Login activity
 -> Login activity
    - check credentials.txt
    - if ok: create session token (Random) -> SharedPreferences -> Profile
    - if fail: toast only
 -> Profile activity
    - logout: clear session token
