Analysis workflow for a1_case1.apk

Local layout
- work/unzip: raw APK contents (zip-extracted)
- work/apktool: apktool decode output (resources + smali)
- work/jadx: jadx decompile output (Java/Kotlin sources)
- work/reports: notes and findings

Required tools (install if missing)
- apktool
- jadx (or jadx-gui)
- Android build-tools (optional): aapt/aapt2

Typical commands (PowerShell)
1) Decode resources + smali
   apktool d .\a1_case1.apk -o .\work\apktool

2) Decompile to Java/Kotlin
   jadx -d .\work\jadx .\a1_case1.apk
   # or interactive:
   # jadx-gui .\a1_case1.apk

3) Quick triage
   # manifest (binary in APK; readable in apktool output)
   Get-Content .\work\apktool\AndroidManifest.xml

   # list DEX classes
   Get-Content .\work\jadx\resources\AndroidManifest.xml

4) Keep notes
   # put findings in:
   # .\work\reports\notes.md
