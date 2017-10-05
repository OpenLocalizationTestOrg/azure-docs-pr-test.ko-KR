---
title: "원격 Docker 호스트에 ASP.NET Core Linux Docker 컨테이너 배포 | Microsoft Docs"
description: "Visual Studio Tools for Docker를 사용하여 Azure Docket 호스트 Linux VM에서 실행 중인 Docker 컨테이너에 ASP.NET Core 웹앱을 배포하는 방법에 대해 설명합니다."
services: azure-container-service
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: e5e81c5e-dd18-4d5a-a24d-a932036e78b9
ms.service: azure-container-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 4a87ee69f23779bf4f6f5db40bc05edbcfc7668d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-an-aspnet-container-to-a-remote-docker-host"></a><span data-ttu-id="3d017-103">원격 Docker 호스트에 ASP.NET 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="3d017-103">Deploy an ASP.NET container to a remote Docker host</span></span>
## <a name="overview"></a><span data-ttu-id="3d017-104">개요</span><span class="sxs-lookup"><span data-stu-id="3d017-104">Overview</span></span>
<span data-ttu-id="3d017-105">Docker는 가상 컴퓨터와 몇 가지 측면에서 비슷하며 응용 프로그램과 서비스를 호스트하는 데 사용할 수 있는 간단한 컨테이너 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="3d017-105">Docker is a lightweight container engine, similar in some ways to a virtual machine, which you can use to host applications and services.</span></span>
<span data-ttu-id="3d017-106">이 자습서에서는 [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) 확장을 사용하여 Azure에서 PowerShell을 사용하여 Docker 호스트에 ASP.NET Core 앱을 배포하는 단계에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3d017-106">This tutorial walks you through using the [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) extension to deploy an ASP.NET Core app to a Docker host on Azure using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d017-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3d017-107">Prerequisites</span></span>
<span data-ttu-id="3d017-108">이 자습서를 완료하는 데 필요한 조건은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3d017-108">The following is required to complete this tutorial:</span></span>

* <span data-ttu-id="3d017-109">[Azure에서 docker-machine을 사용하는 방법](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)의 설명에 따라 Azure Docker 호스트 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3d017-109">Create an Azure Docker Host VM as described in [How to use docker-machine with Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="3d017-110">최신 버전의 [Visual Studio](https://www.visualstudio.com/downloads/)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3d017-110">Install the latest version of [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
* <span data-ttu-id="3d017-111">[Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3d017-111">Download the [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)</span></span>
* <span data-ttu-id="3d017-112">[Windows용 Docker](https://docs.docker.com/docker-for-windows/install/)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3d017-112">Install [Docker for Windows](https://docs.docker.com/docker-for-windows/install/)</span></span>

## <a name="1-create-an-aspnet-core-web-app"></a><span data-ttu-id="3d017-113">1. ASP.NET Core 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="3d017-113">1. Create an ASP.NET Core web app</span></span>
<span data-ttu-id="3d017-114">다음 단계에서는 이 자습서에서 사용할 기본적인 ASP.NET Core 앱을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="3d017-114">The following steps guide you through creating a basic ASP.NET Core app that will be used in this tutorial.</span></span>

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="3d017-115">2. Docker 지원 추가</span><span class="sxs-lookup"><span data-stu-id="3d017-115">2. Add Docker support</span></span>
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-the-dockertaskps1-powershell-script"></a><span data-ttu-id="3d017-116">3. DockerTask.ps1 PowerShell 스크립트 사용</span><span class="sxs-lookup"><span data-stu-id="3d017-116">3. Use the DockerTask.ps1 PowerShell Script</span></span>
1. <span data-ttu-id="3d017-117">프로젝트의 루트 디렉터리에 대해 PowerShell 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3d017-117">Open a PowerShell prompt to the root directory of your project.</span></span> 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. <span data-ttu-id="3d017-118">실행 중인 원격 호스트의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="3d017-118">Validate the remote host is running.</span></span> <span data-ttu-id="3d017-119">상태 = 실행 중이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d017-119">You should see state = Running</span></span> 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
3. <span data-ttu-id="3d017-120">-Build 매개 변수를 사용하여 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="3d017-120">Build the app using the -Build parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  

   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. <span data-ttu-id="3d017-121">-Run 매개 변수를 사용하여 앱 실행</span><span class="sxs-lookup"><span data-stu-id="3d017-121">Run the app, using the -Run parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   <span data-ttu-id="3d017-122">docker가 완료되면 다음 화면과 같은 결과가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d017-122">Once docker completes, you should see results similar to the following:</span></span>
   
   ![앱 보기][3]

[0]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png
