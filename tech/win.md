# windows topics

## Windows Subsystem for Linux

- Enabling via GUI - <https://www.wikihow.com/Enable-the-Windows-Subsystem-for-Linux>
  - Settings -> updates and security -> for developers ->
        developer mode
    - Then search for windows features -> the list of options
        includes activating subsystem
    - Windows restarts and bash app should be available in the options
        menu
- Enabling via windows shell
  - <https://docs.microsoft.com/en-us/windows/wsl/install-win10>
  - Enable-WindowsOptionalFeature -Online -FeatureName
        Microsoft-Windows-Subsystem-Linux

**After enabling the windows subsystem for linux you can install ubuntu
environments etc.**
