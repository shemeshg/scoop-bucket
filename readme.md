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

> ⚠️ Service app folder is: `C:\Windows\System32\config\systemprofile\AppData` unlike 
`c:\users\myUser\AppData`

### Pass-Simple

```
scoop install pass-simple
```

