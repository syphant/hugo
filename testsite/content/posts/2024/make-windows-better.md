+++ 
date = 2024-03-01
title = "Make Windows Better"
+++

Listed in this article are the measures that I take to change the Windows 11 UI to improve visual aesthetics and productivity.

# Restore the old right-click context menu

![](/images/posts/w11-context-menu.png)

You can run the command below in Powershell (or Command Prompt) in order to add a registry key that enables the old right-click context menu from Windows 10:

{{< highlight powershell >}}
reg.exe add "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32" /f /ve
{{< /highlight >}}

# Replace the Start Menu with PowerToys Run

[PowerToys](https://aka.ms/installpowertoys) is an open-source suite of very useful tools in development by Microsoft and freely available on GitHub. One of these tools is PowerToys Run, a launcher for Windows (similar to Spotlight in macOS) that allows you to open files, folders, and apps without ever touching the Start Menu.

![](/images/posts/powertoys-run.jpg)

Preface: To launch an application, I tend to tap the left Windows key `LWin` (which opens the Start Menu), then I type the first few characters of the name of the app, and then I hit `Enter` to launch it.

Problem: I hate the start menu. In PowerToys, you can set a custom keyboard shortcut in launches PowerToys Run to use it for this purpose instead of the Start Menu, but the problem is that it's not possible (at least not natively) to launch it using `LWin` by itself in order to effectively "replace" the Start Menu, it forces you to use a key combination of at least ****two**** keys, e.g. `LWin` + `Space`.

Let's fix that.

After [installing PowerToys](https://aka.ms/installpowertoys) and running PowerToys Run for the first time, modify this section in `$USER\AppData\Local\Microsoft\PowerToys\PowerToys Run\settings.json`:

{{< highlight json >}}
"open_powerlauncher": {
      "win": true,
      "ctrl": false,
      "alt": false,
      "shift": false,
      "code": 134,
      "key": ""
    },
{{< /highlight >}}

This will change the shortcut for PowerToys Run to be `LWin` + `F23`. This is a relatively obscure key and should not interfere with anything else on your system.

So now we need to remap `LWin` pressed by itself to trigger `LWin` + `F23`, without affecting any other key combinations that use `LWin` as a modifier/prefix, for example `LWin` + `L` to lock your current session.

Luckily, [mkmark](https://github.com/mkmark) on GitHub has created a background utility called [LWinRemapper](https://github.com/mkmark/lwin-remapper) that does exactly this. Download the executable from the Releases tab and place it somewhere permanent, like in `C:\Program Files\LWinRemapper`, then create a shortcut to the executable and place this shortcut in your global startup folder `C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup` or your user's startup folder `$USER\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup`.

After starting the executable (or rebooting your machine), `LWin` pressed by itself will now be remapped to `LWin` + `F23`, which now opens PowerToys Run instead of opening the start menu, but does not interfere with other key combinations that utilize the `LWin` key!