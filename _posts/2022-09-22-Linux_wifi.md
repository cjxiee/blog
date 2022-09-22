### Wifi logo is not found in ubuntu 20.04

#About dual-boot with Windows and "fast-boot" enabled
If you have a dual-boot machine with a recent version of Windows and start seeing problems during initialization of the WiFi device when booting Linux, the problem could be due to the “fast startup” feature on Windows.

With this feature enabled, Windows don't really shut down the entire system, but leaves things partially running so you can start the machine faster again. Try to disable this option, on Windows 10 it should be in “Control Panel→Hardware and Sound→Power Options→System Settings”. Select “Chooose what the power buttons do” to access the System Settings from the Power Options. Then disable the “Fast Startup” option in “Shutdown Settings”. This will cause Windows to fully shutdown and may solve the issue.
