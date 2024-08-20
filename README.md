<h1 align='center'>Sunshine-AIO</h1>
<p align="center">
<img src="https://github.com/LeGeRyChEeSe/Sunshine-AIO/blob/main/sunshine_aio.jpg?raw=true" align="center" height=205 alt="Sunshine-AIO" />
</p>
<p align="center">
<img src='https://visitor-badge.laobi.icu/badge?page_id=LeGeRyChEeSe.Sunshine-AIO', alt='Visitors'/>
<a href="https://github.com/LeGeRyChEeSe/Sunshine-AIO/stargazers">
<img src="https://img.shields.io/github/stars/LeGeRyChEeSe/Sunshine-AIO" alt="Stars"/>
</a>
<a href="https://github.com/LeGeRyChEeSe/Sunshine-AIO/issues">
<img src="https://img.shields.io/github/issues/LeGeRyChEeSe/Sunshine-AIO" alt="Issues"/>
</a>

<p align="center">
An all-in-one step-by-step guide to setup Sunshine with all needed tools (Windows only at the moment).<br>
(It's initially just a guide, but as it progresses, it will become more like an AIO tool.)<br>
Contributions to this project are welcomed and highly appreciated.

<p align="center">

# What is the purpose of installing all of these tools?

There are several reasons:

- A dedicated display for your game stream will be created by the <b>Virtual Display Driver</b>.

- <b>Sunshine Virtual Monitor</b> allows you to switch between your current desktop (or any number of displays you have) and the Virtual Display.

- It will also <b>automatically</b> adjust the resolution, quality, HDR option, and frame rate of the Virtual Display based on client settings (Moonlight settings).

- To save resources for your gaming experience, it will deactivate your current displays and return to your first setup once the stream is finished.

- <b>Playnite</b> will allow you to gather all your games from any platform (otherwise downloaded games included) in one launcher for your convenience.

- <b>Playnite Watcher</b> will simply allow you to stop the stream when you close your game. (Sunshine does not support it natively)

- It will also allow you to <b>automatically</b> import all your games into Sunshine with a click.

# Table of Contents
- [Sunshine Installation](#sunshine-installation)
- [Virtual Display Driver](#virtual-display-driver)
- [Sunshine Virtual Monitor](#sunshine-virtual-monitor)
- [Playnite Installation](#playnite-installation)
- [Playnite Watcher](#playnite-watcher)
- [Enjoy](#enjoy)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgements](#acknowledgements)
- [Star History](#star-history)

## [Sunshine](https://github.com/LizardByte/Sunshine) Installation

- Download [Sunshine](https://github.com/LizardByte/Sunshine/releases/latest) and install it on your computer.

  For Windows System, download the file `sunshine-windows-installer.exe`.

To stream remotely, make sure to open these ports in your router settings and redirect them to your PC.

- `TCP`:
	- 47984
	- 47989
	- 47990
	- 48010

- `UDP`:
	- 47998
	- 47999
	- 48000


## [Virtual Display Driver](https://github.com/itsmikethetech/Virtual-Display-Driver)

1. Download [Virtual Display Driver (Windows 11 22H2+)](https://github.com/itsmikethetech/Virtual-Display-Driver/releases/latest).

2. Follow [Installation](https://github.com/itsmikethetech/Virtual-Display-Driver#installation) steps then come back here when done.

3. Disable the new display freshly created from Device Manager or open a privileged terminal and run the command `pnputil /disable-device /deviceid root\iddsampledriver`.

> If you plan to use Moonlight from a Phone, make sure to add the correct resolution of <b>all your clients</b> into the <b>`C:\IddSampleDriver\option.txt`</b> file if they don't exist already.


## [Sunshine Virtual Monitor](https://github.com/Cynary/sunshine-virtual-monitor)

- Download [Sunshine Virtual Monitor](https://github.com/Cynary/sunshine-virtual-monitor/archive/refs/heads/main.zip)

	- Extract the `sunshine-virtual-monitor-main.zip` file to a secure location (if the folder is deleted, the tool will not work anymore) and open it.

In the next steps, you can either choose to follow these quick steps or follow the original steps from [sunshine-virtual-monitor](https://github.com/Cynary/sunshine-virtual-monitor#multi-monitor-tool)

1. Download [MultiMonitorTool for Windows 64-bits](https://www.nirsoft.net/utils/multimonitortool-x64.zip) (<b>Recommended</b>) or [MultiMonitorTool for Windows 32-bits](https://www.nirsoft.net/utils/multimonitortool.zip) (Old computers)

	- Extract the `multimonitortool*.zip` file to `multimonitortool-x64` folder and copy this folder to the `sunshine-virtual-monitor-main` folder.

2. Open a Privileged Powershell by entering your Windows key then type `powershell` and enter `Ctrl + Shift + Enter`.

	- Install the module [WindowsDisplayManager](https://github.com/patrick-theprogrammer/WindowsDisplayManager) by typing the command :
		```powershell
		Install-Module -Name WindowsDisplayManager
		```

	- To enable the script execution you need to set your Execution Policy from `Default` to `RemoteSigned`:
		```powershell
		Set-ExecutionPolicy RemoteSigned
		```
		> Source: [PowerShell execution policies](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.4#powershell-execution-policies)

4. Download [vsync-toggle](https://github.com/xanderfrangos/vsync-toggle/releases/latest) and copy the file to the `sunshine-virtual-monitor-main` folder.

### [Sunshine Setup](https://github.com/Cynary/sunshine-virtual-monitor#sunshine-setup)

Follow the steps in [Sunshine Setup](https://github.com/Cynary/sunshine-virtual-monitor#ui).

<b>(Tip)</b> Copy paste these commands on a PowerShell to get the `config.do_cmd` and `config.undo_cmd` commands written for you:

```powershell
$folderName = "sunshine-virtual-monitor-main"
$folderPath = Get-ChildItem -Path "C:\" -Directory -Filter $folderName -Recurse -ErrorAction SilentlyContinue | Select-Object -First 1
$setupPath = $folderPath.FullName + "\setup_sunvdm.ps1"
$teardownPath = $folderPath.FullName + "\teardown_sunvdm.ps1"
$sunvdmLogPath = $folderPath.FullName + "\sunvdm.log"
Write-Host "$(Clear-Host)config.do_cmd:`n`ncmd /C powershell.exe -File $setupPath %SUNSHINE_CLIENT_WIDTH% %SUNSHINE_CLIENT_HEIGHT% %SUNSHINE_CLIENT_FPS% %SUNSHINE_CLIENT_HDR% > $sunvdmLogPath 2>&1`n`n`n`nconfig.undo_cmd:`n`ncmd /C powershell.exe -File $teardownPath >> $sunvdmLogPath 2>&1`n`n`n`n"
 
```

<i>If you relocated the sunshine-virtual-monitor-main to a different disk, change the letter of the <b>$folderPath</b> in line 2 to match the new one. For example <b>"D:\\"</b></i>

## [Playnite](https://playnite.link) Installation

Download [Playnite](https://playnite.link/download/PlayniteInstaller.exe), install it and add all of your games.

## [Playnite Watcher](https://github.com/Nonary/PlayNiteWatcher)

Download [Playnite Watcher](https://github.com/Nonary/PlayNiteWatcher/releases/latest) and extract it to a secure location.

Make sure to follow these steps: [PlayNite Watcher Script Guide](https://github.com/Nonary/PlayNiteWatcher#playnite-watcher-script-guide)

## Enjoy

Configure your Moonlight client to connect to Sunshine and enjoy optimized streaming :)

## Contributing

Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/NewFeature`)
3. Commit your Changes (`git commit -m 'Add some NewFeature'`)
4. Push to the Branch (`git push origin feature/NewFeature`)
5. Open a Pull Request


<i>Thanks to every [contributors](https://github.com/LeGeRyChEeSe/Sunshine-AIO/graphs/contributors) who have contributed in this project.</i>

## License

Distributed under the MIT License. See [LICENSE](https://github.com/LeGeRyChEeSe/Sunshine-AIO/blob/main/LICENSE) for more information.

## Acknowledgements

Shoutout to <b>LizardByte</b> for the Sunshine repo: https://github.com/LizardByte/Sunshine

Shoutout to <b>itsmikethetech</b> for the Virtual Display Driver repo: https://github.com/itsmikethetech/Virtual-Display-Driver

Thanks to <b>Cynary</b> for the Sunshine Virtual Monitor scripts: https://github.com/Cynary/sunshine-virtual-monitor

Shoutout to <b>JosefNemec</b> for Playnite: https://github.com/JosefNemec/Playnite

Shoutout to <b>Nonary</b> for the PlayNiteWatcher script: https://github.com/Nonary/PlayNiteWatcher

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=LeGeRyChEeSe/Sunshine-AIO&type=Date)](https://star-history.com/#LeGeRyChEeSe/Sunshine-AIO&Date)

----

Author/Maintainer: [Garoh](https://github.com/LeGeRyChEeSe/) | Discord: garohrl