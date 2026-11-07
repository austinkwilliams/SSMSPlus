# Publish for SSMS 22

SSMS 21 / 22 support VSIX installation again via `Microsoft.VisualStudio.Ssms` InstallationTargets.

## Preferred: build and install the VSIX

1. Open `src/SSMSPlus.sln` in Visual Studio 2022 (with the Visual Studio extension development workload).
2. Restore NuGet packages and build **Release**.
3. Install the built VSIX with the SSMS-bundled installer (double-clicking the `.vsix` alone may not target SSMS):

```powershell
$ssmsRoot = "C:\Program Files\Microsoft SQL Server Management Studio 22\Release\Common7\IDE"
$vsix = "<path-to>\SSMSPlus.vsix"
$ssmsVersion = (Get-Item "$ssmsRoot\Ssms.exe").VersionInfo.ProductVersion
& "$ssmsRoot\VSIXInstaller.exe" /skuName:ssms /skuVersion:$ssmsVersion $vsix
```

## Fallback: copy build output (all users)

If VSIX install is unavailable, close SSMS and copy the extension output folder to:

`C:\Program Files\Microsoft SQL Server Management Studio 22\Release\Common7\IDE\Extensions\SSMSPlus`

(Administrator rights required.)

## Older SSMS (18 / 19 / 20)

Those releases still need the historical SFX / manual extract flow into the `Program Files (x86)\Microsoft SQL Server Management Studio <N>\...` Extensions folder. See older tags/releases.
