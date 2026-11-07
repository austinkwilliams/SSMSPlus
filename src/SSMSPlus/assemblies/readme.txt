SSMS host assemblies used as compile-time references only (do not ship in the VSIX).

Refresh these from a local SSMS 22 install when building/updating references:

  C:\Program Files\Microsoft SQL Server Management Studio 22\Release\Common7\IDE\

Files:
  Microsoft.SqlServer.ConnectionInfo.dll
  Microsoft.SqlServer.RegSvrEnum.dll
  SqlPackageBase.dll
  SqlWorkbench.Interfaces.dll

Project references set Private=False / SpecificVersion=False so the running SSMS instance supplies these at runtime.
