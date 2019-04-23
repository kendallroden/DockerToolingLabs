# Visual Studio Docker Tooling Labs

## Overview 
The goal of the following hands-on-lab is to help you leverage the power of Visual Studio and Visual Studio Code as you develop with Docker

## Prerequisites

- [Windows 10 Professional or Enterprise with Anniversary Update (version 1607) or later](https://code.visualstudio.com/Download)
- Hyper-V enabled
-  [Visual Studio 2017 (v 15.7 or later) or Visual Studio 2019](https://visualstudio.microsoft.com/downloads/)
- [Docker Desktop for Windows](https://docs.docker.com/docker-for-windows/install/)
-  [Visual Studio Code](https://code.visualstudio.com/Download)
- [Latest .NET Core 2.2 SDK](https://dotnet.microsoft.com/download)


## Getting Started with Visual Studio 

1.  Open Visual Studio 2017 and `Ctrl+Shift+N` to open the New Project dialogue  
   
2.  Create a new Visual C#, ASP.NET Core Web Application and name it `WebFrontEnd`. Click 'OK' to continue.
    
    ![](content/image1.png)
   
3. Configure your project to use `.NET Core`, the `ASP.NET Core 2.2 SDK` and the `Web Application (Model-View-Controller)` template. You will notice you can select `Enable Docker Support` when creating a new solution. In this lab, we will be adding Docker Support at a later time, but keep in mind you can leverage this feature in the future to add Docker Support during project creation. Click 'OK' to create.
   
   **Note: For this lab, we will not configure for HTTPS.**
   
    ![](content/image2.png)

4. Open the Solution Explorer `Ctrl+Alt+L` to view your project files. Your output should mirror the image below. 
   
   ![](content/image3.png)

5. Use `F5` or `Ctrl+F5` to run your project and confirm it is working as expected.
    
    >*Now for the fun stuff*! Once you have confirmed that your application is running locally, you can get started with Docker tools for Visual Studio

## Adding Docker Support in Visual Studio
**Important: Before continuing with the lab, ensure Docker For Desktop is in Linux-mode.** To confirm you are in Linux-mode, use the following steps:
1. Right-click the Docker Desktop icon located in the lower right-hand corner of your taskbar
2. If you are in Linux-mode already, you will see `Switch to Windows containers`. Otherwise, you will need to select `Switch to Linux containers`.
    > This switch will tell Docker Desktop to use the MobyLinuxVM in Hyper-V in order to run Linux containers. You can view this VM by opening `Hyper-V Manager`. 
    
    ![](content/MobyLinuxVM.png)

3. Once you have confirmed you are in Linux-Mode, return to Visual Studio. Right-click your `WebFrontEnd` project in the Solution Explorer, select `Add` from the menu and then proceed to select `Docker Support`. You will then be prompted to select a target operating system: Windows or Linux. Click 'OK' to continue.

    > Note: Due to the fact .NET Core is cross-platform, the `WebFrontEnd` application is capable of running in a Windows or Linux container. This lab will target Linux. You can adapt the instructions to use Windows containers if you desire.
   
   ![](content/image4.png)

4. By adding Docker Support, you should see that a `Dockerfile` has been added *automagically* at the project level.
   
   > This lab assumes prior experience with Dockerfiles. If you would like to learn more about Dockerfiles, check out the following resources: 
   > - [Dockerfile Reference Documentation by Docker](https://docs.docker.com/engine/reference/builder/)
   > - [.NET and multi-stage Dockerfiles by Steve Lasker](https://blogs.msdn.microsoft.com/stevelasker/2017/09/11/net-and-multistage-dockerfiles/)


    **Recently, Microsoft changed the hosting location for Microsoft .NET Core container images. This change is not yet reflected in the auto-generated Dockerfile. Therefore, we will update it manually to adhere to best practices. For more information about Microsoft Container Registry, check out the links below:**
   
   > - [Microsoft syndicates container catalog by Steve Lasker](https://azure.microsoft.com/en-us/blog/microsoft-syndicates-container-catalog/)

   > - [.NET Core Container Images now Published to Microsoft Container Registry by Richard Lander](https://devblogs.microsoft.com/dotnet/net-core-container-images-now-published-to-microsoft-container-registry/)

5. Modify the initial `FROM` statement in the Dockerfile to use the MCR hosted ASP.NET Core Runtime image: `mcr.microsoft.com/dotnet/core/aspnet:2.2`. 
   
   ![](content/MCRUpdate1.png)

6. Modify the `FROM` statement on `line 5` in the Dockerfile to use the MCR hosted .NET Core SDK image: `mcr.microsoft.com/dotnet/core/sdk:2.2`. 

    ![](content/MCRUpdate1.png)



