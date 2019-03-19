
# Avanade DevOps HOL - Getting Started
In this lab, we will be installing the required development components and verifying that the solution builds and is able to be pushed to Azure DevOps.
## Pre-requisites ##
1. An active Azure subscription<br>
	[Azure Portal](https://portal.azure.com)
2. An active Azure DevOps account.<br>
	[Sign up for Visual Studio Team Services](https://azure.microsoft.com/en-us/services/devops/)

## Set up your machine ##
## In prerequisites you already have virual machine with the Visual Studio 2017 ##
## Verify again in Virtual machine Visual studio 2017 ##
1. Check Visual Studio 2017 in VM.
2. Install [Azure Power Shell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0)

## Create MVC web application ##
1. Open Visual Studio 2017


2. Go to File -> New -> Project... and create a new ASP.NET Core Web Application<br>
    + Name: DevOpsHOL<br>
    + Location: *where ever you put project source*<br>
    + Create Directory for solution: Checked<br>
    + Click OK<br>
    + On the next dialog, choose Web Application (Model-View-Controller) as the application type, No Authentication<br>
    + Configure for https: UnChecked (unless you are up for the challenge)<br>
    + Click OK<br>

3.  Build and run the solution to make sure everything is OK to this point.
    + Debug -> Start Debugging (F5)<br>
		+ If application doesn't start the first time, just run again.
    + Do a quick smoke test to verify that the solution built and runs correctly.<br>
    + Close browser and stop debugging<br>

4. Choose File -> New -> Project... and add a MSTest Test Project (.NET Core) project, to the solution *not the .NET Framework unit test project*.
    + Name: DevOpsHOL.Tests<br>
    + Solution: Add to solution<br>

5. Rename **UnitTest.cs** to **HomeControllerTest.cs** and replace the file contents with the content in the details section below.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<details><summary>Click here to expand the sample unit test code</summary>

     ```csharp
      [TestClass]
      public class HomeControllerTest
      {
          [TestMethod]
          public void Index()
          {
              // Arrange
              HomeController controller = new HomeController();

              // Act
              ViewResult result = controller.Index() as ViewResult;

              // Assert
              Assert.IsNotNull(result);
          }

          [TestMethod]
          public void About()
          {
              // Arrange
              HomeController controller = new HomeController();

              // Act
              ViewResult result = controller.About() as ViewResult;

              // Assert
              Assert.IsNotNull(result);
              Assert.AreEqual("Your application description page.", result.ViewData["Message"]);
          }

          [TestMethod]
          public void Contact()
          {
              // Arrange
              HomeController controller = new HomeController();

              // Act
              ViewResult result = controller.Contact() as ViewResult;

              // Assert
              Assert.IsNotNull(result);
          }
      }
     ```
     </details>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

6. Update all NuGet packages to their 2.x counterparts (Right-click project > Manage NuGet packages)

7. Right Click the project and Unload it. Now edit your project file.

```
<Project Sdk="Microsoft.NET.Sdk.Web">
  <PropertyGroup>
    <TargetFramework>netcoreapp2.1</TargetFramework>
    <RuntimeIdentifiers>win-x64;win-x86;linux-x64</RuntimeIdentifiers>
    <TargetLatestRuntimePatch>true</TargetLatestRuntimePatch>
    <RuntimeFrameworkVersion>2.1.1</RuntimeFrameworkVersion>
    <PlatformTarget>AnyCPU</PlatformTarget>
    <RuntimeIdentifier>win-x64</RuntimeIdentifier>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.App" Version="2.1.1"/>
    <PackageReference Include="Microsoft.AspNetCore.Razor.Design" Version="2.1.2" PrivateAssets="All" />
  </ItemGroup>
</Project>

```
8. Build, run unit tests and run the solution to make sure everything is OK to this point.
    + Test -> Run -> All Tests (Ctrl+R,A)<br>
    + Debug -> Start Debugging (F5)<br>
    + Do another quick smoke test to verify that the solution built and runs correctly.<br>
    + Close browser and stop debugging<br>

9. Add solution to Azure Devops project (Team Explorer -> Sync -> Azure DevOps)
    + Push to Visual Studio Team Services<br>
    + Repository name: DevOpsHOL<br>
    + Publish repository will create a project in Azure DevOps (NOTE: if you have multiple  accounts, make sure this is published to the correct Team Services Domain).<br>

10. Create the first commit for your project (Team Explorer -> Changes -> Commit All and Push).  NOTE: This could be automatically staged so choose Commit Staged and Push.

11. Log in to Azure DevOps with browser and verify that DevOpsHOL project was created and source code is uploaded.

## Next steps

- [Continuous Integration and Continous Deployment](lab-1-azure-devops-project-pipeline.md)
