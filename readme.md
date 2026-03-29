# 🚫 Status

This Scoop bucket is **NOT READY** yet.

Before using anything from this bucket, you **must** remove the existing WinGet installations:

```
winget remove shemeshg.MidiRouterClient
winget remove shemeshg.PassSimple
```

If you skip this step, Windows may end up with **corrupted uninstall entries**.

If that already happened, you can usually fix it by:

1. Running the original installer EXE manually  
2. When prompted, choose **not** to uninstall (this recreates/repairs the uninstall entry)  
3. Run the installer again  
4. This time choose **Uninstall**, without continuing to the install step  

---

# 📦 Installing Scoop

If you don’t already have Scoop installed, install it with:

```
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
irm get.scoop.sh | iex
```
---

# 📦 Installation with Scoop

> ⚠️ This bucket is experimental. Expect things to break.

## 1. Add the required buckets

```
scoop bucket add extras
scoop bucket add shemeshg https://github.com/shemeshg/scoop-bucket
```

The `extras` bucket is required because these apps depend on `vcredist2022`.

## 2. Install the apps

### MidiRouterClient (GUI)

```
scoop install midi-router-client
```

### MidiRouterClient CLI / Windows Service (requires admin)

```
scoop install midi-router-client-cli
```

After installation, start the service from an elevated shell:

```
sc start MidiRouterClientCli
```

## ⚠️ Windows Service Configuration Files (Important)

Windows services **do not** use the same AppData folder as your logged‑in user.  
This means the application and the background service each store their settings in **different locations**.

### **Normal application (when you run the GUI or CLI manually)**  
Your personal settings are stored in:

```
C:\Users\<YourUser>\AppData\Roaming\shemeshg\MidiRouterClient.ini
```

### **Windows service (running as LocalSystem)**  
The service runs under the **system account**, not your user account.  
Its AppData folder is located here:

```
C:\Windows\System32\config\systemprofile\AppData\Roaming\shemeshg\MidiRouterClient.ini
```

This is the configuration file the **service** uses — for example, the port number it listens on.

### 📌 Why this matters  
- Changing the **user** INI file does *not* affect the service.  
- Changing the **service** INI file does *not* affect your user app.  
- If you want the service to use the same settings as your user app, you must copy or edit the service’s INI file in the systemprofile directory.


### Pass-Simple

```
scoop install pass-simple
```

