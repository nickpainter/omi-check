# Purpose

This tool detects vulnerable OMI installations (< 1.6.8.1) in your subscriptions.  By passing the `upgradeOMI` flag it can also upgrade the vulnerable OMI agents.

https://msrc-blog.microsoft.com/2021/09/16/additional-guidance-regarding-omi-vulnerabilities-within-azure-vm-management-extensions/

https://arstechnica.com/information-technology/2021/09/security-researchers-at-wiz-discover-another-major-azure-vulnerability/

https://www.wiz.io/blog/secret-agent-exposes-azure-customers-to-unauthorized-code-execution

The purpose of this repository is to provide only the tools to address vulnerable OMI installations and improve upon the documentation from the https://github.com/microsoft/OMS-Agent-for-Linux repository.

# Using the Script

1. Review the script and update the paths accordingly.  For example, if the project was cloned into `C:\projects` the paths contained within the script would be.
```
$checkScriptPath = "C:\projects\OMS-Agent-for-Linux\tools\OMIcheck\omi_check.sh"
$upgradeScriptPath = "C:\projects\OMS-Agent-for-Linux\tools\OMIcheck\omi_upgrade.sh"
```
2. You can run this script from cloud shell in Azure portal or Windows/Linux/MacOS desktop, make sure to update Az.Compute modules to the latest and or your Powershell version.

```
Install-Module -Name Az.Compute
Update-Module -Confirm Az.Compute
Get-Module -Name Az.Compute
```

3. The tool uses the credentials of the user to list the subscriptions and VMs.  To display the vulnerability status of all Azure Linux VMs that the user has access to run the following command from the directory containing `OMIcheck.ps1`.

```
.\OMIcheck.ps1
```

4. To update all of the vulnerable VMs and patch the vulnerability, run the command with the `-upgradeOMI` flag.
```
.\OMIcheck.ps1 -upgradeOMI
```

# Additional Considerations:
- You can run the script back to back more than once for validations.
- The tool can only detect vulnerable VMs that the user running the script has access to.
- The tool can take quite a long time to run.  You may receive errors if you attempt to run multiple instances of the script or if you try to cancel it and then run it again in a short period of time.