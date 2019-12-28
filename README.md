# Canadian Furious Beaver

<center>
<img src="/Assets/img/logo/Logo_v2.png"/>
</center>


## Idea

Furious Beaver is a distributed tool for capturing IRPs sent to any Windows driver. It operates in 2 parts:

1. the "Broker" cobines both a user-land and driver agent that will self-extract and install a driver on the targeted system. Once running it will expose (depending on the compilation options) a remote named pipe (reachable from `\\target.ip.address\pipe\cfb`), or a TCP port listening on TCP/1337. The communication protocol was made to be simple by design (i.e. not secure) allowing any [3rd party tool](https://github.com/hugsy/cfb-cli) to dump the driver IRPs from the same Broker easily (via simple JSON messages).

2. the GUI is a Windows 10 UWP app made in a `ProcMon`-style: it will connect to wherever the broker is, and provide a convienent GUI for manipulating the broker (driver enumeration, hooking and IRP capturing). It also offers facililties for forging/replaying IRPs, auto-fuzzing (i.e. apply specific fuzzing policies on *each* IRP captured), or extract IRP in various formats (raw, as a Python script, as a PowerShell script) for further analysis. The captured data can be saved on disk in an easily parsable format (`*.cfb` = SQLite) for further analysis, and/or reload afterwards in the GUI.

Although the GUI obviously requires a Windows 10 environment, the Broker itself can be deployed on any Windows 7+ host (x86 or x64). The target host must have `testsigning` BCD policy enabled, as the self-extracting driver is not WHQL friendly.

![Canadian Furious Beaver demo](https://i.imgur.com/xMOIIhC.png)


## Concept

_TODO: add schema_


## Build

### GUI

Clone the repository, and build the `CFB.sln` at the project root with Visual Studio (Debug - very verbose - or Release).



### Command line

Clone the repository and in a VS prompt run

```
> msbuild CFB.sln /p:Configuration=Release
```

## Setup

A Windows 7+ VM ([Windows 10 SDK VM](https://developer.microsoft.com/en-us/windows/downloads/virtual-machines) is recommended)

On this VM:
 - Enable kernel debug
 - Enable test signing

Install VS 2015/2017/2019 redist x86 or x64 depending on your VM architecture.

Follow the indications in the `Docs/` folder to improve your setup.


## Why the name?

Because I had no idea for the name of this tool, so it was graciously generated by [a script of mine](https://github.com/hugsy/stuff/tree/master/random-word).


## Status
Project|Build Status
---|---
App|[![Build Status](https://dev.azure.com/blahcat/CFB/_apis/build/status/hugsy.CFB?branchName=master)](https://dev.azure.com/blahcat/CFB/_build/latest?definitionId=1&branchName=master)
Broker|[![Build Status](https://dev.azure.com/blahcat/CFB/_apis/build/status/hugsy.CFB?branchName=master)](https://dev.azure.com/blahcat/CFB/_build/latest?definitionId=1&branchName=master)
