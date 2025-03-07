#  knowledge doc for ASP.NET Core docs

## API ref pages

To publish API ref pages for a new ASP.NET Core product version:

1. Submit a request with the ref pub template at [Reference content request](https://review.learn.microsoft.com/en-us/content-production-service/topics/service-content-publishing?branch=main#reference-content-request) See [this user story](https://dev.azure.com/msft-skilling/Content/_workitems/edit/316842)
2. cc @Alma Jenks ( https://github.com/v-alje)
4. From the PR, view a page then search for new APIs and spot check. Writers need to approve the PR per the PU. It's impossible to review the file changes.
5. When the PR merges, ref is live, ask Sai or Alma to provide a link to the feedback form. See link in [this user story](https://dev.azure.com/msft-skilling/Content/_workitems/edit/316842) and leave kudos for them.
6. That's all for ASP.NET Core APIs. Instructions below are for new APIs outside of ASP.NET Core.
7. Need a list of packages for the new version. Here are the current configurations for ASP to reference: https://apidrop.visualstudio.com/binaries/_git/mrefconfig?path=/bundlepackages/aspnetcore  What is your ms.service or ms.product value? ms.prod: .NET 
See [this workitem](https://dev.azure.com/msft-skilling/Content/_workitems/edit/86012)

Old notes From Doug: If Alma just needs the list of packages for our main branch, I’d look at the Artifacts / Windows_Packages / Shipping list in an official build e.g. https://dev.azure.com/dnceng/_apis/resources/Containers/10936730/Windows_Packages?itemPath=Windows_Packages%2FRelease%2FShipping&%24format=zip&saveAbsolutePath=false. If they need every package (including the list of runtime packages for non-Windows platforms and non-shipping packages), Artifacts / PackagesArtifacts e.g. https://dev.azure.com/dnceng/7ea9116e-9fac-403d-b258-b31fcf1bb293/_apis/build/builds/1848412/artifacts?artifactName=PackageArtifacts&api-version=7.0&%24format=zip is the best place to look.

## Moniker / version selector changes

[Show Monikers]([url](https://aka.ms/publish-on-docs/monikers)) (from https://ops.microsoft.com/#/monikers which shows all monikers) Filter by ASP.NET Core in the 3rd dropdown/filter box - you can view but not edit this page. In the top right of the page, select ***Request-Monikers***

<img width="194" alt="image" src="https://github.com/user-attachments/assets/f0bb0010-9a36-44e3-b126-9fd01f7e752f">

submit a new request. Do that for new monikers ***OR*** to promote a preview moniker to default (state change). [Request a moniker](https://review.learn.microsoft.com/en-us/help/onboard/versions-monikers?branch=main#request-a-moniker) on the [Moniker help page](https://review.learn.microsoft.com/en-us/help/onboard/versions-monikers?branch=main#request-a-moniker). On new request, be sure it list preview, ie ASP.NET Core 8.0 preview

https://ops.microsoft.com/#/monikers

<img width="406" alt="image" src="https://github.com/Rick-Anderson/Report/assets/3605364/b051de39-0697-4848-944b-9ad89f4e5d27">

* ASP.NET
* Platform value of dotnet and Family value of ASP.NET
* ASP.NET Core 8.0
* aspnetcore-8.0

<img width="269" alt="image" src="https://github.com/Rick-Anderson/Report/assets/3605364/71765d24-84df-4182-8d13-4309f8d6c585">

See [7.0 GA issue](https://portal.microsofticm.com/imp/v3/incidents/details/347401864/home)

To add or change monikers, [request a new moniker](https://aka.ms/publish-on-docs/monikers) -- old method, [open an issue with OPS admin](https://ceapex.visualstudio.com/Onboarding/_workitems/edit/513805). See https://ceapex.visualstudio.com/Onboarding/_workitems/edit/562784/ the 7.0 request

![image](https://user-images.githubusercontent.com/3605364/140599706-2db0176c-5f61-4f77-840e-04e8584ad757.png)
-->

Each time a new ASP.NET Core product version is released, a new moniker is needed to support versioned content for that release. These monikers are managed in the [Docs Portal Monikers page](https://ops.microsoft.com/#/monikers). Filter that page's table using a **Platform** value of *dotnet* and a **Family** value of *ASP.NET*. The resulting monikers are shared by the conceptual docs and the API ref pages. 

<img width="308" alt="image" src="https://user-images.githubusercontent.com/3605364/204360808-daa90828-80f9-4807-993e-212159097570.png">


Speaking of versioning, [this section of *docfx.json*](https://github.com/dotnet/AspNetCore.Docs/blob/main/aspnetcore/docfx.json#L100-L105) supports the version selector in the ASP.NET Core conceptual docs. EDIT: `docfx.json#L100-L105` doesn't exist

## Automatic labeling of GitHub issues

Andy De George's issue labeling tool is used to automatically label incoming GitHub issues based on their associated metadata. To modify the behavior of this tool in the *dotnet/AspNetCore.Docs* repo, see [*.ghal.rules.json*](https://github.com/dotnet/AspNetCore.Docs/blob/main/.ghal.rules.json).

## Code sample builds on pull requests

The Snippets 5000 tool is used to build modified code samples that are part of pull requests. In the *dotnet/AspNetCore.Docs* repo, the [*build-validation.yaml*](https://github.com/dotnet/AspNetCore.Docs/blob/main/.github/workflows/build-validation.yml) file is used to configure how that build behaves.

**IMPORTANT:** When a .NET SDK version newer than 5.x is needed to build code samples, update [this environment variable](https://github.com/dotnet/AspNetCore.Docs/blob/main/.github/workflows/build-validation.yml#L25) with the appropriate SDK version number. I recommend making this change once you want to have ASP.NET Core 6.0 code samples building in pull requests.

David Pine is a great resource for any questions.

## Microsoft Learn modules

Here are some useful resources for the ASP.NET Core Learn modules work:

- [Azure DevOps .NET content issues query](https://ceapex.visualstudio.com/Microsoft%20Learn/_queries?tempQueryId=a9350c42-2123-4058-9f72-51b064c3a117)
- [MicrosoftDocs/learn-pr](https://github.com/MicrosoftDocs/learn-pr) - The repo in which you’ll open PRs for the actual module content
- Sample code / setup script repos:
    - [MicrosoftDocs/mslearn-aspnet-core](https://github.com/MicrosoftDocs/mslearn-aspnet-core) - Repo containing most starter apps and all setup scripts for modules
    - [MicrosoftDocs/mslearn-microservices-devops-aspnet-core](https://github.com/MicrosoftDocs/mslearn-microservices-devops-aspnet-core) - Repo containing starter app for microservices w/ GitHub Actions module
- [GitHub project for ASP.NET Core microservices learning path](https://github.com/dotnet/AspNetCore.Docs/projects/68) - This is where Cam and I were tracking progress for the microservices learning path
- [Gold standard module checker](http://mslearnmetricportal.azurewebsites.net/) - Use this tool to see how well a module scores against the Instructional Design team’s “gold standards”
- [Contributor guide](https://review.docs.microsoft.com/en-us/help/learn/?branch=master)
- [PowerBI dashboard](https://msit.powerbi.com/groups/me/reports/3ad7a43c-5334-4086-b762-8b4bdb2741ff/ReportSection) - Metrics such as completion rates for modules can be found here

## What's New in Docs

I'll still be involved in the project. If I'm not around, Bill Wagner is a great resource for any questions.

### Overview

The page generation tool is a .NET global tool that's distributed via an internal Azure Artifacts feed. The tool uses settings from the *.whatsnew.json* file in the root of the GitHub repo.

The table below includes some helpful links.

|Resource  |Description  |
|---------|---------|
|[README file](https://aka.ms/whats-new-tool) |A *README* file with installation & onboarding instructions.|
|[Contributors guide](https://dev.azure.com/mseng/TechnicalContent/_git/dotnet-docs-tools?path=%2Fwhatsnew%2Fsrc%2FWhatsNew.Cli%2FCONTRIBUTING.md) |A guide for those who want to contribute to the tool's code. Explains how to get the tool running locally on your development machine.|
|[Source code](https://dev.azure.com/mseng/TechnicalContent/_git/dotnet-docs-tools?path=%2Fwhatsnew)|Source code location for the tool. Open the solution in Visual Studio 2019.|
|[Azure Pipelines CI/CD pipeline](https://dev.azure.com/mseng/TechnicalContent/_build?definitionId=10534)|The build and release pipeline. Builds when PRs are opened against specific branches. Also responsible for publishing the tool's NuGet package to Azure Artifacts.|
|[Azure Artifacts package feed](https://dev.azure.com/mseng/TechnicalContent/_packaging?_a=feed&feed=DotnetDocsTools%40Local)|An internal-only packages feed that's accessible to all of DevRel.|
|[Power BI dashboard](https://aka.ms/whatsnewindocs)|A dashboard showing traffic to/from the what's new pages.|
|[whatsnewindocs@microsoft.com](mailto:whatsnewindocs@microsoft.com)|A distribution list (DL) for the project's V-team. If anyone has questions about the tool, this is the best DL to use.|

### ASP.NET Core "what's new" page generation

When the key expires, generate a new PAT and store it in an environment variable named `GitHubKey`.

<img width="290" alt="image" src="https://user-images.githubusercontent.com/3605364/182247697-aa4885de-056a-469b-b011-c7ebd417fd7f.png">

Complete the following steps on the first of each month:

must be run in folder at repo root, ie `C:\GH\aspnet\docs\1\AspNetCore.Docs`
1. Run a variation of the following command:

    ```bash
    cd C:\GH\aspnet\docs\6\AspNetCore.Docs
    dotnet whatsnew --owner dotnet --repo AspNetCore.Docs --savedir C:\tmp
    ```

When When the `startdate | enddate` arguments are omitted, they default to the first and last days of the previous month, respective such as `--startdate 6/1/2022 --enddate 6/30/2022 `
    In the preceding example, all pull requests merged into *main* between March 1st and March 31st will be processed. The *[.whatsnew.json](https://github.com/dotnet/AspNetCore.Docs/blob/main/.whatsnew.json)* file in the *dotnet/AspNetCore.Docs* repo will be used by the tool to determine which pull requests are considered significant and how the Markdown file is generated.

1. Locate the generated Markdown file in the `--savedir` previously specified.
1. Copy the generated Markdown file into the [*whats-new* folder](https://github.com/dotnet/AspNetCore.Docs/tree/main/aspnetcore/whats-new), and rename the file to match the naming convention that's been established. For example, rename *dotnet-AspNetCore.Docs-2021-03-01.md* to *2021-03.md*.
1. Modify the pull request titles so that they're meaningful to the reader. For example, avoid pull request titles like "Edit pass on index.md". After doing this cleanup exercise a few times, you'll understand the importance of descriptive pull request titles. :-)
1. In that same *whats-new* folder, update both *index.yml* and *toc.yml* with a link to the latest "what's new" page. Also, remove the oldest "what's new" page. We've been maintaining ONLY the last 6 months worth of pages.

## Project

Go to https://github.com/orgs/dotnet/projects
<!--
![image](https://user-images.githubusercontent.com/3605364/215637269-b396eb23-4a18-4523-ad58-6b9f4e838896.png) -->
<img width="673" alt="image" src="https://github.com/Rick-Anderson/Report/assets/3605364/a95b3316-a7c2-4f15-939e-5dbd20d3a02e">


<img width="292" alt="image" src="https://user-images.githubusercontent.com/3605364/215639185-3b137738-13f6-46c4-9ea7-9d5334a0e919.png">

Here are the setting I choose for creating a new sprint project:

Name:  "dotnet/docs <Month> sprint"  I include the dotnet/docs prefix because the new projects are org-wide
Template: Backlog.
Columns: 
	"backlog"
	We use "ready", "in progress", "in review" and "done" `next`
Settings/Project settings: Update the description and default reviewer. ~Reviewer moves down one row from the previous month. (2 rows when the reviewer would be the author)~
Settings/Manage access: Entire org has write access, that's all that's needed.
Settings/Workflows: By default all workflows are off. Turn them all on. If the destination "status" has a red background, update the column to one of the configured columns.
Go to [projects](https://github.com/dotnet/AspNetCore.Docs/projects) , select "Add project" and add the new project to the Quick access for our repo.

Finally, email "dotnetossadmin@microsoft.com" and request that the project be moved from private to public. (New projects are private, and it requires an org admin to make them public.)
    


<img width="395" alt="image" src="https://user-images.githubusercontent.com/3605364/214664937-17f45fc7-76ec-4cf4-bbb2-e7617536a5f7.png">

<img width="288" alt="image" src="https://user-images.githubusercontent.com/3605364/214686544-59b75d98-24e0-457d-877e-39d928a83946.png">

<img width="482" alt="image" src="https://user-images.githubusercontent.com/3605364/214690634-f5244d88-4d13-4d46-aa0e-1b3a43a9bf94.png">

<img width="269" alt="image" src="https://user-images.githubusercontent.com/3605364/214718589-9176f058-5508-4f3b-9b69-5e690b340ecb.png">

Go to **https://github.com/orgs/dotnet/projects**
To display the project on the Projects page, select **Link a project**, and check it.
	
<img width="280" alt="image" src="https://user-images.githubusercontent.com/3605364/223883048-8dda9523-ef03-42f2-81ae-e4b752da144c.png">

## Close project
	Go to setting and select close
	
![image](https://github.com/Rick-Anderson/Report/assets/3605364/71ce732d-0294-46e6-8f22-19926fa90598.png)

<img width="450" alt="image" src="https://github.com/Rick-Anderson/Report/assets/3605364/71ce732d-0294-46e6-8f22-19926fa90598.png">
	
## Generate PAT personal access token
	
generate a PAT [here](https://dev.azure.com/msft-skilling/_usersSettings/tokens)
	[here](https://dev.azure.com/msft-skilling/_usersSettings/tokens)
	
## OSPO_TOKEN

* you need one for the OSPO AzDo instance, which is [here]([url](https://ossmsft.visualstudio.com/_usersSettings/tokens)) = must be ossmsft org, not msft-skilling
* the only scope declared is UserProfile: read
	
<img width="450" alt="image" src="https://user-images.githubusercontent.com/3605364/232592275-051eb818-6244-41fc-ad9b-03f15e178979.png">
