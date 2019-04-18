# LTSP Environment

Now we need to install the LTSP environment. This is the framework for the virtual hard disk to sit which will store the ISO image the client computer will receive via the PXE boot process.  

```text
sudo apt-get install ltsp-server-standalone
```

If dnsmasq gives an error while running the above command, the following steps will need to be done to resolve the issue. The error will say port 53 is already in use and dnsmasq can't be started. 



1. **Install `dnsmasq` and dependencies** \(or at least download their packages\) _**before**_ **disabling `systemd-resolved`**:

   ```text
   sudo apt-get install dnsmasq
   ```

2. Disable `systemd-resolved` and verify `dnsmasq` is running:

   ```text
   sudo systemctl stop systemd-resolved
   sudo systemctl disable systemd-resolved

   systemctl status dnsmasq
   ```

3. Season `dnsmasq` to taste. After applying your settings, restart `dnsmasq`:

   ```text
   sudo systemctl stop dnsmasq
   sudo systemctl start dnsmasq
   ```

Now we need to build the LTSP client. This can take some time, usually 10-15 minutes. 

```text
sudo ltsp-build-client
```



