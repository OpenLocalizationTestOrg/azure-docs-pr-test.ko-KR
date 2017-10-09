---
title: "ASP.NET Core Linux Docker 컨테이너 tooa 원격 Docker 호스트 aaaDeploy | Microsoft Docs"
description: "어떻게 toouse Visual Studio Tools for Docker toodeploy ASP.NET Core 웹 Azure Docker 호스트 Linux VM에서 실행 중인 응용 프로그램 tooa Docker 컨테이너에 알아봅니다"
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
ms.openlocfilehash: 27b0c6420628c73220200bc071b47a4cd89fff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-container-tooa-remote-docker-host"></a><span data-ttu-id="45ab5-103">ASP.NET 컨테이너 tooa 원격 Docker 호스트 배포</span><span class="sxs-lookup"><span data-stu-id="45ab5-103">Deploy an ASP.NET container tooa remote Docker host</span></span>
## <a name="overview"></a><span data-ttu-id="45ab5-104">개요</span><span class="sxs-lookup"><span data-stu-id="45ab5-104">Overview</span></span>
<span data-ttu-id="45ab5-105">Docker는 경량 컨테이너 엔진 수 있는 몇 가지 방법으로 tooa 가상 컴퓨터와 비슷한 toohost 응용 프로그램 및 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="45ab5-105">Docker is a lightweight container engine, similar in some ways tooa virtual machine, which you can use toohost applications and services.</span></span>
<span data-ttu-id="45ab5-106">이 자습서에서는 hello를 사용 하 여 [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) 확장 toodeploy PowerShell을 사용 하 여 Azure에는 ASP.NET Core 응용 프로그램 tooa Docker 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="45ab5-106">This tutorial walks you through using hello [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) extension toodeploy an ASP.NET Core app tooa Docker host on Azure using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45ab5-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="45ab5-107">Prerequisites</span></span>
<span data-ttu-id="45ab5-108">hello 다음은 필요한 toocomplete이이 자습서:</span><span class="sxs-lookup"><span data-stu-id="45ab5-108">hello following is required toocomplete this tutorial:</span></span>

* <span data-ttu-id="45ab5-109">에 설명 된 대로 Azure Docker 호스트 VM 만들기 [어떻게 toouse docker-Azure 사용한 컴퓨터](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="45ab5-109">Create an Azure Docker Host VM as described in [How toouse docker-machine with Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="45ab5-110">최신 버전의 hello 설치 [Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="45ab5-110">Install hello latest version of [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
* <span data-ttu-id="45ab5-111">Hello 다운로드 [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)</span><span class="sxs-lookup"><span data-stu-id="45ab5-111">Download hello [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)</span></span>
* <span data-ttu-id="45ab5-112">[Windows용 Docker](https://docs.docker.com/docker-for-windows/install/)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="45ab5-112">Install [Docker for Windows](https://docs.docker.com/docker-for-windows/install/)</span></span>

## <a name="1-create-an-aspnet-core-web-app"></a><span data-ttu-id="45ab5-113">1. ASP.NET Core 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="45ab5-113">1. Create an ASP.NET Core web app</span></span>
<span data-ttu-id="45ab5-114">hello 다음 단계를 안내해이 자습서에 사용 될 기본 ASP.NET Core 응용 프로그램을 만드는 과정입니다.</span><span class="sxs-lookup"><span data-stu-id="45ab5-114">hello following steps guide you through creating a basic ASP.NET Core app that will be used in this tutorial.</span></span>

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="45ab5-115">2. Docker 지원 추가</span><span class="sxs-lookup"><span data-stu-id="45ab5-115">2. Add Docker support</span></span>
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-hello-dockertaskps1-powershell-script"></a><span data-ttu-id="45ab5-116">3. Hello DockerTask.ps1 PowerShell 스크립트를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="45ab5-116">3. Use hello DockerTask.ps1 PowerShell Script</span></span>
1. <span data-ttu-id="45ab5-117">프로젝트의 PowerShell 프롬프트 toohello 루트 디렉터리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="45ab5-117">Open a PowerShell prompt toohello root directory of your project.</span></span> 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. <span data-ttu-id="45ab5-118">유효성 검사 hello 원격 호스트에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="45ab5-118">Validate hello remote host is running.</span></span> <span data-ttu-id="45ab5-119">상태 = 실행 중이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45ab5-119">You should see state = Running</span></span> 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
3. <span data-ttu-id="45ab5-120">사용 하 여 빌드 hello 앱 hello-빌드 매개 변수</span><span class="sxs-lookup"><span data-stu-id="45ab5-120">Build hello app using hello -Build parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  

   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. <span data-ttu-id="45ab5-121">Hello 앱을 실행 하면 사용 하 여 hello-실행 매개 변수</span><span class="sxs-lookup"><span data-stu-id="45ab5-121">Run hello app, using hello -Run parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   <span data-ttu-id="45ab5-122">Docker 완료 되 면 결과 유사한 toohello 다음을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45ab5-122">Once docker completes, you should see results similar toohello following:</span></span>
   
   ![앱 보기][3]

[0]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png
