---

## Fuel the Codecraft

Time is finite. The system endures, but only in bursts of stolen hours. Feature requests gather like stardust—brilliant, infinite, out of reach.
Invoke /coffee to recharge the core and rekindle the forge. Your signal boosts morale. ☕⚡

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/C0C8K83RC)
---

## Invoke: `z`

Harness the echoes of your own movement—`z` learns as you roam.  
With each `cd`, it maps your path, shaping memory into motion.  
A PowerShell-native port of the legendary [*z*](https://github.com/rupa/z) from the Bash realms.

[Install it from the PowerShell Gallery](https://www.powershellgallery.com/packages/z/) and let your history guide your future.

## Origins of the Script

Since the cycle of June 2013, this utility has been forged through hours of iteration—tweaked, refined, and honed to align with PowerShell's rhythm. Born from necessity, it became a tool of mastery, accelerating my traversal through the filesystem—a realm I once wandered daily.

There are no unit tests yet (one day, perhaps), but its true purpose was never perfection. It was time. Time saved. Knowledge gained.

Its mission is simple: bypass the burden of full pathnames and leap to [frecent](https://developer.mozilla.org/en-US/docs/Mozilla/Tech/Places/Frecency_algorithm) locations with speed and grace.
Stable. Swift. Battle-tested.
May it serve you as it has served me.

![ExampleUsage]

## Examples

Once installed, begin the ritual—`cd` into a few directories. Let the system observe. Let the memory form.

`cd foo`

`cd HKLM:\software\Microsoft\Office`

`cd 'C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Temporary ASP.NET Files'`

Based on the examples above, try executing some of these commands.

	z foo				cd to most frecent folder matching foo
	
	z temp				cd to most frecent folder matching `Temporary ASP.NET Files`

	z foo -o r			cd to highest ranked folder matching foo

	z foo -o f			cd to highest frecency folder matching foo
	
	z foo -o t			cd to the most recently accessed folder matching foo
	
	z -l foo			list all dirs matching regex foo
	
	z -l				list all entries

	z office			cd to most frecent folder matching office in drive HKLM (The registry)
	
	z -x				remove the current directory from the datafile
	
	z -clean			delete inaccessible paths from the datafile
	
	z c:\windows			go to c:\windows and log in the datafile (works with any valid path)
	
	z c<TAB>			expand entries in the datafile which match 'c'

OK, enough of the sci-fi poetic style.

## Limitations

Below is a list of features which have not yet been ported from the original `z` bash script...yet.

* Specifying two separate regex's and matching on both, i.e. `z foo bar`
* Does not have the ability to restrict searches to sub-directories of the current directory

## Added sugar

* Tab completion support (will not currently work if you have PowerTab installed)

* Works with registry paths such as `HKLM\Software\....` and NetBIOS paths such as `\\server\share`.

* Executing `pushd` will record the current directory for use with `z`.

## Planned Features

[See the issue listing](https://github.com/vincpa/z/issues)

## PowerShell installation

### The easy way using PowerShellGet

For those with Windows 10, you can issue a `Install-Module z -AllowClobber` command.

For those running the latest version of PowerShell `PowerShellGet\Install-Module z -Scope CurrentUser -Force -AllowClobber`

For those with Windows Vista or 7 who are using PowerShell version 3 or 4, you'll need to install [PackageManagement](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409) first before executing `Install-Module z -AllowClobber`.

See the module listing in the [official PowerShell gallary](https://www.powershellgallery.com/packages/z/)

Once complete, run the command `Import-Module z`. For ease of use I recomend placing this command in your [PowerShell startup profile](https://technet.microsoft.com/en-us/library/bb613488(v=vs.85).aspx). Typically `$env:USERPROFILE\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1`

### The hard way

Download the `z.psm1` file and save it to your PowerShell module directory. The default location for this is `$env:USERPROFILE\Documents\WindowsPowerShell\Modules` (relative to your Documents folder). You can also extract it to another directory listed in your `$env:PSModulePath`. The full installation path should be `$env:USERPROFILE\Documents\WindowsPowerShell\Modules\z\z.psm1`.

Assuming you want `z` to be avilable in every PowerShell session, open your profile script located at `$env:USERPROFILE\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1` and add the following line.

`Import-Module z`

If the file `Microsoft.PowerShell_profile.ps1` does not exist, you can simply create it and it will be executed the next time a PowerShell session starts.

## Running z

Once the module is installed and has been imported in to your session you can start jumping around. Remember, you need to build up the DB of directories first so be sure to `cd` around your file system. You can also use `z` as an alternative to the `cd` command.

[ExampleUsage]: https://raw.githubusercontent.com/vincpa/z/master/example_usage.gif
