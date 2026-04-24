# OmniLM
Loud on AliuCord Dc

 (cd "$(git rev-parse --show-toplevel)" && git apply --3way <<'EOF' 
diff --git a/README.md b/README.md
index 5380aacc025aa67a285bb7a785bbfc4de3b08b5b..7508bacefcaacd7c0b88c67bfc31eb5427487374 100644
--- a/README.md
+++ b/README.md
@@ -1,30 +1,143 @@
-# OmniLM
-# Loud Mic For Revenge
+# LoudMic (Aliucord Plugin)
 
-This repository contains a classic Revenge/Vendetta plugin bundle (`index.js` + `manifest.json`) for the **Loud Mic** plugin.
-## Why it may not load
+This repo contains the LoudMic Aliucord plugin source and build config.
 
-If you paste the GitHub repository page URL into Revenge, the plugin will usually fail to install. Revenge expects a **direct `manifest.json` URL** (raw file), not the HTML repo page.
+## Step-by-step order to use this code
 
-Use:
+Follow these **in order**:
 
-- Manifest URL: `https://raw.githubusercontent.com/SonGokuKakarrot/OmniLM/main/manifest.json`
-- Main bundle URL: `https://raw.githubusercontent.com/SonGokuKakarrot/OmniLM/main/index.js`
-What it does:
+1. **Install prerequisites on your PC**
+   - Java 21
+   - Git
+   - Gradle (or generate/use `gradlew`)
 
-- Tries to boost microphone capture by patching `getUserMedia` constraints when that path exists.
-- Tries to patch Discord's local audio recorder options when Revenge exposes that method.
-- Tries to push input-volume and voice-processing preferences if the build still exposes setters for them.
-- Gives you a small settings screen for AGC, suppression, echo cancellation, and requested gain.
+2. **Clone your repository**
+   ```bash
+   git clone https://github.com/<your-username>/OmniALM.git
+   cd OmniALM
+   ```
 
-## Important limits
+3. **Verify plugin source path is correct**
+   - `plugins/LoudMic/src/main/java/com/omnilm/loudmic/LoudMic.java`
 
-- This is a best-effort plugin for Revenge Classic / Vendetta-style plugin loading.
-- On Android, true raw mic amplification often lives in native audio code, so a JavaScript plugin cannot guarantee a louder mic on every build.
-- The bundle is aimed at Discord Android `325.10`, but if that build moved voice handling behind a native-only path, the plugin will fall back gracefully and log which hooks were or were not found.
+4. **Build the plugin zip**
+   - If you have wrapper:
+     ```bash
+     ./gradlew :plugins:LoudMic:make
+     ```
+   - Or with local Gradle:
+     ```bash
+     gradle :plugins:LoudMic:make
+     ```
 
-## How to use it
+5. **Find the generated zip**
+   - Output file:
+     `plugins/LoudMic/build/outputs/LoudMic.zip`
 
-1. In Revenge, go to Plugins and add a new plugin URL.
-2. Paste the raw `manifest.json` URL above.
-3. Enable the plugin and adjust its settings.
+6. **Move zip to your phone**
+   - Copy `LoudMic.zip` into:
+     `/storage/emulated/0/Aliucord/plugins/`
+
+7. **Enable in Aliucord**
+   - Open Aliucord
+   - Go to **Plugins**
+   - Enable **LoudMic**
+
+8. **Test in a voice call**
+   - Join a voice channel/call
+   - Speak and check if your input is louder for others
+
+9. **If it doesn’t get louder on your device**
+   - This is expected on some ROMs/devices because real mic gain can be controlled by native DSP/HAL.
+
+
+
+## Direct clickable install URL for Aliucord
+
+If your GitHub repo is exactly:
+
+`https://github.com/SonGokuKakarrot/OmniALM`
+
+then use one of these direct links in Aliucord:
+
+- `https://raw.githubusercontent.com/SonGokuKakarrot/OmniALM/builds/LoudMic.zip`
+- `https://github.com/SonGokuKakarrot/OmniALM/raw/builds/LoudMic.zip`
+
+Use this in Aliucord PluginDownloader (or open link context menu) to get the install prompt.
+
+> Important: these URLs only work after you publish `LoudMic.zip` to branch `builds`.
+
+
+## 404 error troubleshooting (like your screenshot)
+
+If Aliucord shows `404 Not Found` for a URL like:
+
+`https://cdn.jsdelivr.net/gh/SonGokuKakarrot/OmniALM@builds/LoudMic.zip`
+
+it means one of these is wrong:
+
+1. **`builds` branch missing**
+   - The URL points to branch `builds`, so a branch/tag named `builds` must exist.
+2. **Using `main` URL for a file that exists only on `builds`**
+   - `LoudMic.zip` must be requested from `builds`, not from `main`.
+3. **`LoudMic.zip` not uploaded**
+   - File must exist at the root of `builds` branch exactly as `LoudMic.zip`.
+4. **Case/path mismatch**
+   - `LoudMic.zip` is case-sensitive.
+5. **Wrong repository owner/name in URL**
+   - It must be exactly `SonGokuKakarrot/OmniALM`.
+
+### Correct URL format
+
+If your repo is `OmniALM`, use:
+
+- jsDelivr:
+  `https://cdn.jsdelivr.net/gh/SonGokuKakarrot/OmniALM@builds/LoudMic.zip`
+- GitHub raw:
+  `https://github.com/SonGokuKakarrot/OmniALM/raw/builds/LoudMic.zip`
+- Raw GitHub CDN:
+  `https://raw.githubusercontent.com/SonGokuKakarrot/OmniALM/builds/LoudMic.zip`
+
+Open the URL in a browser first. If browser shows 404, Aliucord will also fail.
+
+### One-time publish commands (so the URL stops 404)
+
+After building `plugins/LoudMic/build/outputs/LoudMic.zip`, run:
+
+```bash
+git checkout --orphan builds
+git rm -rf .
+cp /path/to/OmniALM/plugins/LoudMic/build/outputs/LoudMic.zip .
+git add LoudMic.zip
+git commit -m "Publish LoudMic.zip"
+git push -u origin builds --force
+git checkout main
+```
+
+Then open:
+`https://raw.githubusercontent.com/SonGokuKakarrot/OmniALM/builds/LoudMic.zip`
+
+If this opens/downloads in browser, Aliucord install will work from the same URL.
+
+## What the name `plugins/LoudMic/src/main/java/com/omnilm/loudmic/LoudMic.java` means
+
+It is not a random name — each part has a purpose:
+
+- `plugins/` → folder that contains plugin modules.
+- `LoudMic/` → this plugin module's name.
+- `src/main/java/` → standard Gradle Java source folder.
+- `com/omnilm/loudmic/` → package path for `package com.omnilm.loudmic;`.
+- `LoudMic.java` → Java class file name (must match `public class LoudMic`).
+
+So the full path must match the package + class name exactly, or the plugin will not compile correctly.
+
+## What LoudMic does
+
+When enabled, it:
+
+- Sets `MODE_IN_COMMUNICATION`
+- Turns speakerphone off
+- Unmutes mic
+- Sets `STREAM_VOICE_CALL` volume to max
+
+When disabled, it restores previous values.
 
EOF
)
