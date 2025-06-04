# Powershell-for-Power-Apps

PowerShell support for managing Power Apps is a bit less mature than for other M365 services like Exchange or SharePoint, but it does exist through the Power Apps Administration module and Microsoft.PowerPlatform.Cds.Client for Dataverse-specific operations.

You need to be Power Platform Admin or Global Admin to run most tenant-wide commands.

## Required Module Installation
```
Install-Module -Name Microsoft.PowerApps.Administration.PowerShell
Install-Module -Name Microsoft.PowerApps.PowerShell -AllowClobber
```
You’ll usually use both modules:

##  List All Power Apps in the Tenant
```
Add-PowerAppsAccount
Get-AdminPowerApp | Select DisplayName, AppName, CreatedTime, EnvironmentName, Owner
```

## List Power Apps by Environment
```
Get-AdminPowerApp -EnvironmentName "Default-<GUID>" | Format-Table DisplayName, AppName, CreatedBy
```

## Remove a Power App
```
$appid = "<AppId>"
$env = "<EnvironmentId>"
Remove-AdminPowerApp -AppName $appid -EnvironmentName $env
```

## Export All Power Apps Metadata to CSV
```
Get-AdminPowerApp | Select DisplayName, AppName, EnvironmentName, CreatedTime, LastModifiedTime |
Export-Csv "C:\Scripts\PowerAppsInventory.csv" -NoTypeInformation
```

## List Environments
```
Get-AdminPowerAppEnvironment
```

## Check App Sharing / Permissions
```
$app = Get-AdminPowerApp -AppName "<AppId>"
Get-AdminPowerAppRoleAssignment -AppName $app.AppName -EnvironmentName $app.EnvironmentName
```
