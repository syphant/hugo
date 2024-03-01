+++ 
date = 2024-02-24
title = "Make Windows Better"
+++

![](/images/posts/autohotkey-shortcuts.gif)

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

# Disable the Taskbar Entirely

Not only do I hate the start menu, but I also hate the taskbar itself (I expect you are sensing a pattern here by this point).

Since I have adopted the habit of quickly switching tasks with `LWin` + `Tab`, the taskbar does little for me other than being a distraction and taking up precious vertical real estate on my display, so here is how I completely disable and re-enable it on the fly.

[NirCmd](https://www.nirsoft.net/utils/nircmd.html) is a small command-line utility that allows you to do a large variety of useful tasks without any user interface, mainly through writing and deleting values and keys in the registry using command-line options without any distracting user interface. In this scenario, we will be using it for a single purpose, but just be aware that it can do much more.

After [downloading NirCmd](https://www.nirsoft.net/utils/nircmd.zip), extract the archive and place the executable `nircmd.exe` somewhere permanent, like in `C:\Program Files\NirCmd`. In this location alongside `nircmd.exe`, we will create two batch files:

`hidetaskbar.bat`:

{{< highlight bat >}}
"C:\Program Files\NirCmd\nircmd.exe" win trans class Shell_TrayWnd 256
{{< /highlight >}}

`showtaskbar.bat`:

{{< highlight bat >}}
"C:\Program Files\NirCmd\nircmd.exe" win trans class Shell_TrayWnd 255
{{< /highlight >}}

You can now test disabling the taskbar by executing `hidetaskbar.bat`, then re-enable it by executing `showtaskbar.bat`, easy and self-explanatory!

Next, create a shortcut for `hidetaskbar.bat` and then place this shortcut in your global startup folder `C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup` or your user's startup folder `$USER\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup` in order for the taskbar to be disabled on startup.

We can optionally configure hotkeys to trigger these batch files in the next section below.

(If you want to try a fully-customizable taskbar replacement, I recommend [Droptop Four](https://droptopfour.com/). It runs as a Rainmeter skin, and while the free version works perfectly fine, I recommend supporting the Droptop team by [purchasing the full version](https://cariboudjan.gumroad.com/l/droptop) for as little as $6 in order to have access to all features.)

# QuickLaunch Shortcuts with AutoHotkey

This section outlines how I use AutoHotkey to create dwm-like hotkeys for launching the terminal, web browser, etc in Windows.

Before we get started, since we will be configuring the key combination `LWin` + `T` to launch Windows Terminal, we will first need to remap `LWin` + `T` to something else, because by default the `LWin` + `T` shortcut is native to Windows for cycling through applications in the taskbar.

We can do this by utilizing the Keyboard Manager tool in PowerToys (good thing we installed this earlier!)

In Keyboard Manager, you can remap `LWin` + `T` to anything you like. In the screenshot example below, I used `LWin` + `F8`:

![](/images/posts/keyboard-manager.png)

Now with that out of the way, you can write an AHK script to create your own custom key shortcuts to launch applications (and optionally disable/re-enable the taskbar using the NirCmd batch files we created before):

`shortcuts.ahk`

{{< highlight ahk >}}
#NoEnv  ; Recommended for performance and compatibility with future AutoHotkey releases.

; #Warn  ; Enable warnings to assist with detecting common errors.

SendMode Input  ; Recommended for new scripts due to its superior speed and reliability.

SetWorkingDir %A_ScriptDir%  ; Ensures a consistent starting directory.

; Launch Chrome with LWin + Enter
#Enter::
Run, chrome.exe
return

; Hide Taskbar with LWin + Page Down
#PgDn::
Run, C:\Program Files\NirCmd\hidetaskbar.bat
return

; Hide Taskbar with LWin + Page Up
#PgUp::
Run, C:\Program Files\NirCmd\showtaskbar.bat
return

; Launch Windows Terminal with LWin + T
#F8::
Run, C:\Program Files\WindowsApps\Microsoft.WindowsTerminal_1.19.10573.0_x64__8wekyb3d8bbwe\WindowsTerminal.exe
return
{{< /highlight >}}

To have the script run automatically on boot, you can now save this script somewhere permanent, create a shortcut to run the script, and then place the shortcut in your startup folder, the same as we did for other utilities in the previous sections.