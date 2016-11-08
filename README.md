# Cake.Sonar

Addin used to execute the [MSBuild scanner for SonarQube](http://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner+for+MSBuild) using cake aliases.
Don't forget to include the tool package.

```csharp

#tool nuget:?package=MSBuild.SonarQube.Runner.Tool
#addin nuget:?package=Cake.Sonar

Task("Sonar")
  .IsDependentOn("SonarBegin")
  .IsDependentOn("Build")
  .IsDependentOn("Unit")
  .IsDependentOn("SonarEnd");
 
Task("SonarBegin")
  .Does(() => {
     SonarBegin(new SonarBeginSettings{
        Url = "sonarcube.contoso.local",
        Login = "admin",
        Password = "admin",
        Verbose = true
     });
  });

Task("SonarEnd")
  .Does(() => {
     SonarEnd(new SonarEndSettings{
        Login = "admin",
        Password = "admin"
     });
  });

```
