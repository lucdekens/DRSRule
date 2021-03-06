## DRSRule PowerShell module

### Changelog
### v2.0.0
Nov 2018
- \[enhancement] Rewrote custom types in native PowerShell Classes. This works around the somewhat cludgey and often problematic DLL-reference-hell. A couple of things to note (**breaking changes!**):
  - This increases the minimum PowerShell version to 5.0 from the previous 4.0 requirement
  - The classes are no longer in a namespace, `DRSRule`, but are "top-level" (due to the way that native PowerShell are implemented). So, class names in the module go from `DRSRule.VMGroup` in pre-v2 to `DRSRule_VMGroup` in this module version, for example
- \[enhancement] [#19](https://github.com/PowerCLIGoodies/DRSRule/issues/19) Added argument completers to parameters, maximizing ease of use! Argument completers are what enable tab-comletion of possible values for parameters
- \[enhancement] [#20](https://github.com/PowerCLIGoodies/DRSRule/issues/20) Added Pester tests for rest of the cmdlets (beyond just the `Get-` cmdlets) -- go-o-o-o, good testing!
- \[enhancement] Restructured repository, putting module components into DRSRule subdirectory, which represents just the items required for the actual module. Rest of items at top-level of repository are supporting/meta items for the module, but not used within the module itself
- \[enhancement] Added `Update-ThisModuleManifest.ps1` for ease of module maintenance for all those module contributors out there
- \[bugfix] Added `-Mandatory` parameter to `New-DrsVMtoVMRule`. Had been in code since v1.0, but commented out (found no reason for it being commented out). Also, `Get-DrsVMToVMRule` was not properly reporting `Mandatory` property on corresponding objects. Corrected that, now

### v1.2.1
Jul 2018
- \[bugfix] fixed [Issue #8](https://github.com/PowerCLIGoodies/DRSRule/issues/8), "Errors not throwing actual errort" -- now throwing the actual errors, for better debugging capabilities (if ever a bug arises again)
- \[bugfix] fixed [Issue #12](https://github.com/PowerCLIGoodies/DRSRule/issues/12), "Error at addition in empty group the VM list" -- can now add a VM to a DrsVMGroup that has no VM members to start, for whatever reason (VM atrophy, maybe?)
- \[bugfix] fixed [Issue #15](https://github.com/PowerCLIGoodies/DRSRule/issues/15), "Metadata file VMware.Vim.dll could not be found" -- now loads items properly for VMware PowerCLI version 10 as well, and on Windows PowerShell and PowerShell Core.

### v1.2.0
25 May 2017
- \[enhancement] per [Issue #2](https://github.com/PowerCLIGoodies/DRSRule/issues/2), added ability to remove one or more target items from a DRS VMGroup or VMHost group via `Set-DrsVMGroup`, `Set-DrsVMHostGroup`
  - added `-AddVM` and `-RemoveVM` parameters to `Set-DrsVMGroup` for easier adds and removes of VMs to/from DRS VM group
  - added `-AddVMHost` and `-RemoveVMHost` parameters to `Set-DrsVMHostGroup` for easier adds and removes of VMHosts to/from DRS VMHost group
  - retained `-VM`/`-VMHost` and `-Append` parameters for these two functions, respectively, to maintain backwards compatibility with older code
- \[errorHandling] added error handling, for now, for problem when the user wants to remove all VMs from a VM group. Further investigation pending
- \[bugfix] fixed [Issue #9](https://github.com/PowerCLIGoodies/DRSRule/issues/9) -- updated code that determines the location of the referenced `VMware.Vim.dll` file based on PowerCLI module version. Tested with PowerCLI 6.3, 6.5rel1, and 6.5.1, and with having installed v6.3 in a non-default location
- \[bugfix] fixed [Issue #10](https://github.com/PowerCLIGoodies/DRSRule/issues/10) -- cmdlet `New-DrsVMtoVMHostRule` previously had `Verbose` and `WhatIf` output that were inaccurate regarding the new rule being a affinity or an anti-affinity rule (was backwards)

### v1.1.0
29 Mar 2017
- \[enhancement] added support for enhancement suggested in [Issue #7](https://github.com/PowerCLIGoodies/DRSRule/issues/7): get a DRS `VMGroup` by the related VM; while at it, added support for:
    - getting a DRS `VMHostGroup` by the related VMHost
    - getting DRS `VMToVMRule` by VM
    - getting DRS `VMToVMHostRule` by VM or VMHost
- \[improvment] added [Pester](https://github.com/pester/Pester) tests for `Get-Drs*` cmdlets

### v1.0.1

30 Jun 2015

- \[bugfix] fixed rare problem with creating new `DRSRule.VMHostGroup` for VMHost group item where `Host` property of corresponding `VMware.Vim.ClusterHostGroup` object is empty and user is using PowerShell v5 (credit [gpduck](https://github.com/gpduck)). This was in `Get-DrsVMHostGroup`. Updated similar situation for functions `Get-DrsVMGroup` and `Get-DrsVMToVMRule`.

### v1.0.0

Initial release, 21 Jan 2015.
