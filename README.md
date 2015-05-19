<a target="_blank" href="https://ci.appveyor.com/project/NaosLLC/naos-WinRM">
![Build status](https://ci.appveyor.com/api/projects/status/github/NaosFramework/Naos.WinRM?branch=master&svg=true)
</a>
<br/> 
<a target="_blank" href="http://nugetstatus.com/packages/Naos.WinRM">
![NuGet Status](http://nugetstatus.com/Naos.WinRM.png)
</a>

Naos.WinRM
================
A .NET wrapper for the WinRM protocol to execute powershell and also send files!

Use - Referencing in your code
-----------
The entire implemenation is in a single file so it can be included without taking a dependency on the NuGet package if necessary preferred.
* Reference the NuGet package: <a target="_blank" href="http://www.nuget.org/packages/Naos.WinRM">http://www.nuget.org/packages/Naos.WinRM</a>.
  <br/><b>OR</b>
* Include the single file (will still REQUIRE System.Management.Automation.dll reference or package reference to Naos.External.MS-WinRM) in your project: <a target="_blank" href="https://raw.githubusercontent.com/NaosFramework/Naos.WinRM/master/Naos.WinRM/Naos.WinRM.cs">https://raw.githubusercontent.com/NaosFramework/Naos.WinRM/master/Naos.WinRM/Naos.WinRM.cs</a>.

```C#
// this is the entrypoint to interact with the system (interfaced for testing).
var machineManager = new MachineManager(
	"10.0.0.1",
	"Administrator",
	MachineManager.ConvertStringToSecureString("xxx"));

// will perform a user initiated reboot.
machineManager.Reboot();

// can run random script blocks WITH parameters.
var fileObjects = machineManager.RunScript("{ param($path) ls $path }", new[] { @"C:\PathToList" });

// can transfer files to the remote server (over WinRM's protocol!).
var localFilePath = @"D:\Temp\BigFileLocal.nupkg";
var fileBytes = File.ReadAllBytes(localFilePath);
var remoteFilePath = @"D:\Temp\BigFileRemote.nupkg";

machineManager.SendFile(remoteFilePath, fileBytes);
```