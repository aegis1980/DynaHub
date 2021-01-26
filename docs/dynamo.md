# Some Dev instructions

## Dynamo Core/Sandbox vs Dynamo Revit


Two versions of Dynamo:

- [Dynamo Sandbox](https://dynamobim.org/download/) which is the standalone version intended for development,and;

- Dynamo for Revit. This used to be a standalone element, now comes installed with Revit (at least for Revit 2020)

When you build `.sln` for **DynaHub** in Visual Studio, the project `.csproj` is configured to automagically put the built package in Dynamo Core's packages folder in **debug** mode, and Dynamo Revit's folder in **release** mode:

```
    <PropertyGroup>
      <!--Copy to Dynamo sandbox for testing -->
      <DeployFolder Condition="'$(Configuration)' == 'Debug'">$(AppData)\Dynamo\Dynamo Core\2.10\packages\$(ProjectName)</DeployFolder>
      <!--Copy to Dynamo revit for publishing -->
      <DeployFolder Condition="'$(Configuration)' == 'Release' Or '$(Configuration)' == 'DebugRevit'">$(AppData)\Dynamo\Dynamo Revit\2.3\packages\$(ProjectName)</DeployFolder>
    </PropertyGroup>
```
Depending on whether you are building in release or debug mode, Dynahub will not appear in the 'other' Dynamo. 

Also, things will not 'work' if the version numbers in these paths do not align with the versions of Dynamo you have `C:\Users\<user>\AppData\Roaming\Dynamo\...`:
- Dynamo Core
- Dynamo Revit


https://developer.dynamobim.org/05-Package-Deployment/5-1-build-package-from-vs.html

