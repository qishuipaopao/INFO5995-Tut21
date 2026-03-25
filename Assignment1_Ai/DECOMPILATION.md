# APK Decompilation Notes

## Tooling

- `jadx 1.5.3` unpacked under `tools/jadx-1.5.3/`
- `apktool 2.12.1` saved as `tools/apktool_2.12.1.jar`

## Rerun Commands

```bash
tools/jadx-1.5.3/bin/jadx -d decompiled/jadx/a1_case1 a1_case1.apk
java -jar tools/apktool_2.12.1.jar d -f -p decompiled/apktool/framework a1_case1.apk -o decompiled/apktool/a1_case1
```

## Output Paths

- `decompiled/jadx/a1_case1/`
- `decompiled/apktool/a1_case1/`

## Verified Findings

- Package name: `com.example.mastg_test0016`
- Launcher activity: `com.example.mastg_test0016.MainActivity`
- Decoded manifest:
  - `decompiled/apktool/a1_case1/AndroidManifest.xml`
  - `decompiled/jadx/a1_case1/resources/AndroidManifest.xml`
- App classes recovered by `jadx`:
  - `decompiled/jadx/a1_case1/sources/com/example/mastg_test0016/MainActivity.java`
  - `decompiled/jadx/a1_case1/sources/com/example/mastg_test0016/Login.java`
  - `decompiled/jadx/a1_case1/sources/com/example/mastg_test0016/Profile.java`

## Auth-Related Classes

- Registration flow is in `MainActivity.java`
  - saves `Username` and `Password` into `credentials.txt`
- Login flow is in `Login.java`
  - reads `credentials.txt`, validates credentials, and creates a session token

## Notes

- `apktool` needed a local framework cache (`-p decompiled/apktool/framework`) because the sandbox blocks writes to the default home-directory cache.
- `jadx` completed with a small number of non-fatal decompilation errors, but the main app package and auth classes were recovered successfully.
