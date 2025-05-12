---

Maintaining software with limited hours in the day can be a challenge and I've had to turn down many feature requests over the years. Boost my motivation and buy me a coffee :-D

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/C0C8K83RC)
---

# z

z lets you quickly navigate the file system in PowerShell based on your `cd` command history. It's a port of [the z bash shell script.](README). Install it from the [official PowerShell gallery](https://www.powershellgallery.com/packages/z/).

## Goals

Since June 2013 I have poured many hours building, tweaking and refining this script to work efficiently with PowerShell. It saves me a great deal of time navigating the file system, which is where I spent a lot of my time and has given me a great oportunity to learn PowerShell at a deeper level. There are no unit tests yet (I'll get around to it one day), but I wrote the script to save me time and learn PowerShell.

The goal is quite simple, save time typing out the fully qualified path names of [frecently](https://developer.mozilla.org/en-US/docs/Mozilla/Tech/Places/Frecency_algorithm) accessed directories. It's stable and fast. Enjoy!

![ExampleUsage]

## Examples

Once installed, `cd` in to a few directories

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
