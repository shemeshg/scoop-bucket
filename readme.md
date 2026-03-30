# 🚫 Status

This Scoop bucket is **not ready for general use** yet.

Before installing anything from this bucket, you **must remove any existing WinGet installations** of these apps:

```
winget remove shemeshg.MidiRouterClient
winget remove shemeshg.PassSimple
```

If you skip this step, Windows may end up with **broken or duplicated uninstall entries**.

If your uninstall entries are already corrupted, you can usually repair them by:

1. Running the original installer EXE manually  
2. When prompted, choose **Not to uninstall** (this recreates the missing uninstall entry)  
3. Run the installer again  
4. This time choose **Uninstall**  

---

# 📦 Installing Scoop

If Scoop is not installed yet, install it with:

```
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
irm get.scoop.sh | iex
```

---

# 📦 Installing apps from this bucket

> ⚠️ This bucket is experimental. Things may change or break.

## 1. Add the required buckets

```
scoop bucket add extras
scoop bucket add shemeshg https://github.com/shemeshg/scoop-bucket
```

The `extras` bucket is required because these apps depend on `vcredist2022`.

# 2. Install the applications

## 🔐 Pass‑Simple

```
scoop install pass-simple
```

## **MidiRouterClient (GUI)**

```
scoop install midi-router-client
```

## **MidiRouterClient CLI / Windows Service**  
*(`sudo` will prompt for administrator privileges)*

```
scoop install midi-router-client-cli
```

After installation, start the service from an elevated shell:

```
sc start MidiRouterClientCli
```

---

### ⚠️ MidiRouterClient Windows Service Configuration Files

Windows services **do not** use the same AppData folder as your logged‑in user.  
This means the GUI/CLI app and the background service each store their configuration in **different locations**.

#### 🧍 Normal application (GUI or CLI run manually)

Your user‑level configuration is stored here:

```
C:\Users\<YourUser>\AppData\Roaming\shemeshg\MidiRouterClient.ini
```

#### 🖥️ Windows service (running as LocalSystem)

The service runs under the **system account**, which has its own profile.  
Its configuration file is stored here:

```
C:\Windows\System32\config\systemprofile\AppData\Roaming\shemeshg\MidiRouterClient.ini
C:\Windows\System32\config\systemprofile\AppData\Local\midiRouterClient.json
```

This is the file the **service** reads — for example, to determine which port to listen on.

#### 📌 Why this matters

- Editing the **user** INI file does *not* affect the service  
- Editing the **service** INI file does *not* affect your user app  
- If you want the service to use the same settings as your user app, you must manually copy or edit the service’s INI file in the `systemprofile` directory

---





